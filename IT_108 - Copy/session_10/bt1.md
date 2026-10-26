## Bài 1 : Chuẩn hóa tài liệu Markdown cho dự án

## Phần 1. Phân tích các lỗi cú pháp:

Đoạn mã của bạn sinh viên mắc các lỗi chính sau khiến trình biên tập (StackEdit) hiển thị sai định dạng:

1.  Lỗi phân cấp tiêu đề :
    
-   Biểu hiện: Dùng # Lợi ích của rau sạch (H1) xong nhảy ngay xuống ### Danh sách các loại rau (H3).
    
-   Nguyên nhân: Bỏ quên thẻ H2 (##). Trong Markdown và chuẩn HTML, việc nhảy cóc cấp độ tiêu đề làm mất tính logic của cấu trúc tài liệu và đôi khi làm bộ render bị lỗi thụt lề, phá vỡ giao diện.
   
2.  Lỗi cú pháp chèn ảnh :
-   Biểu hiện: [Logo Dự án] (https://greentech.vn/logo.png)
-   Nguyên nhân: Thừa dấu cách giữa cặp ngoặc vuông [...] và ngoặc tròn (...). Cú pháp chuẩn của Markdown yêu cầu hai cặp ngoặc này phải dính liền nhau ([Alt text](URL)). Do có khoảng trắng ở giữa, StackEdit hiểu nhầm đây là một đoạn text bình thường kèm link chứ không phải là một hình ảnh, khiến ảnh không hiển thị.
    

  

3.  Lỗi cú pháp in đậm :
    

-   Biểu hiện: Rất quan trọng (chỉ dùng 1 dấu sao *Rất quan trọng*).
    

-   Nguyên nhân: Một cặp dấu sao đơn (*text*) chỉ tạo ra chữ in nghiêng (Italic), trong khi yêu cầu hoặc mục đích là in đậm. Để in đậm (Bold), bắt buộc phải dùng hai cặp dấu sao (**text**) hoặc hai cặp gạch dưới (__text__).
    

  

## Phần 2. Hoàn thiện đoạn mã Markdown chuẩn:
-   Đoạn mã đã được chỉnh sửa toàn bộ lỗi, tuân thủ đúng phân cấp H1 -> H2 và các quy tắc cú pháp cơ bản:
# Lợi ích của rau sạch
## Danh sách các loại rau
![Logo Dự án](https://greentech.vn/logo.png)
**Rất quan trọng**
