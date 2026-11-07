# ĐẶC TẢ YÊU CẦU HỆ THỐNG

------------------------------------------------------------------------

## MỤC LỤC

1.  [Mục tiêu và phạm vi đặc tả](#1-mục-tiêu-và-phạm-vi-đặc-tả)
2.  [Các tác nhân hệ thống (System
    Actors)](#2-các-tác-nhân-hệ-thống-system-actors)
3.  [Đặc tả yêu cầu chức năng (Functional Requirements -
    FR)](#3-đặc-tả-yêu-cầu-chức-năng-functional-requirements---fr)
    - [3.1. Phân hệ Định danh và Phân quyền
      (`Identity Module`)](#31-phân-hệ-định-danh-và-phân-quyền-identity-module)
    - [3.2. Phân hệ Quản lý Khóa học
      (`Course Module`)](#32-phân-hệ-quản-lý-khóa-học-course-module)
    - [3.3. Phân hệ Quản trị Nội dung Học tập
      (`Content Module`)](#33-phân-hệ-quản-trị-nội-dung-học-tập-content-module)
    - [3.4. Phân hệ Học tập
      (`Learning Module`)](#34-phân-hệ-học-tập-learning-module)
    - [3.5. Phân hệ Đánh giá
      (`Assessment Module`)](#35-phân-hệ-đánh-giá-assessment-module)
    - [3.6. Phân hệ Khám phá
      (`Discovery Module`)](#36-phân-hệ-khám-phá-discovery-module)
    - [3.7. Phân hệ Hồ sơ cá nhân
      (`Profile Module`)](#37-phân-hệ-hồ-sơ-cá-nhân-profile-module)
    - [3.8. Phân hệ Thông báo
      (`Notification Module`)](#38-phân-hệ-thông-báo-notification-module)
    - [3.9. Phân hệ Kiểm duyệt
      (`Moderation Module`)](#39-phân-hệ-kiểm-duyệt-moderation-module)
    - [3.10. Phân hệ Trí tuệ nhân tạo
      (`AI Module`)](#310-phân-hệ-trí-tuệ-nhân-tạo-ai-module)
    - [3.11. Phân hệ Thanh toán
      (`Payment Module`)](#311-phân-hệ-thanh-toán-payment-module)
4.  [Ma trận phân quyền Moderator và Admin (RBAC
    Matrix)](#4-ma-trận-phân-quyền-moderator-và-admin-rbac-matrix)
5.  [Đặc tả yêu cầu phi chức năng (Non-Functional Requirements -
    NFR)](#5-đặc-tả-yêu-cầu-phi-chức-năng-non-functional-requirements---nfr)

------------------------------------------------------------------------

## 1. MỤC TIÊU VÀ PHẠM VI ĐẶC TẢ

Tài liệu mô tả các yêu cầu chức năng và những yêu cầu phi chức năng của
mười một module:

1.  **Identity Module:** Xác thực tài khoản, phân quyền và xác định
    quyền thao tác của người dùng.
2.  **Course Module:** Quản lý thông tin, giá, trạng thái, chế độ truy
    cập (Công khai, Riêng tư, Bảo vệ bằng passcode và Chỉ mình tôi),
    cộng tác viên, ghi danh và thống kê khóa học.
3.  **Content Module:** Tổ chức nội dung học tập, quản lý block, ngân
    hàng câu hỏi, cấu hình bài kiểm tra, phiên bản và tài nguyên đính
    kèm.
4.  **Learning Module:** Trang học tập, tiến độ, làm bài kiểm tra và bài
    tập, thảo luận và kiểm tra quyền truy cập học tập.
5.  **Assessment Module:** Kết quả và lịch sử làm bài, chấm tự luận,
    bảng điểm, chuẩn đầu ra, thống kê, đánh giá khóa học và xuất báo
    cáo.
6.  **Discovery Module:** Trang chủ, tìm kiếm, lọc, sắp xếp và xếp hạng
    khóa học.
7.  **Profile Module:** Hồ sơ cá nhân, quyền riêng tư, danh sách khóa
    học của người dùng và cài đặt giao diện.
8.  **Notification Module:** Tạo, gửi và quản lý thông báo trong ứng
    dụng, qua email và thông báo hệ thống.
9.  **Moderation Module:** Báo cáo, xử lý vi phạm, kiểm duyệt nội dung
    thuộc phạm vi kiểm duyệt, áp dụng chế tài theo quyền được cấp, audit
    log và quản lý Moderator.
10. **AI Module:** Tự động tạo câu hỏi và hỗ trợ kiểm duyệt nội dung.
11. **Payment Module:** Đơn hàng, thanh toán, ví, nạp tiền, hoàn tiền,
    doanh thu giảng viên, rút tiền và kiểm soát giao dịch.

Với mỗi phân hệ, phần chức năng được liệt kê chi tiết thành từng dòng
trong bảng; các quy tắc, trạng thái và phân quyền của phân hệ được mô tả
riêng ngay bên dưới bảng.

### 1.1. Quy ước mã yêu cầu

| Tiền tố  | Phân hệ                                   |
|:---------|:------------------------------------------|
| `FR-IDN` | Yêu cầu chức năng của Identity Module     |
| `FR-CRS` | Yêu cầu chức năng của Course Module       |
| `FR-CNT` | Yêu cầu chức năng của Content Module      |
| `FR-LRN` | Yêu cầu chức năng của Learning Module     |
| `FR-AST` | Yêu cầu chức năng của Assessment Module   |
| `FR-DSC` | Yêu cầu chức năng của Discovery Module    |
| `FR-PRF` | Yêu cầu chức năng của Profile Module      |
| `FR-NTF` | Yêu cầu chức năng của Notification Module |
| `FR-MOD` | Yêu cầu chức năng của Moderation Module   |
| `FR-AI`  | Yêu cầu chức năng của AI Module           |
| `FR-PAY` | Yêu cầu chức năng của Payment Module      |
| `NFR`    | Yêu cầu phi chức năng                     |

------------------------------------------------------------------------

## 2. CÁC TÁC NHÂN HỆ THỐNG (SYSTEM ACTORS)

| Tác nhân                           | Vai trò (Role)     | Trách nhiệm trong phạm vi tài liệu                                                                                                                                                                                                                                                                                                                                           |
|:-----------------------------------|:-------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Khách**                          | `Guest`            | Không cần đăng nhập; được xem Discovery và thông tin khóa học công khai; được đọc và sử dụng các nội dung/Block miễn phí, công khai theo phạm vi dành cho khách. Không được truy cập nội dung khóa học trả phí, chương VIP, Private, Protected, Only Me, tạm ẩn hoặc đã xóa; không có dữ liệu học tập cá nhân. Các thao tác cần định danh tài khoản được yêu cầu đăng nhập. |
| **Học viên**                       | `Student`          | Đăng ký, đăng nhập, ghi danh hoặc hủy ghi danh khóa học; truy cập nội dung khi đủ điều kiện; theo dõi tiến độ, đánh dấu bookmark, thảo luận; thực hiện bài kiểm tra và nộp bài tập; đánh giá khóa học đã ghi danh; tìm kiếm khóa học; mua khóa học, nạp tiền, yêu cầu hoàn tiền; gửi báo cáo vi phạm.                                                                        |
| **Giảng viên / Chủ khóa**          | `Course Owner`     | Tạo và quản lý khóa học; thiết lập giá và chế độ truy cập; quản lý cộng tác viên và học viên ghi danh; biên soạn nội dung, câu hỏi, bài kiểm tra; chấm tự luận và nhận xét; thiết lập bảng điểm và chuẩn đầu ra; xem thống kê và xuất báo cáo; duyệt câu hỏi do AI tạo; liên kết tài khoản ngân hàng và yêu cầu rút tiền.                                                    |
| **Giảng viên phụ / Cộng tác viên** | `Co-instructor`    | Chỉ được thực hiện các chức năng mà chủ khóa đã cấp trong từng khóa học; quyền được cấu hình theo nhóm chức năng, không mặc định kế thừa toàn bộ quyền của chủ khóa.                                                                                                                                                                                                         |
| **Moderator**                      | `Moderator`        | Xem và xử lý báo cáo vi phạm; duyệt/từ chối khóa học công khai hoặc có nội dung VIP trước khi xuất bản; ẩn/khôi phục khóa học; xóa bình luận vi phạm; cấm người dùng bình luận tạm thời; cấm giảng viên tạo khóa học tạm thời; khóa tài khoản tạm thời; xem audit log của chính mình. Không có quyền quản trị tài chính, phân quyền hệ thống hoặc xử lý các chế tài chỉ dành cho Admin. |
| **Admin**                          | `Admin`            | Quản trị toàn hệ thống; thực hiện các quyền của Moderator và các quyền quản lý người dùng, phân quyền, tài chính (duyệt hoàn tiền, duyệt rút tiền), xử lý vi phạm nghiêm trọng, giám sát, gửi thông báo hệ thống và cấu hình hệ thống.                                                                                                                                       |
| **Hệ thống / Backend**             | `System / Backend` | Thực hiện các xử lý hệ thống được đề cập trong tài liệu, chẳng hạn kiểm tra quyền thông qua cơ chế dùng chung, tiếp nhận lệnh hạn chế quyền, quản lý trạng thái ghi danh, tự động nộp bài khi hết giờ, tạo và gửi thông báo, nhận webhook, ghi sổ cái, và các xử lý của AI (tạo câu hỏi, gán nhãn nội dung vi phạm). Đây là thành phần xử lý, không phải vai trò người dùng. |
| **Cổng thanh toán**                | `Payment Gateway`  | Hệ thống bên ngoài (VNPay, MoMo, PayOS...) xử lý thanh toán và nạp tiền, gửi webhook/IPN về hệ thống.                                                                                                                                                                                                                                                                        |

------------------------------------------------------------------------

## 3. ĐẶC TẢ YÊU CẦU CHỨC NĂNG (FUNCTIONAL REQUIREMENTS - FR)

*(Mỗi phân hệ gồm bảng chức năng chi tiết; các quy tắc, trạng thái và
phân quyền của phân hệ được mô tả ngay bên dưới bảng)*

### 3.1. Phân hệ Định danh và Phân quyền (`Identity Module`)

| Mã YC         | Tên chức năng                      | Đặc tả chi tiết nghiệp vụ                           | Tác nhân             |
|:--------------|:-----------------------------------|:----------------------------------------------------|:---------------------|
| **FR-IDN-01** | **Đăng ký tài khoản**              | Đăng ký tài khoản bằng email và mật khẩu.           | Người dùng           |
| **FR-IDN-02** | **Xác minh email**                 | Xác minh email của tài khoản đã đăng ký.            | Người dùng           |
| **FR-IDN-03** | **Đăng nhập**                      | Đăng nhập vào hệ thống bằng tài khoản đã đăng ký.   | Người dùng           |
| **FR-IDN-04** | **Đăng xuất**                      | Đăng xuất khỏi hệ thống.                            | Người dùng           |
| **FR-IDN-05** | **Làm mới token (refresh token)**  | Hệ thống hỗ trợ cơ chế refresh token.               | Người dùng, Hệ thống |
| **FR-IDN-06** | **Đăng nhập bằng Google**          | Đăng nhập thông qua OAuth của Google.               | Người dùng           |
| **FR-IDN-07** | **Quên mật khẩu**                  | Hỗ trợ người dùng khi quên mật khẩu.                | Người dùng           |
| **FR-IDN-08** | **Đổi mật khẩu**                   | Cho phép người dùng đổi mật khẩu.                   | Người dùng           |
| **FR-IDN-09** | **Quản lý phiên đăng nhập**        | Quản lý các phiên đăng nhập của người dùng.         | Người dùng           |
| **FR-IDN-10** | **Đăng xuất khỏi tất cả thiết bị** | Cho phép người dùng đăng xuất khỏi tất cả thiết bị. | Người dùng           |

#### 3.1.1. Mô tả phân quyền (Authorization)

Hệ thống kết hợp **Role-Based Access Control (RBAC)** và kiểm tra quyền
theo tài nguyên. Không cấu hình permission riêng cho mọi chức năng; chỉ
tách permission đối với những chức năng cần giao quyền linh hoạt hoặc có
rủi ro cao.

1.  **Role:** Các vai trò có tài khoản gồm Học viên, Giảng viên, Moderator
    và Admin. Khách (`Guest`) là tác nhân chưa xác thực, không có quyền
    của các role có tài khoản và chỉ được dùng các chức năng công khai
    được nêu rõ trong tài liệu.
2.  **Permission theo chức năng có chọn lọc:** Chỉ áp dụng tại các khu
    vực cần thiết:
    - **Cộng tác viên:** Chủ khóa cấp/thu hồi quyền theo nhóm chức năng
      trong từng khóa học, ví dụ xem nội dung, tạo/sửa chương, quản lý
      câu hỏi, quản lý bài kiểm tra, chấm bài và xem thống kê. Cộng tác
      viên không mặc định có quyền quản lý giá, thanh toán, cộng tác
      viên khác hoặc xóa khóa học.
    - **Moderator:** Các quyền kiểm duyệt được gắn mặc định với vai trò
      Moderator, gồm xem và xử lý báo cáo vi phạm; duyệt/từ chối khóa học
      công khai hoặc khóa học có nội dung VIP trước khi xuất bản; ẩn/khôi
      phục khóa học; xóa bình luận vi phạm; cấm bình luận tạm thời; cấm
      giảng viên tạo khóa học tạm thời; và khóa tài khoản tạm thời. Không
      có cơ chế cấp permission kiểm duyệt riêng cho từng Moderator.
    - **Quyền quản trị nhạy cảm:** Thao tác tài chính, cấp/thu hồi role,
      khóa tài khoản vĩnh viễn, xóa vĩnh viễn và cấu hình hệ thống chỉ
      dành cho Admin.
3.  **Phân quyền theo tài nguyên:** Backend kiểm tra quan hệ giữa người
    dùng và tài nguyên, gồm chủ khóa, cộng tác viên được phân công, học
    viên có quyền học và chủ sở hữu dữ liệu cá nhân.
4.  **Policy / authorization handler dùng chung:** Identity cung cấp cơ
    chế kiểm tra quyền qua Contract công khai. Các module gọi cơ chế này
    tại backend/API, tránh tự xây dựng các quy tắc phân quyền không nhất
    quán.
5.  **Hạn chế quyền:** Moderation phát lệnh hạn chế; Identity ghi nhận
    loại hạn chế, phạm vi, thời hạn và lý do. Khi hết hạn, hệ thống tự
    động gỡ hạn chế nếu không có quyết định khác.
6.  **Trạng thái tài khoản:** Tối thiểu gồm Hoạt động, Bị khóa có thời
    hạn và Bị khóa vĩnh viễn. Tài khoản bị khóa phải bị chặn các API yêu
    cầu xác thực theo chính sách hệ thống.

**Thứ tự kiểm tra quyền:** trạng thái tài khoản và chế tài đang có hiệu
lực → vai trò/quyền chức năng → quyền trên tài nguyên. Riêng khóa học ở
chế độ Only Me, backend chỉ cho phép chủ khóa truy cập; vai trò Admin
hoặc Moderator không tạo ngoại lệ. Ẩn nút trên giao diện không thay thế
kiểm tra quyền tại backend.

**Quyền nền tảng của Moderator**

Moderator mặc định có các quyền sau, không cần Admin cấp permission
riêng cho từng tài khoản:

1.  Xem hàng đợi báo cáo trong phạm vi xử lý; chấp nhận hoặc từ chối báo
    cáo và bắt buộc nhập lý do.
2.  Tạm ẩn hoặc khôi phục khóa học theo quy trình xử lý vi phạm.
3.  Xóa bình luận vi phạm.
4.  Cấm người dùng bình luận tạm thời hoặc cấm giảng viên tạo khóa học
    tạm thời, kèm lý do và thời hạn.
5.  Khóa tài khoản tạm thời, kèm lý do và thời hạn.
6.  Duyệt hoặc từ chối khóa học công khai/khóa học có nội dung VIP
    trước khi xuất bản; không áp dụng với khóa học Only Me.
7.  Xem audit log các hành động do chính mình thực hiện.

Moderator không có quyền duyệt rút tiền, xem ví/doanh thu, hoàn tiền,
cấp/thu hồi role, quản lý danh sách Moderator, khóa tài khoản vĩnh viễn,
xóa vĩnh viễn dữ liệu, xem toàn bộ audit log hoặc sửa cấu hình hệ thống.

**Quyền của Admin**

Admin có toàn quyền quản trị hệ thống, bao gồm:

1.  Quản lý người dùng, role và danh sách Moderator.
2.  Thực hiện mọi chức năng kiểm duyệt và chế tài của Moderator.
3.  Thực hiện các thao tác chỉ dành cho Admin, bao gồm khóa tài khoản
    vĩnh viễn, xóa vĩnh viễn dữ liệu và xử lý các trường hợp vi phạm
    nghiêm trọng.
4.  Duyệt/từ chối hoàn tiền và rút tiền; xem doanh thu nền tảng; cấu
    hình tỷ lệ hoa hồng, coupon, gói Pro và đối soát.
5.  Xem toàn bộ audit log, dashboard và lịch sử xử lý của
    Moderator/Admin.
6.  Cấu hình quota AI, ngưỡng kiểm duyệt, thông báo broadcast và tham số
    hệ thống.

#### 3.1.2. Nguyên tắc phân tách Moderator và Admin

Lý do tách hai vai trò này, thay vì cho tất cả vào Admin:

1.  **Nguyên tắc quyền tối thiểu (Least Privilege):** Người xử lý báo
    cáo không cần thấy tiền hay quyền hệ thống. Nếu cấp thừa quyền, một
    tài khoản bị chiếm hoặc một người xấu có thể gây thiệt hại tối đa.
2.  **Giảm rủi ro tiền:** Các thao tác về tiền (rút, hoàn) có rủi ro cao
    nhất, chỉ số ít người đáng tin cậy được thao tác.
3.  **Phân chia trách nhiệm:** Người kiểm duyệt nội dung khác người
    duyệt tiền. Moderator xử lý nhẹ; việc nặng hoặc không thể hoàn tác
    (khóa vĩnh viễn, xóa vĩnh viễn) cần cấp cao hơn.
4.  **Mở rộng đội ngũ:** Muốn thuê thêm cộng tác viên kiểm duyệt thì
    phải có vai trò hạn chế để có thể giao việc.
5.  **Truy vết và kháng nghị:** Admin là cấp xem xét lại quyết định của
    Moderator; nếu ai cũng là Admin thì không còn người giám sát người.
6.  **Hạn chế sai sót:** Quyền nguy hiểm được giao cho ít người sẽ giảm
    nguy cơ xóa nhầm hoặc thao tác nhầm.

------------------------------------------------------------------------

### 3.2. Phân hệ Quản lý Khóa học (`Course Module`)

| Mã YC         | Tên chức năng                              | Đặc tả chi tiết nghiệp vụ                                                                                                                                                                                                             | Tác nhân                              |
|:--------------|:-------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------|
| **FR-CRS-01** | **Tạo khóa học**                           | Cho phép tạo khóa học mới. Thông tin khóa học gồm: tên, mô tả, ảnh bìa, tag, người tạo, cộng tác viên, passcode, ngày tạo và ngày cập nhật.                                                                                           | Giảng viên chủ khóa                   |
| **FR-CRS-02** | **Xem thông tin khóa học**                 | Cho phép xem thông tin khóa học theo quyền truy cập. Khách chỉ xem được thông tin công khai; việc đọc nội dung học tập phải đáp ứng điều kiện Public + Free theo `FR-LRN-17`.                                                                                                                | Khách, Học viên, Giảng viên, Cộng tác viên (theo quyền), Moderator, Admin |
| **FR-CRS-03** | **Chỉnh sửa thông tin khóa học**           | Cho phép chỉnh sửa thông tin khóa học.                                                                                                                                                                                                | Giảng viên chủ khóa                   |
| **FR-CRS-04** | **Xóa khóa học**                           | Chủ khóa có thể yêu cầu xóa khóa học theo cơ chế xóa mềm; khóa học chuyển sang trạng thái Đã xóa/đã ẩn và không còn xuất hiện với người dùng thông thường. Xóa vĩnh viễn chỉ Admin được thực hiện theo `NFR-14`.                      | Giảng viên chủ khóa                   |
| **FR-CRS-05** | **Thiết lập giá khóa học**                 | Thiết lập khóa học miễn phí hoặc trả phí (cần qua kiểm duyệt); giá tính bằng VND.                                                                                                                                                     | Giảng viên chủ khóa                   |
| **FR-CRS-06** | **Thay đổi giá khóa học**                  | Cho phép đổi giá khóa học; việc đổi giá không ảnh hưởng đến các đơn hàng cũ.                                                                                                                                                          | Giảng viên chủ khóa                   |
| **FR-CRS-07** | **Thiết lập hình thức bán**                | Hỗ trợ bán theo giá cả khóa học hoặc theo giá của từng chương VIP riêng.<br><br>Khóa học muốn bật VIP cần qua kiểm duyệt (xem `FR-MOD-13`).                                                                                           | Giảng viên chủ khóa                   |
| **FR-CRS-08** | **Quản lý trạng thái khóa học**            | Khóa học có các trạng thái được mô tả tại mục 3.2.1.<br><br>Việc ẩn hoặc khôi phục khóa học do Moderation thực hiện (xem `FR-MOD-08`, `FR-MOD-09`); không áp dụng với khóa học ở chế độ Only Me.                                                                                   | Giảng viên chủ khóa, Moderator, Admin |
| **FR-CRS-09** | **Thiết lập chế độ truy cập khóa học**     | Chủ khóa thiết lập chế độ truy cập cho khóa học. Các chế độ được mô tả tại mục 3.2.2; chế độ Chỉ mình tôi chỉ cho phép chính chủ khóa nhìn thấy và truy cập khóa học; kể cả Admin và Moderator cũng không được xem thông tin hoặc nội dung qua chức năng nghiệp vụ của ứng dụng. | Giảng viên chủ khóa                   |
| **FR-CRS-10** | **Thiết lập chế độ truy cập chương học**   | Thiết lập chế độ truy cập cho từng chương học, cấu hình riêng biệt với chế độ truy cập của khóa học. Các chế độ truy cập được mô tả tại mục 3.2.2.                                                                                    | Giảng viên chủ khóa                   |
| **FR-CRS-11** | **Thêm cộng tác viên**                     | Cho phép chủ khóa học thêm cộng tác viên/giảng viên phụ vào khóa học.                                                                                                                                                                 | Giảng viên chủ khóa                   |
| **FR-CRS-12** | **Xóa cộng tác viên**                      | Cho phép chủ khóa học xóa cộng tác viên/giảng viên phụ khỏi khóa học; toàn bộ quyền được cấp trong khóa học đó bị thu hồi.                                                                                                            | Giảng viên chủ khóa                   |
| **FR-CRS-13** | **Ghi danh tự do**                         | Học viên tự tham gia khóa học.<br><br>Ghi danh thể hiện ở nút bấm tham gia trong giao diện giới thiệu khóa học. Nút này chỉ để ghi nhận học viên có ghi danh với khóa học hay không, không đồng nghĩa với việc vào đọc ngay chương 1. | Học viên                              |
| **FR-CRS-14** | **Mời học viên**                           | Giảng viên gửi lời mời cho học viên; học viên chấp nhận lời mời để ghi danh (trạng thái Đã mời).                                                                                                                                      | Giảng viên chủ khóa, Học viên         |
| **FR-CRS-15** | **Duyệt yêu cầu tham gia**                 | Học viên gửi yêu cầu tham gia và chờ chủ khóa học duyệt (trạng thái Chờ duyệt, chỉ có khi khóa học ở chế độ Private).                                                                                                                 | Học viên, Giảng viên chủ khóa         |
| **FR-CRS-16** | **Ghi danh bằng mua khóa học**             | Học viên ghi danh thông qua việc mua khóa học.                                                                                                                                                                                        | Học viên                              |
| **FR-CRS-17** | **Hủy ghi danh**                           | Học viên tự hủy ghi danh (trạng thái Đã rời); hệ thống giữ tiến độ học tập.                                                                                                                                                           | Học viên                              |
| **FR-CRS-18** | **Thu hồi quyền học khi hoàn tiền**        | Khi phát sinh hoàn tiền, quyền học của học viên bị thu hồi (trạng thái Bị thu hồi).                                                                                                                                                   | Hệ thống                              |
| **FR-CRS-19** | **Xem danh sách học viên**                 | Cho phép chủ khóa học xem danh sách học viên theo các trạng thái ghi danh tại mục 3.2.3.                                                                                                                                              | Giảng viên chủ khóa                   |
| **FR-CRS-20** | **Xóa học viên khỏi khóa học**             | Chủ khóa học đưa học viên ra khỏi khóa học (trạng thái Bị xóa).                                                                                                                                                                       | Giảng viên chủ khóa                   |
| **FR-CRS-21** | **Thống kê cơ bản khóa học**               | Cung cấp thống kê cơ bản cho chủ khóa học, gồm: số học viên tham gia, số học viên đã hoàn thành, tỷ lệ hoàn thành, số thảo luận, số chương và số flashcard.                                                                           | Giảng viên chủ khóa                   |
| **FR-CRS-22** | **Phân quyền chức năng cho cộng tác viên** | Chủ khóa cấp, điều chỉnh hoặc thu hồi quyền thao tác của từng cộng tác viên theo nhóm chức năng trong khóa học hiện tại. Cộng tác viên chỉ được thao tác trong phạm vi quyền đã cấp; không được tự cấp/thu hồi quyền cho người khác, quản lý cộng tác viên khác, chuyển quyền sở hữu hoặc thực hiện quyền tài chính. Khi khóa học ở chế độ Only Me, cộng tác viên không được truy cập nội dung dù trước đó đã được cấp quyền. | Giảng viên chủ khóa                   |

#### 3.2.1. Các trạng thái khóa học

1.  **Đang cập nhật.**
2.  **Đã hoàn thành.**
3.  **Tạm dừng.**
4.  **Tạm ẩn:** Người dùng không xem hoặc không truy cập được khóa học.
5.  **Đã xóa:** Khóa học đã được xóa mềm và không hiển thị/không truy
    cập được với người dùng thông thường. Dữ liệu vẫn được giữ để phục
    hồi hoặc truy vết; xóa vĩnh viễn chỉ Admin thực hiện.

#### 3.2.2. Các chế độ truy cập

Chế độ truy cập được cấu hình tại khóa học; từng chương có thể có chế độ
truy cập riêng theo các lựa chọn phù hợp. Có bốn chế độ ở cấp khóa học:

1.  **Public (Công khai).**
2.  **Private (Riêng tư):** Chỉ người được mời, người đã ghi danh hoặc
    người được duyệt ghi danh mới được vào xem và tương tác.
3.  **Protected (Bảo vệ bằng passcode):** Dùng passcode để vào khóa học
    hoặc vào chương học.
4.  **Only Me (Chỉ mình tôi):** Chỉ chủ khóa học được nhìn thấy, truy
    cập và sử dụng khóa học. Quy tắc này áp dụng ở tầng ứng dụng cho
    mọi vai trò, bao gồm Admin và Moderator: không tài khoản nào khác
    được tìm thấy, xem thông tin, mở, đọc, tải xuống hoặc thao tác trên
    khóa học thông qua chức năng nghiệp vụ của ứng dụng. Khóa học không xuất hiện
    trong trang chủ, tìm kiếm, bộ lọc, danh sách đề xuất, bảng xếp hạng
    hoặc bất kỳ khu vực Discovery nào; không cho phép ghi danh hay cấp
    quyền truy cập cho cộng tác viên. Nội dung khóa học không thuộc phạm
    vi kiểm duyệt, quét hoặc xử lý chính sách, không được đưa vào hàng
    đợi kiểm duyệt và không được dùng làm nguồn RAG/gợi ý. Quyền quản trị
    kỹ thuật ngoài tầng ứng dụng không thuộc phạm vi quy tắc truy cập này.

**Quy tắc truy cập dành cho Khách (`Guest`):** Khách không cần đăng nhập
để xem Discovery và thông tin công khai của khóa học. Khách chỉ được đọc
nội dung khi khóa học ở chế độ Public và miễn phí, đồng thời chương học
cũng ở chế độ Public và miễn phí. Khách không được đọc khóa học trả phí,
chương VIP, hoặc nội dung Private, Protected, Only Me, tạm ẩn hay đã xóa.
Khách có thể sử dụng các Block công khai miễn phí có thể hoạt động mà
không cần định danh tài khoản, như xem nội dung, phát media, mở tài liệu
được phép, lật flashcard và thử tương tác với câu hỏi ngay trong phiên.
Kết quả/tiến độ của khách không được lưu vào hồ sơ học tập cá nhân. Các
thao tác gắn với danh tính hoặc dữ liệu tài khoản như bình luận, trả lời,
thích/bỏ thích, ghim/báo cáo bình luận, bookmark, ghi danh, nộp bài có
lưu kết quả và đánh giá khóa học yêu cầu đăng nhập.

#### 3.2.3. Các trạng thái ghi danh học viên

| Trạng thái     | Ý nghĩa                                                                                             | Được học? |
|:---------------|:----------------------------------------------------------------------------------------------------|:---------:|
| **Chờ duyệt**  | Học viên đã xin vào và chờ chủ khóa học duyệt; trạng thái này chỉ có khi khóa học ở chế độ Private. |   Không   |
| **Đã mời**     | Giảng viên đã mời; chờ học viên chấp nhận.                                                          |   Không   |
| **Đang học**   | Ghi danh hợp lệ.                                                                                    |    Có     |
| **Đã rời**     | Học viên tự hủy ghi danh; hệ thống giữ tiến độ học tập.                                             |   Không   |
| **Bị xóa**     | Chủ khóa học đưa học viên ra khỏi khóa học.                                                         |   Không   |
| **Bị thu hồi** | Quyền học bị thu hồi do hoàn tiền hoặc vi phạm.                                                     |   Không   |

------------------------------------------------------------------------

### 3.3. Phân hệ Quản trị Nội dung Học tập (`Content Module`)

| Mã YC         | Tên chức năng                                    | Đặc tả chi tiết nghiệp vụ                                                                                                                                                                                                                                                                                                                                                                                                   | Tác nhân                                                                   |
|:--------------|:-------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------------------------------------------------------|
| **FR-CNT-01** | **Tổ chức nội dung theo cấu trúc phân cấp**      | Nội dung khóa học được tổ chức theo cấu trúc **Course → Chapter → Block**.                                                                                                                                                                                                                                                                                                                                                  | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-03** | **Quản lý Block nội dung**                       | Hỗ trợ các loại Block được liệt kê tại mục 3.3.1. Khách chỉ được xem/sử dụng Block thuộc chương Public + Free; thao tác của khách không được lưu thành tiến độ hoặc kết quả học tập cá nhân.                                                                                                                                                                                                                       | Giảng viên, Giảng viên phụ; Học viên; Khách (chỉ nội dung Public + Free) |
| **FR-CNT-04** | **Xem trước ở chế độ lưu nháp**                  | Cho phép xem chương học hoặc bài kiểm tra hiển thị ở chế độ lưu nháp trước khi đăng tải.<br><br>Giao diện tạo Chapter và Content khác với giao diện đọc và tương tác của học viên.                                                                                                                                                                                                                                          | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-05** | **Quản lý ngân hàng câu hỏi theo khóa học**      | Mỗi khóa học có ngân hàng câu hỏi riêng. Mỗi câu hỏi được quản lý với các thông tin: tag (chủ đề, chương, kỹ năng...), độ khó, giải thích, loại câu hỏi/đáp án, điểm và trạng thái (xem mục 3.3.1).                                                                                                                                                                                                                         | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-06** | **Nhập câu hỏi từ Excel/CSV**                    | Cho phép nhập câu hỏi vào ngân hàng câu hỏi từ file Excel/CSV.                                                                                                                                                                                                                                                                                                                                                              | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-07** | **Xuất ngân hàng câu hỏi**                       | Cho phép xuất ngân hàng câu hỏi ra CSV/Excel.                                                                                                                                                                                                                                                                                                                                                                               | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-08** | **Lọc và xem danh sách câu hỏi**                 | Cho phép lọc câu hỏi để xem danh sách câu hỏi trong ngân hàng.                                                                                                                                                                                                                                                                                                                                                              | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-09** | **Xem thông tin sử dụng câu hỏi**                | Cho phép hiển thị thông tin sử dụng của từng câu hỏi: câu hỏi đang nằm trong bài kiểm tra nào, số lượt làm và tỷ lệ trả lời đúng.<br><br>Các thông tin này được đọc từ Assessment qua Contract.                                                                                                                                                                                                                             | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-10** | **Cấu hình câu hỏi trong bài kiểm tra**          | Cho phép cấu hình đáp án, giải thích, điểm và đảo thứ tự cho câu hỏi; dùng khi tạo bài kiểm tra từ ngân hàng câu hỏi hoặc từ câu hỏi thêm thủ công.<br><br>Cho phép chọn có hoặc không:<br>1. Đảo thứ tự đáp án ngẫu nhiên giữa các bài làm của từng học viên.<br>2. Đảo thứ tự câu hỏi ngẫu nhiên giữa các bài làm của từng học viên.                                                                                      | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-11** | **Thiết lập danh sách câu hỏi của bài kiểm tra** | Cho phép:<br>1. Thêm hoặc xóa câu hỏi thủ công, hoặc chọn câu hỏi từ ngân hàng câu hỏi (kèm điểm các câu và tùy chọn xáo trộn thứ tự tại `FR-CNT-10`).<br>2. Lấy ngẫu nhiên một số lượng câu hỏi trong ngân hàng câu hỏi theo các ràng buộc thuộc tính được thiết lập.<br>3. Sắp xếp thứ tự câu hỏi thủ công.<br><br>Khi học viên đã nhận đề, thứ tự câu hỏi và đáp án được giữ cố định nếu học viên vô tình tải lại trang. | Giảng viên, Giảng viên phụ, Hệ thống                                       |
| **FR-CNT-12** | **Cấu hình thông tin bài kiểm tra**              | Cho phép thiết lập:<br>1. Tên bài và mô tả.<br>2. Thời gian mở/đóng bài kiểm tra (cài đặt hẹn giờ tự đăng) hoặc thời gian làm bài (đăng ngay khi nhấn đăng tải).<br>3. Số lần được phép làm bài.<br>4. Điểm tối đa và ngưỡng điểm đạt.                                                                                                                                                                                      | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-13** | **Liên kết điểm chuẩn đầu ra**                   | Bình thường, hệ thống chỉ lưu điểm của học viên ở bài kiểm tra đó. Hệ thống chỉ ghi nhận điểm vào khu vực tính điểm đầu ra riêng theo thiết lập cá nhân khi:<br>1. Giảng viên/người quản lý chủ động lấy điểm của bài kiểm tra đó làm điểm đầu ra; hoặc<br>2. Đã liên kết điểm bài kiểm tra với điểm đầu ra ngay từ đầu.                                                                                                    | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-14** | **Cấu hình hiển thị kết quả**                    | Cho phép thiết lập thời điểm hiển thị kết quả:<br>1. Ngay sau khi chọn đáp án.<br>2. Ngay sau khi nộp.<br>3. Ngay sau khi tới giờ đóng bài.<br>4. Chấm sau.                                                                                                                                                                                                                                                                 | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-15** | **Thiết lập điều kiện truy cập bài kiểm tra**    | Cho phép đặt điều kiện truy cập bài kiểm tra, gồm mật khẩu bài thi và điều kiện tiên quyết.                                                                                                                                                                                                                                                                                                                                 | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-16** | **Thiết lập ngoại lệ cho học viên**              | Cho phép thêm học viên ngoại lệ và chọn kiểu ngoại lệ: thêm thời gian, thêm lượt làm hoặc dời hạn cho một số học viên được chỉ định.                                                                                                                                                                                                                                                                                        | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-17** | **Lưu nháp và đăng tải nội dung**                | Hỗ trợ lưu nháp và đăng tải nội dung.<br><br>Hệ thống không lưu tự động; phiên bản lưu nháp được lưu khi người dùng chủ động thao tác lưu.                                                                                                                                                                                                                                                                                  | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-18** | **Xem lịch sử chỉnh sửa và khôi phục phiên bản** | Cho phép xem lịch sử chỉnh sửa và khôi phục phiên bản trước đó.                                                                                                                                                                                                                                                                                                                                                             | Giảng viên, Giảng viên phụ                                                 |
| **FR-CNT-19** | **Quản lý tài nguyên đính kèm**                  | Hỗ trợ tải lên tài nguyên đính kèm; quản lý dung lượng và định dạng của tài nguyên.                                                                                                                                                                                                                                                                                                                                         | Giảng viên, Giảng viên phụ                                                 |

#### 3.3.1. Các loại Block, loại câu hỏi và thuộc tính câu hỏi

**Các loại Block nội dung**

1.  Rich text.
2.  Hình ảnh.
3.  Video.
4.  Âm thanh.
5.  File đính kèm.
6.  Markdown
7.  Flashcard.
8.  Câu hỏi.
9.  Bài tập: có mô tả, chỗ nộp, giới hạn dung lượng, thời hạn nộp và
    điểm nếu có.

**Các loại câu hỏi**

1.  Trắc nghiệm một hoặc nhiều đáp án.
2.  Đúng/Sai.
3.  Điền khuyết.
4.  Ghép cặp.
5.  Tự luận ngắn.
6.  Tự luận.

**Độ khó của câu hỏi** (tùy chọn) có thể biểu diễn theo một trong ba
cách: tự sửa theo mô tả dễ - khó; theo mức từ 1 đến 5; hoặc theo mức
Nhận biết, Thông hiểu, Vận dụng, Vận dụng cao.

**Trạng thái câu hỏi** gồm Nháp, Sẵn sàng và Lưu trữ. Chỉ câu hỏi có
trạng thái Sẵn sàng trong ngân hàng câu hỏi mới được thêm vào bài thi.

------------------------------------------------------------------------

### 3.4. Phân hệ Học tập (`Learning Module`)

| Mã YC         | Tên chức năng                                  | Đặc tả chi tiết nghiệp vụ                                                                                                                                               | Tác nhân             |
|:--------------|:-----------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------|
| **FR-LRN-01** | **Điều hướng giữa các chương và tiếp tục học** | Học viên điều hướng giữa các chương và tiếp tục học theo tiến độ đã lưu. Khách được điều hướng và đọc các chương Public + Free nhưng không có chức năng tiếp tục từ tiến độ cá nhân đã lưu. | Học viên, Khách (chỉ Public + Free) |
| **FR-LRN-02** | **Đánh dấu bookmark**                          | Học viên đánh dấu bookmark tại một chương cụ thể của một khóa học. Mỗi khóa học chỉ có một bookmark. Bookmark được hiển thị ở phần danh sách bookmark của cá nhân.      | Học viên             |
| **FR-LRN-03** | **Theo dõi tiến độ học tập**                   | Hiển thị phần trăm hoàn thành theo từng chương và theo khóa học, cùng lần học gần nhất.                                                                                 | Học viên             |
| **FR-LRN-04** | **Bắt đầu làm bài kiểm tra**                   | Học viên bắt đầu làm bài kiểm tra.                                                                                                                                      | Học viên             |
| **FR-LRN-05** | **Theo dõi câu hỏi đã làm và chưa làm**        | Trong khi làm bài, học viên theo dõi được câu đã làm và câu chưa làm.                                                                                                   | Học viên             |
| **FR-LRN-06** | **Theo dõi thời gian làm bài**                 | Trong khi làm bài, học viên theo dõi được thời gian.                                                                                                                    | Học viên             |
| **FR-LRN-07** | **Truy cập trực tiếp câu hỏi**                 | Học viên truy cập trực tiếp câu hỏi thông qua danh sách điều hướng.                                                                                                     | Học viên             |
| **FR-LRN-08** | **Nộp bài kiểm tra**                           | Học viên chủ động nộp bài, hoặc hệ thống tự động nộp khi hết giờ.                                                                                                       | Học viên, Hệ thống   |
| **FR-LRN-09** | **Làm và nộp bài tập**                         | Đối với bài tập, hệ thống hỗ trợ tự lưu và nộp bài.                                                                                                                     | Học viên, Hệ thống   |
| **FR-LRN-10** | **Bình luận**                                  | Bình luận theo chương hoặc theo khóa học; hiển thị thời gian đăng bình luận.                                                                                            | Học viên, Giảng viên |
| **FR-LRN-11** | **Trả lời bình luận**                          | Trả lời bình luận, lồng nhau một cấp.                                                                                                                                   | Học viên, Giảng viên |
| **FR-LRN-12** | **Thích và bỏ thích bình luận**                | Thích và bỏ thích bình luận.                                                                                                                                            | Học viên, Giảng viên |
| **FR-LRN-13** | **Sửa và xóa bình luận của mình**              | Người đăng sửa hoặc xóa bình luận của chính mình.                                                                                                                       | Học viên, Giảng viên |
| **FR-LRN-14** | **Ghim bình luận**                             | Cho phép ghim bình luận.                                                                                                                                                | Học viên, Giảng viên |
| **FR-LRN-15** | **Báo cáo bình luận**                          | Cho phép báo cáo bình luận (xem `FR-MOD-01`).                                                                                                                           | Học viên, Giảng viên |
| **FR-LRN-16** | **Kiểm tra quyền truy cập học tập**            | Với học viên, chỉ cho phép thực hiện hoạt động học tập có ghi nhận danh tính/kết quả khi có quyền ghi danh hợp lệ; với khóa học trả phí, học viên phải đã mua khóa học. Các hình thức ghi danh xem tại `FR-CRS-13` đến `FR-CRS-16`. Quyền đọc công khai miễn phí của Khách được quy định riêng tại `FR-LRN-17`. | Học viên, Hệ thống   |
| **FR-LRN-17** | **Truy cập nội dung với tư cách Khách**         | Không yêu cầu đăng nhập để xem Discovery và đọc khóa học/chương học khi cả khóa học và chương đều Public + Free. Khách được sử dụng các Block công khai miễn phí không yêu cầu định danh hoặc lưu trạng thái cá nhân (ví dụ xem nội dung, phát media, mở tài liệu được phép, lật flashcard và thử trả lời câu hỏi trong phiên hiện tại). Không cấp quyền với khóa học trả phí, chương VIP, Private, Protected, Only Me, tạm ẩn hoặc đã xóa; không lưu tiến độ, bookmark, điểm, bài nộp hoặc kết quả vào hồ sơ cá nhân. Các thao tác xã hội cần định danh tài khoản được quy định là yêu cầu đăng nhập. | Khách, Hệ thống |

------------------------------------------------------------------------

### 3.5. Phân hệ Đánh giá (`Assessment Module`)

| Mã YC         | Tên chức năng                                 | Đặc tả chi tiết nghiệp vụ                                                                                                          | Tác nhân             |
|:--------------|:----------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------|:---------------------|
| **FR-AST-01** | **Lưu kết quả và lịch sử làm bài**            | Lưu kết quả từng lần làm bài kiểm tra và lịch sử làm bài.                                                                          | Hệ thống             |
| **FR-AST-02** | **Lưu điểm cao nhất, gần nhất và trung bình** | Lưu điểm cao nhất, điểm gần nhất và điểm trung bình vào hệ thống, gắn với từng khóa học và từng học viên riêng.                    | Hệ thống             |
| **FR-AST-03** | **Chấm tay câu tự luận**                      | Giảng viên chấm tay các câu tự luận.                                                                                               | Giảng viên           |
| **FR-AST-04** | **Nhận xét của giảng viên**                   | Giảng viên ghi nhận xét. Nhận xét được hiển thị dưới bài làm hoặc ở thanh tab bar của bài làm của học viên.                        | Giảng viên, Học viên |
| **FR-AST-05** | **Bảng điểm theo học viên**                   | Hiển thị bảng điểm của học viên theo các chuẩn đầu ra của khóa học.                                                                | Giảng viên, Học viên |
| **FR-AST-06** | **Bảng điểm theo bài kiểm tra**               | Hiển thị bảng điểm riêng của từng bài kiểm tra.                                                                                    | Giảng viên, Học viên |
| **FR-AST-07** | **Thiết lập quy tắc tính điểm tổng kết**      | Thiết lập mặc định cho khóa học: quy tắc tính điểm tổng kết.<br><br>Việc thiết lập bảng điểm thuộc Assessment, không thuộc Course. | Giảng viên chủ khóa  |
| **FR-AST-08** | **Thiết lập ngưỡng đạt**                      | Thiết lập mặc định cho khóa học: ngưỡng đạt.                                                                                       | Giảng viên chủ khóa  |
| **FR-AST-09** | **Thiết lập xếp loại học lực**                | Thiết lập xếp loại học lực theo các mức trong thang điểm: trượt, yếu, kém, khá, giỏi, xuất sắc; hoặc F/D/C/B/A; hoặc tùy biến.     | Giảng viên chủ khóa  |
| **FR-AST-10** | **Định nghĩa chuẩn đầu ra**                   | Cho phép người dùng tự thiết lập định nghĩa chuẩn đầu ra với tên chuẩn (các nhãn như PLO, CLO).                                    | Giảng viên chủ khóa  |
| **FR-AST-11** | **Cấu hình phân cấp chuẩn đầu ra**            | Số tầng phân cấp không giới hạn, nhờ cấu hình đệ quy dạng cây (Tree Node).                                                         | Giảng viên chủ khóa  |
| **FR-AST-12** | **Tính chi tiết điểm theo rubric**            | Cho phép tính chi tiết điểm theo rubric.                                                                                           | Giảng viên chủ khóa  |
| **FR-AST-13** | **Thiết lập ngưỡng đạt cho từng mục tiêu**    | Cho phép tùy chọn ngưỡng đạt cho từng mục tiêu.                                                                                    | Giảng viên chủ khóa  |
| **FR-AST-14** | **Thống kê dành cho giảng viên**              | Cung cấp thống kê: phân bố điểm, câu hỏi khó/dễ và tỷ lệ hoàn thành theo chuẩn đầu ra.                                             | Giảng viên           |
| **FR-AST-15** | **Đánh giá khóa học**                         | Chấm sao và gửi nhận xét cho khóa học. Chỉ học viên đã ghi danh mới đánh giá được.                                                 | Học viên đã ghi danh |
| **FR-AST-16** | **Trả lời đánh giá**                          | Cho phép trả lời đánh giá của học viên.                                                                                            | Giảng viên           |
| **FR-AST-17** | **Hiển thị điểm đánh giá trung bình**         | Hiển thị điểm đánh giá trung bình của khóa học.                                                                                    | Hệ thống             |
| **FR-AST-18** | **Xuất báo cáo**                              | Hỗ trợ xuất báo cáo ra Excel hoặc PDF.                                                                                             | Giảng viên chủ khóa  |

------------------------------------------------------------------------

### 3.6. Phân hệ Khám phá (`Discovery Module`)

| Mã YC         | Tên chức năng                                     | Đặc tả chi tiết nghiệp vụ                                                                                                                                                                                                                                        | Tác nhân   |
|:--------------|:--------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------|
| **FR-DSC-01** | **Hiển thị khóa học mới cập nhật trên trang chủ** | Trang chủ hiển thị các khóa học mới cập nhật đủ điều kiện công khai.                                                                                                                                                                                            | Người dùng, Khách |
| **FR-DSC-02** | **Hiển thị khóa học đề xuất trên trang chủ**      | Trang chủ hiển thị các khóa học đề xuất đủ điều kiện công khai.                                                                                                                                                                                                 | Người dùng, Khách |
| **FR-DSC-03** | **Hiển thị khóa học đang học dở trên trang chủ**  | Trang chủ hiển thị các khóa học học viên đang học dở.                                                                                                                                                                                                            | Học viên   |
| **FR-DSC-04** | **Tìm kiếm khóa học**                             | Tìm kiếm theo tên khóa học và theo giảng viên trong phạm vi dữ liệu được phép công khai.                                                                                                                                                                         | Người dùng, Khách |
| **FR-DSC-05** | **Lịch sử tìm kiếm**                              | Lưu và hiển thị lịch sử tìm kiếm.                                                                                                                                                                                                                                | Người dùng |
| **FR-DSC-06** | **Lọc theo tag**                                  | Lọc danh sách khóa học theo tag trong phạm vi dữ liệu được phép công khai.                                                                                                                                                                                       | Người dùng, Khách |
| **FR-DSC-08** | **Lọc theo miễn phí/trả phí và khoảng giá**       | Lọc theo khóa học miễn phí hoặc trả phí; với khóa học trả phí, lọc thêm theo khoảng giá.                                                                                                                                                                         | Người dùng, Khách |
| **FR-DSC-09** | **Lọc theo chế độ truy cập**                      | Lọc danh sách khóa học theo chế độ truy cập trong phạm vi thông tin được phép công khai.                                                                                                                                                                        | Người dùng, Khách |
| **FR-DSC-10** | **Lọc theo trạng thái khóa học**                  | Lọc danh sách khóa học theo trạng thái khóa học trong phạm vi thông tin được phép công khai.                                                                                                                                                                    | Người dùng, Khách |
| **FR-DSC-11** | **Sắp xếp khóa học**                              | Hỗ trợ sắp xếp theo:<br>1. Mới cập nhật.<br>2. Mới ra mắt (tính từ khóa có 1 chapter trở đi, theo thời gian gần nhất trở về trước).<br>3. Số lượt đánh giá.<br>4. Số lượt đề cử.<br>5. Số học viên.<br>6. Lượt bình luận.                                        | Người dùng, Khách |
| **FR-DSC-12** | **Xếp hạng Top 10 khóa học**                      | Hiển thị bảng xếp hạng Top 10 khóa học theo tuần này, tháng này hoặc toàn thời gian, gồm: khóa học có doanh thu cao nhất, nhiều học viên nhất, nhiều lượt đánh giá nhất và nhiều lượt đề cử nhất. Không xây dựng bảng xếp hạng Top giảng viên hoặc Top học viên. | Người dùng, Khách |

#### 3.6.1. Quy tắc hiển thị khóa học

Danh sách khám phá chỉ hiển thị khóa học đủ điều kiện công khai theo
chính sách hiển thị. Khách được xem Discovery mà không cần đăng nhập;
khách có thể xem thông tin khóa học công khai nhưng chỉ đọc nội dung khi
cả khóa học và chương đều Public + Free. Khóa học Only Me, tạm ẩn hoặc
đã xóa không được hiển thị trong bất kỳ kết quả Discovery nào. Khóa học
Private/Protected chỉ hiển thị thông tin ở mức được chủ khóa cho phép;
nội dung học tập vẫn phải qua kiểm tra quyền truy cập.

------------------------------------------------------------------------

### 3.7. Phân hệ Hồ sơ cá nhân (`Profile Module`)

| Mã YC         | Tên chức năng                          | Đặc tả chi tiết nghiệp vụ                                                                                                                                | Tác nhân   |
|:--------------|:---------------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------|
| **FR-PRF-01** | **Cập nhật tên hiển thị**              | Cho phép người dùng đặt và cập nhật tên hiển thị.                                                                                                        | Người dùng |
| **FR-PRF-02** | **Cập nhật avatar**                    | Cho phép người dùng đặt và cập nhật avatar.                                                                                                              | Người dùng |
| **FR-PRF-03** | **Cập nhật giới thiệu**                | Cho phép người dùng viết phần giới thiệu.<br><br>Mặc định, trang hồ sơ công khai hiển thị thông tin giới thiệu người dùng gia nhập hệ thống từ ngày nào. | Người dùng |
| **FR-PRF-04** | **Thiết lập quyền riêng tư**           | Cho phép ẩn hoặc hiện khóa học và thành tích.                                                                                                            | Người dùng |
| **FR-PRF-05** | **Xem danh sách khóa học của cá nhân** | Hiển thị danh sách khóa đã ghi danh, đã tạo và đã hoàn thành.                                                                                            | Người dùng |
| **FR-PRF-06** | **Trang hồ sơ công khai**              | Cung cấp trang hồ sơ công khai của người dùng.                                                                                                           | Người dùng |
| **FR-PRF-07** | **Cài đặt giao diện**                  | Cho phép người dùng cài đặt giao diện.                                                                                                                   | Người dùng |
| **FR-PRF-08** | **Xem số dư ví và lịch sử đơn**        | Hiển thị số dư ví và lịch sử đơn hàng; dữ liệu chỉ đọc từ Payment.                                                                                       | Người dùng |

------------------------------------------------------------------------

### 3.8. Phân hệ Thông báo (`Notification Module`)

| Mã YC         | Tên chức năng                      | Đặc tả chi tiết nghiệp vụ                                                                                                                                                                                                                                                  | Tác nhân             |
|:--------------|:-----------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------|
| **FR-NTF-01** | **Tạo thông báo từ domain event**  | Tạo thông báo từ các domain event, gồm: ghi danh, bình luận, kết quả báo cáo (đồng ý hoặc từ chối), điểm, nạp/mua/hoàn/rút tiền, chương mới...<br><br>Thông báo được gửi sau khi nghiệp vụ chính đã hoàn thành; lỗi gửi thông báo không được làm rollback nghiệp vụ chính. | Hệ thống             |
| **FR-NTF-02** | **Thông báo trong ứng dụng**       | Lưu thông báo vào cơ sở dữ liệu và hiển thị ở biểu tượng chuông. Kênh này dùng cho mọi thông báo.                                                                                                                                                                          | Hệ thống, Người dùng |
| **FR-NTF-03** | **Thông báo qua email**            | Gửi thông báo qua email cho các trường hợp: xác minh, hoàn tiền, thanh toán.                                                                                                                                                                                               | Hệ thống             |
| **FR-NTF-04** | **Xem danh sách thông báo**        | Hiển thị danh sách thông báo của người dùng.                                                                                                                                                                                                                               | Người dùng           |
| **FR-NTF-05** | **Đánh dấu đã đọc**                | Cho phép đánh dấu đã đọc từng thông báo hoặc tất cả thông báo.                                                                                                                                                                                                             | Người dùng           |
| **FR-NTF-06** | **Xóa thông báo**                  | Cho phép người dùng xóa thông báo.                                                                                                                                                                                                                                         | Người dùng           |
| **FR-NTF-08** | **Thông báo hệ thống (broadcast)** | Admin gửi thông báo hệ thống tới người dùng.                                                                                                                                                                                                                               | Admin                |

------------------------------------------------------------------------

### 3.9. Phân hệ Kiểm duyệt (`Moderation Module`)

| Mã YC         | Tên chức năng                            | Đặc tả chi tiết nghiệp vụ                                                                                                                                                                                                                                                                        | Tác nhân                   |
|:--------------|:-----------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------------|
| **FR-MOD-01** | **Gửi báo cáo vi phạm**                  | Người dùng gửi báo cáo khóa học hoặc bình luận có dấu hiệu vi phạm mà mình có quyền truy cập (chọn lý do, nhập mô tả, đính kèm ảnh/link bằng chứng). Khóa học Only Me không phải đối tượng báo cáo từ tài khoản khác.                                                                                                                                                                       | Học viên, Giảng viên       |
| **FR-MOD-02** | **Chống báo cáo spam**                   | Hệ thống tự động chặn gửi nhiều báo cáo trùng lặp từ một tài khoản lên cùng một đối tượng trong thời gian ngắn.                                                                                                                                                                                  | Hệ thống                   |
| **FR-MOD-03** | **Quản lý hàng đợi báo cáo**             | Gom toàn bộ báo cáo vi phạm hợp lệ vào danh sách chờ; hỗ trợ lọc theo mức độ ưu tiên, loại đối tượng và trạng thái xử lý.                                                                                                                                                                        | Moderator, Admin           |
| **FR-MOD-04** | **Xử lý báo cáo vi phạm**                | Kiểm duyệt viên thẩm định nội dung; đưa ra quyết định: chấp nhận (xác nhận vi phạm) hoặc từ chối kèm lý do bắt buộc.                                                                                                                                                                             | Moderator, Admin           |
| **FR-MOD-05** | **Gửi thông báo kết quả**                | Tự động gửi thông báo kết quả giải quyết và lý do cho cả người báo cáo và người bị báo cáo qua `Notification Module`.                                                                                                                                                                            | Hệ thống                   |
| **FR-MOD-06** | **Xóa bình luận vi phạm**                | Xóa trực tiếp bình luận khiếm nhã, thù địch hoặc spam trên hệ thống.                                                                                                                                                                                                                             | Moderator, Admin           |
| **FR-MOD-07** | **Xóa khóa học vi phạm**                 | Xóa hoàn toàn khóa học vi phạm quy chuẩn nghiêm trọng (cần Admin xác nhận thao tác).                                                                                                                                                                                                             | Admin                      |
| **FR-MOD-08** | **Tạm ẩn khóa học**                      | Tạm ẩn khóa học vi phạm nhẹ để chờ chỉnh sửa; lưu lý do tạm ẩn. Khóa học tạm ẩn sẽ không xuất hiện trên mục tìm kiếm.                                                                                                                                                                            | Moderator, Admin           |
| **FR-MOD-09** | **Khôi phục khóa học**                   | Mở lại khóa học về trạng thái bình thường sau khi chủ khóa sửa đạt yêu cầu, hoặc tự động mở khi hết thời hạn phạt.                                                                                                                                                                               | Moderator, Admin, Hệ thống |
| **FR-MOD-10** | **Hạn chế quyền người dùng**             | Ban hành lệnh phạt tạm thời (cấm bình luận, cấm tạo khóa học) kèm thời hạn; gửi lệnh sang `Identity Module` để cập nhật.                                                                                                                                                                         | Moderator, Admin           |
| **FR-MOD-11** | **Khóa tài khoản ngắn hạn**              | Khóa đăng nhập tài khoản có thời hạn kèm lý do vi phạm; tự động kích hoạt đóng băng ví tiền sang `Payment Module`.                                                                                                                                                                               | Moderator, Admin           |
| **FR-MOD-12** | **Khóa tài khoản vĩnh viễn**             | Vô hiệu hóa vĩnh viễn tài khoản vi phạm đặc biệt nghiêm trọng. Chỉ Admin mới có quyền thực hiện.                                                                                                                                                                                                 | Admin                      |
| **FR-MOD-13** | **Kiểm duyệt khóa học công khai / VIP**  | Khóa học công khai hoặc khóa học muốn bật tính năng bán VIP phải được Moderator hoặc Admin duyệt nội dung trước khi xuất bản. Khóa học Only Me không thuộc bất kỳ quy trình kiểm duyệt, quét hoặc xử lý chính sách nào, dù tự động hay thủ công. | Moderator, Admin           |
| **FR-MOD-14** | **Lịch sử kiểm duyệt (Audit Log)**       | Ghi log bất biến cho mọi thao tác xử lý: người thực hiện, thời gian, đối tượng, hành động và lý do giải trình.                                                                                                                                                                                   | Hệ thống                   |
| **FR-MOD-15** | **Xem nhật ký kiểm duyệt cá nhân**       | Cho phép Moderator tra cứu lại lịch sử các thao tác kiểm duyệt do chính mình đã thực hiện.                                                                                                                                                                                                       | Moderator                  |
| **FR-MOD-16** | **Giám sát toàn diện nhật ký**           | Cho phép Admin xem toàn bộ Audit Log của tất cả Moderator và Admin trong hệ thống.                                                                                                                                                                                                               | Admin                      |
| **FR-MOD-17** | **Dashboard kiểm duyệt**                 | Hiển thị tổng quan: số báo cáo chờ xử lý, số khóa học chờ duyệt, danh sách tài khoản đang bị chế tài.                                                                                                                                                                                            | Moderator, Admin           |
| **FR-MOD-18** | **Quản lý danh sách Moderator**          | Admin cấp quyền, phân công hoặc thu hồi vai trò Moderator đối với các tài khoản.                                                                                                                                                                                                                 | Admin                      |

#### 3.9.1. Quy trình xử lý vi phạm và luồng giao tiếp

1.  **Tiếp nhận & Cách ly:** Khi nhận báo cáo từ người dùng hoặc cảnh
    báo tự động từ `AI Module`, nội dung được đưa vào hàng đợi kiểm
    duyệt tập trung.
2.  **Xử lý:** Moderator thẩm định nội dung khách quan và bắt buộc phải
    nhập lý do khi đưa ra quyết định xử lý.
3.  **Thực thi liên module:**
    - Lệnh phạt tài khoản phát sự kiện sang `Identity Module` để cập
      nhật trạng thái hạn chế quyền.
    - Nếu khóa tài khoản, hệ thống tự động thông báo sang
      `Payment Module` để đóng băng số dư ví.
    - Khóa học bị ẩn/xóa sẽ được đồng bộ sang `Course Module` và
      `Discovery Module` để gỡ bỏ khỏi giao diện người dùng.

------------------------------------------------------------------------

### 3.10. Phân hệ Trí tuệ nhân tạo (`AI Module`)

| Mã YC        | Tên chức năng                                     | Đặc tả chi tiết nghiệp vụ                                                                                                                       | Tác nhân             |
|:-------------|:--------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------|:---------------------|
| **FR-AI-01** | **Tự động sinh câu hỏi trắc nghiệm (Quiz)**       | Đọc nội dung văn bản bài học và tự động tạo câu hỏi trắc nghiệm theo số lượng và độ khó yêu cầu.                                                | Giảng viên, Hệ thống |
| **FR-AI-02** | **Tự động sinh thẻ ghi nhớ (Flashcard)**          | Trích xuất các định nghĩa, thuật ngữ cốt lõi từ bài học để tạo bộ flashcard 2 mặt (thuật ngữ - giải thích).                                     | Giảng viên, Hệ thống |
| **FR-AI-03** | **Duyệt câu hỏi AI (Human-in-the-loop)**          | Nội dung do AI tạo luôn ở trạng thái nháp (`Draft`); giảng viên bắt buộc phải xem trước, chỉnh sửa và bấm duyệt trước khi xuất bản.             | Giảng viên           |
| **FR-AI-04** | **Tóm tắt nội dung bài học**                      | Tóm tắt cô đọng các ý chính và từ khóa quan trọng của từng chương học hoặc trang bài đọc.                                                       | Giảng viên, Học viên |
| **FR-AI-05** | **Gợi ý dàn ý khóa học**                          | Gợi ý khung sườn cấu trúc các chương và bài học dựa trên tiêu đề và mô tả mục tiêu của giảng viên.                                              | Giảng viên           |
| **FR-AI-06** | **Trợ lý học tập theo ngữ cảnh (RAG)**            | Trả lời câu hỏi thắc mắc của học viên dựa trên tài liệu bài giảng của khóa học, kèm trích dẫn rõ tên chương/trang nguồn.                        | Học viên             |
| **FR-AI-07** | **Rào chắn chống ảo giác**                        | Nếu câu hỏi nằm ngoài nội dung tài liệu khóa học, AI bắt buộc từ chối suy đoán và hướng dẫn hỏi giảng viên tại phần Thảo luận.                  | Hệ thống             |
| **FR-AI-08** | **Gợi ý chấm bài tự luận**                        | Phân tích bài làm của học viên so với đáp án mẫu; đưa ra gợi ý điểm số và nhận xét để giảng viên tham khảo.                                     | Giảng viên, Hệ thống |
| **FR-AI-09** | **Phát hiện nội dung vi phạm chính sách**         | Sử dụng mô hình xử lý ngôn ngữ tự nhiên Fine-tune cục bộ để tự động quét bình luận/khóa học; gắn cờ vi phạm và chuyển sang `Moderation Module`. | Hệ thống             |
| **FR-AI-10** | **Gợi ý khóa học cá nhân hóa**                    | Phân tích lịch sử học tập và sở thích của học viên để đề xuất khóa học phù hợp cho `Discovery Module`.                                          | Hệ thống             |
| **FR-AI-11** | **Định tuyến mô hình thông minh (Smart Routing)** | Câu hỏi dễ/tra cứu nhanh chuyển cho mô hình nhỏ chi phí thấp; câu hỏi phân tích phức tạp chuyển cho mô hình lớn.                                | Hệ thống             |
| **FR-AI-12** | **Bộ nhớ đệm ngữ nghĩa (Semantic Cache)**         | Lưu kết quả các câu hỏi phổ biến; tự động trả lời từ bộ nhớ đệm nếu gặp câu hỏi tương tự mà không tốn phí gọi API.                              | Hệ thống             |
| **FR-AI-13** | **Kiểm soát hạn mức gọi AI (Quota Guard)**        | Kiểm tra hạn ngạch gọi AI hàng ngày theo gói tài khoản (Free, Pro, Credit); chặn và nhắc nâng cấp khi hết lượt.                                 | Hệ thống             |
| **FR-AI-14** | **Xử lý nền bất đồng bộ**                         | Các tác vụ tạo câu hỏi và tóm tắt dài được chạy ngầm dưới dạng background job; hiển thị tiến trình cho người dùng theo dõi.                     | Hệ thống             |
| **FR-AI-15** | **Nhật ký và giám sát chi phí AI**                | Ghi log số token tiêu thụ, thời gian phản hồi và chi phí phát sinh của từng người dùng để Admin giám sát.                                       | Hệ thống, Admin      |

#### 3.10.1. Nguyên tắc triển khai và độ tin cậy của AI

1.  **Có sự can thiệp của con người (Human-in-the-loop):** Nội dung học
    thuật do AI sinh ra (đề thi, chấm điểm) chỉ mang tính gợi ý, tuyệt
    đối không tự động công bố hoặc chốt điểm khi giảng viên chưa xác
    nhận.
2.  **Kiến trúc kết hợp:**
    - *Mô hình Fine-tune cục bộ:* Dùng cho việc quét lọc vi phạm
      (`FR-AI-09`), chạy trên máy chủ nội bộ giúp bảo mật, phản hồi tức
      thì (\< 40ms) và không tốn phí API.
    - *Mô hình LLM API ngoài:* Dùng cho trợ lý RAG, tóm tắt và sinh nội
      dung đa dạng (`FR-AI-01`, `FR-AI-04`, `FR-AI-06`).
3.  **Phân quyền truy cập dữ liệu:** AI chỉ được phép đọc dữ liệu từ các
    khóa học công khai hoặc khóa học mà học viên đã ghi danh hợp lệ.
    Tuyệt đối không truy vấn đề thi chưa công bố hoặc khóa học đóng.
    Khóa học Only Me không được đưa vào pipeline quét/phát hiện vi phạm
    chính sách (`FR-AI-09`) và không được dùng làm nguồn cho trợ lý RAG
    hoặc gợi ý khóa học.

------------------------------------------------------------------------

### 3.11. Phân hệ Thanh toán (`Payment Module`)

| Mã YC         | Tên chức năng                           | Đặc tả chi tiết nghiệp vụ                                                                                                                  | Tác nhân                    |
|:--------------|:----------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------|
| **FR-PAY-01** | **Tạo đơn hàng mua khóa học**           | Tạo đơn hàng mới khi học viên mua khóa học/ chương trong khóa học trả phí; lưu bản sao giá và mã giảm giá tại thời điểm giao dịch.                                | Học viên, Hệ thống          |
| **FR-PAY-02** | **Áp dụng mã giảm giá (Coupon)**        | Cho phép nhập mã ưu đãi khi thanh toán; hệ thống xác thực hạn dùng, số lượt còn lại và giảm trừ tiền trực tiếp.                            | Học viên, Hệ thống          |
| **FR-PAY-03** | **Thanh toán cổng trực tuyến**          | Tích hợp cổng thanh toán (VNPay, MoMo, PayOS...) để học viên quét mã QR hoặc thanh toán thẻ ngân hàng.                                     | Học viên, Payment Gateway   |
| **FR-PAY-04** | **Thanh toán bằng số dư ví**            | Cho phép học viên dùng số dư khả dụng trong ví nội bộ để mua khóa học hoặc gói AI.                                                         | Học viên, Hệ thống          |
| **FR-PAY-05** | **Xác thực Webhook / IPN**              | Tiếp nhận thông báo từ cổng thanh toán; kiểm tra chữ ký số, đối chiếu số tiền và áp dụng cơ chế chống xử lý trùng lặp giao dịch.           | Hệ thống, Payment Gateway   |
| **FR-PAY-06** | **Xử lý sau thanh toán (OrderPaid)**    | Khi giao dịch thành công, hệ thống phát sự kiện `OrderPaid` để `Course Module` kích hoạt quyền vào học ngay lập tức.                       | Hệ thống                    |
| **FR-PAY-07** | **Quản lý ví điện tử cá nhân**          | Mỗi tài khoản có ví hiển thị 2 mục: Số dư khả dụng (dùng mua/rút) và Số dư tạm giữ (chờ đối soát). Tiền lưu dạng số nguyên VND.            | Người dùng, Hệ thống        |
| **FR-PAY-08** | **Nạp tiền vào ví**                     | Người dùng nạp tiền từ tài khoản ngân hàng vào ví nội bộ qua cổng thanh toán trực tuyến.                                                   | Người dùng, Payment Gateway |
| **FR-PAY-09** | **Sổ cái giao dịch bất biến (Ledger)**  | Mọi biến động số dư (nạp, trừ, hoàn tiền, nhận hoa hồng) đều được ghi vào sổ cái chỉ thêm mới (append-only), không sửa/xóa.                | Hệ thống                    |
| **FR-PAY-10** | **Xem lịch sử giao dịch và sao kê**     | Người dùng xem lịch sử biến động số dư, lọc theo thời gian và xuất file sao kê giao dịch.                                                  | Người dùng                  |
| **FR-PAY-11** | **Gửi yêu cầu hoàn tiền**               | Học viên gửi yêu cầu hoàn tiền nếu đáp ứng chính sách (trong vòng 7 ngày mua và tiến độ học tập chưa quá 20%).                             | Học viên                    |
| **FR-PAY-12** | **Kiểm duyệt yêu cầu hoàn tiền**        | Admin xem xét lý do hoàn tiền, lịch sử học tập và quyết định chấp thuận hoặc từ chối.                                                      | Admin                       |
| **FR-PAY-13** | **Xử lý hoàn tiền thành công**          | Khi hoàn tiền được duyệt, hệ thống hoàn tiền về ví người mua và gửi sự kiện `RefundApproved` để thu hồi quyền học.                         | Hệ thống                    |
| **FR-PAY-14** | **Tự động chia hoa hồng khóa học**      | Đơn hàng thanh toán thành công được tự động chia tỷ lệ: nền tảng giữ 15% phí sàn, 85% còn lại chuyển vào số dư tạm giữ của giảng viên.     | Hệ thống                    |
| **FR-PAY-15** | **Giải phóng số dư tạm giữ**            | Doanh thu của giảng viên được giữ tạm 7 ngày (thời hạn bảo lưu khiếu nại hoàn tiền); sau 7 ngày tự động chuyển sang số dư khả dụng để rút. | Hệ thống                    |
| **FR-PAY-16** | **Liên kết tài khoản ngân hàng**        | Giảng viên khai báo thông tin tài khoản ngân hàng thụ hưởng (tên ngân hàng, số tài khoản, tên chủ thẻ) để nhận tiền rút.                   | Giảng viên chủ khóa         |
| **FR-PAY-17** | **Tạo yêu cầu rút tiền**                | Giảng viên nhập số tiền muốn rút từ số dư khả dụng; hệ thống kiểm tra hạn mức và trừ trực tiếp số dư ví.                                   | Giảng viên chủ khóa         |
| **FR-PAY-18** | **Thu phí xử lý lệnh rút tiền**         | Hệ thống tự động tính và trừ phí xử lý 1.5% (tối thiểu 10.000 VNĐ) trên mỗi lệnh rút của giảng viên.                                       | Hệ thống                    |
| **FR-PAY-19** | **Duyệt và xử lý lệnh rút tiền**        | Admin kiểm tra tính hợp lệ; duyệt chuyển khoản thủ công hoặc từ chối kèm lý do (tiền được hoàn lại về ví giảng viên).                      | Admin                       |
| **FR-PAY-20** | **Đăng ký gói thuê bao Pro cho AI**     | Người dùng đăng ký gói thuê bao tháng/năm (`Student Pro`: 49.000đ/tháng, `Creator Pro`: 99.000đ/tháng) bằng số dư ví hoặc cổng thanh toán. | Học viên, Giảng viên        |
| **FR-PAY-22** | **Thống kê doanh thu giảng viên**       | Báo cáo trực quan cho giảng viên: doanh thu từng khóa, số tiền đã rút, số tiền đang tạm giữ và số dư khả dụng hiện tại.                    | Giảng viên chủ khóa         |
| **FR-PAY-23** | **Kiểm soát giao dịch và đóng băng ví** | Tự động phát hiện bất thường nạp/rút; đóng băng ví (khóa rút tiền và thanh toán) khi tài khoản nhận lệnh phạt từ `Moderation Module`.      | Hệ thống, Admin             |

#### 3.11.1. Các trạng thái giao dịch và đơn hàng

1.  **Trạng thái đơn hàng (`Order Status`):**

    - **Chờ thanh toán (Pending):** Đơn hàng mới tạo, đang chờ người
      dùng quét mã thanh toán.
    - **Đã thanh toán (Paid):** Giao dịch thành công, tiền đã ghi nhận
      và quyền học được kích hoạt.
    - **Hoàn tiền (Refunded):** Đơn hàng đã được duyệt trả lại tiền cho
      người mua.
    - **Đã hủy (Cancelled):** Người dùng chủ động hủy thanh toán.
    - **Hết hạn (Expired):** Đơn hàng quá thời hạn chờ thanh toán (mặc
      định 15 phút) mà chưa nhận được tiền.

2.  **Trạng thái yêu cầu rút tiền (`Withdrawal Status`):**

    - **Chờ duyệt (Pending):** Giảng viên đã tạo lệnh rút, tiền bị trừ
      khỏi số dư khả dụng và chờ Admin thẩm định.
    - **Đã duyệt (Approved):** Admin xác nhận hợp lệ, chuyển sang bộ
      phận thanh toán ngân hàng.
    - **Đã chuyển (Completed):** Tiền đã chuyển thành công vào tài khoản
      ngân hàng của giảng viên.
    - **Bị từ chối (Rejected):** Lệnh rút bị từ chối do sai thông tin
      ngân hàng hoặc vi phạm; tiền và phí được hoàn trả nguyên vẹn về
      ví.

3.  **Nguyên tắc an toàn tài chính:**

    - Mọi thao tác tiền tệ phải chạy trong một Database Transaction duy
      nhất.
    - Lưu trữ tiền bằng số nguyên VND, tuyệt đối không dùng số thực để
      tránh lỗi làm tròn.
    - Sai sót số liệu phải xử lý bằng bút toán đảo trong sổ cái, không
      ghi đè dữ liệu cũ.

------------------------------------------------------------------------

------------------------------------------------------------------------

## 4. MA TRẬN PHÂN QUYỀN MODERATOR VÀ ADMIN (RBAC MATRIX)


| Nhóm chức năng      | Thao tác                                                        | Moderator | Admin |
|:--------------------|:----------------------------------------------------------------|:---------:|:-----:|
| Báo cáo             | Xem hàng đợi báo cáo trong phạm vi xử lý                        |     ✓     |   ✓   |
| Báo cáo             | Chấp nhận/từ chối báo cáo, nhập lý do                           |     ✓     |   ✓   |
| Kiểm duyệt khóa học | Xem nội dung khóa học thuộc diện kiểm duyệt                     |     ✓     |   ✓   |
| Kiểm duyệt khóa học | Duyệt/từ chối khóa học VIP                                      |     ✓     |   ✓   |
| Kiểm duyệt khóa học | Tạm ẩn khóa học                                                 |     ✓     |   ✓   |
| Kiểm duyệt khóa học | Khôi phục khóa học                                              |     ✓     |   ✓   |
| Nội dung người dùng | Xóa bình luận vi phạm                                           |     ✓     |   ✓   |
| Chế tài tài khoản   | Cấm bình luận có thời hạn                                       |     ✓     |   ✓   |
| Chế tài tài khoản   | Cấm giảng viên tạo khóa học có thời hạn                         |     ✓     |   ✓   |
| Chế tài tài khoản   | Khóa tài khoản có thời hạn                                      |     ✓     |   ✓   |
| Chế tài tài khoản   | Khóa tài khoản vĩnh viễn                                        |     —     |   ✓   |
| Dữ liệu             | Xóa vĩnh viễn khóa học/nội dung/tài khoản                       |     —     |   ✓   |
| Khiếu nại           | Xem xét kháng nghị đối với quyết định kiểm duyệt                |     —     |   ✓   |
| Tài chính           | Xem ví, số dư, doanh thu và sổ cái                              |     —     |   ✓   |
| Tài chính           | Duyệt/từ chối hoàn tiền                                         |     —     |   ✓   |
| Tài chính           | Duyệt/từ chối yêu cầu rút tiền                                  |     —     |   ✓   |
| Quản trị quyền      | Gán/thu hồi role Moderator                                      |     —     |   ✓   |
| Giám sát            | Xem audit log của chính mình                                    |     ✓     |   ✓   |
| Giám sát            | Xem toàn bộ audit log hệ thống                                  |     —     |   ✓   |
| Cấu hình            | Cấu hình hệ thống, quota AI, broadcast                          |     —     |   ✓   |


------------------------------------------------------------------------

## 5. ĐẶC TẢ YÊU CẦU PHI CHỨC NĂNG (NON-FUNCTIONAL REQUIREMENTS - NFR)

| Mã         | Nhóm                    | Yêu cầu / tiêu chí nghiệm thu                                                                                                                                                                                                                                                                                                   |
|:-----------|:------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **NFR-01** | Hiệu năng               | 95% yêu cầu đọc (danh sách khóa học, trang học, tìm kiếm) ≤ 2 giây; 95% yêu cầu ghi (nộp bài, bình luận, ghi danh) ≤ 3 giây ở mức 50 người dùng đồng thời.                                                                                                                                                                      |
| **NFR-02** | Chịu tải                | Hệ thống hỗ trợ ít nhất 50 người dùng đồng thời; tỷ lệ lỗi máy chủ HTTP 5xx \< 1% trong bài kiểm thử liên tục 15 phút.                                                                                                                                                                                                          |
| **NFR-03** | Tải trang               | Trang chủ và trang học tập đạt Lighthouse Performance ≥ 70 ở chế độ mô phỏng mobile. Mọi API danh sách phải phân trang, tối đa 50 bản ghi/trang.                                                                                                                                                                                |
| **NFR-04** | Xác thực                | Các API, ngoại trừ đăng nhập, đăng ký và xem công khai, phải yêu cầu JWT. Access token sống ≤ 30 phút; refresh token có thể thu hồi. Mật khẩu phải được băm BCrypt; không lưu plaintext và không ghi log mật khẩu/token.                                                                                                        |
| **NFR-05** | Phân quyền              | Backend kiểm tra quyền cho mọi API. Người dùng chỉ sửa khóa học do mình sở hữu hoặc được cộng tác với permission phù hợp; cộng tác viên không tự cấp quyền hoặc chuyển quyền sở hữu. Chỉ chủ khóa được truy cập khóa học Only Me, kể cả Admin/Moderator cũng không được truy cập nội dung qua chức năng nghiệp vụ ở tầng ứng dụng. Khách không cần đăng nhập để xem Discovery và chỉ đọc nội dung khi cả khóa học và chương đều Public + Free; khách không được truy cập nội dung trả phí/VIP, Private, Protected, Only Me, tạm ẩn hoặc đã xóa và không được ghi nhận dữ liệu học tập cá nhân. Người dùng đã đăng nhập chỉ xem nội dung chương khi có quyền học hợp lệ; chỉ xem ví và đơn hàng của chính mình. Tài khoản bị khóa/bị hạn chế phải bị chặn ngay theo phạm vi chế tài.                                          |
| **NFR-06** | Truyền dữ liệu an toàn  | Production dùng HTTPS/TLS, tự chuyển HTTP sang HTTPS và bật HSTS. Nếu dùng cookie, cookie phải có Secure, HttpOnly, SameSite=Strict; thao tác thay đổi dữ liệu phải có biện pháp chống CSRF phù hợp.                                                                                                                            |
| **NFR-07** | Chống tấn công phổ biến | Chống SQL Injection bằng truy vấn tham số hóa; làm sạch HTML rich text/bình luận ở server để giảm XSS; CORS chỉ cho phép domain hệ thống. Giới hạn đăng nhập tối đa 5 lần/phút/IP và rate limit cho bình luận, AI, nạp/rút tiền.                                                                                                |
| **NFR-08** | Tệp tải lên             | Chỉ nhận định dạng cho phép và kiểm tra cả nội dung thực tế của tệp, không chỉ phần mở rộng/MIME do client gửi. Ảnh ≤ 5 MB; tệp đính kèm ≤ 20 MB. Tệp thuộc khóa học trả phí không được truy cập công khai nếu người truy cập chưa có quyền.                                                                                    |
| **NFR-09** | Bảo mật thanh toán      | Mọi webhook/IPN phải được xác thực chữ ký và đối chiếu số tiền, mã đơn trước khi ghi nhận. Không lưu số thẻ/dữ liệu thanh toán nhạy cảm không cần thiết; khóa bí mật không nằm trong source code; dùng sandbox khi demo.                                                                                                        |
| **NFR-10** | Toàn vẹn dữ liệu        | Thanh toán, ghi sổ cái, chia doanh thu, ghi danh và tạo sự kiện liên quan phải dùng transaction/outbox hoặc cơ chế nhất quán phù hợp. Lỗi giữa chừng không được để trạng thái dở dang, ví dụ đã trừ tiền nhưng chưa ghi danh.                                                                                                   |
| **NFR-11** | Idempotency             | Thanh toán, nạp tiền, hoàn tiền, rút tiền và webhook dùng mã giao dịch/khóa idempotency duy nhất. Gọi lại hoặc retry không được tạo giao dịch/bút toán trùng.                                                                                                                                                                   |
| **NFR-12** | Chính xác tài chính     | Tiền lưu và tính bằng số nguyên VND; không dùng số thực để tính tiền. Giá tại thời điểm mua phải được snapshot vào đơn hàng; đổi giá sau đó không ảnh hưởng đơn cũ. Frontend và backend hiển thị cùng kết quả.                                                                                                                  |
| **NFR-13** | Bài làm không mất       | Bài kiểm tra tự lưu tối đa mỗi 30 giây. Khi tải lại trang/mất mạng, hệ thống khôi phục phần bài làm đã lưu gần nhất. Đồng hồ đếm giờ dựa trên thời gian server, không phụ thuộc đồng hồ client.                                                                                                                                 |
| **NFR-14** | Xóa mềm                 | Khóa học và bình luận dùng xóa mềm để có thể khôi phục; khóa học bị xóa mềm được xem như tạm ẩn với người dùng thông thường. Chỉ Admin được xóa vĩnh viễn và mọi thao tác xóa vĩnh viễn phải có audit log.                                                                                                                      |
| **NFR-15** | Truy vết                | Lưu người thực hiện, thời gian và lý do cho thao tác quản trị (khóa tài khoản, ẩn/xóa khóa học, xử lý báo cáo, duyệt rút tiền), thay đổi điểm và mọi biến động tiền. Log không chứa mật khẩu/token.                                                                                                                             |
| **NFR-16** | Chất lượng AI           | Nội dung AI sinh ra ở trạng thái “Nháp – do AI tạo”, chỉ xuất bản sau khi giảng viên duyệt; AI không tự quyết điểm cuối. Trợ lý chỉ trả lời dựa trên nội dung khóa học và kèm chương nguồn; nếu không có thông tin, phải trả lời “không có trong khóa học”. Khóa học Only Me không thuộc bất kỳ quy trình kiểm duyệt, quét hoặc xử lý chính sách nào, dù tự động hay thủ công, và không được dùng làm nguồn RAG. |
| **NFR-17** | Sẵn sàng                | Mục tiêu uptime ≥ 99%/tháng, không tính bảo trì đã thông báo trước. Container tự khởi động lại khi lỗi; có endpoint `/health`.                                                                                                                                                                                                  |
| **NFR-18** | Sao lưu / phục hồi      | Backup MySQL hằng ngày, giữ 7 bản; RPO ≤ 24 giờ, RTO ≤ 4 giờ. Có tài liệu khôi phục và đã thử khôi phục thành công ít nhất một lần.                                                                                                                                                                                             |
| **NFR-19** | Bảo trì                 | Hệ thống chia thành 11 module theo nghiệp vụ, mỗi module sở hữu bảng/dữ liệu riêng. Module chỉ giao tiếp qua Contract công khai (đồng bộ) hoặc domain event (bất đồng bộ), không tham chiếu implementation/bảng nội bộ của module khác.                                                                                         |
| **NFR-20** | Kiểm thử                | Unit test ≥ 60% coverage cho Domain/Application của Identity, Payment, Assessment; integration test cho thanh toán, ghi danh, chấm bài, phân quyền; E2E test cho ba luồng: đăng ký/đăng nhập, mua và học khóa học, làm bài kiểm tra.                                                                                            |
| **NFR-21** | Mở rộng                 | Thêm tính năng mới không phải sửa trực tiếp dữ liệu nội bộ hoặc implementation của module không liên quan; thay đổi liên module thông qua Contract/event đã công bố.                                                                                                                                                            |
| **NFR-22** | Tương thích             | Hỗ trợ Chrome, Edge, Firefox và trình duyệt di động hiện đại. Giao diện sử dụng tốt từ chiều rộng 360 px.                                                                                                                                                                                                                       |
| **NFR-23** | Khả dụng                | Lỗi bằng tiếng Việt, chỉ rõ trường sai; giữ dữ liệu biểu mẫu khi gặp lỗi validation/conflict; thao tác dài có trạng thái đang xử lý/thành công/thất bại; thao tác nguy hiểm (xóa khóa, rút tiền) có xác nhận.                                                                                                                   |
| **NFR-24** | Triển khai              | Triển khai bằng Docker Compose một lệnh trên máy cá nhân và VPS Linux. Secrets qua biến môi trường/secret store, không commit. Jenkins CI/CD chạy test và triển khai khi merge vào `main`.                                                                                                                                      |
| **NFR-25** | Dịch vụ bên ngoài       | Cổng thanh toán, AI, email, OAuth có timeout và xử lý lỗi; timeout AI 30 giây, dịch vụ ngoài còn lại 10 giây. Lỗi dịch vụ ngoài không làm mất dữ liệu đơn hàng/thanh toán hoặc làm sập chức năng khác.                                                                                                                          |
