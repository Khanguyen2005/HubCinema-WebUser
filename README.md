# HubCinema-WebUser (Customer Frontend)

<p align="center">
  <img src="https://img.shields.io/badge/.NET%208-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/ASP.NET%20Core%20MVC-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Razor%20Views-512BD4?logo=dotnet&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Bootstrap-7952B3?logo=bootstrap&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/jQuery-0769AD?logo=jquery&logoColor=white&style=flat" />
  <img src="https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=flat" />
</p>

## Introduction
HubCinema-WebUser is the customer-facing frontend of the HubCinema movie ticketing system. It lets users browse movies, choose cinemas/showtimes, select seats, add combos, and pay online through the central API.

Other components of the system:
* **HubCinemaAPI (Backend for User & Admin):** https://github.com/Khanguyen2005/HubCinemaAPI (recommended)
* **HubCinema-WebAdmin (Admin Frontend):** https://github.com/Khanguyen2005/HubCinema-WebAdmin
* **sqa-testing-report (Automated Testing):** https://github.com/Khanguyen2005/sqa-testing-report

> Note: These links follow the **Khanguyen2005** namespace.
> Legacy HubCinemaAPI repo (for historical reference): https://github.com/nguyenxuanbac88/HubCinema-API

## Tech Stack
| Category | Technology | Notes |
| --- | --- | --- |
| Framework/Runtime | .NET 8, ASP.NET Core MVC | Web app following the MVC pattern |
| View Engine | Razor Views | Server-side rendering |
| UI Library | Bootstrap, jQuery | UI components and interactions |
| Form Validation | jQuery Validation, jQuery Validation Unobtrusive | Client-side validation |
| HTTP Client | HttpClient | Calls HubCinemaAPI |
| JSON | Newtonsoft.Json | JSON processing |
| Payment | VNPay, PayPal | Online payment |
| QR | QRCoder | QR generation for tickets |
| Session & Localization | ASP.NET Core Session, Localization (vi/en) | State and localization |
| Containerization | Docker, Docker Compose | Packaging and deployment |

## Architecture & Folder Structure
```
Controllers/        # Request handling (account, booking, payment, ...)
Models/             # DTOs and data models
Views/              # Razor views
Services/           # Payment/transaction services (VNPay/PayPal)
middlewares/        # Token validation middleware
Libraries/          # Helper libraries (VNPay/PayPal helpers)
Resources/          # Localization resources (vi/en)
wwwroot/            # Static assets (css, js, lib, images)
Properties/         # launchSettings
appsettings*.json   # App configuration (ApiSettings, VNPay, PayPal, ...)
```

## Getting Started
### Installation & Local Run
```bash
git clone https://github.com/Khanguyen2005/HubCinema-WebUser.git
cd HubCinema-WebUser
dotnet restore
```

### Environment Configuration
The app reads the backend base URL from `ApiSettings:BaseUrl`. You can configure it via **environment variables** or update `appsettings.Development.json`/`appsettings.json` to point to HubCinemaAPI.

**macOS/Linux (bash/zsh):**
```bash
export ApiSettings__BaseUrl="https://your-hubcinema-api-domain/api"
```

**Windows (PowerShell):**
```powershell
$env:ApiSettings__BaseUrl = "https://your-hubcinema-api-domain/api"
```

> Tip: you can set a default value in `appsettings.Development.json` for local development.

### Run Application
```bash
dotnet run
```
Default URL: `http://localhost:5020` (from `Properties/launchSettings.json`).

## Key Features
- Register an account.
- Log in.
- Browse movies (now showing/coming soon) and view details.
- Filter cinemas, schedules, and select showtimes.
- Choose seats on the seat layout and temporarily hold seats.
- Select food/drink combos before checkout.
- Online payment (VNPay, PayPal) and receive tickets.
- View booking history.
- View news, promotions, and cinema information.

## Contributors
- Khá
- Bắc
- Khoa
- Thành
