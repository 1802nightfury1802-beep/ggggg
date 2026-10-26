# Phần 1. Phân Tích Hệ Thống (I/O & Phần Cứng)

## 1. Xác định Input / Output (IPO)

-   **Input (Đầu vào):**
    
    -   Tín hiệu analog từ cảm biến độ ẩm đất và cảm biến nhiệt độ DHT22.
        
    -   Lệnh cấu hình ngưỡng độ ẩm từ người quản lý trang trại qua giao diện dòng lệnh.
        
-   **Process (Xử lý):**
    
    -   SoC (System-on-Chip) nhận dữ liệu, CPU thực hiện chu kỳ lệnh để phân tích thông số cảm biến so với ngưỡng cài đặt.
        
-   **Output (Đầu ra):**
    
    -   Trạng thái bật/tắt của rơ-le điều khiển máy bơm nước.
        
    -   Nhật ký hệ thống (Log file) và cảnh báo trực quan trên màn hình giám sát.
## 2. Sơ Đồ Phối Hợp Phần Cứng

```
[ Cảm biến độ ẩm / nhiệt độ ] ---> (Tín hiệu Analog/Digital) ---> [ Vi điều khiển / SoC (Raspberry Pi) ]
                                                                       |
                                                           (Xử lý lệnh & Quyết định)
                                                                       |
                                                                       v
                                                           [ Rơ-le & Máy bơm nước ]
```
# Phần 2. Triển Khai File README.md Chuyên Nghiệp:


##  Smart-Farm IoT: Hệ Thống Giám Sát & Tưới Tự Động Cho Trang Trại Lan

 *Hệ thống thông minh ứng dụng công nghệ IoT giúp tối ưu hóa quy trình chăm sóc lan, tiết kiệm nước và nâng cao năng suất cây trồng dựa trên dữ liệu thời gian thực.*

---

###  Mục Lục:
1. [Tổng Quan Hệ Thống & Sơ Đồ](#-tổng-quan-hệ-thống--sơ-đồ)
2. [Cơ Chế Hoạt Động (SoC & Chu Kỳ Lệnh)](#-cơ-chế-hoạt-động-soc--chu-kỳ-lệnh)
3. [Mô Hình Tháp Tri Thức (DIKW)](#-mô-hình-tháp-tri-thức-dikw)
4. [Hướng Dẫn Cài Đặt](#-hướng-dẫn-cài-đặt)
5. [Tính Năng Hệ Thống](#-tính-năng-hệ-thống)
6. [Bảng Thông Số Kỹ Thuật](#-bảng-thông-số-kỹ-thuật)
7. [Lưu Ý & Xử Lý Sự Cố](#-lưu-ý--xử-lý-sự-cố)

---

#### 1. Tổng Quan Hệ Thống & Sơ Đồ:

Dưới đây là sơ đồ kết nối tổng quan giữa các phần cứng trong trang trại:

![Sơ đồ kết nối phần cứng hệ thống Smart-Farm Smart Irrigation](https://images.unsplash.com/photo-1585320806297-9794b3e4eeae?auto=format&fit=crop&w=800&q=80)

---

#### 2. Cơ Chế Hoạt Động (SoC & Chu Kỳ Lệnh):

Khi hệ thống phát hiện độ ẩm xuống dưới mức cho phép, CPU trên vi điều khiển (SoC) sẽ thực hiện chu kỳ Fetch–Decode–Execute để điều khiển máy bơm:

 **Chu kỳ lệnh tưới Lan:**
- **Fetch (Lấy lệnh):** CPU truy xuất tập lệnh điều khiển máy bơm từ bộ nhớ Flash tại địa chỉ `0x0800F400`.
 - **Giải mã (Decode):** Bộ giải mã lệnh xác định đây là mã lệnh điều khiển ngắt chân GPIO 20 chuyển sang mức cao (`HIGH`).
 - **Thực thi (Execute):** ALU và mạch điều khiển ngoại vi kích hoạt dòng điện ra chân GPIO 20, đóng rơ-le và bật máy bơm nước tưới cho giàn lan.

---

#### 3. Mô Hình Tháp Tri Thức (DIKW):

Quá trình chuyển hóa dữ liệu thô thành hành động tưới tự động tại trang trại áp dụng mô hình DIKW:

- **Data :** Các giá trị điện áp thô đọc được từ cảm biến (ví dụ: `1.2V`, `2.4V`).
- **Information :** Dữ liệu được quy đổi thành giá trị phần trăm độ ẩm cụ thể (ví dụ: Độ ẩm đất là `25.5%`, Nhiệt độ là `32°C`).
- **Knowledge :** Phân tích quy luật sinh trưởng của hoa Lan: Lan Hồ Điệp cần độ ẩm đất từ `60% - 80%`. Dưới `30%` là ngưỡng khô hạn nguy hiểm.
- **Wisdom :** Ra quyết định tự động kích hoạt máy bơm nước trong `10` giây để đưa độ ẩm trở về vùng an toàn mà không cần sự can thiệp thủ công của con người.

---

#### 4. Hướng Dẫn Cài Đặt:

Mở Terminal trên thiết bị Raspberry Pi và chạy các lệnh sau để thiết lập môi trường:

```
# Cập nhật danh sách gói hệ thống
sudo apt-get update && sudo apt-get upgrade -y

# Cài đặt môi trường ảo python3
python3 -m venv smartfarm_env
source smartfarm_env/bin/activate

# Cài đặt các thư viện phụ thuộc
pip install RPi.GPIO adafruit-circuitpython-dht

```

#### 5. Tính Năng Hệ Thống:

-   [x] Đọc dữ liệu cảm biến độ ẩm đất và nhiệt độ liên tục thời gian thực.
    
-   [x] Tự động kích hoạt máy bơm khi độ ẩm thấp hơn ngưỡng cài đặt.
    
-   [x] Ghi nhật ký hoạt động (Log system) ra tệp tin hệ thống.
    
-   [x] Hỗ trợ chế độ điều khiển thủ công bằng tay qua giao diện dòng lệnh.
    
-   [ ] Tích hợp bảng điều khiển Web Dashboard từ xa qua mạng nội bộ.

 #### 6. Bảng thông số kĩ thuật:
 |Thành phần|Thông số kĩ thuật chi tiết|Ghi chú|
 |-|-|-|
 |Vi điều khiển chính|Raspberry Pi 4 Model B (SoC Broadcom BCM2711) |Xử lý trung tâm |
 |Cảm biến môi trường|DHT22 (Nhiệt độ & Độ ẩm không khí)|Sai số ~0,5|
 |Cảm biến đất|Cảm biến điện dung chống ăn mòn |Giao diện Analog/Digital|
 |Thiết bị chấp hành|Rơ-le 1 kênh 5V kích hoạt mức thấp|Điều khiển máy bơm 12V|

 #### 7. Lưu Ý & Xử Lý Sự Cố:

** Lưu ý quan trọng khi vận hành hệ thống:**

 -   Định kỳ kiểm tra kết nối nguồn điện để tránh sụt áp gây khởi động lại vi điều khiển.
    
 -   Xử lý sự cố đầy RAM do nhật ký hệ thống (Log Overflow):
    
     1.  Ngừng tiến trình ghi log hiện tại.
  
     2.  Dọn dẹp tệp nhật ký tạm thời đang chiếm dung lượng RAM/Disk.
       
     3. Khởi động lại dịch vụ hệ thống


---

# Phần 3. Kiểm Thử & Xử Lý Sự Cố (RAM Overflow Scenario):


Trong trường hợp hệ thống chạy lâu ngày khiến RAM bị đầy do lưu trữ quá nhiều dữ liệu nhật ký (Log), kỹ thuật viên/người vận hành tại trang trại có thể thực hiện theo các bước ngắt dịch vụ, xóa bớt dữ liệu nhật ký tạm thời và khởi động lại tiến trình giám sát để đảm bảo hệ thống không bị tràn bộ nhớ gây treo máy.

