# Payroll System Design Documentation
# 1. Giới thiệu
Tài liệu trình bày chi tiết về thiết kế hệ thống Payroll System với các tính năng chính như Login, Maintain Timecard và  Run Payroll hệ thống nhằm mục tiêu giảm thiểu sai sót trong việc xử lý lương, tăng hiệu suất quản lý thời gian và chi phí, đảm bảo tính minh bạch và bảo mật dữ liệu.
# 2. Các bước thực hiện
## 2.1. Describe Interaction Among Design Objects
### Mô tả cách các đối tượng thiết kế tương tác để thực hiện từng ca sử dụng:
### Ca sử dụng: Login
**Mục tiêu**: Xác thực thông tin người dùng để cấp quyền truy cập hệ thống.
#### Đối tượng thiết kế:
+ **LoginForm** (Boundary): Giao diện nhận thông tin đăng nhập từ người dùng.

+ **LoginController** (Control): Thực hiện kiểm tra logic xác thực.

+ **EmployeeDatabase** (Entity): Nơi lưu trữ thông tin tài khoản và xử lý yêu cầu xác thực.

#### Mô tả tương tác:
+ Người dùng nhập thông tin đăng nhập thông qua **LoginForm**.
  
+ **LoginForm** chuyển thông tin đến **LoginController** để xử lý.
  
+ **LoginController** kiểm tra thông tin từ **EmployeeDatabase**.
  
+ Kết quả xác thực được gửi lại **LoginForm** để thông báo cho người dùng.
  
### Ca sử dụng: Maintain Timecard
**Mục tiêu**: Cập nhật bảng chấm công cho nhân viên.
#### Đối tượng thiết kế:
+ **TimecardForm** (Boundary): Giao diện hiển thị và chỉnh sửa bảng chấm công.

+ **TimecardController** (Control): Điều phối thao tác nghiệp vụ liên quan đến bảng chấm công.

+ **ProjectManagementDatabase** (Entity): Lưu trữ thông tin giờ làm việc và mã dự án.

#### Mô tả tương tác:
+ Nhân viên mở **TimecardForm** để xem bảng chấm công.
  
+ **TimecardForm** yêu cầu dữ liệu từ **TimecardController**.
  
+ **TimecardController** truy xuất thông tin từ **ProjectManagementDatabase**.
  
+ Người dùng chỉnh sửa dữ liệu trong **TimecardForm** và gửi thay đổi qua **TimecardController** để cập nhật vào cơ sở dữ liệu.
  
### Ca sử dụng: Run Payroll
**Mục tiêu**: Tính toán và thực hiện thanh toán lương cho nhân viên.
#### Đối tượng thiết kế:
+ **PayrollController** (Control): Điều phối các bước tính toán và xử lý lương.

+ **Employee, Timecard, Paycheck** (Entity): Quản lý thông tin nhân viên, giờ làm việc và kết quả tính lương.

+ **BankSystem và PrintService** (Boundary): Thực hiện thanh toán qua ngân hàng hoặc in phiếu lương.

#### Mô tả tương tác:
+ **PayrollController** được kích hoạt bởi **SystemClock**.
  
+ **PayrollController** thu thập thông tin từ các thực thể **Employee** và **Timecard**.
  
+ Lương được tính toán và tạo đối tượng **Paycheck**.
  
+ Thanh toán được thực hiện qua **BankSystem** hoặc **PrintService**, tùy thuộc vào phương thức của từng nhân viên.
   
## 2.2 Simplify Sequence Diagrams Using Subsystems

  #### Hệ thống con sử dụng:
+ **BankSystem**: Xử lý các giao dịch ngân hàng thông qua interface IBankSystem.

+ **PrintService**: Cung cấp chức năng in phiếu lương thông qua interface IPrintService.

+ **ProjectManagementDatabase**: Quản lý dữ liệu liên quan đến dự án và giờ làm việc.
  
**Ví dụ biểu đồ trình tự: Ca sử dụng Run Payroll**
  ![diagram](https://www.planttext.com/api/plantuml/png/X5DBJiD03DtFARnC9BX05wYY1QaII4XmWUd4eQFE9tASHSx6WYDn1IOJt5Hj4xBmo6E_vsUFy_FrlMvP4tVUAMqu4hptBQFVk6YEIkrZ5ofDFRpfdg9pcnXuE94K1hRSmvDlNEmHnV-m7escIlm4D0TCN7_-emx7iSGPETd0IBl1rDgWKcSYuFxXkleAikgYL5UXcVnFP97wOji1gLoC3Jodbb6R0w0q0kcxoIgjPJ9n2i7jjcM6Ic161o5t581bJBFLRc2DTgPpcZ752c4e5odox1EICC4AxTF8UG4X8yejfWoVNkqL-H2hOaHbent3rXAQT60JMylvUfPrUlCLL2EW46rti4_HNQXZUIAPykS64KDjoGjP1g9hSToaPJ6NoxQ2PhWv2PfaN6R-8wOvrSOmh7-briaCFzOl0000__y30000)
  
## 2.3. Describe Persistence-Related Behavior

   #### Các thực thể cần được lưu trữ:
+ **Employee**: Thông tin cá nhân, phương thức thanh toán.

+ **Timecard**: Dữ liệu về giờ làm việc của từng nhân viên.

+ **Paycheck**: Kết quả tính lương sau khi xử lý.

#### Cơ chế lưu trữ:
+ Hệ thống sử dụng cơ sở dữ liệu quan hệ **(RDBMS)** hoặc **Object-Relational Mapping (ORM)** để lưu trữ và quản lý dữ liệu.
  
+ Dữ liệu **Employee, Timecard, và Paycheck** được lưu trong cơ sở dữ liệu trung tâm, cho phép truy xuất, cập nhật và quản lý hiệu quả.
  
+ **ProjectManagementDatabase** đảm nhiệm việc lưu trữ bảng chấm công của nhân viên và mã dự án mà họ tham gia.
  
  **Ví dụ hành vi lưu trữ: Employee**
  
+ Khi một nhân viên mới được thêm vào hệ thống, thông tin của họ như tên, vị trí công việc, phương thức thanh toán và các thông tin cá nhân khác được nhập vào qua giao diện quản lý nhân viên.
  
+ Các thông tin này sẽ được lưu trữ vào **EmployeeDatabase** thông qua **EmployeeController**, cho phép dễ dàng truy xuất và chỉnh sửa sau này.
  
## 2.4. Refine the Flow of Events Description

**Flow of Events: Run Payroll**

**1. Khởi động:**
+ **SystemClock** kích hoạt **PayrollController** theo lịch trình.
  
**2. Lấy dữ liệu:**
+ **PayrollController** truy xuất thông tin nhân viên từ **Employee** và dữ liệu chấm công từ **Timecard**.
  
**3. Tính toán lương:**
Tính toán dựa trên loại nhân viên:
  
+ **HourlyEmployee**: Lương giờ làm việc thực tế.
  
+ **SalariedEmployee**: Lương cố định hàng tháng.
  
+ **CommissionedEmployee**: Lương theo hoa hồng và giờ làm việc.
  
**4. Thực hiện thanh toán:**
+ **Paycheck** được tạo và xử lý qua **BankSystem** hoặc in qua **PrintService**.
  
## 2.5. Unify Classes and Subsystems

  #### Tổ chức các lớp và hệ thống con:
  
  **+ BankSystem:**
  + Giao diện (Interface): **IBankSystem**
  + Chức năng: Quản lý các giao dịch liên quan đến ngân hàng, bao gồm việc chuyển tiền lương vào tài khoản của nhân viên.
    
  **+ PrintService:**
  + Giao diện (Interface): **IPrintService**
  + Chức năng: Cung cấp chức năng in phiếu lương cho nhân viên.
    
  **+ ProjectManagementDatabase:**
  + Chức năng: Lưu trữ thông tin bảng chấm công của nhân viên, bao gồm các giờ làm việc và mã dự án mà nhân viên tham gia.
    
  **+ Employee and Payroll Subsystem:**
  + Chức năng: Quản lý thông tin về nhân viên, bao gồm dữ liệu cá nhân, loại hợp đồng và tình trạng thanh toán.
    
Các lớp như **Employee, Timecard, Paycheck** được tổ chức thành nhóm theo hệ thống con tương ứng để tối ưu hóa cấu trúc thiết kế.

# 3. Ưu điểm của thiết kế
**1. Tính mô-đun**: Hệ thống chia thành các **subsystem** giúp giảm độ phức tạp và dễ dàng bảo trì.

**2. Khả năng mở rộng**: Các lớp và giao diện được thiết kế chuẩn, dễ dàng tái sử dụng trong các hệ thống khác mà không cần thay đổi quá nhiều.

**3. Bảo mật**: Bảo mật nó liên quan đến các dữ liệu nhạy cảm của nhân viên như lương, tài khoản ngân hàng, và thời gian làm việc.

**4. Tái sử dụng**: Dễ dàng thêm tính năng mới nhờ sử dụng **interface** và **subsystem**. 

# Tài liệu giải thích lý do thiết kế hệ thống Payroll System
Tài liệu này giải thích chi tiết lý do đưa ra các thiết kế cho hệ thống **Payroll System**. Các thiết kế này dựa trên phân tích các ca sử dụng **(Use Case Analysis)** và nhận diện các yếu tố thiết kế **(Identify Design Elements)**. Mục tiêu chính của thiết kế là đảm bảo hệ thống có tính linh hoạt, dễ bảo trì, có khả năng mở rộng và đáp ứng yêu cầu quản lý tiền lương hiệu quả.

## 1. Nguyên tắc thiết kế

#### 1.1. Hướng đối tượng (Object-Oriented Design - OOD)
Hệ thống **Payroll System** được thiết kế theo nguyên tắc hướng đối tượng, sử dụng các khái niệm cơ bản như lớp **(class)**, giao diện **(interface)** và hệ thống con **(subsystem)**. Phương pháp này giúp tổ chức hệ thống một cách rõ ràng, dễ hiểu và dễ bảo trì.

#### Lý do sử dụng OOD:

+ **Tính mô-đun**: Chia nhỏ hệ thống thành các phần độc lập, dễ dàng quản lý và phát triển.

+ **Tính tái sử dụng**: Các lớp và giao diện như **IBankSystem**, **IPrintService** có thể tái sử dụng trong các ứng dụng khác.

+ **Tính linh hoạt**: Giúp dễ dàng mở rộng và cập nhật hệ thống mà không làm ảnh hưởng đến các phần khác.

#### 1.2. Tính mô-đun
Hệ thống được phân chia thành các **subsystem** độc lập như **BankSystem**, **PrintService**, và **ProjectManagementDatabase**. Mỗi **subsystem** có trách nhiệm riêng biệt, giúp giảm độ phức tạp tổng thể của hệ thống và làm cho việc bảo trì dễ dàng hơn.

#### Lý do phân chia mô-đun:

+ **Giảm độ phức tạp**: Mỗi **subsystem** có một chức năng cụ thể, giúp người phát triển dễ dàng quản lý và hiểu được các phần của hệ thống.

+ **Dễ bảo trì và mở rộng**: Các **subsystem** có thể được cập nhật hoặc thay đổi mà không làm ảnh hưởng đến các phần khác của hệ thống.

#### 1.3. Khả năng tái sử dụng
Các lớp và giao diện trong hệ thống được thiết kế để có thể tái sử dụng. 

**Ví dụ**: **IBankSystem** và **IPrintService** có thể dễ dàng được áp dụng cho các hệ thống khác ngoài hệ thống Payroll.

#### Lý do tái sử dụng:

+ **Tiết kiệm chi phí**: Việc tái sử dụng các module như IBankSystem giúp giảm thiểu chi phí phát triển và bảo trì.

+ **Tính linh hoạt cao**: Các giao diện có thể thay đổi và mở rộng mà không ảnh hưởng đến các tính năng chính của hệ thống.

#### 1.4. Bảo mật và tin cậy
Bảo mật là một yếu tố quan trọng trong thiết kế, đặc biệt đối với các dữ liệu nhạy cảm như thông tin tài khoản ngân hàng, bảng chấm công và phiếu lương của nhân viên. Dữ liệu được mã hóa và các quyền truy cập được kiểm soát chặt chẽ.

#### Lý do bảo mật:

+ **Bảo vệ dữ liệu nhạy cảm**: Cần phải bảo vệ các thông tin như tài khoản ngân hàng và bảng chấm công để tránh bị lộ hoặc bị tấn công.

+ **Tuân thủ quy định pháp lý**: Hệ thống phải tuân thủ các tiêu chuẩn bảo mật và quy định liên quan đến việc xử lý thông tin cá nhân và tài chính.

## 2. Giải thích thiết kế từng ca sử dụng
#### 2.1. Ca sử dụng: Login
**Mục tiêu**: Xác thực người dùng và cấp quyền truy cập vào hệ thống.

**Lý do thiết kế**:
+ Tách biệt giao diện và logic: Việc phân chia giữa **LoginForm** (giao diện) và **LoginController** (logic xác thực) giúp giảm sự phụ thuộc giữa các phần của hệ thống, đồng thời dễ dàng thay đổi phương thức xác thực mà không làm ảnh hưởng đến giao diện người dùng.
  
#### 2.2. Ca sử dụng: Maintain Timecard
**Mục tiêu**: Cho phép nhân viên quản lý và cập nhật thời gian làm việc.

**Lý do thiết kế**:

+ Giảm phức tạp trong logic nghiệp vụ: Việc xử lý nghiệp vụ được chuyển giao cho **TimecardController**, trong khi **TimecardForm** chỉ cần hiển thị và nhận dữ liệu từ người dùng. Điều này giúp mã nguồn trở nên dễ bảo trì và thay đổi hơn.

#### 2.3. Ca sử dụng: Run Payroll
**Mục tiêu**: Tính toán và thực hiện các thanh toán lương cho nhân viên.

**Lý do thiết kế**:

+ Tách biệt phương thức thanh toán: Các phương thức thanh toán có thể thay đổi (thêm phương thức thanh toán mới như ví điện tử) mà không làm gián đoạn các chức năng khác của hệ thống. Việc sử dụng các giao diện như **IBankSystem** và **IPrintService** cho phép dễ dàng thay đổi hoặc bổ sung các phương thức thanh toán mà không cần thay đổi logic chính.
  
# 3. Ưu điểm của thiết kế

**1. Tính mô-đun**: Việc phân chia hệ thống thành các **subsystem** độc lập giúp giảm độ phức tạp của toàn bộ hệ thống.

**2. Khả năng mở rộng**: Hệ thống có khả năng mở rộng dễ dàng nhờ vào việc sử dụng các giao diện và subsystem. Các phương thức thanh toán hoặc báo cáo có thể được mở rộng mà không thay đổi hệ thống cũ.

**3. Bảo mật**: Các thông tin nhạy cảm như dữ liệu ngân hàng và phiếu lương được mã hóa và bảo vệ, giúp bảo đảm tính bảo mật và tuân thủ các quy định.

**4. Tái sử dụng**: Các module được thiết kế để tái sử dụng trong các hệ thống khác, giúp tiết kiệm chi phí và tăng hiệu quả phát triển. 

# 4. Kết luận
Thiết kế hệ thống **Payroll System** sử dụng các nguyên tắc của hướng đối tượng để đảm bảo tính linh hoạt, khả năng mở rộng và dễ bảo trì. Các subsystem được phân chia rõ ràng giúp giảm độ phức tạp, tăng cường bảo mật và đảm bảo tính tái sử dụng. Hệ thống sẵn sàng đáp ứng các yêu cầu quản lý lương và có thể dễ dàng mở rộng trong tương lai.





  
  
  


