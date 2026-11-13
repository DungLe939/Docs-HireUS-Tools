# Hồ sơ phân tích yêu cầu Week02 — Nhóm 02

> Bản làm việc 1.1 cập nhật ngày 13/11/2026; bản 1.0 ban đầu đề ngày 07/11.
> Baseline nội dung trong Git có lần cập nhật ngày 08/11/2026 (`5777fba`). Các ghi chú dưới đây mô tả bản hiện có,
> không xác nhận đã nộp hoặc được giảng viên duyệt.

## File cần dùng

- [Requirements_Analysis.md](./Requirements_Analysis.md) và
  [Requirements_Analysis.html](./Requirements_Analysis.html): nội dung báo cáo hiện tại.
- `images/`: sơ đồ và ảnh prototype; báo cáo đang tham chiếu 26 file riêng.
- `image/`: bốn ảnh chữ ký lấy từ Week01 theo yêu cầu trước đó của nhóm.

Khi chia sẻ/nộp, giữ nguyên cả hai thư mục ảnh cạnh báo cáo. `index.html` nếu có
trong checkout là bản xem local của HTML, đang được ignore; không lấy đó làm nguồn
đặc tả riêng. Bài nguồn/research không tự cần đưa vào gói nộp.

## Phạm vi và số đếm hiện tại

Đếm theo **dòng yêu cầu trong bảng**, không theo số lớn nhất của mã. FR đã được gộp
hành vi, giữ mã đại diện và các khoảng trống; không suy từ đó rằng mọi mã nguồn cũ
còn là một dòng riêng trong báo cáo.

| Phân hệ | FR | BR | NFR | Use Case |
| --- | ---: | ---: | ---: | ---: |
| CV Builder & SeekerBot | 9 | 8 | 4 | 7 |
| Voice Mock Interview | 9 | 5 | 4 | 5 |
| Job Matching & Skill Gap | 12 | 6 | 4 | 4 |
| Job Tracking | 8 | 5 | 8 | 4 |
| **Tổng** | **38** | **24** | **20** | **20** |

Con số **93 FR** trong ghi chú trước là số đếm của phiên bản trước khi gộp, không
còn mô tả bản hiện tại. Số 26 là ảnh được tham chiếu, không phải tổng mọi file còn
lưu trong thư mục `images/`; không xóa ảnh dư chỉ vì không được dùng trong báo cáo.

## Các điều chỉnh đã có trong bản tổng hợp

- Bài nguồn bốn phân hệ nằm ở [Team Decision](../Team%20Decision/README.md).
  Báo cáo mới hơn đã chuẩn hóa câu chữ, gộp yêu cầu, bỏ cột Jira và dùng mã UC có
  tiền tố phân hệ. Không dùng bản ghép nguyên văn làm bản nộp hiện tại.
- Job Tracking tích hợp từ [PR #6 của Cao](https://github.com/DungLe939/Docs-HireUS-Tools/pull/6),
  commit `c59a5c1d3c9e9a9ce08e2bb77c1a676235368a6d`: bản nguồn có 18 FR;
  bản báo cáo hiện gộp thành 8 dòng FR, giữ 5 BR, 8 NFR và 4 Use Case.
- CV Builder đã bỏ tutorial/hướng dẫn người mới và CV song ngữ khỏi phạm vi bản
  tổng hợp. Theo Dũng xác nhận ngày 13/11/2026, giữ **cả xem trước trang in và xuất PDF**.
  FR-CV-22 và UC-CV-09 gộp luồng xem trước/xuất; BR-CV-04/08 và NFR-CV-05 áp dụng
  cho dữ liệu, lỗi xuất và khả năng đọc file. SCRUM-49 là preview, SCRUM-16 là xuất PDF.
  Không khôi phục chức năng song ngữ hoặc tutorial từ các mục F04/F06 cũ.
- Sơ đồ CV trong báo cáo dùng `images/CV_Builder_Use_Case_Current.svg`, cập nhật
  nhãn UC-CV-09 cho preview + xuất PDF. PNG cũ được giữ làm tài nguyên lịch sử.
- NFR-VMI-01 hiện dùng mục tiêu phản hồi **không quá 5 giây** khi mạng ổn định.
  UC-VMI-02 hiện dẫn NFR-VMI-01, không còn giá trị 4 giây trong bản báo cáo.
  Giá trị cũ còn ở bài nguồn không thay mục tiêu hiện tại.
- Mục 3.1 dùng sơ đồ ngữ cảnh chung. Bảng thành viên, chữ ký và phát biểu bài toán
  lấy từ Week01 theo xác nhận trước đó; lần rà này không tự đánh giá lại tỷ lệ đóng góp.
- Proposal và các bài nguồn được giữ làm lịch sử; nội dung trong đó không tự bổ sung
  lại các chức năng đã cắt ở bản mới.

## Đối chiếu prototype với đặc tả

Ảnh là minh họa từ Figma, chưa được dựng lại theo mọi lần chỉnh yêu cầu.
**FR/BR/NFR và Use Case trong báo cáo là căn cứ triển khai**, ảnh không thay quy tắc.

| Vị trí có thể lệch | Đọc theo bản hiện tại |
| --- | --- |
| CV: chức năng tutorial/song ngữ còn ở bài nguồn hoặc thiết kế cũ | Phạm vi CV rút gọn trong mục 3.2, 4.2 và 5.1 |
| CV: chưa có ảnh prototype cho thao tác xuất PDF vừa xác nhận | FR-CV-22, BR-CV-08, NFR-CV-05 và UC-CV-09; cần bổ sung ảnh theo thiết kế được nhóm chọn |
| VMI: ảnh phòng phỏng vấn hiển thị số câu khác; ảnh báo cáo dùng tiêu chí/thang điểm cũ | BR-VMI-01 và BR-VMI-04/05: 5–8 câu; ba tiêu chí 50/30/20 trên thang 100 |
| Job Matching: ảnh điểm và cách thể hiện mức đáp ứng có thể chưa phản ánh đủ quy tắc | FR-JM-15 và BR-JM-04/05/06: các mức bằng chứng, trọng số và giới hạn khi thiếu yêu cầu bắt buộc |

Liên kết Figma nằm trong mục 5 của báo cáo. Chưa kiểm tra Figma Present trong lần
đồng bộ này; ảnh mẫu không chứng minh AI, API hoặc lưu dữ liệu đã hoạt động.

## Điểm nghiệp vụ còn cần chốt

- **CV Builder:** mẫu CV triển khai và ánh xạ các trường Profile cần được xác nhận
  khi triển khai. Phạm vi preview và xuất PDF đã được Dũng chốt ngày 13/11/2026;
  không đánh dấu đã triển khai chỉ vì yêu cầu đã được bổ sung.
- **UI chung:** Hoàng được giao `ui_context`/nhánh UI trong
  [họp 09/11](../../Meetings/Meeting_05.md). Lần rà tài liệu này chưa xác minh artifact
  đã hoàn thành hoặc thiết kế Figma nào được chọn làm chuẩn cuối.

Phân công và deadline hiện tại nằm tại [bối cảnh](../../PROJECT_CONTEXT.md) và
[timeline](../../WEEKLY_TIMELINE.md), không lấy phân công dự kiến trong Proposal
để thay xác nhận mới của nhóm.

## Kiểm tra khi sửa

- Đối chiếu dòng bảng, mã dẫn chiếu, ảnh và nội dung giữa Markdown/HTML.
- Nếu đổi yêu cầu, cập nhật số đếm và ghi chú phạm vi ở trang này.
- Nếu có `index.html` local, đồng bộ từ HTML; không biên tập thành một bản thứ ba.
- Chạy từ repo tài liệu: `python3 .agents/scripts/check_docs.py`.
