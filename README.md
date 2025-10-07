# 1. Mô tả yêu cầu hệ thống (Hotel Booking System)
## Mục tiêu
Xây dựng hệ thống quản lý đặt phòng khách sạn cho phép khách hàng đặt phòng online, thanh toán trực tuyến, và hỗ trợ nhân viên khách sạn trong các quy trình check-in / check-out, quản lý phòng, báo cáo doanh thu, và buồng phòng.
Hệ thống hướng đến tính tự động hóa, thuận tiện, và chính xác trong quy trình vận hành khách sạn.
## Các tác nhân (Actors)
| Tác nhân                              | Mô tả vai trò                                                                                   |
| ------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Guest (Khách hàng)**                | Người dùng bên ngoài, có thể tìm phòng, xem thông tin chi tiết, đặt phòng và thanh toán online. |
| **Receptionist (Lễ tân)**             | Quản lý đặt phòng, hỗ trợ khách check-in / check-out, cập nhật trạng thái phòng.                |
| **Manager (Quản lý)**                 | Theo dõi doanh thu, điều chỉnh giá phòng, và xem báo cáo hoạt động.                             |
| **Housekeeping (Buồng phòng)**        | Cập nhật trạng thái vệ sinh phòng (đã dọn, cần dọn, đang sử dụng).                              |
| **Payment Gateway (Cổng thanh toán)** | Thực hiện và xác nhận giao dịch thanh toán online cho khách hàng.                               |

## Các chức năng chính (Use Case)
| STT | Tên Use Case                       | Mô tả ngắn gọn                                                                            | Tác nhân chính         |
| --- | ---------------------------------- | ----------------------------------------------------------------------------------------- | ---------------------- |
| 1   | **Tìm phòng / Xem chi tiết phòng** | Cho phép khách tìm kiếm phòng trống theo ngày, loại phòng, giá và xem thông tin chi tiết. | Guest                  |
| 2   | **Đặt phòng online (Booking)**     | Khách chọn phòng, nhập thông tin cá nhân, và gửi yêu cầu đặt phòng.                       | Guest                  |
| 3   | **Thanh toán online**              | Liên kết với cổng thanh toán để thực hiện giao dịch và xác nhận đặt phòng.                | Guest, Payment Gateway |
| 4   | **Check-in / Check-out**           | Lễ tân xác nhận khách đến, gán phòng thực tế, tính chi phí và hoàn tất trả phòng.         | Receptionist           |
| 5   | **Quản lý phòng & giá**            | Quản lý danh sách phòng, loại phòng, cập nhật giá, trạng thái.                            | Manager                |
| 6   | **Quản lý đặt phòng**              | Xem, sửa, hủy, xác nhận đặt phòng của khách.                                              | Receptionist           |
| 7   | **Công việc buồng phòng**          | Cập nhật tình trạng vệ sinh phòng sau khi khách rời đi.                                   | Housekeeping           |
| 8   | **Báo cáo doanh thu**              | Thống kê doanh thu theo ngày, tháng, năm, hoặc theo loại phòng.                           | Manager                |

## Mô tả dữ liệu (Entities)
| Bảng            | Mô tả                                     | Các thuộc tính chính                                                |
| --------------- | ----------------------------------------- | ------------------------------------------------------------------- |
| **Guest**       | Lưu thông tin khách hàng đặt phòng        | GuestID, Name, Phone, Email, Address                                |
| **RoomType**    | Mô tả loại phòng (Deluxe, Standard...)    | TypeID, Name, Price, Capacity, Description                          |
| **Room**        | Quản lý từng phòng cụ thể                 | RoomID, TypeID, Status, Floor                                       |
| **Reservation** | Ghi nhận thông tin đặt phòng              | ResvID, GuestID, RoomID, StaffID, CheckInDate, CheckOutDate, Status |
| **Payment**     | Lưu chi tiết thanh toán cho mỗi đặt phòng | PaymentID, ResvID, Amount, Method, Status, Date                     |
| **Staff**       | Quản lý thông tin nhân viên               | StaffID, Name, Role, Username, PasswordHash                         |

## Luồng xử lý chính
a) Đặt phòng online
Khách tìm phòng trống → chọn phòng.
Hệ thống giữ phòng tạm thời (hold).
Khách nhập thông tin cá nhân.
Thanh toán online qua cổng Payment Gateway.
Hệ thống xác nhận, lưu dữ liệu và gửi email cho khách.
b) Check-in / Check-out
Lễ tân tra cứu mã đặt phòng.
Check-in: gán phòng thực tế, cập nhật trạng thái phòng
Check-out: tính tổng chi phí, thu tiền, cập nhật buồng phòng và trạng thái phòng.
## Yêu cầu phi chức năng
| Nhóm yêu cầu          | Mô tả                                                            |
| --------------------- | ---------------------------------------------------------------- |
| **Hiệu năng**         | Tìm phòng và phản hồi kết quả trong ≤ 3 giây.                    |
| **Bảo mật**           | Mã hóa mật khẩu nhân viên, giao thức thanh toán an toàn (HTTPS). |
| **Khả năng mở rộng**  | Cho phép thêm chi nhánh khách sạn hoặc loại phòng mới.           |
| **Khả năng tích hợp** | Hệ thống có thể kết nối với API thanh toán hoặc CRM khách hàng.  |
| **Tính thân thiện**   | Giao diện dễ sử dụng, hỗ trợ khách đặt phòng nhanh chóng.        |
