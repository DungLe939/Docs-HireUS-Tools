# Cập nhật nhánh, đối chiếu tài liệu và công bố

Áp dụng [quy tắc nguồn](./source-of-truth.md). Các lệnh ở đây chạy từ repo tài liệu;
trong workspace, skill `team-sync` tại `../.agents/skills/team-sync/SKILL.md`
phối hợp repo con và gitlink cha. Clone riêng vẫn dùng được quy trình dưới đây.

## Khi bắt đầu việc có sửa

Xem nhánh/upstream, staged/unstaged/untracked và ghi HEAD làm mốc đầu việc.
Tự fetch và tích hợp `origin/main` trước việc sửa tài liệu chung theo quyền thường
trực của nhóm; chỉ dẫn đích khác được ưu tiên. Thực hiện một lần cho đầu việc.
Đọc/review local không tự cho phép pull hoặc lấy Drive.

Trong workspace dùng `python3 ../.agents/scripts/sync_main.py --repo .` từ repo này.
Clone độc lập: fetch main và xem ahead/behind/diff; giữ nhánh. Nếu đích đã nằm trong
HEAD thì tiếp tục; tree sạch thì fast-forward hoặc merge bảo toàn lịch sử với
`--no-autostash --no-overwrite-ignore`. Merge commit tích hợp được phép tự tạo, không
gồm feature commit hoặc push. Nếu conflict, abort lượt merge vừa bắt đầu từ tree
sạch và báo điểm cần xử lý; không abort thao tác Git dở có sẵn.
Working tree bẩn cần tích hợp thì giữ file/index, không stash/reset hay stage phần
ngoài phạm vi. Detached HEAD/thao tác Git dở/mạng lỗi cần báo, không gọi cache là mới nhất.
Plan riêng và chỉ dẫn offline/không sync không kích hoạt cập nhật tự động.

## Rà tài liệu và tổng hợp công việc

Dùng [docs-maintenance](../skills/docs-maintenance/SKILL.md) cho cả commit chưa push,
diff và file mới liên quan. Tìm tài liệu bị tác động theo epic, mã yêu cầu, API,
lệnh chạy và callers; đừng chỉ xem commit cuối.

- Sửa hướng dẫn/tổng hợp sai; gộp/bỏ bản dẫn xuất trùng hoặc đã được thay thế có căn cứ,
  cập nhật dẫn chiếu/ảnh còn dùng. Giữ nguồn lịch sử có ghi chú về bản hiện hành.
- Đồng bộ nội dung Markdown/HTML, mã và số đếm; mở/render khi đổi bố cục.
- Chỉ đổi timeline khi có tiến độ thực tế hoặc điều chỉnh kế hoạch liên quan.
  Đổi cách dùng skills/scripts thì sửa hướng dẫn tương ứng.
- Tổng hợp đã làm gì, bằng chứng/kiểm tra, tài liệu sửa/giữ/xóa và lý do, phần còn thiếu.
  Không cần sửa tài liệu thì ghi đã đối chiếu những gì. Mặc định tổng hợp trong
  phản hồi/PR description; không tạo báo cáo/changelog riêng cho mọi lần push.
- Rà tài liệu không mặc định tải Drive. Chỉ dùng
  [drive-sync](../skills/drive-sync/SKILL.md) nếu yêu cầu gồm nguồn ngoài đó.

## Khi được yêu cầu commit hoặc push

Yêu cầu commit cho phép stage/commit phần việc liên quan. Yêu cầu push bao gồm
commit cần thiết và cập nhật tài liệu liên quan cho phần việc đang trao đổi, trừ
khi người dùng giới hạn chỉ push commit có sẵn hoặc một repo cụ thể.
Quyền cho một lần công bố không tự áp dụng cho đầu việc mới.

1. Xác minh repo, nhánh, remote và ref đích; giữ nhánh thành viên.
   Kiểm tra cả thay đổi có sẵn, không tự đưa tất cả vào commit.
2. Chạy kiểm tra phù hợp; stage đúng file/hunk, đọc staged diff, chạy
   `git diff --cached --check` và `bash .agents/scripts/pre_commit_check.sh`.
   Cảnh báo không chứng minh nội dung đúng; đối chiếu thủ công phần liên quan.
3. Dùng Conventional Commits mô tả kết quả cụ thể. Không bỏ qua hook hoặc công bố
   khi kiểm tra bắt buộc còn lỗi; báo giới hạn nếu công cụ không chạy được.
4. Trước push, fetch/xác minh remote lại nếu có thể đã thay đổi trong lúc làm.
   Nếu remote đi trước hoặc non-fast-forward, xem diff hai phía và tích hợp cùng
   upstream đã xác minh. Yêu cầu cập nhật/push cho phép merge thông thường bảo toàn
   lịch sử; không tự rebase nhánh đã chia sẻ, force-push hoặc đổi đích.
5. Giải quyết conflict có căn cứ; chọn nội dung mới nhất của phần liên quan,
   không lấy hàng loạt `ours/theirs` hay dùng timestamp commit để bỏ quyết định local.
   Hỏi chỉ phần nghiệp vụ/quyền/dữ liệu chưa rõ, tiếp tục phần độc lập.
6. Sau tích hợp, rà lại tài liệu và chạy lại kiểm tra phần bị tác động rồi push đúng ref.
   Nếu remote tiếp tục đi trước, chỉ thêm một vòng fetch/tích hợp/push; sau đó
   dừng retry và báo tình trạng, giữ nguyên phần đã làm.
7. Xác minh phản hồi Git và commit/ref đích. Báo nhánh, commit, kết quả và phần chưa
   công bố; không báo đã push chỉ vì đã commit.

## Nhiều repo

Khi yêu cầu công bố workspace, commit/push các repo con liên quan trước rồi mới
cập nhật gitlink và push repo cha. Không đưa gitlink ngoài phạm vi vào commit.
Nếu một repo chưa push thành công, báo phần đã công bố và phần còn chờ; không push
repo cha trỏ tới commit con chưa công bố, không tự rollback lịch sử đã push.

Không gửi keys/cache/incoming vào Git và không tự đăng Jira/Drive hay cài hook
global từ yêu cầu push. Kết thúc chỉnh sửa tài liệu không tự cấp quyền commit công
việc/push; quyền tạo merge commit tích hợp main ở đầu việc đã được nêu riêng ở trên.
