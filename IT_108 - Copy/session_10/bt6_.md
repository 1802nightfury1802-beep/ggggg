# Phần 1. Phân tích bài toán

- Nam đã mắc 2 sai lầm căn bản trong tư duy khi lưu trữ tài liệu kĩ thuật và quản lý mã nguồn:

## 1. Dùng file Rich Text nhị phân (.docx) cho hệ thống quản lý phiên bản (Git):

-   **Bản chất vấn đề:** File `.docx` không phải là văn bản thuần mà thực chất là một lưu trữ nén chứa nhiều file XML, hình ảnh, thông tin định dạng và font chữ bên trong.
    
-   **Tác động tới Git:**
    
    -  Git hoạt động dựa trên cơ chế theo dõi sự thay đổi theo từng dòng văn bản . Do `.docx` là file nhị phân , Git không thể đọc hoặc so sánh cấu trúc bên trong.
        
    -   Khi Nam sửa dù chỉ 1 dấu phẩy hay đổi font chữ, toàn bộ tệp nén nhị phân bị thay đổi hoàn toàn. Git buộc phải lưu đè một file nhị phân mới hoàn toàn, gây ra tình trạng **Conflict toàn bộ file** và làm phình to dung lượng repository cực kỳ nhanh.
        
    -   Ngược lại, **Markdown (.md)** là **Plain Text (văn bản thô)**. Git hiểu chính xác dòng nào vừa được sửa, cho phép so sánh `Git Diff` trực quan từng từ, từng câu và tự động hợp nhất công sức của nhiều người mà không bị xung đột.
        

### 2. Sử dụng định dạng phụ thuộc vào ứng dụng thương mại để hiển thị trực tiếp

-   **Bản chất vấn đề:** Muốn đọc hoặc render nội dung file `.docx`, hệ thống buộc phải có phần mềm tương thích (như Microsoft Word) để giải nén và render các thẻ XML bên trong. GitHub và hầu hết các trình duyệt web không hỗ trợ render trực tiếp file Word trên giao diện repository.
    
-   **Đối chiếu tính an toàn & Khả năng phục hồi dữ liệu khi lỗi mạng (Bẫy dữ liệu):**
    
    -   **Trường hợp `.docx`:** Nếu tệp Word bị lỗi mạng làm mất/méo 1 byte dữ liệu ở cấu trúc nén ZIP hoặc thẻ mở XML, phần mềm sẽ không thể giải nén hay phân tích cú pháp (parse), dẫn đến lỗi _"File is corrupted and cannot be opened"_ (**hỏng hoàn bộ file, không thể đọc được gì**).
        
    -   **Trường hợp Markdown (`.md`):** Do là Plain Text thuần túy, kể cả khi mất 1 byte dữ liệu (mất 1 ký tự / 1 ký hiệu `#`), những nội dung còn lại vẫn hiển thị và đọc được bình thường** bằng bất kỳ trình đọc text đơn giản nào .
        
    -   **Dung lượng:** File Markdown chỉ chứa mã ASCII/UTF-8 nguyên bản nên dung lượng cực kỳ nhẹ (vài KB), tải xuống gần như tức thì và cực kỳ an toàn.
        

# Phần 2. Hoàn thiện: Chuyển đổi đoạn giới thiệu sang Markdown (.md)

Đoạn mã Markdown đã được chuyển đổi từ bản thảo Word của Nam, hiển thị tối ưu trên trình duyệt GitHub và StackEdit:

# 🌿 Dự Án GreenTech — Giải Pháp Nông Nghiệp Thông Minh:

> **GreenTech** là dự án nghiên cứu và phát triển các thiết bị IoT phục vụ tự động hóa quy trình chăm sóc cây trồng, tối ưu hóa lượng nước và phân bón.

---

##  Mục Tiêu Dự Án:

* **Tự động hóa:** Giảm $80\%$ sức lao động thủ công trong việc tưới tiêu.
* **Tiết kiệm tài nguyên:** Tối ưu lượng nước sử dụng dựa trên dữ liệu cảm biến thời gian thực.
* **Dễ dàng tiếp cận:** Giao diện quản lý thân thiện cho người nông dân trên thiết bị di động.

---

##  Cấu Trúc Hệ Thống:

1. **Cảm biến :** Thu thập nhiệt độ, độ ẩm đất, ánh sáng.
2. **Bộ xử lý trung tâm :** Tiếp nhận dữ liệu, phân tích và phát lệnh điều khiển.
3. **Thiết bị chấp hành :** Rơ-le kích hoạt máy bơm, van từ và quạt thông gió.

---

## 📌 Liên Hệ & Đóng Góp:

* **Đơn vị phát triển:** Sinh viên PTIT — Nhóm Nông Nghiệp Số.
* **Mã nguồn:** Lưu trữ và quản lý phiên bản trực tiếp tại [GitHub Repository] (https://github.com/greentech/smart-farm).
