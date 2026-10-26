
# Báo cáo phân tích (I/O):
## 1. Input ( văn bản thô ): 
-   **Loại dữ liệu:** Văn bản thô chưa chuẩn hóa (Unstructured Text) chứa thông tin hướng dẫn lắp đặt cảm biến độ ẩm, mã nguồn Python điều khiển máy bơm tự động, dữ liệu thông số kỹ thuật cảm biến và danh sách công việc kiểm tra.
    
-   **Đặc điểm:** Dễ gây nhầm lẫn giữa văn bản giải thích và câu lệnh hệ thống; chưa phân biệt rõ dữ liệu bảng và danh sách kiểm tra.

## 2. Output ( Giao diện render chuyên nghiệp ):
- -   **Định dạng:** Tài liệu `Markdown` chuẩn (.md) được hiển thị chuyên nghiệp (Rendered View).
    
-   **Thành phần giao diện:**
    
    -   **Inline Code:** Phân biệt rõ các tên biến (ví dụ: `sensor_pin`), đường dẫn, lệnh Terminal ngắn.
        
    -   **Code Block:** Mã nguồn Python điều khiển máy bơm có hỗ trợ Highlight cú pháp (`python`).
        
    -   **Bảng (Table):** So sánh trực quan giữa Cảm biến độ ẩm đất điện dung (Loại mới) và Cảm biến trở kháng (Loại cũ).
        
    -   **Danh sách công việc (Task List):** Các mục kiểm tra trạng thái thiết bị (`[x]` và `[ ]`).
        
    -   **Ký tự Escape:** Hiển thị chính xác các ký tự đặc biệt như `\*` hoặc `\#` mà không bị lỗi định dạng Markdown.
    
# Source code:
## 1. Chuẩn Bị & Cấu Hình Môi Trường:

- Để khởi chạy hệ thống, mở Terminal trên Raspberry Pi và chạy lệnh cập nhật danh sách gói: `sudo apt-get update && sudo apt-get upgrade -y`

- Khởi tạo môi trường ảo Python bằng lệnh `python3 -m venv venv` và kích hoạt môi trường bằng `source venv/bin/activate`.

- Thiết lập biến môi trường chỉ định cổng kết nối: `export SENSOR_PORT="/dev/ttyUSB0"`


>     

## 2. So Sánh Thiết Bị Cảm Biến:

Bảng so sánh các thông số kỹ thuật giữa cảm biến loại cũ và loại mới được trang bị cho trang trại Lan:

|Tiêu Chí So Sánh|Cảm Biến Trở Kháng (Cũ)|Cảm Biến Điện Dung (Mới)|
|-|-|-|
|Nguyên lý hoạt động|Đo điện trở giữa 2 cực|Đo độ dung điện của môi trường|
|Độ bền/Độ ăn mòn |Kém (Dễ bị ăn mòn kim loại sau 2-3 tháng)|Cao (Không bị ăn mòn, lớp phủ chống oxy hóa)|
|Độ chính xác |~5%|~1,5%|
|Tín hiệu đầu ra|Analog (`A0`)|Analog (`A0`)/RS485|
|Điện áp hoạt động|3,3V - 5V|3,3V - 5V|
|Chi phí đầu tư|Thấp (~15.000 VNĐ)|Trung bình (~45.000 VNĐ) |



## 3. Danh Sách Kiểm Tra Vận Hành (Task List):

Trước khi nghiệm thu và đưa hệ thống vào vận hành thực tế tại trang trại, kỹ thuật viên cần hoàn thành các danh mục sau:

-   [x] Kiểm tra nguồn điện  5V-2A cấp cho Raspberry Pi và cảm biến.
    
-   [x] Kết nối cảm biến độ ẩm điện dung vào chân `GPIO 21`.
    
-   [x] Kiểm tra dây tín hiệu rơ-le kết nối máy bơm tại chân `GPIO 20`.
    
-   [x] Chạy thử đoạn code kiểm tra `python3 -m unittest test_sensors.py`.
    
-   [ ] Hiệu chỉnh lại ngưỡng `THRESHOLD_DRY` cho từng loài Lan (Lan Hồ Điệp, Lan Dendro).
    
-   [ ] Bọc băng dính cách điện và hộp bảo vệ chống nước cho các mối nối outdoor.
    
-   [ ] Thiết lập tiến trình chạy ngầm `systemd` cho script Python khi khởi động lại Pi.
