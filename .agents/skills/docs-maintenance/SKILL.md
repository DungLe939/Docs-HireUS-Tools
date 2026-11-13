---
name: docs-maintenance
description: Rà tài liệu HireUS theo thay đổi thực tế trước bàn giao hoặc push; cập nhật tổng hợp, sửa nội dung lỗi thời, gộp hoặc xóa bản dẫn xuất đã được thay thế.
---

# Giữ tài liệu khớp công việc

Đọc [AGENTS.md](../../../AGENTS.md) và [quy tắc nguồn](../../rules/source-of-truth.md).
Dùng khi code/contract/quyết định đổi hoặc được yêu cầu dọn tài liệu; khác với
`drive-sync` là lấy dữ liệu từ Drive. Không cần tải nguồn ngoài cho mọi lần rà local.

## Đọc bằng chứng và tìm tài liệu bị tác động

Đọc yêu cầu, diff/commit chưa công bố, file mới và kết quả kiểm tra liên quan;
xác định thay đổi có sẵn ngoài phạm vi. Nếu thiếu checkout code hoặc nguồn quyết định,
ghi phần chưa kiểm chứng và hỏi dữ kiện cần thiết, không dựng tiến độ.

Tìm theo tên epic, mã FR/UC, API, tên file, lệnh chạy và link/ảnh của phần thay đổi.
Rà các nơi liên quan: README/cài đặt, config mẫu, contract và consumer, spec/tasks,
Week02, bối cảnh, timeline, mục lục và hướng dẫn agent. Không viết lại toàn repo vì
một sửa nhỏ; không mặc định mọi file cũ đều sai.

## Quyết định theo nội dung

| Tình trạng | Xử lý |
| --- | --- |
| Vẫn đúng và cần dùng | Giữ; nêu đã đối chiếu khi bàn giao |
| Hướng dẫn/tổng hợp sai so với bằng chứng hoặc quyết định mới | Sửa tại nơi sở hữu; cập nhật các bản hiển thị và callers liên quan |
| Tài liệu dẫn xuất trùng, sai hoặc đã có bản thay thế rõ | Gộp hoặc xóa trong phạm vi dọn/sync được giao; giữ một nguồn hiện hành và cập nhật mọi dẫn chiếu |
| Proposal, bài nguồn, biên bản/PDF hoặc bản nộp lịch sử | Giữ bằng chứng gốc, ghi rõ phạm vi lịch sử/bản thay thế ở mục lục; không sửa quyết định cũ thành lời nói của hiện tại |
| Yêu cầu còn hiệu lực nhưng code chưa đáp ứng | Ghi thiếu sót, sửa code nếu được giao; không đổi đặc tả để hợp thức hóa code |
| Không có nguồn hoặc chưa rõ bản nào mới | Nêu điểm cần xác nhận; tiếp tục phần độc lập, chưa xóa thông tin duy nhất |

Theo quy ước nhóm, tác vụ rà/sync tài liệu trước bàn giao/push bao gồm sửa/bỏ bản
dẫn xuất lỗi thời, không cần hỏi lại cho từng sửa cơ học có căn cứ.
Trước xóa, đọc nội dung và tìm callers kể cả từ
repo khác trong workspace, kiểm tra bản thay thế giữ đủ thông tin cần dùng.
File tracked được khôi phục qua Git; với bản độc nhất chưa tracked, giữ bản đối chiếu
ngoài working tree trước khi loại bỏ. Không xóa dữ liệu gốc hoặc nguồn ngoài chỉ vì
không còn nằm trong phạm vi sản phẩm; hỏi nếu giá trị lưu giữ/phạm vi xóa chưa rõ.

## Cập nhật và tổng hợp

- Ghi nguồn/revision cho thay đổi quyết định. Mới nhất theo **nội dung liên quan**,
  không theo mtime hoặc việc file vừa được pull.
- Đồng bộ Markdown/HTML, số đếm, mã, liên kết và tài nguyên. Ảnh cũ chưa cập nhật
  phải được ghi nhận; không gọi prototype là chức năng đã chạy.
- Sửa README/cách chạy/contract khi hành vi kỹ thuật thay đổi. Cập nhật spec/tasks
  hiện có theo phần đã hoàn thành, không đánh dấu cả epic xong từ một commit.
- Chỉ đổi bối cảnh/timeline khi có thay đổi phạm vi, phân công, mốc hoặc kết quả có
  bằng chứng; sửa chính tả không bắt buộc ghi tiến độ hay sinh changelog riêng.
- Tóm tắt **đã làm, đã kiểm tra, còn thiếu**, kèm file/commit; liệt kê tài liệu
  sửa/giữ/xóa và lý do. Mặc định trả trong phản hồi hoặc PR description, dùng lại
  artifact sẵn có khi cần; không tự đăng Jira, Drive hoặc tạo biên bản họp.

Chạy `python3 .agents/scripts/check_docs.py` từ repo tài liệu; kiểm tra callers khi
xóa ảnh/file và render khi đổi bố cục. Dùng [project-utility](../project-utility/SKILL.md)
cho phần định dạng/đóng gói. Trước commit/push theo
[quy trình công bố](../../rules/pre-commit-workflow.md), không coi cập nhật tài liệu là quyền push.
