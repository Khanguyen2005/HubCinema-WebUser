# HubCinema WebUser

End-user web application for the online movie ticket booking system. The app focuses on browsing movies, selecting showtimes and seats, adding combos, and completing payments while consuming data from the HubCinema backend API.

## Team
- Khá
- Duy Khoa
- Bắc
- Thành

## Key features
- Browse movies, movie details, and showtimes by cinema/region.
- Select showtime, seat layout, hold seats, and book tickets.
- Add food/combos before checkout.
- Online payment via VNPay and seat status updates after payment.
- Register/login and view booked tickets.
- News, promotions, and cinema information pages.

## Tech stack
- **.NET 8** + **ASP.NET Core MVC (Razor Views)**.
- **Bootstrap**, **jQuery**, **jQuery Validation** for UI and interactions.
- **Newtonsoft.Json** for JSON processing.
- **VNPay** payment integration.
- **QRCoder** for ticket QR generation.
- **Session** and **Localization (vi/en)**.
- **Docker/Compose** for deployment.

## High-level architecture (WebUser)
- **Controllers** handle booking flow, movies/cinemas, accounts, news.
- **Services**: VNPay + Transaction.
- **Models/Views**: data models and Razor views.
- **Middleware**: token validation for protected flows.
- **HttpClient** to call the backend API.

## Backend API integration
Backend repository: **https://github.com/nguyenxuanbac88/HubCinema-API**

API summary:
- **Goal**: Backend for online movie ticket booking, cinema/movie/showtime management, seat booking, food combos, invoices, reports, and content management.
- **Tech**: ASP.NET Core Web API (.NET 8), EF Core + SQL Server, Redis, JWT, Swagger, SMTP email; Docker/compose deployment.
- **Architecture**: Controllers → Services/AdminServices → Data (DbContext) → Models/Entities + DTOs + Helpers.
- **Main features**:
  - Auth & accounts: JWT login/register, OTP password reset, OTP email change, password change, logout.
  - Public API: list/detail cinemas, movies, foods, rooms; combos by cinema.
  - Showtimes: filter by region/cinema, show dates, showtimes by movie/date/region/cinema, conflict checking, daily timelines.
  - Booking: create invoices, save booked seats and food, update paid seat status.
  - Seats & layout: temporary seat holds via Redis, layout/pricing by showtime/seat type, JSON layout creation, seat-type configuration by row.
  - Admin: CRUD cinemas/movies/rooms/foods, assign combos, dashboard stats, manage users + invoices.
  - Content: CRUD banners and news/categories.
  - Invoices: list all, by user token, by id.
  - Health check: DB/Redis/SMTP response checks.
- **Key data models**: User, Movie, Cinema, Room, Showtime, ShowtimeType, SeatTypeInRoom, BookedSeat, Invoice, InvoiceFood, Food, Combo_Cinema, Banner, News, Category.

## Testing (Selenium)
All four members (Khá, Duy Khoa, Bắc, Thành) also wrote Selenium UI/integration tests for this project.
Test project: **https://github.com/nguyenxuanbac88/sqa-testing-report**

## Configuration
- **API base URL**: `appsettings.json` → `ApiSettings:BaseUrl` (see default value in the config file).
  **Security note**: in production, **HTTPS is required**; if the backend has no TLS, place a reverse proxy/ingress to encrypt traffic.
- **VNPay**: configured in `appsettings.json` and `appsettings.Development.json` (callback URL for dev).
- Config can be overridden via **Environment Variables** in production.

## Run locally
```bash
dotnet restore
dotnet run
```
Default URL: `http://localhost:5020` (from `launchSettings.json`).

## Run with Docker
```bash
docker-compose up -d --build
```
Default exposed port: `8080`. See `DOCKER_DEPLOYMENT.md` for details.
