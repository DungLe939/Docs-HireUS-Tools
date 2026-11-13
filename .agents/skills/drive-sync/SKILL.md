---
name: drive-sync
description: Lấy và đối chiếu tài liệu Google Drive khi người dùng yêu cầu; bảo vệ chỉnh sửa local và phân biệt bản tải về với nguồn nghiệp vụ mới nhất.
---

# Đồng bộ tài liệu từ Drive

Đọc [quy trình sync](../../rules/drive-sync-workflow.md) và
[quy tắc nguồn](../../rules/source-of-truth.md).
Chỉ dùng khi được yêu cầu lấy/sync tài liệu; đọc repo local không kích hoạt sync.

Ưu tiên connector Drive đang có nếu truy cập được nguồn; không giả định tên tool,
quyền tài khoản hoặc API của một agent cụ thể.
Ghi ID/đường dẫn, revision/ngày sửa của nguồn để so sánh đúng tài liệu.
Nếu chỉ có nguồn công khai, có thể dùng script chuẩn Python từ repo tài liệu:

```bash
python3 .agents/scripts/sync_drive.py --week Week02
```

Đổi `--week`/`--folder` theo nguồn được giao, không tự coi Week02 là mặc định.
Script không bảo đảm đọc thư mục con hoặc nguồn cần đăng nhập.
`sync.sh` còn thực hiện Git pull; chỉ dùng khi yêu cầu gồm cập nhật Git.

Đối chiếu local, remote và baseline trước khi thay thế.
Bảo vệ file sửa local, bản Submission, file bị xóa/di chuyển local và file có sẵn
chưa có baseline: giữ bản khác biệt để đối chiếu, không ghi đè tự động.
“Lấy bản mới nhất làm gốc” là quy tắc chọn nội dung, không phải quyền xóa thay đổi local.
Không đổi quyền chia sẻ hoặc tự xóa file theo remote.

Báo file mới/cập nhật/không đổi/xung đột/lỗi và nguồn đã đọc.
Không báo đã đồng bộ toàn Drive nếu chỉ đọc được một tập con.
Chỉ kết luận nội dung mới hơn sau khi kiểm tra revision và phạm vi thay đổi.
Nếu tác vụ gồm cập nhật tài liệu làm việc, dùng
[docs-maintenance](../docs-maintenance/SKILL.md) để đưa thay đổi đã xác minh vào
báo cáo/tổng quan liên quan. Không coi tải xong file là đã cập nhật mọi bản tổng hợp.
