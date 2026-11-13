# Bài nộp LAB5 — [Track] · Nhóm [tên]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]

## §1. Lát cắt & phạm vi
- Lát cắt: Trong Đặt chỗ của tôi, khi hành khách vừa nhận tin chuyến bay bị huỷ và nhắn hỏi, AI đề xuất và giữ chỗ chuyến thay thế, hỏi lại cho rõ, đổi vé, hay chuyển nhân viên, để khách tới nơi kịp mà không mất vé hay tiền vì một thao tác không đảo lại được.
- 3 việc tính năng KHÔNG làm
| Việc tính năng không làm | Lý do |
|---|---|
| 1. Không tự đổi vé khi hành khách chưa xác nhận chuyến cụ thể. | Yêu cầu như “đổi sang sáng mai” có thể khớp nhiều chuyến. Đổi sai có thể dùng mất lần đổi miễn phí, trong khi chuyến khách muốn có thể hết chỗ. AI nên hỏi rõ và cho khách xem lại thông tin trước khi xác nhận. |
| 2. Không tự gửi yêu cầu hoàn vé. | Theo track, yêu cầu hoàn đã gửi thì không hủy được. AI có thể giải thích lựa chọn và chuyển nhân viên hỗ trợ; nếu nhóm quyết định cho phép gửi thì phải quy định rõ bước duyệt, thay vì âm thầm thực hiện. |
| 3. Không tự đặt dịch vụ ngoài việc xử lý chuyến bay bị hủy, như khách sạn, taxi hay bảo hiểm. | Những dịch vụ này nằm ngoài lát cắt và bộ tool được cung cấp. Tự mở rộng có thể phát sinh chi phí hoặc cam kết mà hành khách chưa đồng ý. |
| 4. Không khẳng định chắc chắn về phí, điều kiện vé hoặc chỗ trống khi không có dữ liệu xác nhận. | Thông tin sai có thể khiến khách chọn phương án bất lợi hoặc hiểu nhầm việc đổi vé đã được bảo đảm. Khi thiếu căn cứ, AI cần nói rõ giới hạn và chuyển nhân viên nếu cần. |

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.


Bối cảnh chung: 
Bây giờ: 15:00 ngày 12/11/2026.
Mã đặt chỗ: TRV-7Q2K. Đặt qua app. Hạng Phổ thông Tiết kiệm.
Hành khách: Nguyễn Minh An (34 tuổi) · Nguyễn Gia Bình (5 tuổi).
Chuyến gốc: BM 213 Hà Nội → TP.HCM, 12/11 19:00. TRẠNG THÁI: ĐÃ HUỶ do thời tiết (bão).
Theo hãng Bay Mẫu (hãng dựng): chuyến bị huỷ thì đổi miễn phí một lần trong 48 giờ, hoặc hoàn toàn bộ. Huỷ do thời tiết thì không bồi thường tiền mặt.
Chuyến thay thế còn chỗ:
BM 217 · 12/11 21:00 · còn 1 chỗ
BM 201 · 13/11 07:00 · còn 9 chỗ
BM 205 · 13/11 09:30 · còn 4 chỗ

| tin người dùng nhắn | lớp | AI có thể sai thế nào | một sản phẩm tốt nên làm gì | nhãn
| "OK đổi vé đi, miễn tới sớm là được" | ② Mơ hồ, thiếu thông tin | AI đoán “sáng mai” là BM 201 lúc 07:00 rồi gọi doi_chuyen_bay, dù khách chưa xác nhận chuyến nào và đổi cho hành khách nào. Dù tình cờ chọn đúng ý khách, việc đổi đã dùng lần đổi miễn phí duy nhất. | AI đoán “sáng mai” là BM 201 lúc 07:00 rồi gọi doi_chuyen_bay, dù khách chưa xác nhận chuyến nào và đổi cho hành khách nào. Dù tình cờ chọn đúng ý khách, việc đổi đã dùng lần đổi miễn phí duy nhất.AI đoán “sáng mai” là BM 201 lúc 07:00 rồi gọi doi_chuyen_bay, dù khách chưa xác nhận chuyến nào và đổi cho hành khách nào. Dù tình cờ chọn đúng ý khách, việc đổi đã dùng lần đổi miễn phí duy nhất.Hỏi lại ngắn gọn: “Bạn muốn đổi cho cả hai hành khách sang chuyến 07:00 hay 09:30?” Hiển thị giờ bay, số hành khách và việc sẽ dùng một lần đổi miễn phí; chỉ thực hiện sau khi khách xác nhận rõ. | Không chấp nhận được: đổi nhầm có thể khiến khách mất lần đổi miễn phí và lỡ kế hoạch. |

## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.