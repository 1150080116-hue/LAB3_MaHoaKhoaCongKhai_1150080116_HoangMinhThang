# BÁO CÁO

## 1. THÔNG TIN SINH VIÊN
- **Họ và tên**: Hoàng Minh Thắng
- **Mã số sinh viên (MSSV)**: 1150080116
- **Môn học**: An toàn và Bảo mật Hệ thống Thông tin (ATVBMHTTT)
- **Bài thực hành**: Bài số 3 – MÃ HÓA KHÓA CÔNG KHAI (RSA, ECC, RSA+AES, ECDSA, SQL SERVER)


---

## 2. YÊU CẦU MÔI TRƯỜNG & PHẦN MỀM
- **Hệ điều hành**: Windows 10/11
- **Java Development Kit (JDK)**: JDK 17 (LTS) hoặc mới hơn
- **IDE**: Apache NetBeans 15 trở lên (hỗ trợ Maven)
- **Hệ quản trị CSDL**: Microsoft SQL Server 2016+ (bật chế độ SQL Server and Windows Authentication mode - Mixed Mode)
- **Thư viện JDBC**: `com.microsoft.sqlserver:mssql-jdbc:12.8.1.jre11` (được cấu hình tự động tải qua file `pom.xml`)

---

## 3. HƯỚNG DẪN THỰC THI

### Bước 1: Khởi tạo Cơ sở Dữ liệu Microsoft SQL Server
1. Mở **SQL Server Management Studio (SSMS)** và đăng nhập bằng quyền Windows Authentication (hoặc `sa`).
2. Mở và thực thi file `02_SQL/01_Tao_CSDL.sql` (bấm `F5`) để tạo CSDL `LAB3_MaHoaKhoaCongKhai` và bảng `dbo.History`.
3. Mở và thực thi file `02_SQL/02_Tao_TaiKhoan_LAB.sql` (bấm `F5`) để tạo tài khoản `lab3_user` (mật khẩu: `LabUser@2026`) và cấp quyền `SELECT, INSERT` trên bảng `dbo.History`.

### Bước 2: Mở và chạy Project trên NetBeans
1. Mở **Apache NetBeans**.
2. Chọn menu **File** $\rightarrow$ **Open Project...**
3. Điều hướng tới thư mục `01_Java_NetBeans/LAB3_MaHoaKhoaCongKhai` (có biểu tượng icon Maven) và bấm **Open Project**.
4. Chờ NetBeans nạp và tự động tải thư viện Maven JDBC nếu cần.
5. Chuột phải vào project $\rightarrow$ chọn **Run** (hoặc mở file `frm_Menu.java` $\rightarrow$ chuột phải chọn **Run File** / phím tắt `Shift + F6`).

### Bước 3: Kiểm thử các chức năng trên giao diện
1. **Kết nối SQL Server** (`frm_KetNoiSQL`):
   - Nhập thông tin Server: `127.0.0.1`, Port: `14333` (hoặc cổng cấu hình của máy), Database: `LAB3_MaHoaKhoaCongKhai`, User: `lab3_user`, Password: `LabUser@2026`.
   - Bấm **Test Connection** để kiểm tra và kích hoạt ghi log tự động.
2. **Bài 3.1 - Demo Console RSA** (`RSADemo.java`):
   - Chạy trực tiếp class `RSADemo.java` để xem so sánh tạo khóa, mã hóa, giải mã giữa 2048-bit và 3072-bit trên Console.
3. **Bài 3.2 - Mật mã RSA-OAEP** (`frm_RSA`):
   - Bấm **Generate Keys**, nhập Plaintext `HELLO RSA`, bấm **Encrypt**, sau đó bấm **Decrypt**.
   - Thử nhập văn bản dài trên 190 byte để quan sát cơ chế bắt lỗi giới hạn độ dài của RSA.
4. **Bài 3.3 - Mật mã Đường cong Elliptic ECC** (`frm_ECC`):
   - Tạo khóa `secp256r1`, mã hóa và giải mã theo cơ chế ECIES (ECDH + HKDF + AES-GCM). Thử nghiệm lưu/nạp khóa và thử giải mã với khóa sai.
5. **Bài 3.4 - Hệ mã lai RSA + AES** (`frm_RSA_AES`):
   - Mã hóa và giải mã văn bản dài trên 1.000 ký tự bằng AES-256-GCM kết hợp RSA-OAEP bọc khóa. Bấm **Sửa 1 ký tự bản mã** để kiểm tra tính toàn vẹn (GCM phát hiện sửa đổi).
6. **Bài 3.5 - Chữ ký số ECDSA** (`frm_ECC_Signature`):
   - Ký thông điệp bằng Khóa riêng, xác minh bằng Khóa công khai (`VALID` màu xanh). Sửa thông điệp hoặc đổi cặp khóa để quan sát kết quả `INVALID` màu đỏ.
7. **Xem Lịch sử thao tác** (`frm_LichSu`):
   - Bấm **Tải lại** để xem các thao tác đã được lưu trữ trong bảng `dbo.History`.
   - Mở file `02_SQL/03_KiemTra_LichSu.sql` trong SSMS để xem thống kê dữ liệu.

---
