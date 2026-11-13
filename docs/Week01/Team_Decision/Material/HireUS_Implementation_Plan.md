# Kế hoạch triển khai HireUS Tools

> Cập nhật 13/11/2026 theo đặc tả Week02, hồ sơ họp và xác nhận của Dũng.
> Kế hoạch ban đầu vẫn được giữ trong Proposal; các mục dưới đây tách kế hoạch khỏi kết quả.

## 1. Nguồn và phạm vi hiện tại

- [Phân tích yêu cầu Week02](../../../Week02/Submission/Requirements_Analysis.md) và [HTML](../../../Week02/Submission/Requirements_Analysis.html): hành vi, FR/BR/NFR và Use Case.
- [Hồ sơ họp](../../../Meetings/README.md): quyết định giao việc, lịch và xác nhận bổ sung.
- [Bối cảnh dự án](../../../PROJECT_CONTEXT.md): phân công epic và phần phối hợp chung hiện tại.
- [Proposal](../../Submission/Project_Proposal.md) và [HTML](../../Submission/Project_Proposal.html): bối cảnh, dự toán và kế hoạch 8 tuần ban đầu.

Khi cùng nội dung khác nhau, dùng nội dung mới nhất. Phân công theo công nghệ trong
Proposal đã được thay bằng mỗi thành viên phụ trách một epic; không dùng bảng cũ
để giới hạn người làm FE/BE cho tính năng của họ.

| Phân hệ | Phạm vi cần bám |
| --- | --- |
| CV Builder & SeekerBot | Tạo/sửa/lưu CV theo mẫu; duyệt gợi ý AI; thành tựu và GitHub; preview và xuất PDF đã được Dũng chốt 13/11. Tutorial và CV song ngữ đã cắt. |
| Voice Mock Interview | Thiết lập và kiểm tra thiết bị; hội thoại giọng nói; báo cáo, lịch sử và khôi phục khi lỗi theo FR/BR/NFR mới nhất. |
| Job Matching & Skill Gap | CV hiện có + JD; xác nhận dữ liệu bóc tách; tính điểm từ bằng chứng; hướng cải thiện và lịch sử snapshot. |
| Job Tracking | Theo dõi nguồn, thu thập và sàng lọc tin; xem/lưu/xóa cá nhân; thời hạn và thông báo. Không tự ứng tuyển hoặc tính điểm CV–JD. |

Không chép công thức/số liệu từ ảnh prototype. Điểm cần chốt còn lại nằm trong
[ghi chú Week02](../../../Week02/Submission/README.md).

## 2. Giao việc gần nhất

| Nguồn | Đầu việc | Mốc ghi trong nguồn |
| --- | --- | --- |
| Họp 01/11, bản ghi 04 | Mỗi người phân tích, vẽ diagram và prototype epic; Khoa tìm style Figma/MCP cho nhóm | Deadline chung 19:00 ngày 06/11; hẹn họp 21:00 cùng ngày |
| Họp 09/11, bản ghi 05 | Mỗi người triển khai epic theo PA02; Hoàng tạo `ui_context` và nhánh UI; Cao tạo database và chia sẻ thông tin kết nối | Deadline triển khai 23:59 ngày 15/11; hẹn họp 21:00 ngày 16/11 |
| Xác nhận 13/11 | Khoa phụ trách CV; Hoàng phụ trách VMI; Dũng phụ trách Job Matching; Cao phụ trách Job Tracking. CV có preview và xuất PDF. | Áp dụng cho công việc hiện tại |

Xem [timeline](../../../WEEKLY_TIMELINE.md) để phân biệt lịch hẹn với cuộc họp đã có
biên bản. Không suy hoàn thành prototype, UI chung, database hoặc epic từ việc đã giao.

## 3. Công nghệ và hạ tầng

| Thành phần | Căn cứ và trạng thái lựa chọn |
| --- | --- |
| Frontend / Backend / Database | Next.js / NestJS / PostgreSQL, thống nhất trong họp 12/10 |
| Persistence và tác vụ nền | Prisma ORM và Task Scheduling là lựa chọn trong Proposal |
| Âm thanh và AI | Web Audio API, FastAPI trên Kaggle, DeepSeek API và mô hình Hugging Face là phương án trong Proposal |
| Đóng gói | Docker Compose chạy cục bộ là kế hoạch trong Proposal |
| Quản lý | Scrum trên Jira; mã nguồn GitHub, repo cha kèm FE/BE/Docs |

Bảng này không xác nhận package, service hoặc database đã được cài/vận hành.
Cấu hình AI, giao thức âm thanh và schema thực tế phải đối chiếu code/contract khi triển khai.

## 4. Kế hoạch và dự toán ban đầu

[Proposal, mục 4–5](../../Submission/Project_Proposal.md) giữ bảng kế hoạch và chi phí
gốc. Không chép lại thành một lịch sprint thứ hai trong tài liệu này.

- Thời lượng dự kiến: 8 tuần, 4 sprint, 2 tuần/sprint.
- Công số dự kiến: 8 giờ/người/tuần; 64 giờ/thành viên, tổng 256 người-giờ.
- Coverage Jest từ 70% là mục tiêu kế hoạch, chưa phải kết quả kiểm thử.
- Chi phí khoảng 20.000 VNĐ là dự toán; không coi là khoản chi đã đối soát.

Các mốc tháng 11 chưa được ánh xạ thành sprint Jira trong lần rà này.
Không tự coi thứ tự thư mục Week01/Week02 là tuần lịch hoặc trạng thái hoàn thành.

## 5. Phối hợp và kiểm tra

1. Đọc đặc tả của epic, phần dùng chung và ghi chú chưa chốt; giữ phạm vi mới nhất.
2. Thống nhất dữ liệu/API giữa các phần liên quan; backend sở hữu contract, FE bám contract.
3. Dùng chuẩn UI được nhóm thống nhất; việc giao Hoàng tạo `ui_context` chưa tự xác nhận artifact đã có.
4. Kiểm tra luồng chính, quyền dữ liệu và lỗi dịch vụ; chỉ báo đã đạt khi có kết quả thực tế.
5. Cập nhật yêu cầu trong Week02, quyết định trong hồ sơ họp và các mốc trong timeline;
   đồng bộ Markdown/HTML khi thay nội dung chung.

Không đưa keys vào tài liệu. Không khôi phục tự gửi hồ sơ, tutorial, CV song ngữ
hoặc chỉ tiêu không có trong đặc tả mới. Công nghệ dự kiến và prototype không
chứng minh đã tích hợp; trạng thái nộp/duyệt phải có xác nhận riêng.
