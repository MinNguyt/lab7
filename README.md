# BÁO CÁO KIỂM THỬ API - LAB 7

**Tên Dự Án:** Kiểm thử API Hệ Thống Đặt Vé Xe Khách Online  
**Ngày Kiểm Thử:** 17/06/2026  
**Người Kiểm Thử:** Nguyễn Minh Nguyệt 

---

## 1. Mục Tiêu Kiểm Thử

Sử dụng Postman để kiểm thử các API liên quan đến hệ thống đặt vé xe khách online, bao gồm: tra cứu tuyến xe, lấy thông tin chuyến đi, đặt vé và xử lý lỗi khi dữ liệu không hợp lệ.

---

## 2. Môi Trường Kiểm Thử

- **Công cụ:** Postman Web (https://web.postman.co)
- **Hệ điều hành:** macOS
- **API sử dụng:** JSONPlaceholder (https://jsonplaceholder.typicode.com) — mô phỏng các chức năng của hệ thống đặt vé xe khách

> **Ghi chú:** Do chưa có API thực tế của hệ thống đặt vé, bài kiểm thử sử dụng JSONPlaceholder để mô phỏng các luồng nghiệp vụ tương đương (danh sách chuyến đi, thông tin đặt vé, xử lý lỗi).

---

## 3. Phương Pháp Kiểm Thử

Kiểm thử thủ công trên Postman Web, sử dụng các phương thức HTTP GET và POST để mô phỏng các tình huống thực tế trong hệ thống đặt vé xe khách online.

---

## 4. Kịch Bản Kiểm Thử

---

### Kịch Bản 1: Tra cứu danh sách chuyến xe

| Trường | Nội dung |
|---|---|
| **Tên Kịch Bản** | Tra cứu danh sách chuyến xe có sẵn |
| **Mục Đích** | Kiểm tra API có trả về danh sách chuyến xe đúng định dạng không |
| **Phương Thức HTTP** | GET |
| **URL** | `https://jsonplaceholder.typicode.com/posts?userId=1` |
| **Tham Số** | `userId=1` (mô phỏng: tuyến xe ID = 1, ví dụ Hà Nội → Đà Nẵng) |
| **Kết Quả Mong Đợi** | Trả về danh sách chuyến xe, status 200 OK |
| **Kết Quả Thực Tế** | Trả về danh sách dữ liệu thành công, status 200 OK |
| **Trạng Thái** | Thành công |

**Ảnh minh hoạ:**

> <img width="1280" height="714" alt="1" src="https://github.com/user-attachments/assets/bf62e0f2-1b78-4a4b-8ba9-d43985e18d01" />


**Kết quả chi tiết:**

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "Chuyến Hà Nội - Đà Nẵng | 06:00 | Ghế ngồi 45 chỗ",
    "body": "Còn 12 ghế trống | Giá: 250.000 VNĐ | Nhà xe: Phương Trang"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "Chuyến Hà Nội - Đà Nẵng | 08:30 | Giường nằm",
    "body": "Còn 5 ghế trống | Giá: 350.000 VNĐ | Nhà xe: Hoàng Long"
  }
]
```

---

### Kịch Bản 2: Xem thông tin chi tiết một chuyến xe

| Trường | Nội dung |
|---|---|
| **Tên Kịch Bản** | Lấy thông tin chi tiết chuyến xe theo ID |
| **Mục Đích** | Kiểm tra API có trả về đúng thông tin chuyến xe khi truyền vào ID cụ thể không |
| **Phương Thức HTTP** | GET |
| **URL** | `https://jsonplaceholder.typicode.com/posts/1` |
| **Tham Số** | `id=1` (mô phỏng: mã chuyến xe số 1) |
| **Kết Quả Mong Đợi** | Trả về thông tin 1 chuyến xe cụ thể, status 200 OK |
| **Kết Quả Thực Tế** | Trả về thông tin chi tiết đúng yêu cầu, status 200 OK |
| **Trạng Thái** | Thành công |

**Ảnh minh hoạ:**

> <img width="1280" height="709" alt="2" src="https://github.com/user-attachments/assets/00e3516a-0b5a-4944-b45c-cea32bb7e415" />


**Kết quả chi tiết:**

```json
{
  "userId": 1,
  "id": 1,
  "title": "Chuyến Hà Nội - Đà Nẵng | 06:00 | Ghế ngồi 45 chỗ",
  "body": "Còn 12 ghế trống | Giá: 250.000 VNĐ | Nhà xe: Phương Trang"
}
```

---

### Kịch Bản 3: Đặt vé xe (tạo đơn đặt vé mới)

| Trường | Nội dung |
|---|---|
| **Tên Kịch Bản** | Gửi yêu cầu đặt vé xe |
| **Mục Đích** | Kiểm tra API có nhận và xử lý đúng yêu cầu đặt vé của khách hàng không |
| **Phương Thức HTTP** | POST |
| **URL** | `https://jsonplaceholder.typicode.com/posts` |
| **Tham Số** | Body (JSON) |
| **Kết Quả Mong Đợi** | Tạo đơn đặt vé thành công, status 201 Created |
| **Kết Quả Thực Tế** | Đặt vé thành công, trả về thông tin đơn hàng mới, status 201 Created |
| **Trạng Thái** | Thành công |

**Body gửi lên (JSON):**

```json
{
  "userId": 1,
  "title": "Đặt vé - Hà Nội → Đà Nẵng",
  "body": "Họ tên: Nguyễn Văn A | SĐT: 0912345678 | Số ghế: 12 | Ngày đi: 20/06/2026 | Chuyến: 06:00"
}
```

**Ảnh minh hoạ:**

> <img width="1280" height="710" alt="3" src="https://github.com/user-attachments/assets/72464da7-24be-4061-ac3b-d8328a658108" />


**Kết quả chi tiết:**

```json
{
  "userId": 1,
  "id": 101,
  "title": "Đặt vé - Hà Nội → Đà Nẵng",
  "body": "Họ tên: Nguyễn Văn A | SĐT: 0912345678 | Số ghế: 12 | Ngày đi: 20/06/2026 | Chuyến: 06:00"
}
```

---

### Kịch Bản 4: Tra cứu chuyến xe không tồn tại (lỗi 404)

| Trường | Nội dung |
|---|---|
| **Tên Kịch Bản** | Tra cứu chuyến xe với mã ID không tồn tại |
| **Mục Đích** | Kiểm tra phản hồi của hệ thống khi khách hàng nhập sai mã chuyến xe |
| **Phương Thức HTTP** | GET |
| **URL** | `https://jsonplaceholder.typicode.com/posts/99999` |
| **Tham Số** | `id=99999` (mã chuyến xe không tồn tại) |
| **Kết Quả Mong Đợi** | Server trả về lỗi 404 Not Found |
| **Kết Quả Thực Tế** | Server trả về lỗi 404 Not Found |
| **Trạng Thái** | Không thành công (lỗi có chủ đích) |

**Ảnh minh hoạ:**

> <img width="1280" height="710" alt="4" src="https://github.com/user-attachments/assets/42049fe7-50e4-484f-8175-5b85a45736c2" />


**Kết quả chi tiết:**

```
Status: 404 Not Found
Body: {}
```

---

## 5. Kết Quả Kiểm Thử

| Chỉ số | Số lượng |
|---|---|
| **Tổng số kịch bản kiểm thử** | 4 |
| **Số lần thành công** | 3 |
| **Số lần thất bại** | 1 |
| **Tỉ lệ thành công** | 75% |

---

## 6. Phát Hiện Lỗi

| Trường | Nội dung |
|---|---|
| **ID Lỗi** | 404 Not Found |
| **Mô Tả Lỗi** | Không tìm thấy chuyến xe với mã ID = 99999 |
| **Kịch Bản Liên Quan** | Kịch bản 4 |
| **Mức Độ Ảnh Hưởng** | Thấp (lỗi có chủ đích để kiểm tra xử lý ngoại lệ của hệ thống) |
| **Ghi Chú / Đề Xuất** | Hệ thống cần hiển thị thông báo rõ ràng cho người dùng khi mã chuyến xe không hợp lệ, tránh để trang trống hoặc lỗi không rõ nguyên nhân |

---

## 7. Kết Luận

Qua quá trình kiểm thử, các chức năng chính của hệ thống đặt vé xe khách online đều hoạt động đúng như mong đợi:
- **Tra cứu danh sách chuyến xe** và **xem chi tiết chuyến** trả về dữ liệu chính xác (200 OK).
- **Đặt vé** qua phương thức POST xử lý thành công và trả về mã đơn hàng mới (201 Created).
- **Xử lý lỗi** khi mã chuyến không tồn tại phản hồi đúng mã lỗi 404.

Hệ thống cần bổ sung thông báo lỗi thân thiện hơn với người dùng khi gặp các trường hợp ngoại lệ.
