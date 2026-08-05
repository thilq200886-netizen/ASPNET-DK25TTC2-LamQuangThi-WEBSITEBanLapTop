# Website Bán Laptop - DoAn_LapTrinhWeb

> Đồ án môn Lập Trình Web - Website thương mại điện tử bán laptop

## Mục lục

- [Giới thiệu](#giới-thiệu)
- [Công nghệ sử dụng](#công-nghệ-sử-dụng)
- [Cấu trúc Database](#cấu-trúc-database)
- [Cài đặt](#cài-đặt)
  - [Yêu cầu hệ thống](#yêu-cầu-hệ-thống)
  - [Cách 1: Cài đặt Database bằng SSMS](#cách-1-cài-đặt-database-bằng-ssms)
  - [Cách 2: Khôi phục từ file Backup](#cách-2-khôi-phục-từ-file-backup)
  - [Chạy dự án bằng Visual Studio](#chạy-dự-án-bằng-visual-studio)
- [Các chức năng của đồ án](#các-chức-năng-của-đồ-án)
  - [Người dùng (User)](#người-dùng-user)
  - [Quản trị (Admin)](#quản-trị-admin)
- [Tài khoản đăng nhập](#tài-khoản-đăng-nhập)
- [Sitemap / Map của trang web](#sitemap--map-của-trang-web)
  - [Trang người dùng](#trang-người-dùng)
  - [Trang quản trị Admin](#trang-quản-trị-admin)
- [Các link quan trọng](#các-link-quan-trọng)
- [Cấu hình kết nối Database](#cấu-hình-kết-nối-database)
- [Xử lý lỗi thường gặp](#xử-lý-lỗi-thường-gặp)

---

## Giới thiệu

Website bán laptop là một hệ thống **thương mại điện tử (E-Commerce)** được xây dựng bằng **ASP.NET MVC 5** và **Entity Framework 6** với **SQL Server** làm cơ sở dữ liệu. Đồ án được phát triển với mục tiêu xây dựng một trang web bán hàng trực tuyến hoàn chỉnh, bao gồm giao diện người dùng và trang quản trị.

**Tính năng chính:**
- Mua sắm laptop trực tuyến
- Quản lý giỏ hàng & thanh toán
- Quản lý tài khoản người dùng
- Trang quản trị cho admin
- Đánh giá sản phẩm
- Mã giảm giá / Khuyến mãi
- Theo dõi đơn hàng
- Phân quyền người dùng (Admin / Member / Mod)

---

## Công nghệ sử dụng

| Thành phần | Công nghệ | Phiên bản |
|---|---|---|
| Framework | ASP.NET MVC 5 | .NET Framework 4.7.2 |
| ORM | Entity Framework | 6.0 |
| Database | SQL Server / SQL Server Express | 2019+ |
| Ngôn ngữ | C# | - |
| IDE | Visual Studio | 2019 / 2022 |
| UI (Admin) | Metronic 8 (Keen) | - |
| Authentication | Forms Authentication | - |
| Email | SMTP (Gmail) | - |

---

## Cấu trúc Database

**Database name:** `kaome`

### Danh sách bảng (Tables)

| STT | Tên bảng | Mô tả |
|-----|---------|--------|
| 1 | `Account` | Tài khoản người dùng |
| 2 | `Product` | Sản phẩm laptop |
| 3 | `Genre` | Danh mục sản phẩm (loại laptop) |
| 4 | `Brand` | Thương hiệu (ASUS, Dell, HP...) |
| 5 | `ProductImages` | Hình ảnh sản phẩm |
| 6 | `Discount` | Chương trình giảm giá / Mã khuyến mãi |
| 7 | `Order` | Đơn hàng |
| 8 | `Oder_Detail` | Chi tiết đơn hàng |
| 9 | `Payment` | Phương thức thanh toán |
| 10 | `Delivery` | Phương thức vận chuyển |
| 11 | `AccountAddress` | Địa chỉ giao hàng của người dùng |
| 12 | `OrderAddress` | Địa chỉ giao hàng của đơn hàng |
| 13 | `Provinces` | Tỉnh / Thành phố |
| 14 | `Districts` | Quận / Huyện |
| 15 | `Wards` | Phường / Xã |
| 16 | `Feedback` | Đánh giá sản phẩm |
| 17 | `ReplyFeedback` | Phản hồi đánh giá |
| 18 | `Contact` | Liên hệ |

### Vai trò người dùng (Role)

| Mã | Vai trò | Mô tả |
|----|---------|--------|
| `0` | Admin | Quản trị viên - toàn quyền hệ thống |
| `1` | Member | Thành viên - người mua hàng |
| `2` | Mod | Moderator - quản lý nội dung |

### Trạng thái tài khoản (Status)

| Giá trị | Ý nghĩa |
|---------|---------|
| `"1"` | Hoạt động (Active) |
| `"0"` | Bị vô hiệu hóa (Disabled / Trash) |

---

## Cài đặt

### Yêu cầu hệ thống

- **Windows 10/11**
- **Visual Studio 2019** hoặc **Visual Studio 2022**
- **SQL Server** hoặc **SQL Server Express** (2019 trở lên)
- **.NET Framework 4.7.2**

---

### Cách 1: Cài đặt Database bằng SSMS

**Bước 1: Mở SQL Server Management Studio (SSMS)**

```
Start Menu → SQL Server Management Studio
```

**Bước 2: Kết nối SQL Server**

```
Server name:  .\SQLEXPRESS01
              (hoặc localhost\SQLEXPRESS01)
Authentication: Windows Authentication
```

> **Lưu ý:** Nếu không kết nối được, hãy kiểm tra:
> - SQL Server service đã chạy chưa (`SQL Server (SQLEXPRESS)` đang Running)
> - Bật TCP/IP trong SQL Server Configuration Manager

**Bước 3: Mở file script SQL**

Mở file **`script.sql`** nằm trong thư mục:
```
\WebsiteLaptop\src\1Quan trọng\Database\script.sql
```

**Bước 4: Chạy script**

1. Trong SSMS, mở **New Query**
2. Copy toàn bộ nội dung `script.sql` và paste vào
3. Nhấn **Execute** (hoặc phím `F5`)
4. Chờ database `kaome` được tạo cùng với các bảng và dữ liệu

---

### Cách 2: Khôi phục từ file Backup

**Bước 1: Mở SSMS và kết nối SQL Server**

**Bước 2: Khôi phục Database**

1. Right-click vào **Databases** → **Restore Database...**
2. Chọn **Device** → nhấn `...` → **Add**
3. Dẫn đến file backup:
   ```
   D:\tvu-Project\Thi\WebsiteLaptop\WebsiteLaptop\src\1Quan trọng\Database\backupnew.bak
   ```
4. Đặt tên Database: **`kaome`**
5. Nhấn **OK** để khôi phục

**Lưu ý:** Nếu gặp lỗi về file path, hãy tạo thư mục đích trước hoặc chỉnh sửa đường dẫn trong file `.bak`.

---

### Chạy dự án bằng Visual Studio

**Bước 1: Mở Solution**

Mở file:
```
D:\tvu-Project\Thi\WebsiteLaptop\WebsiteLaptop\src\DoAn_LapTrinhWeb.sln
```

**Bước 2: Cài đặt Connection String (nếu cần)**

Kiểm tra và chỉnh sửa file **`Web.config`**:

```xml
<connectionStrings>
    <add name="Model11"
         connectionString="Server=.\SQLEXPRESS01;Database=kaome;Trusted_Connection=True;MultipleActiveResultSets=true"
         providerName="System.Data.SqlClient"/>
</connectionStrings>
```

**Hướng dẫn sửa Connection String theo SQL Server của bạn:**

| Server Name | Connection String |
|-------------|-----------------|
| SQL Express Local | `Server=.\SQLEXPRESS01;Database=kaome;Trusted_Connection=True;MultipleActiveResultSets=true` |
| SQL LocalDB | `Server=(localdb)\mssqllocaldb;Database=kaome;Trusted_Connection=True;MultipleActiveResultSets=true` |
| SQL Server có tên | `Server=YOUR_SERVER_NAME\SQLEXPRESS01;Database=kaome;Trusted_Connection=True;MultipleActiveResultSets=true` |

**Bước 3: Build dự án**

```
Build → Build Solution (Ctrl + Shift + B)
```

**Bước 4: Chạy dự án**

Nhấn **F5** hoặc **Ctrl + F5** để chạy ứng dụng.

Trình duyệt sẽ tự động mở tại địa chỉ:
```
http://localhost:xxxxx/
```

---

## Các chức năng của đồ án

### Người dùng (User)

| STT | Chức năng | Mô tả chi tiết |
|-----|-----------|---------------|
| 1 | **Trang chủ** | Hiển thị sản phẩm nổi bật, banner, danh mục |
| 2 | **Danh sách sản phẩm** | Xem, lọc, tìm kiếm laptop theo thương hiệu, danh mục, giá |
| 3 | **Chi tiết sản phẩm** | Xem thông tin, hình ảnh, đánh giá sản phẩm |
| 4 | **Giỏ hàng** | Thêm / xóa / cập nhật sản phẩm trong giỏ hàng |
| 5 | **Thanh toán** | Điền thông tin giao hàng, chọn phương thức vận chuyển & thanh toán |
| 6 | **Đăng ký** | Tạo tài khoản mới (yêu cầu email chưa đăng ký) |
| 7 | **Đăng nhập / Đăng xuất** | Xác thực tài khoản bằng email + mật khẩu |
| 8 | **Quên mật khẩu** | Gửi link reset mật khẩu qua email |
| 9 | **Trang cá nhân** | Xem / chỉnh sửa thông tin cá nhân |
| 10 | **Đổi mật khẩu** | Thay đổi mật khẩu tài khoản |
| 11 | **Quản lý địa chỉ** | Thêm / sửa / xóa / đặt địa chỉ mặc định |
| 12 | **Theo dõi đơn hàng** | Xem lịch sử đơn hàng và chi tiết từng đơn |
| 13 | **Đánh giá sản phẩm** | Gửi đánh giá (sao + bình luận) cho sản phẩm đã mua |
| 14 | **Áp dụng mã giảm giá** | Nhập mã khuyến mãi khi thanh toán |

### Quản trị (Admin)

Truy cập trang admin tại: `/Admin/`

| STT | Chức năng | Mô tả chi tiết |
|-----|-----------|---------------|
| 1 | **Dashboard** | Thống kê tổng quan (đơn hàng, doanh thu, sản phẩm) |
| 2 | **Quản lý sản phẩm** | Thêm / sửa / xóa / xem sản phẩm |
| 3 | **Quản lý thương hiệu** | CRUD thương hiệu laptop |
| 4 | **Quản lý danh mục** | CRUD danh mục sản phẩm (loại laptop) |
| 5 | **Quản lý đơn hàng** | Xem / cập nhật trạng thái đơn hàng |
| 6 | **Quản lý tài khoản** | Xem / phân quyền / vô hiệu hóa tài khoản |
| 7 | **Quản lý đánh giá** | Xem / phản hồi đánh giá của khách hàng |
| 8 | **Quản lý mã giảm giá** | Thêm / sửa / xóa chương trình khuyến mãi |
| 9 | **Thùng rác (Trash)** | Xem / khôi phục các mục đã xóa |

---

## Tài khoản đăng nhập

> **Quan trọng:** Bạn cần tự tạo tài khoản Admin trong database nếu chưa có.

### Cách tạo tài khoản Admin

**Cách 1: Qua SQL (SSMS)**

Chạy câu lệnh SQL sau trong database `kaome`:

```sql
-- Insert tài khoản Admin (Role = 0, Status = "1")
INSERT INTO Account (password, Email, Name, Phone, Role, status, create_by, create_at, update_by, update_at)
VALUES (
    '201BCE2458F00A54130C695CA8D1658319B32206D495ADF175847B57BD4A4151',  -- Mật khẩu: Admin123@ (đã mã hóa SHA1)
    'admin@kaome.com',
    'Administrator',
    '0123456789',
    0,
    '1',
    'system',
    GETDATE(),
    'system',
    GETDATE()
);
```

**Cách 2: Qua trang đăng ký**

1. Truy cập trang đăng ký: `/Account/Register`
2. Tạo tài khoản mới
3. Sau đó chạy SQL để nâng quyền lên Admin:

```sql
UPDATE Account SET Role = 0 WHERE Email = 'email_cua_ban@xxx.com';
```

### Thông tin đăng nhập mẫu (sau khi tạo)

| Vai trò | Email | Mật khẩu |
|---------|-------|---------|
| **Admin** | `admin@kaome.com` | `Admin123@` |
| **Member** | *(tự đăng ký)* | *(tự đặt)* |

> **Lưu ý:** Mật khẩu được mã hóa bằng `Crypto.Hash()` (SHA1 + salt). Nếu muốn đăng nhập với mật khẩu dạng plain-text, bạn cần đăng ký tài khoản mới rồi gán quyền Admin.

---

## Sitemap / Map của trang web

### Trang người dùng

```
Trang chủ (/)
├── /Products
│   └── /Products/ProductDetail/{id}
├── /Cart
│   ├── /Cart/ViewCart
│   ├── /Cart/PreviewCart
│   └── /Cart/Checkout
├── /Account
│   ├── /Account/Login
│   ├── /Account/Register
│   ├── /Account/ForgotPassword
│   ├── /Account/ResetPassword/{code}
│   ├── /Account/Dashboard          (yêu cầu đăng nhập)
│   ├── /Account/Editprofile        (yêu cầu đăng nhập)
│   ├── /Account/ChangePassword      (yêu cầu đăng nhập)
│   ├── /Account/Address             (yêu cầu đăng nhập)
│   ├── /Account/TrackingOrder       (yêu cầu đăng nhập)
│   └── /Account/TrackingOrderDetail/{id} (yêu cầu đăng nhập)
├── /Home/SentRequest
└── /pagenotfound
```

### Trang quản trị Admin

```
/Admin/
├── /Admin/DashBoards/Index         (Dashboard - Thống kê)
├── /Admin/ProductsAdmin/
│   ├── /Admin/ProductsAdmin/Index
│   ├── /Admin/ProductsAdmin/Create
│   ├── /Admin/ProductsAdmin/Edit/{id}
│   ├── /Admin/ProductsAdmin/Details/{id}
│   └── /Admin/ProductsAdmin/Trash
├── /Admin/Brands/
│   └── /Admin/Brands/Index
├── /Admin/Genres/
│   └── /Admin/Genres/Index
├── /Admin/Orders/
│   ├── /Admin/Orders/Index
│   ├── /Admin/Orders/Details/{id}
│   └── /Admin/Orders/Trash
├── /Admin/Auth/                     (Quản lý tài khoản)
│   ├── /Admin/Auth/Index
│   ├── /Admin/Auth/Details/{id}
│   └── /Admin/Auth/Trash
├── /Admin/Feedbacks/
│   └── /Admin/Feedbacks/Index
└── /Admin/Discounts/
    └── /Admin/Discounts/Index
```

---

## Các link quan trọng

| Mục | Đường dẫn |
|-----|-----------|
| Trang chủ | `http://localhost:xxxxx/` |
| Trang Admin | `http://localhost:xxxxx/Admin/` |
| Dashboard Admin | `http://localhost:xxxxx/Admin/DashBoards/Index` |
| Đăng nhập | `http://localhost:xxxxx/Account/Login` |
| Đăng ký | `http://localhost:xxxxx/Account/Register` |
| Quên mật khẩu | `http://localhost:xxxxx/Account/ForgotPassword` |
| Danh sách sản phẩm | `http://localhost:xxxxx/Products` |
| Giỏ hàng | `http://localhost:xxxxx/Cart/ViewCart` |
| Thanh toán | `http://localhost:xxxxx/Cart/Checkout` |
| Trang cá nhân | `http://localhost:xxxxx/Account/Dashboard` |
| Quản lý địa chỉ | `http://localhost:xxxxx/Account/Address` |
| Theo dõi đơn hàng | `http://localhost:xxxxx/Account/TrackingOrder` |
| Lỗi 404 | `http://localhost:xxxxx/pagenotfound` |

---

## Cấu hình kết nối Database

File cấu hình: **`Web.config`** (dòng 79-81)

```xml
<connectionStrings>
    <add name="Model11"
         connectionString="Server=.\SQLEXPRESS01;Database=kaome;Trusted_Connection=True;MultipleActiveResultSets=true"
         providerName="System.Data.SqlClient"/>
</connectionStrings>
```

**Thành phần:**
- `Server=.\SQLEXPRESS01` → Tên SQL Server instance
- `Database=kaome` → Tên database
- `Trusted_Connection=True` → Dùng Windows Authentication
- `MultipleActiveResultSets=true` → Cho phép nhiều command cùng lúc

### Cấu hình Email (Gửi mail)

File: **`Common/EmailConfig.cs`**

Cấu hình SMTP Gmail để gửi email reset mật khẩu. Bạn cần thay đổi:
- `emailID` → Email gửi (Gmail của bạn)
- `emailPassword` → Mật khẩu ứng dụng Gmail (App Password)
- `emailName` → Tên hiển thị người gửi
- `emailHost` → `smtp.gmail.com`

> **Lưu ý:** Với Gmail, bạn cần bật **2-Factor Authentication** và tạo **App Password** để sử dụng SMTP.

---

## Xử lý lỗi thường gặp

### Lỗi 1: "A network-related or instance-specific error occurred..."

**Nguyên nhân:** SQL Server không tìm thấy hoặc không chạy.

**Cách sửa:**
1. Mở **SQL Server Configuration Manager**
2. Kiểm tra **SQL Server (SQLEXPRESS01)** đang chạy (Running)
3. Bật **TCP/IP** protocol nếu chưa bật
4. Khởi động lại SQL Server service

### Lỗi 2: "Connection string is not valid"

**Nguyên nhân:** Connection string trong `Web.config` sai.

**Cách sửa:**
1. Mở SSMS, ghi nhận đúng **Server Name** của bạn
2. Sửa `Server=.\SQLEXPRESS01` trong `Web.config` cho đúng
3. Kiểm tra tên database `kaome` đã tồn tại chưa

### Lỗi 3: Database chưa được tạo

**Cách sửa:**
1. Chạy file `script.sql` trong SSMS
2. Hoặc khôi phục từ file `backupnew.bak`
3. Entity Framework sẽ tự động chạy Migration khi ứng dụng khởi động

### Lỗi 4: "Login failed" hoặc "Cannot open database"

**Cách sửa:**
1. Kiểm tra tên database đúng là `kaome`
2. Kiểm tra user có quyền truy cập database
3. Thử dùng `Trusted_Connection=True` (Windows Auth) thay vì SQL Auth

### Lỗi 5: Entity Framework Migration lỗi

**Cách sửa:**
1. Xóa folder `Migrations` trong project
2. Mở **Package Manager Console** trong Visual Studio:
   ```
   Enable-Migrations
   Add-Migration InitialCreate
   Update-Database
   ```

---

## Liên hệ / Hỗ trợ

Nếu gặp vấn đề khi cài đặt, vui lòng kiểm tra:
1. SQL Server service đã chạy
2. Connection string đúng với SQL Server của bạn
3. Database `kaome` đã được tạo
4. Visual Studio đã restore NuGet packages

---

*Đồ án Lập Trình Web - Website Bán Laptop*
