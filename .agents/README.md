# Hướng dẫn và công cụ cho agent

Bắt đầu bằng [AGENTS.md](../AGENTS.md) và [quy tắc nguồn dữ liệu](./rules/source-of-truth.md). Skills giúp thực hiện tác vụ, không xác nhận dữ kiện của dự án. Chỉ dẫn của người dùng xác định phạm vi công việc, đọc tài liệu không tự cho phép sync hoặc commit.

## Skills

Nội dung `SKILL.md` không phụ thuộc một hãng agent. Khi công cụ không tự tìm
skills trong repo, đọc trực tiếp file cần dùng. Cách gọi skill và quyền dùng
file/shell/connector theo môi trường thực tế của thành viên.

| Skill | Dùng khi |
| :--- | :--- |
| [project-navigator](./skills/project-navigator/SKILL.md) | Tra cứu cấu trúc, nguồn và tiến độ |
| [se-proposal-writer](./skills/se-proposal-writer/SKILL.md) | Soạn/chỉnh Proposal theo nguồn đã xác nhận |
| [anti-ai-fluff](./skills/anti-ai-fluff/SKILL.md) | Biên tập văn phong, giữ nguyên dữ kiện |
| [project-utility](./skills/project-utility/SKILL.md) | Kiểm tra liên kết, tài nguyên và Markdown/HTML |
| [docs-maintenance](./skills/docs-maintenance/SKILL.md) | Đối chiếu công việc với tài liệu, cập nhật tổng hợp, sửa/gộp/bỏ bản lỗi thời |
| [drive-sync](./skills/drive-sync/SKILL.md) | Lấy tài liệu Drive khi được yêu cầu |

## Quy trình

Đọc yêu cầu → kiểm tra nhánh và nhắc cập nhật khi cần → xác định nguồn → sửa đúng
phạm vi → rà tài liệu liên quan → kiểm tra nội dung/hiển thị → tổng hợp kết quả →
commit/push theo yêu cầu. Pull/Drive sync chỉ chạy khi đã được yêu cầu cho phần đó.

- [Nguồn dữ liệu](./rules/source-of-truth.md): phân biệt nguồn chuẩn, ghi chép gốc, kế hoạch và kết quả thực tế.
- [Đồng bộ Drive](./rules/drive-sync-workflow.md): bảo vệ bản local, xử lý xung đột, dừng khi pull lỗi.
- [Commit/push](./rules/pre-commit-workflow.md): tách việc kiểm tra khỏi quyền tạo commit và đẩy GitHub.

Trong workspace, skill `team-sync` ở `../.agents/skills/` phối hợp Git của cả ba repo
và gitlink repo cha. Khi clone documents độc lập, quy trình commit/push trong repo này
vẫn dùng được. Trước push, phải nêu tài liệu sửa/giữ/xóa và căn cứ; không mặc định
tải Drive, đổi timeline hoặc sinh changelog vì mọi sửa nhỏ.

## Công cụ

- Các lệnh bên dưới chạy từ gốc repo tài liệu (`documents/` trong workspace); khi mở workspace ở gốc, thêm tiền tố `documents/` vào đường dẫn script Python.
- `./.agents/scripts/sync.sh --week Week01`: cập nhật Git fast-forward và đối chiếu Drive. Chỉ chạy khi cần đồng bộ.
- `python3 .agents/scripts/check_docs.py`: kiểm tra tài liệu trong working tree. Thêm `--staged` để kiểm tra Git index.
- `bash .agents/scripts/pre_commit_check.sh`: kiểm tra staged diff và tài liệu trước commit.
- `python3 -m unittest discover -s .agents/scripts/tests -v`: kiểm thử offline cho sync và kiểm tra tài liệu, không gọi Drive/GitHub thật.

Git hook không tự được chia sẻ khi clone; kiểm tra hook thực tế của checkout trước khi dựa vào nó. Có thể chạy script kiểm tra thủ công trước commit.

Kiểm tra tài liệu chặn link/ảnh local bị thiếu và đường dẫn tuyệt đối trong tài liệu được kiểm tra. Khi xóa tài nguyên, kiểm tra các tài liệu còn lại để phát hiện tham chiếu hỏng. Chênh lệch Markdown/HTML chỉ là cảnh báo cần đối chiếu, không phải phép xác minh toàn bộ nội dung hoặc layout. Công cụ không xác nhận tính đúng của dữ kiện.

Skills, rules và scripts là tài nguyên dùng chung, giữ trong Git và không thêm vào ignore. Cache `.sync_manifest.json` và `.sync_incoming/` vẫn được bỏ qua.
