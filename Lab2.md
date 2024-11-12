## Phân tích ca sử dụng Payment
# 1. Quản lý nghỉ phép
# Xác định tác nhân (Actors):
* Employee (Nhân viên): Đăng ký và kiểm tra số ngày nghỉ phép còn lại.
* Admin (Quản trị viên): Phê duyệt các yêu cầu nghỉ phép và theo dõi tổng số ngày nghỉ phép.
# Quy trình nghiệp vụ:
* Đăng ký nghỉ phép: Nhân viên gửi yêu cầu nghỉ phép qua hệ thống.
* Phê duyệt: Quản trị viên nhận yêu cầu và phê duyệt hoặc từ chối.
* Cập nhật số ngày nghỉ: Nếu yêu cầu được phê duyệt, hệ thống trừ số ngày nghỉ vào số ngày nghỉ phép còn lại của nhân viên.
* Lưu trữ thông tin: Hệ thống lưu trữ thông tin nghỉ phép vào cơ sở dữ liệu để làm căn cứ tính lương cho nhân viên.
# Các lớp phân tích:
* Employee (Nhân viên): Lưu thông tin cá nhân và số ngày nghỉ phép còn lại.
* LeaveRequest (Yêu cầu nghỉ phép): Quản lý yêu cầu nghỉ phép, bao gồm thông tin về lý do, số ngày nghỉ, và trạng thái phê duyệt.
* PayrollDatabase (Cơ sở dữ liệu): Lưu trữ lịch sử nghỉ phép của nhân viên.

# 2. Quản lý nhân viên
# Xác định tác nhân (Actors):
* Admin (Quản trị viên): Thực hiện các chức năng quản lý hồ sơ nhân viên.
* Payroll System (Hệ thống thanh toán): Sử dụng thông tin nhân viên để tính toán lương và phúc lợi.
# Quy trình nghiệp vụ:
* Thêm nhân viên mới: Quản trị viên nhập thông tin nhân viên vào hệ thống.
* Cập nhật thông tin: Khi có thay đổi về thông tin (như mức lương, chức vụ), quản trị viên có thể cập nhật.
* Xóa nhân viên: Khi nhân viên nghỉ việc, hệ thống sẽ chuyển thông tin sang lưu trữ hoặc xóa khỏi hệ thống.
* Tra cứu: Quản trị viên có thể tra cứu thông tin nhân viên khi cần thiết.
# Các lớp phân tích:
* Employee (Nhân viên): Chứa thông tin cơ bản của nhân viên như tên, ID, chức vụ, và mức lương.
* PayrollDatabase (Cơ sở dữ liệu): Lưu trữ thông tin chi tiết về nhân viên để phục vụ tính toán lương và phúc lợi.

# 3. Quản lý phúc lợi
# Xác định tác nhân (Actors):
* Employee (Nhân viên): Kiểm tra các quyền lợi của mình, như bảo hiểm, trợ cấp.
* Admin (Quản trị viên): Cập nhật và quản lý các thông tin về phúc lợi của nhân viên.
# Quy trình nghiệp vụ:
* Đăng ký phúc lợi: Nhân viên đăng ký các chương trình phúc lợi mà họ đủ điều kiện.
* Cập nhật phúc lợi: Quản trị viên cập nhật phúc lợi theo quy định, như bảo hiểm và các khoản trợ cấp khác.
* Kiểm tra và điều chỉnh: Quản trị viên kiểm tra, theo dõi các khoản phúc lợi mà nhân viên đang nhận và điều chỉnh khi cần thiết.
Báo cáo phúc lợi: Quản trị viên có thể tạo các báo cáo phúc lợi chi tiết.
# Các lớp phân tích:
* Employee (Nhân viên): Chứa thông tin về các phúc lợi mà nhân viên đã đăng ký.
* Benefit (Phúc lợi): Chứa thông tin về các loại phúc lợi mà công ty cung cấp, bao gồm điều kiện và mức hỗ trợ.
* PayrollDatabase (Cơ sở dữ liệu): Lưu trữ các thông tin về phúc lợi của nhân viên và các khoản trợ cấp khác.

## Viết code Java mô phỏng ca sử dụng Maintain Timecard.
```java
package lab2_maintaintimecard;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

class Timecard {
    private String employeeId;
    private Date date;
    private int hoursWorked;

    public Timecard(String employeeId, Date date, int hoursWorked) {
        this.employeeId = employeeId;
        this.date = date;
        this.hoursWorked = hoursWorked;
    }

    public String getEmployeeId() {
        return employeeId;
    }

    public Date getDate() {
        return date;
    }

    public int getHoursWorked() {
        return hoursWorked;
    }

    public void setHoursWorked(int hoursWorked) {
        this.hoursWorked = hoursWorked;
    }

    @Override
    public String toString() {
        return "Date: " + date + ", Hours Worked: " + hoursWorked;
    }
}

class Employee {
    private int employeeId;
    private String name;
    private List<Timecard> timecards;

    public Employee(int employeeId, String name) {
        this.employeeId = employeeId;
        this.name = name;
        this.timecards = new ArrayList<>();
    }

    public int getEmployeeId() {
        return employeeId;
    }

    public String getName() {
        return name;
    }

    public void addTimecard(Timecard timecard) {
        timecards.add(timecard);
    }

    public List<Timecard> getTimecards() {
        return timecards;
    }

    public void displayTimecards() {
        System.out.println("Timecards for " + name + ":");
        for (Timecard timecard : timecards) {
            System.out.println(timecard);
        }
    }
}

 public class PayrollSystem {
    public static void main(String[] args) {
    	
    	// tạo đối tượng nhân viên
    	
        Employee emp1 = new Employee(1, "Bui Nguyen Diem Quynh");
        
        // tạo thẻ chấm công và thêm danh sách thẻ chấm công của nhân viên
        
        emp1.addTimecard(new Timecard("1", new Date(), 8));
        emp1.addTimecard(new Timecard("1", new Date(), 7));
        
        // hiển thị danh sách thẻ chấm công
        
        emp1.displayTimecards();
    }
}







