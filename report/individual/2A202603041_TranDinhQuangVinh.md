# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202603041
- Ngày / CVAT local: 11/11/2026 / CVAT local
- Công cụ đã dùng: Polygon, Brush, CVAT AI Tools

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | **14 / 14** | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh số 1 trong `medium_instance`, chiếc xe ô tô (car) đỗ phía bên phải làn đường.
- Class và quy tắc tôi dùng để chọn biên: Dùng class `car`. Quy tắc chọn biên: bám sát viền ngoài nhìn thấy của thân xe và bánh xe chạm mặt đường. Không vẽ lan sang bóng đổ dưới gầm xe hoặc vỉa hè phía sau.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Vùng gợi ý ban đầu hay bị lem vào bóng râm của gầm xe và mép vỉa hè; tôi đã dùng công cụ chỉnh sửa node polygon để co sát lại theo đúng đường viền cơ khí của xe.
- Nếu không dùng gợi ý: ghi “không dùng”; vẫn giải thích một quyết định gán nhãn của mình.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task `cp2_slice`, ảnh có hai xe ô tô đỗ liền kề sát cạnh nhau.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Lỗi gộp-tách (gộp 2 instance thành 1).
- Bằng chứng tôi nhìn thấy: Mask ban đầu bao phủ liền mạch cả hai chiếc xe tạo thành một object ID duy nhất, vi phạm nguyên tắc instance segmentation.
- Quy tắc và hành động sửa: Quy tắc: Cùng class không có nghĩa là cùng một instance. Hành động sửa: Cắt đôi mask tại khe hở ranh giới giữa hai thân xe và tạo thành hai object riêng biệt với hai nhãn instance độc lập.
- Sau sửa đã Save và export lại chưa? Đã Save và xuất lại file `cp2_slice.zip` hợp lệ theo chuẩn COCO 1.0.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Đã chạy `scripts/inspect_submissions.py` xác nhận 13 annotations phân tách hợp lệ. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `cp4_curb` - ranh giới giữa lòng đường và vỉa hè phía bên phải, gần gốc cây. | Tôi cân nhắc giữa việc gộp vùng sát lề vào road vì bề mặt có màu xám gần giống mặt đường, hoặc tách thành sidewalk vì đây là phần lối đi dành cho người đi bộ. Vùng gần gốc cây và mép bó vỉa khiến ranh giới khó xác định nếu chỉ dựa vào màu sắc.| Theo quy tắc của task, ranh road–sidewalk cần được xác định bằng chức năng sử dụng và dấu hiệu bó vỉa, không chỉ bằng màu vật liệu. Tôi đối chiếu đường mép lề, sự thay đổi độ cao và phần mặt bê tông nối với lối đi phía trong. Các vùng đất quanh gốc cây, rác hoặc vật nằm trên vỉa hè không tự động trở thành sidewalk. | Tôi quyết định gán phần mặt đường dành cho xe chạy là road, phần lối đi phía trong bó vỉa là sidewalk. Khi chọn biên, tôi bám theo mép phân chia nhìn thấy, tránh tô road lan vào vỉa hè hoặc tô sidewalk ra lòng đường. Với đoạn ranh bị vật khác che, tôi chỉ gán phần nhìn thấy và không tự nối biên xuyên qua vật che.|
| 2. `cp5_occlusion` - xe ở phía sau bị phương tiện phía trước, đặc biệt xe taxi màu vàng ở tiền cảnh bên phải, che một phần. | Tôi cân nhắc giữa việc xem các phần thân xe còn nhìn thấy là những object độc lập, hoặc giữ chúng thuộc cùng một instance vì chúng là các phần của một chiếc xe bị che khuất. Một cách làm khác cần tránh là tô nối qua vùng bị che để tạo thành hình chiếc xe hoàn chỉnh. | Quy tắc instance xác định đối tượng theo vật thể thực tế, không theo số mảng pixel nhìn thấy. Có thể đối chiếu vị trí, màu thân xe, hướng xe và sự liên tục của các chi tiết để nhận biết các phần thuộc cùng một xe. Tuy nhiên, không được suy đoán rồi gộp hai xe khác nhau chỉ vì chúng cùng class hoặc có màu gần giống.| Tôi quyết định giữ một instance cho cùng một chiếc xe, chỉ gán những phần còn nhìn thấy. Nếu mask có các mảng rời do bị che, các mảng đó vẫn thuộc cùng đối tượng; tôi không tô xuyên lên xe taxi hoặc phương tiện đang che phía trước. Trường hợp không đủ dấu hiệu để xác định hai mảng có thuộc cùng một xe hay không, tôi cần ghi rõ vị trí để hỏi coach trước khi gộp.|
| 3. `cp1_holes` - vùng kính cửa sổ của xe lớn bên trái, phía sau xe máy Honda. | Tôi cân nhắc giữa việc khoét vùng cửa kính khỏi mask vì kính có màu khác thân xe hoặc có thể phản chiếu cảnh vật, và việc giữ vùng kính trong mask vì kính là bộ phận của chính chiếc xe. Sự khác biệt về màu sắc dễ khiến vùng kính bị hiểu nhầm thành một khoảng nền xuyên qua vật thể. | Quy tắc riêng của cp1_holes yêu cầu giữ kính và các chi tiết bên trong mask của vật, không tự khoét lỗ. Màu kính, phản chiếu hoặc rèm phía sau kính không đủ để kết luận đó là background. Tôi cần phân biệt chi tiết nằm trong đường bao của xe với vùng nền thật sự nằm ngoài thân xe. | Tôi quyết định giữ phần kính nhìn thấy trong cùng mask với chiếc xe, bám theo đường bao ngoài nhìn thấy của xe và không tạo lỗ chỉ vì kính khác màu. Đồng thời, tôi không tô lấn ra nền ngoài thân xe hoặc tô lên xe máy đang che phía trước. Cách này giữ được vùng kính theo quy tắc task mà vẫn tôn trọng ranh giới che khuất giữa các vật.|

