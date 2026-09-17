# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602149
- Ngày / CVAT local: 17/09/2026 / CVAT local (localhost:8080)
- Công cụ đã dùng: Brush, Polygon, Intelligent Scissors

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 |  |
| medium_instance | medium_instance.zip | 3 / 3 |  |
| hard_panoptic | hard_panoptic.zip | 2 / 2 |  |
| cp1_holes | cp1_holes.zip | 1 / 1 |  |
| cp2_slice | cp2_slice.zip | 1 / 1 |  |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 |  |
| cp3_thin | cp3_thin.zip | 1 / 1 |  |
| cp4_curb | cp4_curb.zip | 1 / 1 |  |
| cp6_coverage | cp6_coverage.zip | 1 / 1 |  |
| **Tổng tối đa** | | | **** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; "quy tắc biên" là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg` — chiếc xe máy (motorcycle) nằm ở góc trái giữa ảnh, phần thân nằm ngang mặt đường, người lái ngồi trên.
- Class và quy tắc tôi dùng để chọn biên: Class `motorcycle`. Tôi dừng mask tại viền ngoài của khung xe nhìn thấy được; phần bánh xe chạm mặt đường thì kẻ biên theo đường tiếp xúc với mặt đường (không kéo dài xuống dưới). Phần tay lái nhô lên trên được bao gồm trong mask vì vẫn thuộc vật thể. Phần bị người lái che khuất thì giữ nguyên một mask liền mạch (không cắt xuyên qua người).
- Nếu dùng gợi ý sau đó: Sau khi vẽ thủ công bằng Polygon, tôi dùng Intelligent Scissors để tinh chỉnh viền phần bánh trước và tay lái. Gợi ý đúng ở viền bánh xe (vì cạnh màu tương phản rõ), nhưng sai ở vùng tiếp giáp giữa áo người lái và thân xe — công cụ kéo biên vào trong người. Tôi đã kéo lại điểm neo về đúng viền kim loại của xe.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi "đã sửa" khi chưa sửa.

- Task/ảnh/vùng: `cp1_holes` — ảnh `000000144300.jpg`, vùng kính chắn gió xe máy góc trái ảnh.
- Lỗi thuộc loại: biên / phủ vùng (khoét lỗ nhầm)
- Bằng chứng tôi nhìn thấy: Sau khi vẽ xong mask `motorcycle`, tôi thấy vùng kính chắn gió (windshield trong suốt) bị cắt ra khỏi mask tạo thành một "lỗ hổng" — tức là tôi đã áp dụng Subtract/Hole nhầm vào khu vực kính, trong khi quy tắc cp1_holes yêu cầu giữ kính nguyên trong mask (windows/gaps stay inside the mask).
- Quy tắc và hành động sửa: Theo quy tắc "Holes: windows/gaps stay inside the mask — do NOT cut them out", kính chắn gió là bộ phận của xe, không phải lỗ hổng thật. Tôi vào Edit mask, chọn Add mode rồi tô lại vùng kính đã bị khoét, đảm bảo mask phủ toàn bộ bao bọc xe kể cả kính.
- Sau sửa đã Save và export lại chưa? Đã Save trong CVAT và export lại file ZIP `cp1_holes.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): chưa có điểm. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `medium_instance` — ảnh `000000373353.jpg`, xe buýt (bus) góc phải, phần đuôi bị cắt bởi mép ảnh | (A) Chỉ vẽ phần nhìn thấy trong ảnh, mask kết thúc tại mép khung; (B) Đoán thêm phần xe nằm ngoài khung và kéo mask ra đến mép ảnh | Thân xe có dấu hiệu bị cắt rõ ràng (không thấy đuôi xe). Quy tắc instance segmentation thường chỉ mask phần pixel quan sát được. | Quyết định: kéo mask đến mép ảnh (mép phải) vì pixel của xe vẫn hiện diện đến đó; không đoán phần nằm ngoài khung. Xin coach xác nhận cách xử lý vật bị cắt bởi mép ảnh. |
| `cp5_occlusion` — ảnh `000000336232.jpg`, xe máy bên phải bị xe tải che khuất một phần | (A) Vẽ hai mask riêng: một cho xe tải, một cho phần xe máy nhìn thấy; (B) Xe máy bị che → gộp vào mask xe tải vì không phân biệt được | Vẫn nhìn thấy bánh sau và một phần thân xe máy lộ ra bên phải xe tải. Quy tắc cp5: "an object split by another is still ONE mask" — áp dụng cho trường hợp một xe bị chia đôi, không phải trường hợp che khuất một phần. | Quyết định: vẽ xe máy là một mask riêng bao gồm phần nhìn thấy; xe tải là mask riêng. Không gộp vì đây là hai vật thể khác nhau. |
| `hard_panoptic` — ảnh `000000460147.jpg`, vùng bó vỉa (curb) giữa `road` và `sidewalk` | (A) Gán toàn bộ phần bó vỉa vào `sidewalk` vì bề mặt nâng cao; (B) Gán vào `road` vì màu bê tông tương tự mặt đường và tiếp giáp trực tiếp | Bó vỉa có màu xám nhạt giống mặt đường nhưng độ cao rõ ràng hơn vỉa hè. Quy tắc cp4_curb ghi "road vs sidewalk is a functional boundary". | Quyết định: gán bó vỉa vào `sidewalk` vì chức năng phân cách và chiều cao nâng lên. Câu hỏi coach: nếu bó vỉa không có rãnh phân cách rõ, có nên gộp vào `road` hay không? |
