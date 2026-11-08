# Hồ sơ phân tích yêu cầu Week02 — Nhóm 02

## Bản nộp Markdown

- [Requirements_Analysis.md](./Requirements_Analysis.md): báo cáo tổng hợp theo template Week02.
- `images/`: sơ đồ và hình prototype được báo cáo tham chiếu.
- `image/`: bốn ảnh chữ ký được sao chép nguyên bản từ hồ sơ Week01 theo yêu cầu người dùng.

Khi nộp hoặc sao chép, giữ nguyên hai thư mục ảnh cạnh file Markdown. Không cần nộp các bản research riêng.

## Cách tổng hợp

- Job Tracking đã tích hợp nội dung và 8 ảnh từ [PR #6 của Cao](https://github.com/DungLe939/Docs-HireUS-Tools/pull/6), commit `c59a5c1d3c9e9a9ce08e2bb77c1a676235368a6d`: 18 FR, 5 BR, 8 NFR và 4 Use Case. Chỉ bỏ cột Jira, điều chỉnh cấp tiêu đề và thêm liên kết nội bộ theo định dạng báo cáo; giữ mục 3.1 toàn hệ thống và phần prototype chung. Không merge PR hoặc sửa bài nguồn.
- Theo yêu cầu giảm khối lượng triển khai: bỏ FR-CV-11, 12, 18–21, BR-CV-07, UC-CV-05, UC-CV-08 và các phần prototype F04, F06; giữ chức năng xem trước trang in. Mã còn lại không đánh lại. Sơ đồ CV Builder dùng SVG mới; file nguồn và thiết kế Figma được giữ nguyên.
- Mục 4.2 hiện có 20 Use Case và các trường theo mẫu; rút các luồng xử lý, gộp ghi chú vào bảng, bỏ dòng truy vết Jira riêng của Job Tracking và cập nhật dẫn chiếu NFR sau khi gộp.
- Mục 3.2.2 hiện có 20 NFR: CV giữ bản rút gọn; Job Tracking dùng đủ 8 NFR của PR #6, gồm NFR-JT-06 và NFR-JT-08. Các liên kết từ Use Case đã được cập nhật tương ứng.
- Mục 3.1 dùng sơ đồ ngữ cảnh chung toàn hệ thống (ảnh PNG) cùng bảng stakeholder đã được người dùng duyệt, thay cho các sơ đồ riêng từng phân hệ.
- Bảng thành viên (gồm tỷ lệ đóng góp và chữ ký) và phần phát biểu bài toán được lấy nguyên nội dung Week01 theo xác nhận của người dùng trong phiên này.
- Nội dung yêu cầu, quy tắc nghiệp vụ và bảng Use Case được tổng hợp từ bốn bài trong `../Team Decision/`. Mục 3.2.1 đã rút gọn câu chữ và gom giải thích mã trùng lặp theo yêu cầu người dùng; giữ các hành vi, điều kiện, quy tắc, mã FR/NFR/BR. ID Use Case đã được chuẩn hóa theo tiền tố phân hệ. Cột Story/Jira đã được bỏ khỏi bảng yêu cầu chức năng theo yêu cầu người dùng.
- Mã Use Case trong mục 4.2 dùng dạng `UC-CV-01`, `UC-VMI-01`, `UC-JM-01`, `UC-JT-01` để không trùng giữa các phân hệ. Mã và dẫn chiếu trong phần văn bản đã được cập nhật; sơ đồ CV Builder đã được cập nhật theo phạm vi rút gọn; sơ đồ Job Tracking dùng bản 4 Use Case từ PR #6; các sơ đồ khác giữ nguyên.
- Phần prototype CV Builder đã bỏ hướng dẫn người mới và CV song ngữ; ảnh F06 gộp song ngữ và trang in không còn được đưa vào bản nộp. Sáu ảnh Job Tracking được lấy từ PR #6 của Cao. Ảnh Job Matching và Voice Mock Interview đã được xuất từ Figma; không tạo màn hình mới.
- Các file bài làm riêng và bản Proposal gốc không bị sửa.

## Điểm cần nhóm xác nhận trước khi nộp

1. Voice Mock Interview: NFR-VMI-01 ghi độ trễ không quá **5 giây**, nhưng ràng buộc trong Use Case tham gia phỏng vấn ghi **4 giây**. Báo cáo giữ nguyên cả hai giá trị từ bài nguồn, chưa tự quyết định thay nhóm.
2. Voice Mock Interview: bảng FR hiện chuyển từ FR-VMI-23 sang FR-VMI-27, 28. Giữ mã nguồn, không tự thêm yêu cầu hoặc đánh số lại.
3. CV Builder: SCRUM-16 (in/xuất PDF) vẫn là phạm vi cần nhóm xác nhận theo bài nguồn.
4. Thử các liên kết và thao tác trên Figma Present. Ảnh và dữ liệu mẫu không chứng minh ứng dụng, AI hoặc lưu dữ liệu thật đã triển khai.

## Kiểm tra tự động đã thực hiện

- Bảng thành viên và phần phát biểu bài toán khớp nội dung Week01.
- Hiện có 93 FR và 20 NFR sau khi tích hợp bản Job Tracking mới; mã yêu cầu, quy tắc nghiệp vụ và công thức điểm được đối chiếu sau khi rút gọn.
- Các file nguồn và Proposal giữ nguyên nội dung.
- Các đường dẫn ảnh và chữ ký đều trỏ đến file tồn tại.

| Nội dung | Số lượng |
| --- | ---: |
| FR | 93 |
| NFR | 20 |
| UseCase | 20 |
| images | 26 |

Báo cáo này được chuẩn bị để nhóm xem và nộp; việc tạo file không xác nhận đã nộp hoặc được giảng viên duyệt.

## Ghi chú biên tập

Ghi chú làm việc cuối bài CV Builder dưới đây được chuyển ra khỏi bản nộp để tránh câu “chưa khai % đóng góp” mâu thuẫn với bảng thành viên đã được người dùng yêu cầu lấy từ Week01. Nội dung nghiệp vụ và các file nguồn được giữ nguyên.

*Cần nhóm chốt SCRUM-16, mẫu CV và ánh xạ Profile; thử Present. Bảng đánh giá thành viên thuộc báo cáo chung, chưa khai % đóng góp.*
