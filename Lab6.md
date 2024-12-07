# Thiết kế chi tiết các lớp trong Payroll System
## 1. Xác định các operations và methods
### 1.1. Operations và methods chính
#### Lớp BankSystem
+ **Chức năng**: Thực hiện các giao dịch ngân hàng cho phiếu lương.
+ **Phương thức**:
     +  **deposit(paycheck: Paycheck, bankInfo: BankInformation): void**

          Chuyển khoản phiếu lương vào tài khoản ngân hàng của nhân viên.

     + **getTransactionHistory(employee: Employee): List<BankTransaction>**

          Lấy danh sách các giao dịch của nhân viên.

#### Lớp PrintService
+ **Chức năng**: Hỗ trợ in phiếu lương.
+ **Phương thức**:
     +  **print(paycheck: Paycheck): void**
   
          In phiếu lương cho nhân viên.
        
     +  **addToQueue(paycheck: Paycheck): void**
       
          Thêm phiếu lương vào hàng đợi để in.
        
     +  **processPrintQueue(): void**
       
          Xử lý hàng đợi để in phiếu lương.

#### Lớp ProjectManagementDatabase
+ **Chức năng** Quản lý bảng chấm công và mã dự án.
+ **Phương thức**:
    +  **getChargeNumbers(criteria: String): List<ChargeNum>**
      
         Lấy danh sách mã dự án phù hợp.
       
    +  **getTimecard(employee: Employee): Timecard**
      
         Lấy bảng chấm công của nhân viên.
       
    +  **saveTimecard(timecard: Timecard): void**
      
         Lưu bảng chấm công sau khi chỉnh sửa.

#### Lớp PayrollController
+ **Chức năng**: Điều phối việc tính toán và xử lý thanh toán lương.
+ **Phương thức**:
    +  **runPayroll(): void**
      
         Thực hiện quy trình tính lương.
       
    +  **calculatePay(employee: Employee, timecard: Timecard): float**
      
         Tính toán lương từ bảng chấm công và thông tin nhân viên.
       
    +  **generatePaycheck(employee: Employee, amount: float): Paycheck**
      
         Tạo phiếu lương cho nhân viên.
       
    +  **processPayment(paycheck: Paycheck)**: void: Xử lý thanh toán.

#### Lớp Employee
+ **Chức năng**: Quản lý thông tin cá nhân và phương thức thanh toán của nhân viên.
+ **Phương thức**:
    +  **getPaymentMethod(): String**
      
         Lấy phương thức thanh toán. (e.g., "bank" hoặc "print").
       
    +  **getEmployeeDetails(): Map<String, String>**: Lấy thông tin nhân viên.

#### Lớp Timecard
+ **Chức năng**: Lưu trữ và quản lý giờ làm việc theo mã dự án.
+ **Phương thức**:
    +  **getTotalHours(): float**
      
         Tính tổng giờ làm việc.
       
    +  **addHours(chargeNum: ChargeNum, hours: float): void:** Thêm giờ làm việc vào dự án.
      
    +  **removeHours(chargeNum: ChargeNum): void:** Xóa giờ làm việc khỏi dự án.

## 2. Xác định đúng các trạng thái và mô tả sự thay đổi trạng thái
### 2.1. Lớp Paycheck
#### Trạng thái chính:

+ **Created**: Phiếu lương được tạo mới.

+ **Pending**: Phiếu lương đang chờ xử lý thanh toán.

+ **Paid**: Thanh toán thành công.

+ **Printing**: Phiếu lương được gửi đến hệ thống in.

+ **Printed**: Phiếu lương đã in thành công.

#### Biểu đồ trạng thái:
![diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWdDHQc99Qeg2bO9tniFTypCLIXxkMfYlK92H-N3N_bA5d6CRZYtCI-VYWga3wGb8pKl9p4i7wd7EAArykBivJw7YuUwr2Zc7zogKP2JcPIYKv1zUcCS5KmVMavW9iYG48GrKUdW1a9DyU0lG0XIrHPbv9H0Bd1xkMb-YS6JYmrtBInKoyxYuu79mXM37U-G3pOAP25G7am6f0daLw3sWVqf0AdObSt4v06q3XG80003__mC0)

### 2.2. Lớp Timecard
#### Trạng thái chính:

+ **Initialized**: Bảng chấm công được tạo.
+ **InProgress**: Đang nhập giờ làm.
+ **Submitted**: Hoàn tất nhập liệu.

#### Mô tả sự thay đổi trạng thái:

+ **Initialized → InProgress**: Khi nhân viên bắt đầu nhập giờ làm việc vào bảng chấm công.

+ **InProgress → Submitted**: Khi nhân viên hoàn tất nhập liệu và gửi bảng chấm công để lưu vào hệ thống.

#### Biểu đồ trạng thái:
![diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bUqLgo2hgwTWcTUPabcOavcLMgAWfL2oCDT2_CLaXxkMfoNhf2SyN3Nqbo5vCDRyjAvk90LGZG65EMd5wKM5mFr-G6LhYrGICzyk7kkGixX1RaAPK1cUp8NaYgGfk3IfDpCaXAmNUuFTw_DL3WoyU7kPeMSOnjAkRWGiY2r81TQANZa7rwGfr02T4a9bqDgNWh8xG00003__mC0)

## 3. Xác định đúng các thuộc tính và mô tả rõ ràng
### 3.1. Các thuộc tính chính
#### Lớp BankSystem
+ **transactionList: List<BankTransaction>**: Lưu lịch sử giao dịch.

#### Lớp PrintService
+ **printerName: String**: Tên máy in.

+ **printQueue: Queue<Paycheck>**: Hàng đợi các phiếu lương cần in.

#### Lớp ProjectManagementDatabase
+ **chargeNumbers: List<ChargeNum>**: Danh sách mã dự án.

+ **timecards: Map<Employee, Timecard>**: Lưu bảng chấm công.

#### Lớp PayrollController
+ **paycheckList: List<Paycheck>**: Danh sách phiếu lương.

#### Lớp Employee
+ **employeeID: String**: Mã số nhân viên.

+ **name: String**: Tên nhân viên.

+ **paymentMethod: String**: Phương thức thanh toán.

#### Lớp Timecard
+ **hoursWorked: Map<ChargeNum, float>**: Số giờ làm việc theo mã dự án.

## 4. Xác định đúng các phụ thuộc và quan hệ kết hợp
### 4.1. Quan hệ kết hợp
+ **PayrollController ↔ BankSystem**: Xử lý thanh toán.

+ **PayrollController ↔ PrintService**: Hỗ trợ in phiếu lương.

+ **PayrollController ↔ Employee, Timecard**: Tính toán lương.

+ **Timecard ↔ ChargeNum**: Quản lý giờ làm việc theo dự án.
### 4.2. Quan hệ phụ thuộc
+ **PayrollController → ProjectManagementDatabase**: Lấy bảng chấm công.

+ **PrintService → Paycheck**: Xử lý in.

+ **BankSystem → BankInformation**: Xử lý giao dịch ngân hàng.

### 5. Biểu đồ lớp
![diagram](https://www.planttext.com/api/plantuml/png/Z5PBRjim4Dth5Dp51kmB286HrYcG04tW9W6wdb1ZYur42YJbGYXwiYvwf5wX9CMVPRbf5h7C-Rx7DoF_-VNxHccGkc-RehWYsmQK8hUuPvnf9hWgg3lv2FpjUL0QM_AZ8EPlJRG4he1QhyzCwPBO_zVMyILPDiwPa0exePXUT33G6kbRINR-QKLUJSWztulILR5FiWKRl2p9KR3AfpYWpXBVcM923WjikqOCY2Nvv9-MbphvMNWmEycuVaPvP1GZdCuUedo4rkHwrkRR8RTywR4t1lTn7NeFw9p73BPJ051LBy8bUDUrauAYKhjOUH7i6GZn3Qb-00u7R97hMz3m2YeXeZN80pxsxIjAvKdPXhDDk4NM8WLP6OS7wAu3YIlouWsRHFysJxYWaXc-60IsblCbnelpoUQlArYzlu8Zne3GN_8wPm86APfcAxYsdoZJdNfoCtrEhqxstCSlJg-0GaFx1ZGQyqpRApBRsRuHe2DkZd9Cu4hEPe5Mz5pxm6NImqG8CDWh_eTk8XiXTIGXLBs_dUYQpqXzhFE0kXRLn5QBNZR3am6KmrpFyE0D5-SwwS9Ec-KzA-JETtaVSmvtiPd56Uj9RUVQCjRGZBLE6uiiXh38eaMllWhvXjKuAL7cgx5yhdQXeR4TgcbpPWMCvt4sIv8bSaMI5Z8rIcp54I_7pWs5qyUP39BulE54WGb4yB8GJYASzOCBIl1YtSdMFHl5YSB_IoLnWFBvY1KZ1sdnJJPJji6y9PFKIUTP-PWDABLOnxMNXrsH9soShwfPfuhpFRHUR_8tPqbwXPVyJbvAxtXUslobVSyYhnGnzCq7n_LGXjrYwiH3wn6bNv8QL16_MblYEdKuocoIsn0gA3FZMP7lJDV5L1OEHuZDMvbpdDwChrtS6AZsTyjV0000__y30000)

