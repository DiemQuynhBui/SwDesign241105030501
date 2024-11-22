# Payroll System Design Documentation
# 1. giới thiệu
Tài liệu trình bày chi tiết về thiết kế hệ thống Payroll System với các tính năng chính như Login, Maintain Timecard và  Run Payroll hệ thống nhằm mục tiêu giảm thiểu sai sót trong việc xử lý lương, tăng hiệu suất quản lý thời gian và chi phí, đảm bảo tính minh bạch và bảo mật dữ liệu.
# 2. Các bước thực hiện
## 2.1 Describe Interaction Among Design Objects
### Mô tả cách các đối tượng thiết kế tương tác để thực hiện từng ca sử dụng:
### Ca sử dụng: Login
**Mục tiêu**: Người dùng xác thực để truy cập hệ thống.
#### Đối tượng thiết kế:
+ **LoginForm** (boundary): Nhận thông tin đăng nhập từ người dùng.
+ **LoginController** (control): Xử lý logic xác thực.
+ **EmployeeDatabase** (entity): Lưu trữ thông tin người dùng và kiểm tra xác thực.
#### Mô tả tương tác:
+ Người dùng nhập tên đăng nhập và mật khẩu vào **LoginForm**.
+ **LoginForm** gửi thông tin đến **LoginController** để kiểm tra.
+ **LoginController** tương tác với EmployeeDatabase để xác thực thông tin.
+ Trả kết quả xác thực về **LoginForm** để thông báo cho người dùng.
  ## 2.2 Simplify Sequence Diagrams Using Subsystems
  
  


