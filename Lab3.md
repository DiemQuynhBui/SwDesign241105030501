# 1. Subsystem context diagrams
* Biểu đồ ngữ cảnh của các hệ thống con.
 # BankSystem:
  ![digram](https://www.planttext.com/api/plantuml/png/l59BJiCm4Dtx5BEZbKWF425KqMwwgK0zWUjCKwl-HFOOgOAkMRDcnGauG1OiE4bFm1MmcwHDYzYIHPAPD_FUZFs-wy-n9-ueQCNO5Ko-tWMeVVrM0JbhIbZlwnUW-7wDmHqtcyNM4sec5FSUxldMMQKcrb3weeCd1kbnmRJOOCXsZ4b3w5PS8CnE95rnWPNraWOyjeWrYaqEtTyrn4wRMlA3-ioihDESf3N3fbbOiv9EJrkE8UJmQ6MHH9iPUtfILmer6lB_DaR2iX8DEaxOqHtWBZXDscNQWJAkRJ0KImiRbWgRP15vPju7B28mZK6ZtqdySG2zWJlsPKpFkSPOlo0dJTcA2f5Kvq4lutMUOL644jaKYKlb3r8jl4lcUGZSD8OfvRx-u22ERcA_dP9bjsUta4Fmw5a_TVCy6lLDruDIz_6yykFw_hBcSlaSueBean8ReocIxty0003__mC0)
  * #  Giải thích:
+ PayrollController: Lớp điều khiển, có phương thức runPayroll() để bắt đầu quá trình trả lương.
+ IBankSystem: Giao diện cho hệ thống ngân hàng, định nghĩa phương thức deposit() và confirmDeposit().
+ BankSystem: Lớp triển khai giao diện IBankSystem, có phương thức generatePaycheck() để tạo phiếu lương.
+ Paycheck: Thực thể phiếu lương với các thuộc tính amount, dateIssued và phương thức generate() để tạo phiếu lương.
+ BankInformation: Thực thể thông tin ngân hàng với các thuộc tính bankName, accountNumber và phương thức getBankDetails() để lấy thông tin chi tiết.
# PrintSevice:
 ![digram](https://www.planttext.com/api/plantuml/png/b58xJiGm4Etd5DFjKcGF426qqj9i5yG9Z3ra8nmxsEELLa1DJKt52JX02WfEaXDm1Umakqf05BYmv_VUU9xzrNwiFGl7eTO02znyladKNVlQ83jhIjnrxJDot5-YKxZAy3MvVIK9f1RUOo4EpcgziORJIGuV0DDoT1_8SmzPdi4JG3J8tGf9k9qI7G5DNzc8WzoHlCiJSs_rsB7P55RLZQQQ3Fl_ygLi9ct2CnL_bM6EUrkfIVSnCpR8H6s3uLYcRBZHD0ILODfw7qZ5n6LqXikKPCX5RpcbNU1L46QGkAowzbsWFEaFlvNDieiVe-OOF7cO1yyVLwlvKytIYUKqIev77Jp0cenA_-0R003__mC0)
 * # Giải thích:
+ PayrollController: Lớp điều khiển, có phương thức requestPrint() để yêu cầu in phiếu lương.
+ IPrintService: Giao diện cho dịch vụ in ấn, định nghĩa phương thức print() để in phiếu lương.
+ PrintService: Lớp triển khai giao diện IPrintService, có phương thức completePrint() để hoàn tất việc in phiếu lương.
+ Paycheck: Thực thể phiếu lương với các thuộc tính amount và dateIssued, có phương thức generate() để tạo phiếu lương.

# ProjectManagementDatabase:
  ![digram](https://www.planttext.com/api/plantuml/png/j58nJiCm5DrzYh-r7T83H0XLAai7gY9Ey4a-mIXnWlqT2G4pCpCJ9-006HWuIKx05R3hg2IjaeqCiVFytdylt_-d-LePHisso8MOmVhx8u6yRTuhO5sg3ExQvXNOlT_SnqwNzvJm9IhCg2355yXuWuP4agCniCD7NURvkbJiLzBm9C0_cXui6UxqNZLVY1SXf6BIjvWGR4Ph_zLWBQcclReAx4qACRWY2xVqYWU1uzGo3VnZWlFk8e_QogBAzuZvZt2sIf43tMrmIF6AkfJfIKn_s5b6Hou3S8i5EVZQXL9PE76tpDOCGSY83-tfuo7Tl9zZ1bSMLPY7JBRD9q9o61PnUlDHT3xLjnYi8ICc66VFo-N4n8qBlNE_Nt7tEqQ85QdKJ_el0000__y30000)
  * # Giải thích:
+ PayrollController: Lớp điều khiển, có phương thức requestProjectData() để yêu cầu dữ liệu dự án.
+ IProjectManagementDatabase: Giao diện cho hệ thống quản lý dự án, định nghĩa các phương thức retrieveData() và provideData() để lấy dữ liệu dự án.
+ ProjectManagementDatabase: Lớp triển khai giao diện IProjectManagementDatabase, có thêm phương thức updateData() để cập nhật dữ liệu dự án.
+ ProjectData: Thực thể lưu trữ dữ liệu dự án, có các thuộc tính như projectId, projectName, status và phương thức getData() để lấy thông tin chi tiết.

# 2. Analysis class to design element map
Bảng ánh xạ các lớp phân tích đến các phần tử thiết kế. 

| Analysis Class               | Design Element                  |
|------------------------------|----------------------------------|
| **PayrollController**        | PayrollController               |
| **BankSystem**               | BankSystem                      |
| **IBankSystem**              | IBankSystem Interface           |
| **PrintService**             | PrintService                    |
| **IPrintService**            | IPrintService Interface         |
| **ProjectManagementDatabase**| ProjectManagementDatabase       |
| **IProjectManagementDatabase** | IProjectManagementDatabase Interface |
| **Paycheck**                 | Paycheck Entity                 |
| **ProjectData**              | ProjectData Entity              |
| **LoginForm**                | LoginForm                       |
| **MaintainTimecardForm**     | MainEmployeeForm, TimecardForm  |
| **TimecardController**       | TimecardController              |
| **SystemClockInterface**     | SystemClockInterface            |
| **MainApplicationForm**      | MainApplicationForm             |

# 3. Design element to owning package map
Bảng ánh xạ các phần tử thiết kế vào các gói.

| Design Element                  | Owning Package               |
|----------------------------------|------------------------------|
| **PayrollController**            | payroll.controller           |
| **BankSystem**                   | banking.system               |
| **IBankSystem Interface**        | banking.system               |
| **PrintService**                 | printing.service             |
| **IPrintService Interface**      | printing.service             |
| **ProjectManagementDatabase**    | project.management.database |
| **IProjectManagementDatabase Interface** | project.management.database |
| **Paycheck Entity**              | payroll.entity               |
| **ProjectData Entity**           | project.entity               |
| **LoginForm**                    | ui.form                      |
| **MaintainTimecardForm**         | ui.form                      |
| **MainEmployeeForm**             | ui.form                      |
| **TimecardForm**                 | ui.form                      |
| **TimecardController**           | payroll.controller           |
| **SystemClockInterface**         | system.clock                 |
| **MainApplicationForm**          | ui.form                      |

# 4. Architectural layers and their dependencies

![digram](https://www.planttext.com/api/plantuml/png/V95Foi903CNtSuhWtWku44LT51G4SIKkuZJgO3jJalJxWtWo5nx9AzXMHKV5vRptViaBSpwUUgB8MkQPAT3kS4FGcZ89UKLrmSCO_ubRi3S0Yta2Wv0NmLVkqXpC0-aNHURiE_6ipuX_dAKO78OSNSpSf4b8AOl3YLypYd9fjMIA8LHSeH3qhIMHPQsD_fJOOtRV38bNsd3JfXaS7mJjTlTpO-Z0N4ZCPxF1ej9LVX02fywZrbXiNlClVIjaIYnEzEkQhoTLC-vF4lXrkZMcHpwjF_S2003__mC0)
* # Giải thích các lớp kiến trúc:
+ Presentation Layer: UI Component: Thành phần giao diện người dùng, nơi người dùng tương tác với hệ thống.
+ Application Layer: Application Service: Các dịch vụ ứng dụng, nơi xử lý các logic điều khiển chính và phối hợp các thành phần khác.
+ Domain Layer: Domain Model: Các mô hình nghiệp vụ, định nghĩa các quy tắc và logic nghiệp vụ của hệ thống.
+ Infrastructure Layer: Database Access: Thành phần truy cập cơ sở dữ liệu, quản lý việc lưu trữ và truy xuất dữ liệu.
+ External Service Integration: Thành phần tích hợp với các dịch vụ bên ngoài, như API bên thứ ba.
## Mối quan hệ giữa các lớp:
+ UI Component sử dụng Application Service để thực hiện các yêu cầu từ người dùng.
+ Application Service điều phối các hoạt động của Domain Model và tích hợp với External Service Integration.
+ Domain Model tương tác với Database Access để lưu trữ và truy xuất dữ liệu.
+ Application Service tích hợp với External Service Integration để giao tiếp với các dịch vụ bên ngoài.



  

  
