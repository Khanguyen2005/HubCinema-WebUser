# HubCinema-WebUser (Customer Frontend)

<p align="center">
  <img src="https://img.shields.io/badge/.NET%208-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/ASP.NET%20Core%20MVC-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Razor%20Views-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Bootstrap-7952B3?logo=bootstrap&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/jQuery-0769AD?logo=jquery&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=flat" />
</p>

## Giới thiệu
HubCinema-WebUser là giao diện dành cho khách hàng trong hệ thống bán vé xem phim HubCinema. Ứng dụng hỗ trợ người dùng duyệt phim, chọn rạp/suất chiếu, chọn ghế, đặt combo và thanh toán trực tuyến thông qua API trung tâm.

Hệ sinh thái HubCinema:
- **HubCinemaAPI (Backend cho User & Admin)**: https://github.com/Khanguyen2005/HubCinemaAPI (khuyến nghị sử dụng repo này)
- **HubCinema-WebAdmin (Frontend Quản trị viên)**: https://github.com/Khanguyen2005/HubCinema-WebAdmin
- **sqa-testing-report (Automated Testing)**: https://github.com/Khanguyen2005/sqa-testing-report
> Ghi chú: Các liên kết trên theo namespace **Khanguyen2005** (theo mô tả dự án).
> Tham khảo legacy repo (nếu cần đối chiếu lịch sử): https://github.com/nguyenxuanbac88/HubCinema-API

## Tech Stack
| Nhóm | Công nghệ | Ghi chú |
| --- | --- | --- |
| Framework/Runtime | .NET 8, ASP.NET Core MVC | Ứng dụng web theo mô hình MVC |
| View Engine | Razor Views | Render giao diện phía server |
| UI Library | Bootstrap, jQuery | Thành phần UI và tương tác |
| Form Validation | jQuery Validation, jQuery Validation Unobtrusive | Kiểm tra dữ liệu trên client |
| HTTP Client | HttpClient | Gọi HubCinemaAPI |
| JSON | Newtonsoft.Json | Xử lý dữ liệu JSON |
| Payment | VNPay | Thanh toán trực tuyến (PayPal chưa được tích hợp trong repo này) |
| QR | QRCoder | Tạo QR cho vé |
| Session & Localization | ASP.NET Core Session, Localization (vi/en) | Lưu trạng thái và đa ngôn ngữ |
| Containerization | Docker, Docker Compose | Đóng gói và triển khai |

## Kiến trúc & Cấu trúc thư mục
```
Controllers/        # Điều phối luồng nghiệp vụ (account, booking, payment, ...)
Models/             # DTOs và model dữ liệu
Views/              # Razor views
Services/           # Dịch vụ thanh toán/transaction
middlewares/        # Middleware kiểm tra token
Libraries/          # Thư viện hỗ trợ (VNPay helpers)
Resources/          # Tài nguyên localization (vi/en)
wwwroot/            # Static assets (css, js, lib, images)
Properties/         # launchSettings
appsettings*.json   # Cấu hình ứng dụng (ApiSettings, VNPay, ...)
```

## Cài đặt & Khởi chạy (Getting Started)
### 1) Clone project
```bash
git clone https://github.com/Khanguyen2005/HubCinema-WebUser.git
cd HubCinema-WebUser
```

### 2) Cài đặt dependencies
```bash
dotnet restore
```

### 3) Cấu hình biến môi trường
Dự án đọc Base URL của backend từ `ApiSettings:BaseUrl`. Bạn có thể cấu hình bằng **environment variables** hoặc cập nhật trực tiếp trong `appsettings.Development.json`/`appsettings.json` để trỏ tới HubCinemaAPI.

**macOS/Linux (bash/zsh):**
```bash
export ApiSettings__BaseUrl="https://your-hubcinema-api-domain/api"
```

**Windows (PowerShell):**
```powershell
$env:ApiSettings__BaseUrl = "https://your-hubcinema-api-domain/api"
```

> Mẹo: có thể đặt giá trị mặc định trong `appsettings.Development.json` khi chạy local.

### 4) Chạy ứng dụng
```bash
dotnet run
```
Mặc định ứng dụng chạy tại: `http://localhost:5020` (theo `Properties/launchSettings.json`).

## Tính năng chính
- Xác thực người dùng: đăng ký, đăng nhập.
- Duyệt danh sách phim (đang chiếu/sắp chiếu), xem chi tiết phim.
- Lọc rạp, lịch chiếu và chọn suất chiếu.
- Chọn ghế theo sơ đồ, giữ ghế tạm thời.
- Chọn combo đồ ăn/nước uống trước khi thanh toán.
- Thanh toán trực tuyến (VNPay) và nhận vé.
- Xem lịch sử vé đã đặt.

## Contributors
- Khá
- Bắc
- Duy Khoa
- Thành
