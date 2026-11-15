# HireUS Tools — tài liệu

Repo này sở hữu yêu cầu nghiệp vụ, bài nộp và quyết định dùng chung.
Đọc [.agents/rules/source-of-truth.md](.agents/rules/source-of-truth.md) trước
khi dùng hoặc sửa thông tin dự án.

Với cùng nội dung có mâu thuẫn, ưu tiên phiên bản nội dung mới nhất theo chỉ dẫn
nhóm. Đặc tả hiện tại bắt đầu từ `Week02/Submission/Requirements_Analysis.md`;
Proposal phục vụ bối cảnh/kế hoạch ban đầu trong phần chưa bị bản mới thay.

## Điều hướng và skills

Skills trong repo dùng chung cho các agent. Nếu công cụ không tự nhận `.agents/`,
đọc đúng `SKILL.md` trực tiếp. Dùng công cụ file/shell/connector tương đương đang có;
không giả định agent có tool của một hãng hoặc có thể tạo subagent.

- `docs/Week01/Submission/`: Proposal Markdown/HTML.
- `docs/Week02/Submission/`: phân tích yêu cầu, FR/BR/NFR, use case và prototype.
- `docs/PROJECT_CONTEXT.md`, `docs/WEEKLY_TIMELINE.md`: tổng hợp để điều hướng,
  cần đối chiếu nguồn và hiện trạng.
- `docs/Meetings/README.md`: mục lục biên bản, PDF gốc và các xác nhận mới của Dũng;
  dùng để tra phân công/mốc công việc, không suy chúng từ Proposal cũ.
- Đọc [.agents/README.md](.agents/README.md) và chỉ dùng skill khớp tác vụ:
  điều hướng tài liệu, soạn Proposal, biên tập, bảo trì tài liệu, tiện ích Markdown/HTML hoặc Drive.

Chỉ sửa nội dung được yêu cầu, giữ ghi chép gốc và dữ kiện đã xác nhận.
Với thay đổi nội dung tài liệu có cả Markdown/HTML, đồng bộ hai bản.
Không cập nhật tiến độ hoặc trạng thái nộp/duyệt chỉ vì đã tạo file.
Đọc local không tự sync Drive, pull Git, commit hoặc push.

## Bắt buộc comment và giải thích bằng tiếng Việt

- Với mọi tác vụ tạo mới hoặc chỉnh sửa code, **bắt buộc viết comment bằng tiếng
  Việt ngay trong file**. Áp dụng cho code ứng dụng, test, script, SQL/migration,
  cấu hình có hỗ trợ comment và ví dụ kỹ thuật trong tài liệu.
- Mỗi hàm, component, class hoặc khối logic được tạo/sửa phải có comment tiếng
  Việt đặt ngay phía trên hoặc bên trong phần xử lý liên quan. Khi sửa phần code
  cũ chưa có comment tiếng Việt, bổ sung comment cho phần đó trong cùng thay đổi.
- Comment giải thích mục đích, luồng xử lý, quy tắc nghiệp vụ, lý do lựa chọn và
  điều kiện đặc biệt để thành viên khác dễ review. Viết ngắn, rõ, đúng hành vi;
  không cần chú thích từng dòng. Khi logic đổi, sửa comment tương ứng.
- Giữ nguyên tên biến, API, kiểu dữ liệu, tên thư viện và thuật ngữ kỹ thuật khi
  cần chính xác; phần giải thích phải bằng tiếng Việt có dấu.
- Với định dạng không hỗ trợ comment như JSON, ghi giải thích tiếng Việt trong
  README hoặc tài liệu liên quan và chỉ rõ file/phần cấu hình được giải thích.
  Không chèn comment làm hỏng định dạng.
- Khi lập kế hoạch, review, viết tài liệu hoặc bàn giao, các nhận xét và giải thích
  cũng phải bằng tiếng Việt. Mô tả trong phản hồi/PR không thay thế comment trong code.
- Trước bàn giao hoặc chuẩn bị commit/push, tự rà diff để bảo đảm mọi phần code
  tạo/sửa đã có comment tiếng Việt phù hợp; bổ sung phần còn thiếu trước khi báo
  hoàn tất. Quy tắc này áp dụng cho mọi agent; không tự sửa code ngoài phạm vi tác vụ.

## Cập nhật nhánh và rà tài liệu trước công bố

Khi bắt đầu việc có sửa tài liệu chung, tự fetch và tích hợp `origin/main` vào nhánh
hiện tại một lần cho đầu việc; chỉ dẫn đích khác được ưu tiên. Main là nguồn nền,
upstream cá nhân là đích công bố riêng. Trong workspace có thể chạy từ repo này
`python3 ../.agents/scripts/sync_main.py --repo .`. Giữ việc local: tree bẩn cần tích
hợp thì báo phần chưa cập nhật, không stash/reset/ghi đè; merge conflict cần xử lý thêm.
Chỉ đọc/review/plan riêng hoặc chỉ dẫn offline/không sync thì không tự tích hợp.
Trong workspace, đọc `../.agents/skills/team-sync/SKILL.md` để phối hợp nhiều repo;
clone riêng dùng [quy trình Git trong repo](.agents/rules/pre-commit-workflow.md).

Trước bàn giao/push, dùng
[docs-maintenance](.agents/skills/docs-maintenance/SKILL.md) để tổng hợp công việc
có bằng chứng, đối chiếu tài liệu còn đúng không, sửa/gộp/bỏ bản dẫn xuất lỗi thời
và cập nhật các dẫn chiếu. Giữ bản ghi/bài nguồn lịch sử có ghi chú thay thế.
Chỉ đổi timeline khi có mốc hoặc kết quả liên quan; không tạo báo cáo cho mọi sửa nhỏ.
Rà tài liệu local không mặc định phải tải Drive. Bàn giao nêu tài liệu sửa/giữ/xóa,
lý do và phần còn thiếu, kể cả khi không cần sửa nội dung.

## Kiểm tra

Chạy từ repo tài liệu:

```bash
python3 .agents/scripts/check_docs.py
```

Chạy bộ test offline sau khi đổi công cụ sync/checker:

```bash
python3 -m unittest discover -s .agents/scripts/tests -v
```

Sync theo [.agents/skills/drive-sync/SKILL.md](.agents/skills/drive-sync/SKILL.md);
commit theo [.agents/rules/pre-commit-workflow.md](.agents/rules/pre-commit-workflow.md)
khi được yêu cầu, ngoại lệ là merge commit tích hợp main an toàn ở đầu việc.
Skills và scripts là tài nguyên nhóm, giữ trong Git;
cache sync và bản incoming vẫn được bỏ qua.

Tác vụ tài liệu không tự cho phép sửa FE/BE. Với yêu cầu phối hợp nhiều repo,
đọc hướng dẫn repo liên quan và chỉ sửa phần nằm trong phạm vi đó.
