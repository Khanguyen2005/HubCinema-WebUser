# HubCinema WebUser

Giao diện web dành cho người dùng cuối của hệ thống đặt vé xem phim online. Ứng dụng tập trung vào trải nghiệm đặt vé, chọn ghế, chọn combo và thanh toán, đồng thời tiêu thụ dữ liệu từ API backend HubCinema.

## Thành viên
- Khá
- Duy Khoa

## Tính năng chính
- Xem danh sách phim, chi tiết phim và lịch chiếu theo rạp/khu vực.
- Chọn suất chiếu, sơ đồ ghế, giữ ghế và đặt vé.
- Chọn combo/đồ ăn kèm trước khi thanh toán.
- Thanh toán online qua VNPay và cập nhật trạng thái ghế sau thanh toán.
- Đăng ký/đăng nhập, quản lý vé đã đặt.
- Trang tin tức, khuyến mãi và thông tin rạp.

## Tech stack
- **.NET 8** + **ASP.NET Core MVC (Razor Views)**.
- **Bootstrap**, **jQuery**, **jQuery Validation** cho giao diện và tương tác.
- **Newtonsoft.Json** để xử lý JSON từ API.
- **VNPay** cho luồng thanh toán.
- **QRCoder** phục vụ tạo QR cho vé.
- **Session** và **Localization (vi/en)**.
- **Docker/Compose** cho triển khai.

## Kiến trúc tổng quan (WebUser)
- **Controllers** xử lý luồng đặt vé, phim/rạp, tài khoản, tin tức.
- **Services**: VNPay + Transaction.
- **Models/Views**: mô hình dữ liệu và giao diện Razor.
- **Middleware**: kiểm tra token cho các luồng cần xác thực.
- **HttpClient** gọi API backend.

## Backend API tích hợp
Backend được triển khai tại: **https://github.com/nguyenxuanbac88/HubCinema-API**

Tóm tắt API:
- **Mục tiêu**: Backend cho hệ thống đặt vé xem phim online, quản trị rạp/phim/suất chiếu, đặt ghế, combo đồ ăn, hóa đơn, báo cáo và quản lý nội dung.
- **Công nghệ**: ASP.NET Core Web API (.NET 8), Entity Framework Core + SQL Server, Redis, JWT, Swagger, SMTP email; triển khai Docker/compose.
- **Kiến trúc**: Controllers → Services/AdminServices → Data (DbContext) → Models/Entities + DTOs + Helpers.
- **Chức năng chính**:
  - Xác thực & tài khoản: đăng nhập/đăng ký JWT, OTP quên mật khẩu, đổi email/đổi mật khẩu, logout.
  - Public API: danh sách/chi tiết rạp, phim, đồ ăn, phòng; combo theo rạp.
  - Lịch chiếu: lọc theo khu vực/rạp, ngày chiếu, suất chiếu theo phim/ngày, timeline theo ngày/rạp.
  - Đặt vé: tạo hóa đơn, lưu ghế đã đặt, lưu đồ ăn, cập nhật trạng thái ghế.
  - Ghế & layout: giữ ghế tạm bằng Redis, layout + giá theo loại, cấu hình loại ghế.
  - Quản trị: CRUD rạp/phim/phòng/đồ ăn, gán combo, dashboard thống kê, quản lý users + hóa đơn.
  - Nội dung: CRUD banner, tin tức/danh mục.
  - Hóa đơn: lấy danh sách hóa đơn, theo user token, theo id.
  - Health check: kiểm tra DB/Redis/SMTP.
- **Mô hình dữ liệu**: User, Movie, Cinema, Room, Showtime, ShowtimeType, SeatTypeInRoom, BookedSeat, Invoice, InvoiceFood, Food, Combo_Cinema, Banner, News, Category.

## Cấu hình
- **API base URL**: `appsettings.json` → `ApiSettings:BaseUrl` (hiện tại trong repo là `http://api.dvxuanbac.com:2030/api`).
  **Lưu ý bảo mật**: khi triển khai production, hãy đổi sang HTTPS nếu backend hỗ trợ TLS để tránh truyền dữ liệu plaintext.
- **VNPay**: cấu hình tại `appsettings.json` và `appsettings.Development.json` (callback URL khi dev).
- Có thể override cấu hình qua **Environment Variables** khi chạy production.

## Chạy local
```bash
dotnet restore
dotnet run
```
Mặc định chạy tại: `http://localhost:5020` (theo `launchSettings.json`).

## Chạy bằng Docker
```bash
docker-compose up -d --build
```
Mặc định expose cổng `8080`. Xem thêm tại `DOCKER_DEPLOYMENT.md`.
