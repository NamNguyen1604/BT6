# BT6
# Họ tên : Nguyễn Phương Nam 
# Môn học : Hệ quản trị cơ sở dữ liệu 
# Lớp : K58.KMT
# Yêu cầu bài tập : 
Cho file sv_tnut.sql (1.6MB)
1. Hãy nêu các bước để import được dữ liệu trong sv_tnut.sql vào sql server của em
2. dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên (của sv đang làm bài tập này)
3. nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
4. nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với em?
5. nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với em?
6. nhập sql để tìm xem có những sv nào trùng tên với em?
7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với em.
8. nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em.
9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH.
10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)
# Bài làm : 
# 1.Các bước để import được dữ liệu trong sv_tnut.sql vào sql server 
![image](https://github.com/user-attachments/assets/35a2deda-5990-48e6-b9a5-f7ab9c1e8a7a)
![image](https://github.com/user-attachments/assets/7cc219d4-9c46-42f2-8ed8-8b72a7dc0261)
- Sau đó tạo database mới :
![image](https://github.com/user-attachments/assets/68f50793-6fc1-4f24-b72a-6152e6bd3e1e)
- Ấn Excute để chạy file thành công ở database trong server 
![image](https://github.com/user-attachments/assets/6d370cba-66c2-4705-b071-7d6ebb1f45d7)
# 2.Đưa dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên
-Để thêm dữ liệu cá nhân của mình (Nguyễn Phương Nam, 0898632486, sinh ngày 2004-10-16) vào bảng SV trong file sv_tnut.sql thì chúng ta sử dụng code :
IF NOT EXISTS (
    SELECT 1 FROM SV WHERE masv = 'k225480106092'
)
BEGIN
    INSERT INTO SV (masv, hodem, ten, ns, lop, sdt)
    VALUES ('k225480106092', N'Nguyễn Phương', N'Nam', '2004-10-16', N'KMT-TEST', '0898632486');
END

![image](https://github.com/user-attachments/assets/12bc344a-8a01-4ad8-bb4e-d73be3f562cb) 
# 3.nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm của em 
- Muốn nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm của mình thì chúng ta sử dụng code : 
SELECT * 
FROM SV 
WHERE ns = '2004-10-16'
 Ta được kết quả  :
![image](https://github.com/user-attachments/assets/1ba88e38-7728-42ee-ab71-6bef503f6521)

# 4. Nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với mình 
- Muốn nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với mình ta nhập code 
  SELECT * 
FROM SV 
WHERE DAY(ns) = 16 AND MONTH(ns) = 10;
 Ta được kết quả : 
![image](https://github.com/user-attachments/assets/6d524364-2122-4086-92fd-93d0c97ec1a1)

# 5. Nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với mình 
- Muốn nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với mình ta dùng code :
  SELECT * 
FROM SV 
WHERE MONTH(ns) = 10 AND YEAR(ns) = 2004;
Ta được kết quả  : 
![image](https://github.com/user-attachments/assets/923fb5cc-9fde-4c3d-9e1d-ac710203c028)

# 6. Nhập sql để tìm xem có những sv nào trùng tên với mình 
- Muốn nhập sql để tìm xem có những sv nào trùng tên với mình  ta dùng code :
  SELECT * 
FROM SV 
WHERE ten = N'Nam';

  Ta được kết quả :
  ![image](https://github.com/user-attachments/assets/75547424-b209-4c62-bdd6-d51840e26dd6)
# 7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với mình
- Để nhập sql để tìm xem có những sv nào trùng họ và tên đệm với mình thì ta sử dụng :
  SELECT * 
FROM SV 
WHERE hodem = N'Nguyễn Phương';
Ta được kết quả :
![image](https://github.com/user-attachments/assets/b3e96d18-24b2-4d9c-ab6b-e42d358f9ac9)
# 8. Nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của mình
  - Để so sánh từng ký tự bằng master.dbo.spt_values: ta có
  SELECT * 
FROM SV
WHERE LEN(sdt) = LEN('0898632486')
AND (
    SELECT COUNT(*) 
    FROM (
        SELECT TOP (LEN(sdt)) 
               CASE WHEN SUBSTRING(sdt, number, 1) <> SUBSTRING('0898632486', number, 1) THEN 1 ELSE 0 END AS diff
        FROM master.dbo.spt_values 
        WHERE type = 'P' AND number BETWEEN 1 AND LEN(sdt)
    ) AS differences
    WHERE diff = 1
) = 1;
- ta được :
  ![image](https://github.com/user-attachments/assets/b66a6e9c-7e5f-49cb-8c46-4565f9826624)

# 9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH.
- ta sử dụng code sau :
SELECT * 
FROM SV 
WHERE lop LIKE N'%KMT%' 
ORDER BY ten COLLATE Vietnamese_CI_AS, hodem COLLATE Vietnamese_CI_AS;
Ta có kết quả  :
![image](https://github.com/user-attachments/assets/33a88c1f-ce70-49c2-a8a3-124a42f52c2f)

# 10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)
Ta có code sau :
SELECT * 
FROM SV 
WHERE lop LIKE N'%KMT%' 
AND ten IN (N'Lan', N'Hương', N'Hằng', N'Hà', N'Linh', N'Phương', N'Trang', N'Mai', N'Ngọc', N'Anh') ;
- ta được kết quả :
![image](https://github.com/user-attachments/assets/90aea488-46e8-41bf-a190-bcd0b081261a)
* những suy nghĩ của em và khắc phục :
1. Bảng SV không có cột gioitinh ⇒ không thể biết chính xác ai là nữ 
Thêm cột gioitinh vào bảng SV ta sử dụng code sau : 
ALTER TABLE SV ADD gioitinh NVARCHAR(3);
-- Sau đó cập nhật thủ công hoặc bằng dữ liệu hỗ trợ
UPDATE SV SET gioitinh = N'Nữ' WHERE ten IN (N'Phương', N'Hương', N'Trang');

2. Phải dựa vào tên riêng (ten) để đoán giới tính ⇒ độ chính xác không cao
3. Có thể trùng tên giữa nam và nữ (ví dụ: “Anh”, “Linh”…)
4. Tên lớp không nhất quán : WHERE lop LIKE N'%KMT%' OR lop LIKE N'%KTMT%' OR lop LIKE N'%Kỹ thuật máy tính%'
5. Viết hoa, viết thường, có dấu hoặc không dấu (lấy ví dụ : Phương , phuong , phương ) : WHERE ten COLLATE Vietnamese_CI_AI = N'phuong' 
6. Thiếu hoặc sai thông tin : SELECT * FROM SV WHERE ten IS NULL OR LEN(ten) < 2; 
7. Trùng tên nhưng khác giới



