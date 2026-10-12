# Thiết kế REST API cho ứng dụng Quản lý nhân sự

## Phần 1: Lý thuyết — Lý do chọn REST thay vì SOAP

Em chọn kiến trúc REST cho ứng dụng Quản lý nhân sự vì REST linh hoạt, dễ xây dựng và dễ tích hợp với ứng dụng web hoặc di động. REST hỗ trợ nhiều định dạng dữ liệu, trong đó JSON thường được sử dụng vì gọn nhẹ, dễ đọc và dễ xử lý. Trong khi đó, SOAP sử dụng thông điệp XML với cấu trúc chặt chẽ, thường làm tăng kích thước dữ liệu truyền tải. Khi sử dụng JSON, REST có thể giảm lượng dữ liệu truyền qua mạng và chi phí xử lý so với thông điệp SOAP tương đương, phù hợp với các thao tác quản lý nhân viên thường xuyên. REST cũng tận dụng các phương thức HTTP như GET, POST, PUT và DELETE, giúp thiết kế API rõ ràng và thuận tiện bảo trì. Vì ứng dụng chủ yếu thực hiện các chức năng CRUD và chưa cần các cơ chế chuyên biệt của SOAP, REST là lựa chọn phù hợp. Tuy nhiên, hiệu năng thực tế còn phụ thuộc vào cách triển khai, không chỉ vào việc chọn REST hay SOAP.

## Phần 2: Thiết kế API cho tài nguyên Employee

Quy ước đường dẫn gốc là `/employees`. Tên tài nguyên dùng danh từ số nhiều, không đưa động từ vào URL. `{id}` là mã định danh của nhân viên, ví dụ `/employees/1`.

| STT | Hành động | HTTP Method | Endpoint | Mô tả |
| --- | --- | --- | --- | --- |
| 1 | Lấy danh sách tất cả nhân viên | `GET` | `/employees` | Trả về danh sách nhân viên. |
| 2 | Lấy thông tin một nhân viên theo ID | `GET` | `/employees/{id}` | Trả về thông tin nhân viên có ID được chỉ định. |
| 3 | Tạo mới một nhân viên | `POST` | `/employees` | Nhận thông tin nhân viên trong request body dạng JSON và tạo nhân viên mới. |
| 4 | Cập nhật thông tin nhân viên | `PUT` | `/employees/{id}` | Cập nhật toàn bộ các trường thông tin có thể chỉnh sửa của nhân viên theo ID bằng dữ liệu JSON trong request body. |
| 5 | Xóa một nhân viên | `DELETE` | `/employees/{id}` | Xóa nhân viên có ID được chỉ định. |

**Lưu ý:** Bảng trên sử dụng `PUT` cho cập nhật toàn bộ thông tin. Nếu chỉ cập nhật một phần, chẳng hạn chỉ đổi email, có thể dùng `PATCH /employees/{id}`. Các URL không sử dụng dạng chứa động từ như `/getEmployees`, `/createEmployee` hoặc `/deleteEmployee/1`.
