# HỆ THỐNG QUẢN LÝ CLB PICKLEBALL "VỢT THỦ PHỐ NÚI" - MOBILE EDITION

**Mobile_Flutter_1771020298_NguyenHuyhoang**

## 📋 Tổng Quan

Dự án bao gồm:
- **Backend**: ASP.NET Core Web API (.NET 8) với Entity Framework Core, Identity, JWT Authentication
- **Mobile**: Flutter App (sẽ được tạo riêng)
- **Database**: SQL Server (LAPTOP-OATMIPEE) với Windows Authentication
- **Prefix tables**: `378_` (từ MSSV: 1771020298)

## 🏗️ Cấu Trúc Backend

```
PcmBackend/
├── PcmBackend.API/              # Web API Layer
│   ├── Controllers/             # API Controllers
│   ├── Program.cs               # App configuration
│   └── appsettings.json         # Configuration
├── PcmBackend.Core/             # Domain Models
│   ├── Entities/                # Database entities
│   └── Enums/                   # Enumerations
├── PcmBackend.Infrastructure/   # Data Access
│   └── Data/
│       ├── ApplicationDbContext.cs
│       └── SeedData.cs          # Database seeding
└── PcmBackend.Services/         # Business Logic
    ├── WalletService.cs
    ├── BookingService.cs
    └── TournamentService.cs
```

## 🚀 Hướng Dẫn Chạy Backend

### Yêu Cầu
- .NET 8 SDK
- SQL Server (LAPTOP-OATMIPEE với Windows Authentication)
- Visual Studio 2022 hoặc VS Code

### Các Bước

#### 1. Restore Dependencies
```bash
cd d:\Baikiemtra\PcmBackend\PcmBackend.API
dotnet restore
```

#### 2. Tạo Database Migration
```bash
dotnet ef migrations add InitialCreate --project ..\PcmBackend.Infrastructure --startup-project .
```

####  3. Apply Migration & Seed Database
```bash
dotnet ef database update --project ..\PcmBackend.Infrastructure --startup-project .
```

Hoặc chạy trực tiếp app (sẽ tự động seed):
```bash
dotnet run
```

#### 4. Kiểm Tra API
- Swagger UI: `https://localhost:5001/swagger`
- API Base URL: `https://localhost:5001/api`

## 📊 Database Schema

Tất cả bảng đều có prefix `378_`:

### Nhóm Quản Trị & Wallet
- **378_Members**: Thành viên (wallet, tier, rank DUPR)
- **378_WalletTransactions**: Giao dịch ví (nạp, trừ, hoàn tiền)

### Nhóm Booking  
- **378_Courts**: Sân đấu
- **378_Bookings**: Đặt sân (có hỗ trợ recurring)

### Nhóm Tournaments
- **378_Tournaments**: Giải đấu
- **378_TournamentParticipants**: Người tham gia giải
- **378_Matches**: Trận đấu chi tiết

### Khác
- **378_News**: Tin tức
- **378_Notifications**: Thông báo

## 👤 Tài Khoản Mặc Định (Sau Khi Seed)

### Admin
- Email: `admin@pcm.com`
- Password: `Admin@123`
- Role: Admin
- Wallet: 10,000,000 VND

### Treasurer
- Email: `treasurer@pcm.com`
- Password: `Treasurer@123`
- Role: Treasurer
- Wallet: 5,000,000 VND

### Referee
- Email: `referee@pcm.com`
- Password: `Referee@123`
- Role: Referee
- Wallet: 3,000,000 VND

### Members (20 thành viên)
- Email: `member1@pcm.com` đến `member20@pcm.com`
- Password: `Member@123`
- Role: Member
- Wallet: 2,000,000 - 10,000,000 VND (ngẫu nhiên)

## 🔑 API Endpoints Chính

### Authentication
```
POST /api/auth/login            - Đăng nhập (trả về JWT token)
POST /api/auth/register         - Đăng ký
GET  /api/auth/me               - Thông tin user hiện tại
```

### Wallet
```
GET  /api/wallet/balance        - Số dư ví
POST /api/wallet/deposit        - Tạo yêu cầu nạp tiền
GET  /api/wallet/transactions   - Lịch sử giao dịch
PUT  /api/wallet/approve/{id}   - Admin duyệt nạp tiền
```

### Bookings
```
GET  /api/bookings/calendar     - Lịch đặt sân
POST /api/bookings              - Đặt sân
DELETE /api/bookings/{id}       - Hủy sân
```

### Tournaments
```
GET  /api/tournaments           - Danh sách giải đấu
POST /api/tournaments/{id}/join - Tham gia giải
POST /api/tournaments/{id}/generate-schedule - Tạo lịch thi đấu
POST /api/matches/{id}/result   - Cập nhật kết quả
```

## 🎯 Tính Năng Đã Implement

### ✅ Backend Hoàn Thành
- [x] Entity Framework Core với Code First
- [x] ASP.NET Identity với JWT Authentication
- [x] Wallet System (Nạp tiền, trừ tiền, hoàn tiền)
- [x] Automatic Tier Management (Standard/Silver/Gold/Diamond)
- [x] Booking System với kiểm tra conflict
- [x] Tournament System với auto-scheduler
- [x] Data Seeding (Admin, 20 members, courts, tournaments)
- [x] Database với prefix `378_`

### 🚧 Cần Hoàn Thiện
- [ ] Controllers API (AuthController, WalletController, BookingsController, TournamentsController)
- [ ] SignalR Hub implementation
- [ ] Background Services (Auto-cancel, Auto-remind)
- [ ] Flutter Mobile App
- [ ] Testing & Video Demo

## 📱 Flutter Mobile App (Tiếp Theo)

Sẽ được tạo trong folder riêng `PcmMobile/` với:
- State Management: Riverpod
- HTTP Client: Dio
- SignalR: signalr_netcore
- Navigation: go_router
- Features: Auth, Dashboard, Booking, Tournament, Wallet, Profile

## 🔧 Troubleshooting

### Lỗi Connection String
Nếu không kết nối được SQL Server:
- Kiểm tra server name: `LAPTOP-OATMIPEE`
- Đảm bảo SQL Server đang chạy
- Thử thêm instance name nếu cần (VD: `LAPTOP-OATMIPEE\\SQLEXPRESS`)

### Lỗi Migration
```bash
# Xóa migrations nếu cần
dotnet ef migrations remove --project ..\PcmBackend.Infrastructure

# Tạo lại
dotnet ef migrations add InitialCreate --project ..\PcmBackend.Infrastructure
```

## 📞 Thông Tin

- **MSSV**: 1771020298
- **Họ Tên**: Nguyen Huy Hoang
- **Dự Án**: Hệ Thống Quản Lý CLB Pickleball - Mobile Edition
- **Môn Học**: Lập Trình Mobile với Flutter

---

**LƯU Ý**: Đây là project lớn. Backend core đã được thiết lập. Tiếp theo cần:
1. Tạo các Controllers API đầy đủ
2. Test API với Postman/Swagger
3. Tạo Flutter app
4. Integrate và test end-to-end
5. Quay video demo

