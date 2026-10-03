# Bài tập: Chuyển đổi ERD sang mô hình dữ liệu quan hệ

## Bước 1: Xác định các thực thể

Từ mô hình ERD, xác định được 5 thực thể chính:

1. **PHIEUXUAT**
   - SoPX (Khóa chính)
   - NgayXuat

2. **VATTU**
   - MaVTU (Khóa chính)
   - TenVTU

3. **PHIEUNHAP**
   - SoPN (Khóa chính)
   - NgayNhap

4. **DONDH**
   - SoDH (Khóa chính)
   - NgayDH

5. **NHACC**
   - MaNCC (Khóa chính)
   - TenNCC
   - DiaChi
   - SDT (thuộc tính đa trị)

## Bước 2: Xác định các mối quan hệ

### Quan hệ 1: Chi tiết phiếu xuất
PHIEUXUAT và VATTU có quan hệ N-N.

Tạo bảng trung gian:

**CT_PHIEUXUAT**
- SoPX (PK, FK)
- MaVTU (PK, FK)
- DGXuat
- SLXuat

### Quan hệ 2: Chi tiết phiếu nhập
PHIEUNHAP và VATTU có quan hệ N-N.

Tạo bảng trung gian:

**CT_PHIEUNHAP**
- SoPN (PK, FK)
- MaVTU (PK, FK)
- DGNhap
- SLNhap

### Quan hệ 3: Chi tiết đơn đặt hàng
DONDH và VATTU có quan hệ N-N.

Tạo bảng trung gian:

**CT_DONDH**
- SoDH (PK, FK)
- MaVTU (PK, FK)

### Quan hệ 4: Cung cấp
NHACC và DONDH có quan hệ 1-N.

Một nhà cung cấp có thể có nhiều đơn đặt hàng, mỗi đơn đặt hàng thuộc một nhà cung cấp.

Do đó thêm MaNCC làm khóa ngoại trong bảng DONDH.

## Bước 3: Xử lý thuộc tính đa trị

Thuộc tính **SDT** của NHACC là thuộc tính đa trị nên tách thành một bảng riêng:

**SDT_NHACC**
- MaNCC (PK, FK)
- SDT (PK)

## Bước 4: Danh sách các bảng sau khi chuyển đổi

### PHIEUXUAT
- SoPX (PK)
- NgayXuat

### VATTU
- MaVTU (PK)
- TenVTU

### PHIEUNHAP
- SoPN (PK)
- NgayNhap

### NHACC
- MaNCC (PK)
- TenNCC
- DiaChi

### DONDH
- SoDH (PK)
- NgayDH
- MaNCC (FK)

### CT_PHIEUXUAT
- SoPX (PK, FK)
- MaVTU (PK, FK)
- DGXuat
- SLXuat

### CT_PHIEUNHAP
- SoPN (PK, FK)
- MaVTU (PK, FK)
- DGNhap
- SLNhap

### CT_DONDH
- SoDH (PK, FK)
- MaVTU (PK, FK)

### SDT_NHACC
- MaNCC (PK, FK)
- SDT (PK)

## Kết luận

Sau khi chuyển đổi từ ERD sang mô hình dữ liệu quan hệ, thu được **9 bảng**:
PHIEUXUAT, VATTU, PHIEUNHAP, NHACC, DONDH, CT_PHIEUXUAT, CT_PHIEUNHAP, CT_DONDH và SDT_NHACC.
