# 1. Bảng Guest (Khách hàng)
| Trường  | Kiểu dữ liệu | Khóa | Mô tả             |
| ------- | ------------ | ---- | ----------------- |
| GuestID | INT (PK)     | PK   | Mã khách hàng     |
| Name    | VARCHAR(100) |      | Họ tên khách hàng |
| Phone   | VARCHAR(15)  |      | Số điện thoại     |
| Email   | VARCHAR(100) |      | Email khách hàng  |
| Address | VARCHAR(200) |      | Địa chỉ           |

# 2. Bảng RoomType (Loại phòng)
| Trường      | Kiểu dữ liệu  | Khóa | Mô tả                          |
| ----------- | ------------- | ---- | ------------------------------ |
| TypeID      | INT (PK)      | PK   | Mã loại phòng                  |
| Name        | VARCHAR(50)   |      | Tên loại phòng (Standard, VIP) |
| Price       | DECIMAL(10,2) |      | Giá phòng                      |
| Capacity    | INT           |      | Sức chứa (số khách tối đa)     |
| Description | VARCHAR(200)  |      | Mô tả chi tiết                 |

# 3. Bảng Room (Phòng cụ thể)
| Trường | Kiểu dữ liệu | Khóa | Mô tả                           |
| ------ | ------------ | ---- | ------------------------------- |
| RoomID | INT (PK)     | PK   | Mã phòng                        |
| TypeID | INT (FK)     | FK   | Liên kết đến RoomType.TypeID    |
| Status | VARCHAR(20)  |      | Tình trạng (Available/Occupied) |
| Floor  | INT          |      | Tầng                            |

# 4. Bảng Reservation (Đặt phòng)
| Trường       | Kiểu dữ liệu | Khóa | Mô tả                                      |
| ------------ | ------------ | ---- | ------------------------------------------ |
| ResvID       | INT (PK)     | PK   | Mã đặt phòng                               |
| GuestID      | INT (FK)     | FK   | Khách đặt phòng (Guest.GuestID)            |
| RoomID       | INT (FK)     | FK   | Phòng được đặt (Room.RoomID)               |
| StaffID      | INT (FK)     | FK   | Nhân viên xử lý (Staff.StaffID)            |
| CheckInDate  | DATE         |      | Ngày nhận phòng                            |
| CheckOutDate | DATE         |      | Ngày trả phòng                             |
| Status       | VARCHAR(20)  |      | Trạng thái (Pending/Confirmed/Checked-out) |

# 5. Bảng Payment (Thanh toán)
| Trường    | Kiểu dữ liệu  | Khóa | Mô tả                             |
| --------- | ------------- | ---- | --------------------------------- |
| PaymentID | INT (PK)      | PK   | Mã giao dịch                      |
| ResvID    | INT (FK)      | FK   | Mã đặt phòng (Reservation.ResvID) |
| Amount    | DECIMAL(10,2) |      | Số tiền thanh toán                |
| Method    | VARCHAR(50)   |      | Hình thức (Card, Cash, eWallet)   |
| Status    | VARCHAR(20)   |      | Trạng thái (Pending/Success)      |
| Date      | DATETIME      |      | Ngày giờ thanh toán               |

# 6. Bảng Staff (Nhân viên)
| Trường       | Kiểu dữ liệu | Khóa | Mô tả                          |
| ------------ | ------------ | ---- | ------------------------------ |
| StaffID      | INT (PK)     | PK   | Mã nhân viên                   |
| Name         | VARCHAR(100) |      | Tên nhân viên                  |
| Role         | VARCHAR(50)  |      | Vai trò (Receptionist/Manager) |
| Username     | VARCHAR(50)  |      | Tài khoản đăng nhập            |
| PasswordHash | VARCHAR(200) |      | Mật khẩu mã hóa                |

# 7. Mối quan hệ (ERD)
| Quan hệ               | Loại quan hệ |
| --------------------- | ------------ |
| Guest – Reservation   | 1 → N        |
| Reservation – Payment | 1 → N        |
| RoomType – Room       | 1 → N        |
| Room – Reservation    | 1 → N        |
| Staff – Reservation   | 1 → N        |
