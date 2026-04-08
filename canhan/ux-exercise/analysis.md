# UX exercise — Vietnam Airlines Chatbot NEO

## Sản phẩm: Vietnam Airlines — Chatbot NEO

## 4 paths

### 1. AI đúng
- User hỏi ngắn, rõ ràng: “Hành lý xách tay được bao nhiêu kg?” hoặc “Kiểm tra giờ cất cánh chuyến VNxxx”
- NEO trả lời đúng nhóm thông tin phổ biến như vé máy bay, chuyến bay, hành lý, thanh toán, hoàn/đổi vé
- User thấy mình đã vào đúng luồng hỗ trợ, không cần rời chat
- UI hiện có khuyến khích user hỏi ngắn, rõ ràng và tra cứu từ các mục nội dung có sẵn

### 2. AI không chắc
- User hỏi mơ hồ: “Tôi đổi vé được không?” nhưng không nói rõ hạng vé, hành trình, điều kiện vé
- Fallback hiện tại chủ yếu là:
  - khuyên user hỏi ngắn, rõ ràng hơn
  - cho user tra cứu từ các mục nội dung có sẵn
  - nếu chưa giải đáp được thì chuyển hướng gặp tư vấn viên
- Vấn đề:
  - chưa thấy flow hỏi lại kiểu “Bạn đang hỏi booking nào / hạng vé nào?”
  - chưa có lớp clarify intent đủ mạnh ngay trong chat
  - user dễ cảm giác bot “không hiểu” hơn là “đang giúp làm rõ”

### 3. AI sai
- User hỏi: “Vé của tôi đổi ngày được không? Phí bao nhiêu?”
- NEO trả lời một câu nghe hợp lý nhưng không đúng với điều kiện cụ thể của booking
- User chỉ phát hiện khi tự đối chiếu lại website, FAQ hoặc hỏi người thật
- Vấn đề:
  - user không có tín hiệu mạnh để biết câu trả lời này có rủi ro sai
  - không thấy rõ nút “xem nguồn chính thức”, “báo câu trả lời sai”, hay “chuyển người thật kèm transcript”
  - recovery flow còn yếu, trách nhiệm kiểm tra lại bị đẩy nhiều cho user

### 4. User mất niềm tin
- Sau 1–2 lần bot trả lời không rõ hoặc sai case cụ thể, user không muốn hỏi tiếp
- Điểm tốt là vẫn có fallback ở mức hệ sinh thái hỗ trợ:
  - chuyển hướng gặp tư vấn viên
  - FAQ / trung tâm trợ giúp / liên hệ hỗ trợ
- Vấn đề:
  - exit có, nhưng chủ yếu là rời sang kênh khác
  - chưa có handoff mượt ngay trong hội thoại
  - user có thể bỏ chat hoàn toàn thay vì được “cứu niềm tin”

## Path yếu nhất: Path 3
- Khi AI sai, user khó biết sai ở đâu và sửa bằng cách nào
- Legal đã thừa nhận AI có thể sai, nhưng UX chưa biến điều đó thành trust-recovery flow rõ ràng
- User phải tự kiểm tra lại hoặc tự chuyển sang người thật

## Sketch
(Ảnh đính kèm: sketch.jpg)
### As-is
- User hỏi: “Vé của tôi đổi ngày được không? Phí bao nhiêu?”
- NEO trả lời bằng 1 đoạn text hoặc dẫn sang thông tin chung
- User không chắc câu trả lời này có áp đúng booking/hạng vé của mình không
- Nếu vẫn rối, user tự mở FAQ / tìm mục khác / gặp tư vấn viên
- Chỗ gãy:
  - không confirm intent
  - không hỏi lại thông tin còn thiếu
  - không hiện mức chắc chắn
  - không có trust-recovery rõ ngay tại chỗ

### To-be
- User hỏi: “Vé của tôi đổi ngày được không? Phí bao nhiêu?”
- NEO trả lời:
  - “Mình có thể hỗ trợ, nhưng cần làm rõ để trả lời đúng hơn.”
- Hiện 3 lựa chọn nhanh:
  - **Tra cứu theo mã đặt chỗ**
  - **Xem điều kiện đổi vé theo hạng vé**
  - **Gặp tư vấn viên**
- Nếu confidence thấp:
  - hiện nhãn **“Mình chưa chắc 100%”**
  - hiện nút **“Xem nguồn chính thức”**
  - hiện nút **“Chuyển người thật”**
- Nếu handoff:
  - gửi kèm tóm tắt hội thoại để user không phải kể lại từ đầu