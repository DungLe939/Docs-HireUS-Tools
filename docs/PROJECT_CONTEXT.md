# Bối cảnh dự án HireUS Tools

> Cập nhật 13/11/2026 từ đặc tả Week02, biên bản họp và xác nhận của Dũng.

## Nguồn đang dùng

| Nội dung | Nguồn |
| --- | --- |
| Hành vi, FR/BR/NFR, Use Case | [Requirements Analysis Week02](./Week02/Submission/Requirements_Analysis.md) và [HTML](./Week02/Submission/Requirements_Analysis.html) |
| Quyết định họp, phân công và mốc công việc | [Hồ sơ họp](./Meetings/README.md), gồm PDF gốc và xác nhận bổ sung |
| Bối cảnh, dự toán và kế hoạch ban đầu | [Proposal](./Week01/Submission/Project_Proposal.md) và [HTML](./Week01/Submission/Project_Proposal.html) |
| Theo dõi các mốc có nguồn | [Timeline](./WEEKLY_TIMELINE.md) |

Khi cùng nội dung mâu thuẫn, lấy phiên bản nội dung mới nhất theo
[quy tắc nguồn](../.agents/rules/source-of-truth.md). Proposal và bài nguồn thành viên
không thay thế các điều chỉnh mới hơn trong Week02. Biên bản xác nhận việc giao việc,
không chứng minh công việc đã hoàn thành.

## Môn học và thành viên

- Môn: Nhập môn Công nghệ Phần mềm, Trường Đại học Khoa học Tự nhiên, ĐHQG-HCM.
- GVTH: Thầy Ngô Ngọc Đăng Khoa. GVLT: Thầy Phạm Minh Tuấn.
- Nhóm 02; trưởng nhóm: Lê Tấn Dũng.
- Scrum trên Jira; mã nguồn tổ chức thành repo cha và ba repo con Frontend, Backend, Docs
  theo [biên bản 12/10](./Week01/Team_Decision/Meeting_01.md).

## Phạm vi và người phụ trách hiện tại

Phân công dưới đây được Dũng xác nhận ngày 13/11/2026, thay phân công dự kiến trong
Proposal cho công việc hiện tại. Mỗi thành viên triển khai epic của mình qua các lớp
FE/BE cần thiết; vai trò công nghệ trong Proposal không giới hạn thành viên vào một lớp.

| Thành viên | MSSV | Epic phụ trách | Phối hợp chung |
| --- | --- | --- | --- |
| Võ Minh Khoa | 24120194 | CV Builder & SeekerBot | Tìm hiểu style prototype Figma và MCP theo họp 01/11 |
| Võ Nguyễn Việt Hoàng | 24120249 | Voice Mock Interview | Tạo `ui_context` và nhánh UI theo họp 09/11 |
| Đỗ Chí Cao | 24120270 | Job Tracking | Tạo database và chia sẻ thông tin kết nối theo họp 09/11 |
| Lê Tấn Dũng | 24120290 | Job Matching & Skill Gap | Trưởng nhóm; rà phạm vi và duyệt các đầu việc đề xuất |

Chi tiết nghiệp vụ và các điểm cần chốt xem [ghi chú Week02](./Week02/Submission/README.md).
CV có cả xem trước trang in và xuất PDF theo xác nhận của Dũng ngày 13/11/2026.
Ảnh prototype có thể khác đặc tả mới nhất; không lấy số câu hỏi, công thức điểm hoặc
chức năng trong ảnh để thay FR/BR/NFR.

## Công nghệ và tình trạng

Next.js, NestJS và PostgreSQL được thống nhất trong họp 12/10. Prisma, dịch vụ AI
FastAPI trên Kaggle, DeepSeek, mô hình âm thanh Hugging Face và Docker Compose là
các lựa chọn trong Proposal; tài liệu này không xác nhận chúng đã được tích hợp.

Kế hoạch ban đầu là 8 tuần, 4 sprint, 8 giờ/người/tuần, tổng 256 người-giờ.
[Kế hoạch triển khai](./Week01/Team_Decision/Material/HireUS_Implementation_Plan.md)
tách các giả định này khỏi công việc được giao trong tháng 11.

Họp 09/11 giao triển khai từng epic đến **23:59 ngày 15/11/2026**, họp tiếp lúc
**21:00 ngày 16/11/2026**. Đây là mốc giao việc, chưa phải trạng thái hoàn thành.
Chưa xác nhận đã nộp bài, được giảng viên duyệt, database hoạt động hay tiến độ Jira.

## Quy ước duy trì

- Nội dung thay đổi trong báo cáo phải được cập nhật ở cả Markdown và HTML.
- Bài nguồn và PDF gốc được giữ để truy vết; không sửa lịch sử cho giống đặc tả mới.
- Cập nhật quyết định trong hồ sơ họp, yêu cầu trong Week02; các trang tổng quan dẫn
  về đó thay vì tạo thêm bản đặc tả.
- Không lưu khóa kết nối thực tế vào tài liệu hoặc suy trạng thái đã làm từ kế hoạch.
