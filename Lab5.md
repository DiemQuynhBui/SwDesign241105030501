# Thiết kế hệ thống con trong Payroll System
## 1. Giới thiệu
Để thiết kế các hệ thống con (subsystems) trong Payroll System, chúng ta sẽ dựa vào các phân tích ca sử dụng (Login, Maintain Timecard, và Run Payroll) từ bài Lab4, với trọng tâm là tổ chức các đối tượng thiết kế thành các subsystem hợp lý. 
## 2. Thiết kế các hệ thống con
### 2.1. Login Subsytems
#### Mục đích:
+ Cung cấp chức năng đăng nhập cho người dùng.  
+ Đảm bảo an toàn trong việc xác thực tài khoản.
  
#### Chức năng chính:
+ Nhận thông tin đăng nhập từ người dùng.
+ Xác thực thông tin người dùng dựa vào cơ sở dữ liệu.
+ Quản lý phiên đăng nhập.
  
#### Thành phần:
+ **LoginForm**: Giao diện người dùng để nhập thông tin đăng nhập.
+ **LoginController**: Điều phối logic xử lý đăng nhập.
+ **AuthenticationService**: Xác thực thông tin người dùng.
+ **EmployeeDatabase**: Lưu trữ thông tin tài khoản.
  
#### Luồng hoạt động chính:
 **1**. Người dùng nhập username và password vào **LoginForm**.

 **2**. **LoginController** gửi thông tin đến **AuthenticationService** để xác thực.

 **3**. **AuthenticationService** kiểm tra thông tin trong **EmployeeDatabase**.
+ Nếu hợp lệ, khởi tạo phiên làm việc.
+ Nếu không hợp lệ, trả về thông báo lỗi.
  
#### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/b99DJiCm48NtEOML5InwWIvGKQ4hLerWFt56gLN_H3FZeWhrP2mu4bV0iO8II8h4BBpmlFUDtjYVxnyR5Y29pXOTw2EqgCgdq1glgbZpcGLTgTuAbKfRO5QvkGlaXjjSaP4yE5HhLGaPtuwjBfbU0pKBBOwrCt9pcsyk-VmzQ1kyKB0MQJhk1DOq89WbWp-N0vyILCXiWhy6lezoG2z6WoHLXNGo6gTuVK1zt18slGeiNmCzkiw6C-832DJ0FnWjodDQof-KSPMhrTqixrgLLLwGqYEa78qJQMzVJfKWByEovfXbIm-R9KkS7Oe-v9V-3saXrHubalz-nAHNX1ojbCMbsA1l-h_u1G00__y30000)

### 2.2. Timecard Management Subsystem
#### Mục đích:
+ Cung cấp chức năng quản lý bảng chấm công cho nhân viên.
  
#### Chức năng chính:
+ Hiển thị và chỉnh sửa bảng chấm công.
+ Lưu bảng chấm công vào cơ sở dữ liệu.
+ Xác thực mã dự án hợp lệ.
  
#### Thành phần:
+ **TimecardForm**: Giao diện nhập liệu bảng chấm công.
+ **TimecardController**: Điều phối logic xử lý nghiệp vụ.
+ **TimecardDatabase**: Lưu trữ dữ liệu bảng chấm công và mã dự án.
  
#### Luồng hoạt động chính:
 **1**. **TimecardForm** hiển thị bảng chấm công hiện tại của nhân viên.

 **2**. Người dùng nhập hoặc chỉnh sửa bảng chấm công.

 **3**. **TimecardController** kiểm tra tính hợp lệ và lưu vào **TimecardDatabase**.
 
#### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/X99D2i8m44RtFSNGbIwyG1SYA88BGT0BZCrGelafcL4euibSU2IlO2ksfYewgv1yl3UJv7QvJbWmoC6QfCHyZmL1kj6MSWmAbkZg3KjEO7tOSiL2DeLJ0dNb1fcXZSvziC-3HodDfS6gFHwGBOslY1Qp3DOIj2k6hp0fBLrIdeltv3dvefrw9y4RGo6M7z5eXK8TCt8n7kd3bNN07wuP2cwHAJQn-F0VzwY2P1NyZdAPUaKyw9bwrpWQZRyDc45QFuBL0gq7wY4nxG6YV8pfUcyWJS_lZ7Co8QUQNt07003__mC0)

### 2.3. Payroll Processing Subsystem
#### Mục đích:
+ Xử lý tính toán lương và quản lý thanh toán.
  
#### Chức năng chính:
+ Thu thập dữ liệu nhân viên và bảng chấm công.
+ Tính toán lương.
+ Tạo phiếu lương và điều phối thanh toán.
  
#### Thành phần:
+ **PayrollController**: Điều phối toàn bộ quy trình.
+ **PaycheckManager**: Quản lý việc tạo và lưu trữ phiếu lương.
+ **EmployeeDatabase, TimecardDatabase**: Cung cấp dữ liệu cần thiết.
  
#### Luồng hoạt động chính:

 **1**. **PayrollController** khởi động quá trình tính lương theo lịch.

 **2**. Thu thập dữ liệu từ các cơ sở dữ liệu.

 **3**. **PaycheckManager** tạo phiếu lương và gửi thông tin đến hệ thống thanh toán hoặc in ấn.

#### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/XD9DQiCm40NWlKynUDKkSe4kIg3jiX2QNc0o7bmJ_HZDE61AJjP5ZzGhL3OAaItIQc63tlEdGVZdwtihYa47QweUwOWjGxt3CNXZO1SyiKZdMjWF1nb5sTRmMK5SP504KlF9EvtU758whnbEZIjrTtzjqFGDwJCgfktp_5oUG1zCnrTqSRQ5Ju5H-LB8NS7JUh-0Nsnl_CWy7Nv0uLnkMVFu5l7UMIOCpGqYZqkYlBhDvh6SwW7gDzRGyOc1KmXDJEi_b6AmND4K_gkihpuYUtOD41eQ36hdtT9Oj9EmSYz6dzeWWxKOnhewLziOJF_XBm000F__0m00)
 

### 2.4. Banking Subsystem
#### Mục đích:
+ Thực hiện các giao dịch thanh toán lương qua ngân hàng.
  
#### Chức năng chính:
+ Chuyển khoản ngân hàng cho nhân viên.
+ Kiểm tra trạng thái giao dịch.
  
#### Thành phần:
+ **BankingService**: Kết nối và giao tiếp với hệ thống ngân hàng bên ngoài.
  
#### Luồng hoạt động chính:
 **1**. **PayrollController** gửi thông tin thanh toán đến BankingService.

 **2**. **BankingService** thực hiện giao dịch chuyển khoản.

 **3**. Trả kết quả giao dịch về **PayrollControlle**.

  #### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/V54xRiCm3Drz2a9JE-G27OeWcReLTIx0AW-9O5bsHIf0KEHa7NgaNg6suYA2ZPI3D3o-7_ZpzRqMvQYfzLNFjk43o6muD2uSg4xlSXP5Q-Ypec6iPn5wvNFilDzsGSSVSKBp2C9-M6WHz0qV2Q8FZnczvBUGcLngn9EpA3Nws5c8x287OQkk2vD67dk4RGgiLjOa_xcKsX4MxeGfufArBBTQFS-pFf6fXvxKNrLe3sNdnMI5sUuVVIIz1AUE5QIt-3VI7QUYAadkUjTd6Nx6Zv3arLINQZta7u_-2m00__y30000)

### 2.5. Printing Subsystem
#### Mục đích:
+ Hỗ trợ in phiếu lương cho nhân viên không dùng phương thức thanh toán qua ngân hàng.
  
#### Chức năng chính:
+ Tạo và in phiếu lương dưới dạng tài liệu.
  
#### Thành phần:
+ **PrintingService**: Quản lý việc in ấn phiếu lương.
  
#### Luồng hoạt động chính:
 **1**. **PayrollController** gửi yêu cầu in đến **PrintingService**.

 **2**. **PrintingService** tạo tài liệu từ dữ liệu phiếu lương và in ra máy in

#### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/P51B3e8m4Dtt59EkTC45M1WIEG2H4unrGXfBY-tKX1XEvi8ZUGN5WcAOpMJolfdd_L44Hi-nDQ93TSQ6G5PUMzQsWJeUGn-OMWat0UzH1aE06Q_9NxMY2VjCGvOyCfLEnPOiRphilJEcHCOSgdHiV_nkjFgI4p28PLQIx9tbSPDVfdcwH0eyz_dNhvLPjbjrpq4UaWkmItLWwYp580gof_4tBm000F__0m00)

### 2.6. Security Subsystem 
#### Mục đích:
+ Đảm bảo an toàn cho dữ liệu nhạy cảm trong hệ thống.
+ Quản lý xác thực người dùng và kiểm soát quyền truy cập.
  
#### Chức năng chính:
+ Kiểm tra thông tin đăng nhập của người dùng.
+ Quản lý quyền truy cập dựa trên vai trò của người dùng.
+ Mã hóa dữ liệu nhạy cảm trong hệ thống.
  
#### Thành phần:
+ **AuthenticationManager**:
  
  + Kiểm tra thông tin đăng nhập.
  + Cung cấp phương thức xác thực:
      +  **validate(username, password)**
      + **manageAccess(employeeID, resource)**
        
+ **RoleManager**:
  + Quản lý quyền của từng vai trò trong hệ thống.
  + Xác định các tài nguyên mà mỗi vai trò có thể truy cập.
    
+ **EmployeeDatabase**: Lưu trữ thông tin tài khoản và vai trò của nhân viên.
  
+ **EncryptionService**: Mã hóa dữ liệu nhạy cảm như mật khẩu.
  
#### Luồng hoạt động chính:
**1**. **LoginController** gửi yêu cầu xác thực đến **AuthenticationManager** với thông tin đăng nhập của người dùng.
   
**2**. **AuthenticationManager** kiểm tra thông tin trong **EmployeeDatabase**:
+ Nếu thông tin hợp lệ, trả về trạng thái thành công.
+ Nếu không, trả về lỗi xác thực.

**3**. **AuthenticationManager** sử dụng **RoleManager** để kiểm tra quyền truy cập của người dùng vào tài nguyên.

**4**. **EncryptionService** hỗ trợ mã hóa và giải mã mật khẩu trong suốt quá trình xác thực.

#### Mô hình hệ thống con:
![diagram](https://www.planttext.com/api/plantuml/png/Z5AxJiGm4Epp5LQg876YlmBTYO14GNCHz7lEAh58x6XtSoX2zsKKV1A_WFE094hGuTBZcPsTyTV7vuu5IEgo22hGhv2X2XFKDHbfL58VkM71CbJlWV975y2izhNaQCLe4EFi4rZFek55TqvGc1G4evgHB9IuLOcGiTcrghp0cwFqv-PgP9MTq5vhP8wmh0hN83x68vUGNKqQvznpCB5sS0Mk6FAGoMmBhWjxOCLGXjAxEPWi5uwMpsQpxmVb60IEm3WruAMUVHQBG2RJM1pX7M7QHWi5_pkykGchgQdQNXAaaz4p5zY3aUy6LXoa-1SyZ5WlVhEvNUw-LU43YiwL7ZSABuXCo_Fyb-4NAUXAKDIrS4ba6O2N6Yvludx3to2zsZdOeKtR__yD003__mC0)

## 3. Kết Luận
Thiết kế các hệ thống con trong Payroll System nhằm đảm bảo hệ thống hoạt động ổn định, có khả năng mở rộng và dễ bảo trì. Mỗi subsystem chịu trách nhiệm một phần công việc cụ thể, từ đăng nhập, quản lý bảng chấm công, đến xử lý lương và thanh toán. Việc phân chia này giúp giảm thiểu sự phụ thuộc giữa các thành phần, đồng thời tạo điều kiện để phát triển từng phần một cách độc lập.







  

  


