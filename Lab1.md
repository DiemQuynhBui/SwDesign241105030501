# 1. Phân tích kiến trúc
 # Đề xuất kiến trúc, giải thích lý do lựa chọn và ý nghĩa từng thành phần trong kiến trúc, vẽ biểu đồ package mô tả kiến trúc.

### Đề xuất kiến trúc: 
# Hệ thống Payroll System là một hệ thống quản lý bảng lương phức tạp, có nhiều người dùng và tích hợp với cơ sở dữ liệu khác nhau(ví dụ: Project Management Database). Kiến trúc phù hợp cho hệ thống này là kiến trúc phân lớp (Layered Architecture), với 4 lớp chính:

#### Lớp Giao diện (Presentation Layer): 
Chịu trách nhiệm hiển thị thông tin và nhận đầu vào từ người dùng. Lớp này sẽ gồm các giao diện cho các chức năng như nhập bảng chấm công, chọn phương thức thanh toán, và báo cáo.
Các công nghệ có thể sử dụng: Java Swing hoặc .NET Windows Forms cho giao diện desktop.

#### Lớp Dịch vụ (Service Layer):
Đảm nhiệm xử lý các logic nghiệp vụ của hệ thống, ví dụ như xử lý các yêu cầu liên quan đến tính lương, ghi nhận bảng chấm công, và thanh toán lương.
Lớp này tương tác với cơ sở dữ liệu thông qua các dịch vụ và API, đảm bảo sự tách biệt giữa giao diện và dữ liệu.

#### Lớp Dữ liệu (Data Access Layer): 
Lớp này quản lý việc truy xuất, cập nhật dữ liệu từ cơ sở dữ liệu (Payroll Database, Project Management Database).
Lớp này sẽ kết nối với cơ sở dữ liệu DB2 của Project Management Database, nhưng chỉ truy xuất thông tin mà không cập nhật.

#### Lớp Lưu trữ (Storage Layer): 
Chứa cơ sở dữ liệu cần thiết cho hệ thống. Hệ thống Payroll cần một cơ sở dữ liệu riêng (ví dụ như SQL Server hoặc MySQL) để lưu trữ thông tin về nhân viên, bảng chấm công, và phiếu lương.

# Biểu đồ package mô tả kiến trúc:
  ![diagram ](https://www.planttext.com/api/plantuml/png/X5FBJiCm4BpxArQzzyAH0sghS402AUBn0Okp1KDi1tjRAK9y6GS-YLzWKvecTLprbkpCxCnEbD_ldqLa3BonjMfGl-CBmQmC5Canil4ERh6bC8DF1Q1hZ16kRLFxbkZfvZ1QLjOuUVzImv872bkZQQeliGs-hlVuOVneB6aCLJeNkfKm_NXiKI0ZBBKcePsCUK-DZuPzQ2TM6QXONPJ1lv7cEtHYqbaNg-F3HD0zd3giI_MCSHTrw0hcywlaTBW4uvW2QevgN-4vMW9rxAGueGVws53Ciu_h79FJFUFTGrEYM1FhLufGoQ4gsTU9firdH6ckVF6xV1mCRKNQ_EFInjghJB9HTVqt47qKhFVD93ilMf2hvFVu0m00__y30000)
# 2. Cơ chế phân tích
Đề xuất các cơ chế cần giải quyết trong bài toán và giải thích lý do. Kết quả mong đợi là một danh sách cơ chế phù hợp.
## Đề xuất các cơ chế:
  ## Quản lý quyền truy cập người dùng:
 + Lý do: Hệ thống có nhiều người dùng với vai trò khác nhau.Vì vậy cần xác thực và phân quyền để bảo vệ dữ liệu.
  ## Tính toán lương tự động:
 + Lý do: Giúp hệ thống tự động tính lương dựa trên bảng chấm công mà không cần can thiệp thủ công.
  ## Quản lý thời gian làm việc:
 + Lý do: Theo dõi thời gian làm việc để đảm bảo tính lương chính xác và quản lý phụ cấp hợp lý cho nhân viên.
  ## Bảo mật dữ liệu:
 + Lý do: Bảo vệ thông tin về lương, chấm công và thông tin cá nhân của nhân viên khỏi các truy cập trái phép.
  ## Thông báo tự động:
 + Lý do: Gửi thông báo tự động cho nhân viên và quản lý về lương như bảng lương được cập nhật hoặc khi thanh toán hoàn tất.
# 3. Phân tích ca sử dụng Payment
  ## 1. Xác định các tác nhân (Actors):
 + Admin (Quản trị viên): Theo dõi và truy vấn các báo cáo liên quan đến thanh toán lương.
 + Payroll System (Hệ thống thanh toán): Thực hiện tự động tính toán và thanh toán lương cho nhân viên vào các thời điểm quy định.
  ## 2. Mô tả quy trình nghiệp vụ:
 + Bắt đầu: Hệ thống Payroll tự động kích hoạt  vào các ngày thanh toán ( vào cuối tuần cho nhân viên trả lương theo giờ, hoặc cuối tháng cho nhân viên trả lương cố định).
 + Tính toán lương: Hệ thống Payroll tính toán số tiền lương của nhân viên dựa trên: số giờ làm việc (ghi nhận từ thẻ chấm công) hoặc các phụ cấp, hoa hồng (nếu có) hoặc mức lương cố định.
 + Thanh toán: Hệ thống thực hiện thanh toán cho nhân viên dựa trên phương thức như: Chuyển khoản ngân hàng, nhận tiền mặt trực tiếp.
 + Xác nhận: Hệ thống cập nhật trạng thái thanh toán thành công và lưu trữ các thông tin vào cơ sở dữ liệu PayrollDatabase.
 + Báo cáo: Quản trị viên có thể truy vấn hệ thống để xem các báo cáo chi tiết liên quan đến các khoản thanh toán đã thực hiện.
  ## 3. Xác định các lớp phân tích:
 + Employee (Nhân viên): Chứa thông tin cá nhân của nhân viên như: tên, ID, phương thức thanh toán, tài khoản ngân hàng, mức lương.
 + Payroll (Bảng lương): Thực hiện tính toán lương dựa trên các yếu tố như số giờ làm việc, phụ cấp, hoa hồng, và thực hiện quá trình thanh toán.
 + Timecard (Thẻ chấm công): Ghi nhận thông tin về thời gian làm việc của nhân viên, sử dụng để tính lương cho nhân viên theo giờ.
 + PaymentMethod(Phương thức thanh toán): Lưu thông tin về phương thức thanh toán (chuyển khoản, tiền mặt).
 + PaymentTransaction(Giao dịch thanh toán): Quản lý các giao dịch thanh toán.
 + PayrollDatabase(Cơ sở dữ liệu): Lưu trữ thông tin lương.
  ## 4. Biểu đồ lớp phân tích (Analysis Class Diagram)
  ![diagram](https://www.planttext.com/api/plantuml/png/R59BJiGm3Dtd55cMnLmW2pH8HO8526agiNOJYwd8fueTf0fnCXOSYIlGqcdQJhkfOllv-Jsxlzy_HsA8d9mLsWAHl7Uj3HsY_1HIoiTIoHF7nhyDqJCuNCOdi10x9SkGQej3vWKwXvwVaC_1g7KeliHbHf-EmTfnX0QhamN6FbkWQrMMS9EPSsVLEDGGpTZw45Aarn3VqMoXgzaZVdnNNJkxk8PN4Jo1vYRuiUVEXUHvwR7ijQh_xyPHduGQwB8yuX1nChEnzX4Qar6JhuAroYOte5bRqRBQaJnrzBho7G-7swjTA7a6MWFoNfMaLBk6IKn76iePg-PphH4BWaHpBIzaoR9Rd0XsYrkdueZU37_j7m000F__0m00)
  ## 5. Biểu đồ Sequence (Sequence Diagram)
  ![diagram](https://www.planttext.com/api/plantuml/png/T9CnReCm58PtJl6KFHTWg5A9ZaYHoWKSWu9Li2cOg9oWGwVUeBIAgaQAcagTOCZWAlVm2Ng5FaEGe8G56Vlpv_yzmszzN6IIf3AF8ujGALAuzcF6hGJd66K9uH9cIrAa8ehWjiXa4C-0P72U6d8tSHA98WWQ0bz6bZZ0WHl8KFYjnRsCU2dX6SPXWhUSTpcGGoHPaQmzSEbOLXCUvbTTFXiAjSk1wkez1naI7e8KgkHMPp2eOqEagss1WFhcQv2euA5wvR1XQeUi0_E-KgQwUfk2fyowge7YSni3DHidhIEmRyIc8gdsNHqGdGwd4Y5SWB6jMns4ScruK2M5dsTTFw4e2LlAd5r_qCasUMZLLIbWpOW07pVJS0XxdT-OlYY4JDUFVCYuRTNUEGJ7IlTyf1cNSgUheuJxt8nx0SRzFXtowOJ_UjwFq6p4i-hFWRFvecnOwthFkZjVAUn2pslcN_2blQz5m7tpE_q1003__mC0)
  # 4. Phân tích ca sử dụng Maintain Timecard
   ## 1. Xác định các tác nhân (Actors)
  + Employee (Nhân viên): Người sẽ nhập và quản lý thời gian làm việc của mình thông qua thẻ chấm công.
  + Timecard System (Hệ thống Thẻ chấm công): Hệ thống chịu trách nhiệm xử lý các yêu cầu liên quan đến việc thêm, cập nhật và xóa thẻ chấm công.
   ## 2. Mô tả quy trình nghiệp vụ
  + Bắt đầu: Nhân viên đăng nhập vào hệ thống để truy cập thẻ chấm công của mình.
  + Nhập thời gian làm việc: Nhân viên nhập thông tin về thời gian làm việc vào thẻ chấm công (bao gồm ngày và số giờ làm việc).
  + Cập nhật thẻ chấm công: Nếu cần thiết, nhân viên có thể chỉnh sửa thông tin trên thẻ chấm công đã ghi nhận.
  + Xóa thẻ chấm công: Nhân viên có thể xóa thẻ chấm công nếu không cần thiết hoặc đã nhập sai thông tin.
  + Lưu trữ: Hệ thống cập nhật và lưu trữ thông tin vào cơ sở dữ liệu.
  + Xác nhận: Xác nhận các thay đổi với nhân viên.
  ## 3. Xác định các lớp phân tích:
  + Employee (Nhân viên): Chứa thông tin cá nhân của nhân viên như: tên, ID và các phương thức có liên quan đến thẻ chấm công.
  + Payroll (Bảng lương): Thực hiện tính toán lương dựa trên các yếu tố như số giờ làm việc, phụ cấp, hoa hồng, và thực hiện quá trình thanh toán.
  + Timecard (Thẻ chấm công): Ghi nhận thông tin về thời gian làm việc của nhân viên, bao gồm ngày và số giờ làm việc.
  + TimecardService (Dịch vụ Thẻ chấm công): Thực hiện các chức năng quản lý thẻ chấm công như thêm, cập nhật và xóa.
  + TimecardDatabase (Cơ sở dữ liệu thẻ chấm công): Lưu trữ thông tin thẻ chấm công của nhân viên.
  ## 4. Biểu đồ lớp phân tích (Analysis Class Diagram)
   ![diagram](https://www.planttext.com/api/plantuml/png/d9DBIWD148RtVOfQHZ0NQ2Ha4K51H8ZWkj9TP0PhfcC_0a4yJ70TT9qWBWAvHqxW5Un9vg4J8-XceBhw--llgfgFrNlVURG-P2mKetDmdatOp8ZWKG30vK32qDiq7nVHDMRqDHwJlqqpKcYrwvn8k4gTFwjEUk99b9etEBE6UI-fa5LWz3H4HZlhK3QHTTKeCZ1XnDJ0bTwU7aHGxhv5T662TNV6tfEkmTANySYxTESNpI7PQQhAjwBMrVbtKwVWbQoPA3SrgIw8CD7Ho1yXJKp78Ls_hq8EJCSaZj2Lhfqtjb4xKjDId1bDgPbMk-kjqVtFPxqxtMwlcPk4SP92dcoNYroqEr_Sh349Fa43VZrNFruyw804thm6y7QxUX47sPQBXx1TFkV0wpTHBMIx-dgH9uNaPXuNl4-vBlwBJm000F__0m00)
 ## 5. Biểu đồ Sequence (Sequence Diagram)
   ![diagram](https://www.planttext.com/api/plantuml/png/l5GzJiCm5DvzYdS1Bj015GbE01Tm7Qkn53kHurRj4HYv0GMnLAf0WYaU68nw3v-WL-2bQQiqibmli7Ymt_U-Fyax-psk3TLc9Wj2cIart6HIA5BXdM2Yeih0Wv2SKPtTSpqNZ9-ztScgA9US1m71orjgw8JMd90z4rnT3mbW12PtQucdRommFDyaCFUbfcGuYkYZ18GLEBbimJWA1fUhtBqec0ktLkGqrsDigNopAcDKOOLJRpUYJvKcTfX2AthxCGEZlNsFxJW1WceMRiNGh6ysghSl9A0BVNHKFd5xyrtQxbdb1zfOEGnfgexD_4z7kDu-ehOQGwT_qXNyFBdNCsU9xQM6aTxV9H6X1WSg4ejSkCzecd7dbz3fZjjDgKuFh3s7Owwozllw1G00__y30000)
 # 5. Hợp nhất kết quả phân tích ca sử dụng "Payment" và "Maintain Timecard"
 ## Lớp Employee (Nhân viên):
+ Vai trò trong Payment: Nhận lương dựa trên số giờ làm việc, mức lương cố định hoặc hoa hồng. 
+ Vai trò trong Maintain Timecard: Nhập thông tin về giờ làm việc qua thẻ chấm công.
+ Tích hợp: Nhân viên vừa nhập thẻ chấm công vừa nhận lương từ hệ thống.
 ## Lớp Timecard (Thẻ chấm công):
+ Vai trò: Chứa dữ liệu về giờ làm việc và ngày làm việc của nhân viên.
+ Tích hợp: Là nguồn dữ liệu đầu vào cho việc tính lương.
 ## Lớp Payroll (Xử lý lương):
+ Vai trò: Tính toán lương dựa trên thẻ chấm công và thông tin lương/hoa hồng.
+ Tích hợp: Liên kết giữa thẻ chấm công và thanh toán lương.
 ## Lớp TimecardService (Dịch vụ thẻ chấm công):
+ Vai trò: Xác minh, thêm, cập nhật và lưu trữ thông tin thẻ chấm công.
 ## Lớp PayrollDatabase (Cơ sở dữ liệu lương):
+ Vai trò: Lưu trữ tất cả thông tin liên quan đến nhân viên, thẻ chấm công và giao dịch thanh toán.
 # Mô hình tổng hợp: Nhân viên nhập thẻ chấm công, dữ liệu được xử lý để tính lương và thanh toán, quản trị viên có thể truy vấn báo cáo thanh toán đầy đủ.
 
 
   
   


  
  

