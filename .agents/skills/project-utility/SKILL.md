---
name: project-utility
description: Kiểm tra hoặc chỉnh cấu trúc tài liệu HireUS, link, ảnh, Markdown/HTML và gói bài nộp; không thay quyết định nghiệp vụ.
---

# Kiểm tra tài liệu và tài nguyên

Đọc [AGENTS.md](../../../AGENTS.md) và
[quy tắc nguồn](../../rules/source-of-truth.md).
Xác định file sở hữu nội dung trước khi sửa; dùng công cụ tương đương của agent đang chạy.
Khi cần xác định tài liệu cũ còn đúng không hoặc phải sửa/gộp/xóa,
dùng [docs-maintenance](../docs-maintenance/SKILL.md) trước phần kiểm tra cấu trúc.

- Link local tính từ file chứa link; mã hóa `#` trong tên file thành `%23`.
  Không đổi tên/di chuyển tài nguyên nếu không cần; nếu đổi, cập nhật callers.
- Đối chiếu Markdown/HTML về nội dung hiển thị, ảnh, bảng, sơ đồ và anchor.
  HTML toolbar hoặc nút xuất PDF của báo cáo không tự là chức năng sản phẩm.
- Khi rút gọn/gộp yêu cầu, kiểm tra mã còn dùng, dẫn chiếu, số lượng bảng và README.
  Giữ IDs nếu người dùng không yêu cầu đánh lại; không dùng số đếm cũ làm bằng chứng.
- Prototype có thể chứa chức năng đã bị cắt; chọn đặc tả mới nhất cho hành vi,
  giữ ảnh nguồn nếu tác vụ không yêu cầu sửa/xóa ảnh.
- Khi sửa bố cục, mở/render phần hiển thị để kiểm tra; so sánh từ ngữ tự động
  không chứng minh layout đúng.

Chạy từ repo tài liệu: `python3 .agents/scripts/check_docs.py`.
Dùng `--staged` khi kiểm tra index cho commit đã được yêu cầu.
Checker chỉ xác minh link/tài nguyên và cảnh báo chênh lệch lớn, không xác nhận
tính đúng nghiệp vụ, trạng thái nộp hoặc mọi anchor.

Đóng gói phải giữ các thư mục ảnh/tài nguyên được tham chiếu; tên gói và cách nộp
theo thông báo thực tế. Báo file đã kiểm tra, lỗi còn lại và phần chưa render.
