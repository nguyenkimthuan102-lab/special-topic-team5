## 1. SƠ ĐỒ KIẾN TRÚC TỔNG THỂ

```mermaid
flowchart TB
    subgraph ClientLayer["TẦNG NGƯỜI DÙNG (CLIENT)"]
        Guest["Khách (Guest)<br/>Discovery + nội dung Public Free"]
        Browser["Trình duyệt Web<br/>Học viên / Giảng viên / Cộng tác viên / Moderator / Admin"]
    end

    subgraph CloudflareLayer["TẦNG BẢO MẬT & PHÂN PHỐI (CLOUDFLARE)"]
        CF_DNS["Cloudflare DNS"]
        CF_SSL["Cloudflare Edge Proxy<br/>HTTPS / TLS 1.3 / HSTS"]
    end

    subgraph VPS_Docker["MÁY CHỦ VPS (DOCKER COMPOSE NETWORK)"]
        Nginx["Nginx Reverse Proxy<br/>Origin CA, chuyển HTTP sang HTTPS"]
        ReactUI["Frontend React + TypeScript<br/>Bản build tĩnh do Nginx phục vụ"]

        subgraph DotNetBackend["Backend Container: C# ASP.NET Core - Modular Monolith + Layered"]
            APIHost["BrainMemo.WebApi Host<br/>REST API<br/>JWT, Rate Limiter, ProblemDetails tiếng Việt"]
            BG["Hosted Services chạy nền<br/>Outbox Dispatcher, Job Runner AI,<br/>Scheduler: hết hạn đơn, giải phóng tiền tạm giữ, tự nộp bài, gỡ chế tài"]
            BB["BuildingBlocks<br/>SharedKernel, Event Bus in-process, Outbox / Inbox, Phân trang, Clock"]

            subgraph Modules["11 MODULE NGHIỆP VỤ (mỗi module: Api / Application / Domain / Infrastructure / Contracts)"]
                subgraph GrpNen["Nền tảng & Kiểm soát"]
                    ModIdn["Identity<br/>Xác thực, RBAC, chế tài"]
                    ModMod["Moderation<br/>Báo cáo, duyệt VIP, Audit Log"]
                    ModNtf["Notification<br/>In-app (polling), Email, Broadcast"]
                end
                subgraph GrpHocLieu["Học liệu & Đánh giá"]
                    ModCrs["Course<br/>Khóa học, ghi danh, truy cập, đề cử"]
                    ModCnt["Content<br/>Chương, Block, ngân hàng câu hỏi, phiên bản"]
                    ModLrn["Learning<br/>Tiến độ, thi, bình luận"]
                    ModAst["Assessment<br/>Chấm điểm, chuẩn đầu ra, đánh giá"]
                end
                subgraph GrpKhac["Khám phá & Cá nhân"]
                    ModDsc["Discovery<br/>Tìm kiếm, lọc, Top 10"]
                    ModPrf["Profile<br/>Hồ sơ, quyền riêng tư"]
                end
                subgraph GrpTien["Giao dịch"]
                    ModPay["Payment<br/>Đơn, ví, Ledger, hoa hồng, rút / hoàn tiền"]
                end
                subgraph GrpAI["Trí tuệ nhân tạo"]
                    ModAI["AI<br/>Sinh câu hỏi, RAG, Quota Guard, Smart Routing, Cache"]
                end
            end

            Infra["Infrastructure Adapters<br/>EF Core (DbContext riêng mỗi module), IFileStorage (S3), ILlmClient,<br/>IPaymentGateway, IEmailSender, IPhoBertClient, Google OAuth"]
        end

        subgraph PythonAI["AI Service Container: Python (CPU)"]
            FastAPI_AI["FastAPI Moderation Controller"]
            PhoPipe["PhoBERT Pipeline<br/>Tách từ tiếng Việt + PhoBERT (ONNX int8)"]
        end

        MySQL[("MySQL 8<br/>1 database, bảng tiền tố theo module")]
    end

    subgraph ExternalCloud["DỊCH VỤ BÊN NGOÀI (EXTERNAL)"]
        R2Storage[("Cloudflare R2 / MinIO<br/>Object Storage - S3 API")]
        LLMApi["LLM API bên ngoài<br/>Nhà cung cấp trừu tượng hóa qua ILlmClient"]
        PayGW["Cổng thanh toán<br/>VNPay / MoMo / PayOS"]
        SMTP["Dịch vụ Email SMTP"]
        GoogleOAuth["Google OAuth 2.0"]
    end

    %% Luồng người dùng
    Guest -->|"HTTPS (443)"| CF_DNS
    Browser -->|"HTTPS (443)"| CF_DNS
    CF_DNS --> CF_SSL
    CF_SSL -->|"TLS (Origin CA)"| Nginx
    Nginx -->|"Static / SPA"| ReactUI
    Nginx -->|"REST /api/*"| APIHost
    Browser -.->|"Presigned PUT/GET: tải tệp trực tiếp"| R2Storage
    PayGW -->|"Webhook / IPN (chữ ký số)"| CF_SSL

    %% Luồng nội bộ backend
    APIHost --> Modules
    BG --> Modules
    BG -->|"Poll Outbox / Jobs"| MySQL
    Modules -.->|"dùng chung"| BB
    Modules --> Infra

    %% Hạ tầng và dịch vụ ngoài
    Infra -->|"EF Core (TCP 3306)"| MySQL
    Infra -->|"S3 SDK (Presigned URL)"| R2Storage
    Infra -->|"HTTP nội bộ (timeout, fallback hàng đợi thủ công)"| FastAPI_AI
    FastAPI_AI --> PhoPipe
    Infra -->|"HTTPS (timeout 30s, retry + circuit breaker)"| LLMApi
    Infra -->|"HTTPS (timeout 10s)"| PayGW
    Infra -->|"SMTP"| SMTP
    Infra <-->|"OAuth 2.0"| GoogleOAuth

    classDef mod fill:#e8f1ff,stroke:#3b6fd4,color:#000
    class ModIdn,ModMod,ModNtf,ModCrs,ModCnt,ModLrn,ModAst,ModDsc,ModPrf,ModPay,ModAI mod
```

## 2. KIẾN TRÚC PHÂN TẦNG BÊN TRONG MỘT MODULE (LAYERED)

```mermaid
flowchart TB
    Host["Host (Composition Root, đăng ký DI)"]
    Other["Module khác"]

    subgraph ModuleX["Một module (ví dụ: Course)"]
        Api["X.Api<br/>Endpoint / Controller, Request - Response"]
        App["X.Application<br/>Use case / Handler, Validator, Ports (IRepository...)"]
        Dom["X.Domain<br/>Entity, Aggregate, Domain Event, Quy tắc nghiệp vụ<br/>(không phụ thuộc EF / HTTP)"]
        Inf["X.Infrastructure<br/>DbContext riêng, Repository, Adapter ngoài, Consumer event"]
        Con["X.Contracts<br/>Interface công khai, Integration Event, DTO công khai"]
    end

    DB[("Bảng tiền tố x_ trong MySQL")]

    Host --> Api
    Host -.->|"đăng ký DI"| Inf
    Api --> App
    App --> Dom
    Inf -->|"implements ports"| App
    Inf --> Dom
    App -.->|"implements"| Con
    Inf -->|"EF Core"| DB
    Other -->|"CHỈ tham chiếu"| Con
    Other -.->|"KHÔNG tham chiếu Domain / Application / Infrastructure / bảng nội bộ"| ModuleX
```

## 3. QUAN HỆ PHỤ THUỘC VÀ GIAO TIẾP GIỮA CÁC MODULE

Quy ước: `A → B` nghĩa là A chỉ tham chiếu `B.Contracts`. Nét liền: gọi Contract đồng bộ. Nét đứt: nhận event hoặc implement port do B định nghĩa (Dependency Inversion). Project `*.Contracts` không tham chiếu module nào nên không có vòng phụ thuộc.

```mermaid
flowchart BT
    Identity["Identity"]
    Payment["Payment"]
    Course["Course"]
    Content["Content"]
    Learning["Learning"]
    Assessment["Assessment"]
    AI["AI"]
    Moderation["Moderation"]
    Notification["Notification"]
    Discovery["Discovery"]
    Profile["Profile"]
    AllMods["Tất cả module khác"]

    AllMods -->|"IAccessChecker, trạng thái tài khoản"| Identity

    Content --> Course
    Learning --> Course
    Learning --> Content
    Assessment --> Content
    Assessment --> Course
    AI --> Course
    AI --> Content
    Moderation -->|"ICourseModerationPort: ẩn, khôi phục, duyệt"| Course
    Moderation --> Content
    Moderation -->|"Lệnh hạn chế, khóa tài khoản"| Identity
    Profile --> Course
    Profile -->|"Đọc ví, đơn hàng"| Payment

    Course -.->|"OrderPaid, RefundApproved"| Payment
    Learning -.->|"implements IRefundEligibilityProvider"| Payment
    Payment -.->|"implements IAiPlanProvider"| AI
    Payment -.->|"AccountLocked, RestrictionApplied"| Identity
    Assessment -.->|"AttemptSubmitted"| Learning
    Assessment -.->|"implements IQuestionUsageProvider"| Content
    AI -.->|"CommentPosted"| Learning
    Moderation -.->|"ContentFlagged"| AI
    Moderation -.->|"CourseSubmittedForReview"| Course
    Notification -.->|"Event của mọi module"| Course
    Notification -.-> Payment
    Notification -.-> Learning
    Notification -.-> Assessment
    Notification -.-> Moderation
    Discovery -.->|"Event cập nhật read model"| Course
    Discovery -.-> Assessment
    Discovery -.-> Payment
    Discovery -.-> Learning
```

## 4. LUỒNG KIỂM TRA QUYỀN TRUY CẬP

```mermaid
flowchart TB
    Req["Request đến API"] --> HasJwt{"Có JWT?"}

    HasJwt -->|"Không"| GuestChk{"Endpoint công khai và<br/>khóa + chương đều Public Free?"}
    GuestChk -->|"Có"| AllowG["Cho phép<br/>(không lưu tiến độ / điểm cá nhân)"]
    GuestChk -->|"Không"| Deny401["401 / 403"]

    HasJwt -->|"Có"| S1{"Bước 1: Tài khoản bị khóa<br/>hoặc chế tài còn hiệu lực?"}
    S1 -->|"Có"| DenyRestrict["Chặn theo phạm vi chế tài"]
    S1 -->|"Không"| S2{"Bước 2: Role / permission<br/>chức năng hợp lệ?"}
    S2 -->|"Không"| Deny403a["403"]
    S2 -->|"Có"| OM{"Khóa học ở chế độ Only Me?"}
    OM -->|"Có"| Own{"Là chủ khóa?"}
    Own -->|"Không"| Deny404["404 (không lộ sự tồn tại)<br/>kể cả Admin / Moderator"]
    Own -->|"Có"| Allow["Cho phép"]
    OM -->|"Không"| S3{"Bước 3: Quyền trên tài nguyên<br/>(chủ khóa / cộng tác viên / ghi danh hợp lệ / đã mua)?"}
    S3 -->|"Có"| Allow
    S3 -->|"Không"| Deny403b["403"]
```

## 5. Sơ đồ tuần tự
### 5.1. LUỒNG MUA KHÓA HỌC (THANH TOÁN, OUTBOX, GHI DANH)

```mermaid
sequenceDiagram
    autonumber
    actor HV as Học viên (React)
    participant API as WebApi
    participant CRS as Course
    participant PAY as Payment
    participant GW as Cổng thanh toán
    participant OB as Outbox Dispatcher
    participant NTF as Notification

    HV->>API: POST /courses/:id/purchase
    API->>CRS: Kiểm tra điều kiện bán và giá (Contract)
    CRS-->>API: Giá tại thời điểm mua
    API->>PAY: Tạo đơn Pending (snapshot giá + coupon)
    PAY-->>HV: Mã QR / URL thanh toán
    HV->>GW: Thanh toán
    GW->>API: Webhook / IPN (chữ ký số)
    API->>PAY: Xác thực chữ ký, đối chiếu số tiền, khóa idempotency
    Note over PAY: 1 DB transaction: Order=Paid, ghi Ledger, chia 85% giảng viên / 15% nền tảng, ghi Outbox OrderPaid
    PAY-->>API: 200 OK (bản trùng cũng trả 200)
    OB->>CRS: OrderPaid (Inbox idempotent) kích hoạt ghi danh
    OB->>NTF: OrderPaid tạo thông báo + email
    HV->>API: GET /notifications (polling 30-60 giây)
    API->>NTF: Lấy thông báo chưa đọc
    NTF-->>HV: Thông báo thanh toán thành công
```

### 5.2. LUỒNG LÀM BÀI KIỂM TRA (REST + GIỜ SERVER)

```mermaid
sequenceDiagram
    autonumber
    actor HV as Học viên (React)
    participant API as WebApi
    participant LRN as Learning
    participant SCH as Scheduler
    participant OB as Outbox Dispatcher
    participant AST as Assessment

    HV->>API: POST /exams/:id/attempts
    API->>LRN: Kiểm tra quyền học, lượt làm, mật khẩu, ngoại lệ (Contract Course)
    LRN-->>HV: Attempt: snapshot câu hỏi + đáp án đã xáo, deadline UTC, serverNow
    Note over HV: Đồng hồ đếm ngược chỉ để hiển thị, tính từ deadline của server
    loop Mỗi tối đa 30 giây
        HV->>API: PUT /attempts/:id/answers (version)
        API->>LRN: Lưu nháp, kiểm tra deadline
        LRN-->>HV: OK + deadline hiện tại (đổi nếu được cộng thêm giờ)
    end
    alt Học viên nộp bài
        HV->>API: POST /attempts/:id/submit
        API->>LRN: Nộp bài (idempotent)
    else Hết giờ hoặc tới giờ đóng bài
        Note over LRN: Request sau deadline bị từ chối, bài coi là đã nộp (lazy)
        SCH->>LRN: Quét attempt quá hạn mỗi 10-15 giây, tự nộp
    end
    LRN->>OB: Outbox AttemptSubmitted
    OB->>AST: Chấm trắc nghiệm tự động, tự luận chờ giảng viên
    AST->>OB: Outbox AttemptGraded
    HV->>API: GET /attempts/:id/result
    API->>AST: Lấy kết quả theo cấu hình hiển thị
    AST-->>HV: Điểm hoặc trạng thái chờ chấm
```

## 6. SƠ ĐỒ TRIỂN KHAI VÀ CI/CD

```mermaid
flowchart LR
    Dev["Nhóm phát triển<br/>Git push / merge vào main"] --> Repo["Git Repository"]

    subgraph LocalPC["MÁY CÁ NHÂN"]
        Jenkins["Jenkins (Poll SCM)"]
        S1["Restore + Build"] --> S2["Unit Test + Architecture Test"]
        S2 --> S3["Integration Test<br/>(Testcontainers MySQL)"]
        S3 --> S4["Build Docker Image<br/>(api, phobert-svc, frontend)"]
        S4 --> S5["Push Registry"]
    end
    
    Repo -->|"Poll"| Jenkins
    Jenkins --> S1
    S5 --> Reg["Container Registry"]

    subgraph VPS["VPS LINUX"]
        Deploy["docker compose pull && up -d"]
        Health["Health check /health<br/>restart: unless-stopped"]
        Backup["Cron: mysqldump hằng ngày<br/>giữ 7 bản"]
    end

    Jenkins -->|"SSH deploy"| Deploy
    Reg --> Deploy
    Deploy --> Health
    Backup -->|"Đẩy bản sao lưu"| R2["Cloudflare R2"]
    Secrets["Secrets: biến môi trường<br/>và Jenkins Credentials (không commit)"] -.-> Deploy
```