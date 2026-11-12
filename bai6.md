# Bài 6: Phân tích cơ chế "Tràn cốc ngữ cảnh" (Truncation) trong luồng tư vấn CSKH
## Phần 1: Giải thích hiện tượng "chiếc cốc nước" 
Content Window "chiếc cốc nước" giống như một chiếc cốc thủy tinh có dung tích cố định. Toàn bộ nội dung cuộc hội thoại, bao gồm đầu vào và đầu ra đều biến thành "nước" (Token) đổ vào chiếc cốc này.
Ở lượt 1, cốc còn trống khoảng 95%. Tuy nhiên qua 40 lượt tư vấn, lượng lớn nước mới được rót thêm cho đến khi chạm 100%.
Hiện tượng Truncation( cắt gọt dữ liệu cũ): khi cốc tràn mà vẫn tiếp tục rót thêm nược ở lượt 42, phần nước cũ nhất nằm ở đáy cốc buộc phải bị đẩy văng ra ngoài nhường chỗ cho lượng nước mới dẫn đến AI bị quên dữ liệu ở lượt 1
## Phương án quản lý RAM bộ nhớ 
### Phương án từ phía người dùng 
1. Mở phiên chat mới: tách riêng từng khách hàng hoặc từng luồng nghiệp vụ
2. Tóm tắt và chuyển phiên: sau khoảng 20 lượt, yêu cầu AI tóm tắt ngắn gọn thông tin cốt lõi rồi dán sang phiên chat mới
3. giới hạn độ dài phản hồi: yêu cầu AI trả lời ngắn gọn, súc tích để tiết kiệm Tokens
### Phương án từ phía hệ thống
1. Bộ nhớ tóm tắt trượt (Summary Memory): Tự động nén các hội thoại cũ thành bản tóm tắt ngắn gọn và ghim cố định ở đầu Content Window thay vì xóa hoàn toàn 
2. Truy xuất dữ liệu ngoài (RAG / Database): Kết nối AI trực tiếp với hệ thống CRM/đơn hàng của MartX để tra cứu mã #MTX-9988 theo thời gian thực, không lưu trữ cứng trong luồng chat