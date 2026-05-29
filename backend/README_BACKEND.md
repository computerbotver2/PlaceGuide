PlaceGuide Backend
1. Giới thiệu

PlaceGuide là hệ thống web hỗ trợ khách du lịch tìm kiếm quán ăn, xem thông tin quán, xem menu, nghe thuyết minh quán/món ăn, lựa chọn món phù hợp, đặt món, thanh toán và đánh giá dịch vụ.

Backend của hệ thống được xây dựng bằng ASP.NET Core Web API và tổ chức theo mô hình Clean Architecture rút gọn, kết hợp Service Layer và Repository Pattern. Mục tiêu của cách tổ chức này là giúp mã nguồn rõ ràng, dễ mở rộng, dễ bảo trì và phù hợp với đồ án có nhiều module nghiệp vụ.

2. Công nghệ sử dụng

Backend sử dụng các công nghệ chính:

.NET 10
ASP.NET Core Web API
Entity Framework Core
PostgreSQL
JWT Authentication
Clean Architecture rút gọn
Repository Pattern
Service Layer
3. Kiến trúc hệ thống

Backend được chia thành 4 project chính:

PlaceGuide
│
├── PlaceGuide.Api
├── PlaceGuide.Domain
├── PlaceGuide.Application
└── PlaceGuide.Infrastructure
3.1 PlaceGuide.Api

Đây là tầng ngoài cùng của backend.

Nhiệm vụ chính:

Nhận request từ frontend.
Định nghĩa API Controller.
Cấu hình Swagger/OpenAPI.
Cấu hình CORS.
Cấu hình Authentication/Authorization.
Gọi service ở tầng Application.
Trả response về cho frontend.

Tầng này không xử lý nghiệp vụ trực tiếp và không truy cập database trực tiếp.

3.2 PlaceGuide.Domain

Đây là tầng lõi của hệ thống.

Nhiệm vụ chính:

Chứa các Entity đại diện cho bảng trong database.
Chứa các Enum dùng chung trong hệ thống.
Chứa các lớp nền tảng như BaseEntity.

Tầng này không phụ thuộc vào các tầng khác.

3.3 PlaceGuide.Application

Đây là tầng xử lý nghiệp vụ.

Nhiệm vụ chính:

Chứa DTO dùng để nhận/trả dữ liệu với frontend.
Chứa Interface của Service.
Chứa Interface của Repository.
Chứa các Service xử lý nghiệp vụ.
Mapping dữ liệu từ Entity sang DTO và ngược lại.
Kiểm tra logic nghiệp vụ trước khi thao tác dữ liệu.

Ví dụ nghiệp vụ:

Đăng nhập, đăng ký.
Tạo quán ăn.
Thêm menu.
Thêm món ăn.
Tạo đơn hàng.
Xử lý thanh toán.
Lấy thống kê doanh thu.
3.4 PlaceGuide.Infrastructure

Đây là tầng làm việc với cơ sở dữ liệu và các dịch vụ hạ tầng.

Nhiệm vụ chính:

Cấu hình DbContext.
Cấu hình Entity Framework Core.
Tạo migration.
Triển khai Repository.
Seed dữ liệu ban đầu.
Kết nối PostgreSQL.
4. Luồng xử lý request

Luồng xử lý chuẩn của backend:

Frontend React
    ↓
Controller - PlaceGuide.Api
    ↓
Service - PlaceGuide.Application
    ↓
Repository - PlaceGuide.Infrastructure
    ↓
DbContext / PostgreSQL

Ví dụ khách du lịch xem danh sách quán ăn:

GET /api/restaurants

RestaurantsController
→ RestaurantService
→ RestaurantRepository
→ PlaceGuideDbContext
→ restaurants table
5. Quy tắc phụ thuộc giữa các project

Các project được phép tham chiếu như sau:

PlaceGuide.Application → PlaceGuide.Domain

PlaceGuide.Infrastructure → PlaceGuide.Application
PlaceGuide.Infrastructure → PlaceGuide.Domain

PlaceGuide.Api → PlaceGuide.Application
PlaceGuide.Api → PlaceGuide.Infrastructure

Không được tham chiếu ngược:

PlaceGuide.Domain không tham chiếu project nào khác.

PlaceGuide.Application không tham chiếu PlaceGuide.Infrastructure.

PlaceGuide.Infrastructure không tham chiếu PlaceGuide.Api.

PlaceGuide.Domain không tham chiếu PlaceGuide.Api.
6. Cấu trúc thư mục backend
PlaceGuide.Api
│
├── Controllers
├── Middlewares
├── Extensions
├── Program.cs
└── appsettings.json
PlaceGuide.Domain
│
├── Common
├── Entities
└── Enums
PlaceGuide.Application
│
├── Common
├── DTOs
│   ├── Auth
│   ├── Users
│   ├── Restaurants
│   ├── Menus
│   ├── Dishes
│   ├── Orders
│   ├── Payments
│   ├── Reviews
│   └── Statistics
│
├── Interfaces
├── Services
└── Mappings
PlaceGuide.Infrastructure
│
├── Data
├── Repositories
├── Configurations
├── Migrations
└── SeedData
## 7. Công cụ cần cài đặt

Để phát triển backend PlaceGuide, cần cài đặt các công cụ sau:

### 7.1 Visual Studio

Sử dụng **Visual Studio** để quản lý solution, project, viết code và chạy backend.

Khi cài Visual Studio, nên chọn workload:

```text
ASP.NET and web development
```

Workload này hỗ trợ tạo và chạy project ASP.NET Core Web API.

---

### 7.2 .NET SDK

Backend sử dụng **.NET SDK 10.0**.

Kiểm tra phiên bản .NET SDK bằng lệnh:

```powershell
dotnet --version
```

Kiểm tra toàn bộ SDK đã cài:

```powershell
dotnet --list-sdks
```

Nếu máy đã có SDK `10.0.x` thì có thể tạo project với target framework:

```text
net10.0
```

---

### 7.3 PostgreSQL

Hệ thống sử dụng **PostgreSQL** làm hệ quản trị cơ sở dữ liệu.

PostgreSQL dùng để lưu trữ:

* Người dùng.
* Quán ăn.
* Menu.
* Món ăn.
* Đơn hàng.
* Thanh toán.
* Đánh giá.
* Thống kê.

Tên database dự kiến:

```text
placeguide_db
```

---

### 7.4 pgAdmin

`pgAdmin` là công cụ giao diện để quản lý PostgreSQL.

Có thể dùng pgAdmin để:

* Tạo database.
* Xem danh sách bảng.
* Kiểm tra dữ liệu.
* Chạy câu lệnh SQL.
* Kiểm tra quan hệ giữa các bảng.

---

### 7.5 Terminal / PowerShell

Trong quá trình tạo project và cài package, sử dụng Terminal hoặc PowerShell.

Trong Visual Studio có thể mở Terminal bằng:

```text
View → Terminal
```

---

## 8. Các package NuGet cần cài đặt

Backend PlaceGuide sử dụng một số package NuGet để hỗ trợ kết nối database, migration, xác thực và OpenAPI.

---

### 8.1 Package cho PlaceGuide.Infrastructure

`PlaceGuide.Infrastructure` là project làm việc với database nên cần cài Entity Framework Core và PostgreSQL provider.

Chạy các lệnh sau tại thư mục gốc solution:

```powershell
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Microsoft.EntityFrameworkCore
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Npgsql.EntityFrameworkCore.PostgreSQL
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Microsoft.EntityFrameworkCore.Design
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Microsoft.EntityFrameworkCore.Tools
```

Ý nghĩa:

| Package                                 | Mục đích                                 |
| --------------------------------------- | ---------------------------------------- |
| `Microsoft.EntityFrameworkCore`         | Thư viện ORM để làm việc với database    |
| `Npgsql.EntityFrameworkCore.PostgreSQL` | Provider giúp EF Core kết nối PostgreSQL |
| `Microsoft.EntityFrameworkCore.Design`  | Hỗ trợ tạo migration                     |
| `Microsoft.EntityFrameworkCore.Tools`   | Hỗ trợ các lệnh EF Core                  |

---

### 8.2 Package hỗ trợ Dependency Injection cho PlaceGuide.Infrastructure

Cài thêm các package hỗ trợ cấu hình dependency injection và đọc cấu hình:

```powershell
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Microsoft.Extensions.Configuration.Abstractions
dotnet add PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package Microsoft.Extensions.DependencyInjection.Abstractions
```

Ý nghĩa:

| Package                                                 | Mục đích                                      |
| ------------------------------------------------------- | --------------------------------------------- |
| `Microsoft.Extensions.Configuration.Abstractions`       | Hỗ trợ đọc cấu hình từ `appsettings.json`     |
| `Microsoft.Extensions.DependencyInjection.Abstractions` | Hỗ trợ đăng ký service, repository, DbContext |

---

### 8.3 Package cho PlaceGuide.Api

`PlaceGuide.Api` là project chạy Web API nên cần package xác thực JWT và hỗ trợ EF Design.

```powershell
dotnet add PlaceGuide.Api\PlaceGuide.Api.csproj package Microsoft.AspNetCore.Authentication.JwtBearer
dotnet add PlaceGuide.Api\PlaceGuide.Api.csproj package Microsoft.EntityFrameworkCore.Design
```

Ý nghĩa:

| Package                                         | Mục đích                                 |
| ----------------------------------------------- | ---------------------------------------- |
| `Microsoft.AspNetCore.Authentication.JwtBearer` | Hỗ trợ đăng nhập/xác thực bằng JWT token |
| `Microsoft.EntityFrameworkCore.Design`          | Hỗ trợ chạy migration từ project API     |

---

### 8.4 Package OpenAPI

Khi tạo project bằng template ASP.NET Core Web API, package OpenAPI thường đã được tạo sẵn:

```text
Microsoft.AspNetCore.OpenApi
```

Package này dùng để sinh tài liệu API dạng OpenAPI.

Có thể kiểm tra bằng lệnh:

```powershell
dotnet list PlaceGuide.Api\PlaceGuide.Api.csproj package
```

Nếu chưa có, có thể cài bằng:

```powershell
dotnet add PlaceGuide.Api\PlaceGuide.Api.csproj package Microsoft.AspNetCore.OpenApi
```

---

## 9. Công cụ Entity Framework CLI

Để sử dụng các lệnh migration như `dotnet ef migrations add`, cần cài công cụ `dotnet-ef`.

Cài đặt:

```powershell
dotnet tool install --global dotnet-ef
```

Nếu đã cài trước đó, có thể cập nhật:

```powershell
dotnet tool update --global dotnet-ef
```

Kiểm tra phiên bản:

```powershell
dotnet ef --version
```

---

## 10. Kiểm tra package đã cài

Sau khi cài package, kiểm tra toàn bộ package trong solution:

```powershell
dotnet list package
```

Kết quả hiện tại dự kiến:

```text
PlaceGuide.Api
- Microsoft.AspNetCore.Authentication.JwtBearer
- Microsoft.AspNetCore.OpenApi
- Microsoft.EntityFrameworkCore.Design

PlaceGuide.Infrastructure
- Microsoft.EntityFrameworkCore
- Microsoft.EntityFrameworkCore.Design
- Microsoft.EntityFrameworkCore.Tools
- Npgsql.EntityFrameworkCore.PostgreSQL
- Microsoft.Extensions.Configuration.Abstractions
- Microsoft.Extensions.DependencyInjection.Abstractions
```

`PlaceGuide.Domain` không cần cài package vì đây là tầng lõi, chỉ chứa Entity và Enum.

`PlaceGuide.Application` hiện tại chưa bắt buộc cài package nếu dùng mapping thủ công.

---

## 11. Ghi chú về AutoMapper

Ban đầu có thể cài AutoMapper để mapping Entity sang DTO. Tuy nhiên trong dự án PlaceGuide hiện tại, backend sẽ **không dùng AutoMapper** để tránh phụ thuộc package không cần thiết.

Thay vào đó, hệ thống sẽ mapping thủ công trong Service.

Ví dụ:

```csharp
var dto = new RestaurantDto
{
    Id = restaurant.Id,
    Name = restaurant.Name,
    Address = restaurant.Address
};
```

Nếu đã lỡ cài AutoMapper, có thể gỡ bằng lệnh:

```powershell
dotnet remove PlaceGuide.Application\PlaceGuide.Application.csproj package AutoMapper
dotnet remove PlaceGuide.Application\PlaceGuide.Application.csproj package AutoMapper.Extensions.Microsoft.DependencyInjection
```

Nếu AutoMapper xuất hiện ở project khác thì gỡ tiếp:

```powershell
dotnet remove PlaceGuide.Api\PlaceGuide.Api.csproj package AutoMapper
dotnet remove PlaceGuide.Infrastructure\PlaceGuide.Infrastructure.csproj package AutoMapper
```

---

## 12. Cấu hình database

Connection string sẽ được đặt trong file:

```text
PlaceGuide.Api/appsettings.json
```

Ví dụ:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Port=5432;Database=placeguide_db;Username=postgres;Password=your_password"
  }
}
```

Trong đó:

| Thành phần               | Ý nghĩa                      |
| ------------------------ | ---------------------------- |
| `Host=localhost`         | Database chạy trên máy local |
| `Port=5432`              | Cổng mặc định của PostgreSQL |
| `Database=placeguide_db` | Tên database của dự án       |
| `Username=postgres`      | Tài khoản PostgreSQL         |
| `Password=your_password` | Mật khẩu PostgreSQL          |

Khi dùng thực tế, thay `your_password` bằng mật khẩu PostgreSQL trên máy.

---

## 13. Lệnh build backend

Sau khi tạo project và cài package, build toàn bộ solution bằng lệnh:

```powershell
dotnet build
```

Nếu thành công, kết quả sẽ hiển thị:

```text
Build succeeded.
```

---

## 14. Lệnh chạy backend

Chạy API bằng lệnh:

```powershell
dotnet run --project PlaceGuide.Api
```

Nếu chạy thành công, Terminal sẽ hiển thị dạng:

```text
Now listening on: http://localhost:5096
Application started.
```

Khi đó backend đang chạy tại:

```text
http://localhost:5096
```

---

## 15. Kiểm tra OpenAPI

Khi backend đang chạy, có thể kiểm tra OpenAPI tại:

```text
http://localhost:5096/openapi/v1.json
```

Sau này nếu cấu hình Swagger UI, có thể truy cập:

```text
http://localhost:5096/swagger
```

---

## 16. Trạng thái hiện tại của backend

Backend hiện tại mới ở giai đoạn tạo khung.

Đã hoàn thành:

* Tạo solution `PlaceGuide`.
* Tạo project `PlaceGuide.Api`.
* Tạo project `PlaceGuide.Domain`.
* Tạo project `PlaceGuide.Application`.
* Tạo project `PlaceGuide.Infrastructure`.
* Cấu hình reference giữa các project.
* Tạo khung thư mục.
* Cài các package cần thiết.
* Build project thành công.
* Chạy API thành công.

Chưa thực hiện:

* Chưa tạo Entity chính thức.
* Chưa tạo DbContext chính thức.
* Chưa tạo Repository.
* Chưa tạo Service.
* Chưa tạo Controller nghiệp vụ.
* Chưa chạy migration.
* Chưa kết nối database thật.
