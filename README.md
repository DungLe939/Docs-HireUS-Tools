# HireUS Tools — Tài liệu đồ án

Đồ án môn Nhập môn Công nghệ Phần mềm, Nhóm 02, Trường Đại học Khoa học Tự nhiên, ĐHQG-HCM.

## Đọc từ đâu

| Cần biết | Tài liệu |
| --- | --- |
| Tổng quan, công nghệ và phân công hiện tại | [Bối cảnh dự án](./docs/PROJECT_CONTEXT.md) |
| Hành vi và tiêu chí của bốn phân hệ | [Phân tích yêu cầu Week02](./docs/Week02/Submission/Requirements_Analysis.md), [HTML](./docs/Week02/Submission/Requirements_Analysis.html) và [ghi chú phạm vi](./docs/Week02/Submission/README.md) |
| Quyết định họp và PDF gốc | [Hồ sơ họp](./docs/Meetings/README.md) |
| Mốc công việc và trạng thái có nguồn | [Timeline](./docs/WEEKLY_TIMELINE.md) |
| Ý tưởng, dự toán và kế hoạch ban đầu | [Proposal](./docs/Week01/Submission/Project_Proposal.md), [HTML](./docs/Week01/Submission/Project_Proposal.html) và [hướng dẫn đóng gói](./docs/Week01/Submission/README.md) |
| Kế hoạch đã đối chiếu các quyết định mới | [Kế hoạch triển khai](./docs/Week01/Team_Decision/Material/HireUS_Implementation_Plan.md), [HTML](./docs/Week01/Team_Decision/Material/HireUS_Implementation_Plan.html) |
| Công cụ và hướng dẫn AI dùng chung | [AGENTS.md](./AGENTS.md) và [.agents](./.agents/README.md) |

HireUS Tools gồm CV Builder & SeekerBot, Voice Mock Interview, Job Matching & Skill Gap,
Job Tracking. Theo xác nhận ngày 13/11/2026, Khoa, Hoàng, Dũng và Cao lần lượt phụ trách
bốn epic này. Chi tiết và phần phối hợp chung được giữ tại trang bối cảnh.

## Nguồn và cách cập nhật

Khi cùng nội dung mâu thuẫn, dùng phiên bản nội dung mới nhất theo
[quy tắc nguồn](./.agents/rules/source-of-truth.md), không theo ngày copy file.
Week02 sở hữu yêu cầu hiện tại; Proposal giữ bối cảnh và kế hoạch ban đầu;
biên bản ghi quyết định và giao việc. Kế hoạch hoặc ảnh prototype không xác nhận code đã chạy.

- `docs/Week01/`: thông báo/template, bài mẫu, Proposal và các bản ghi đầu dự án.
- `docs/Week02/Submission/`: báo cáo đã chuẩn hóa; `Team Decision/` giữ bài nguồn thành viên.
- `docs/Meetings/`: mục lục họp, biên bản bổ sung và PDF gốc; hai biên bản đầu vẫn ở Week01.
- `.agents/`: skills và script dùng chung, được giữ trong Git.

Sửa nội dung báo cáo phải đồng bộ Markdown/HTML và giữ tài nguyên được tham chiếu.
Không sửa bài nguồn lịch sử cho giống bản mới hoặc ghi khóa kết nối vào tài liệu.
Không tự sync Git/Drive, commit/push hay cập nhật trạng thái nộp/duyệt chỉ vì sửa tài liệu.

Kiểm tra từ repo tài liệu: `python3 .agents/scripts/check_docs.py`.
