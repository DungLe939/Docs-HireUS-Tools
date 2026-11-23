# Nguồn thu thập câu hỏi phỏng vấn VMI

Bàn giao cho nhóm data · 23/11/2026

**Đầu ra mong muốn:** khoảng **1.000 câu hỏi chữ khác ý** cho ứng viên IT Intern và Fresher. Có thể lấy câu hỏi từ ngân hàng chữ hoặc bài kể lại buổi phỏng vấn. Đáp án mẫu là tùy chọn. Chỉ tiêu bên dưới là đề xuất sau lọc, chưa phải số câu đã thu thập.

## Chỉ tiêu sau lọc trùng

| Nhóm | Số câu | Phạm vi | Nguồn bắt đầu |
| --- | ---: | --- | --- |
| Frontend | 220 | HTML, CSS, JavaScript, TypeScript, React, trình duyệt và accessibility | [h5bp](https://github.com/h5bp/Front-end-Developer-Interview-Questions), [Duyet](https://github.com/duyet/vietnamese-frontend-interview-questions), [Learning Hub](https://github.com/TheLearningHubOrg/learn-interview-questions#-master-navigation--tracks) |
| Backend | 240 | HTTP, REST, Node.js, Java/Spring cơ bản, SQL, transaction, index và cache | [AS Backend Institute](https://github.com/AS-Backend-Institute/backend-interview-questions), [Backend Interview Questions](https://github.com/alitalhacoban/backend-interview-questions-2026) |
| Fullstack | 160 | Luồng từ UI đến API và database, phân trang, đăng nhập, xử lý lỗi, kiểm thử tích hợp và triển khai cơ bản | [Learning Hub — danh mục track](https://github.com/TheLearningHubOrg/learn-interview-questions), [h5bp — trình duyệt và mạng](https://github.com/h5bp/Front-end-Developer-Interview-Questions) |
| Mobile | 120 | Khoảng 70 Android/Kotlin và 50 iOS/Swift, ưu tiên vòng đời, bất đồng bộ, dữ liệu cục bộ và gọi API | [Android Interview Questions](https://github.com/amitshekhariitbhu/android-interview-questions), [iOS & Swift Interview Questions](https://github.com/raitechlabs/ios-interview-questions) |
| AI/Data | 150 | Python, xử lý dữ liệu, thống kê, ML cơ bản và đánh giá mô hình. Chọn thêm một số câu LLM ở mức nhập môn | [Data Science Interviews](https://github.com/alexeygrigorev/data-science-interviews), [Learning Hub — AI Engineering](https://github.com/TheLearningHubOrg/learn-interview-questions) |
| Dùng chung | 110 | Giới thiệu, dự án, teamwork, Git, debugging, kiểm thử và câu kết thúc. Soạn thêm câu tình huống khi nguồn mở thiếu | [h5bp — câu hỏi chung và kiểm thử](https://github.com/h5bp/Front-end-Developer-Interview-Questions), [Learning Hub](https://github.com/TheLearningHubOrg/learn-interview-questions) |
| **Tổng** | **1.000** | **Mỗi ý hỏi có một ID, gắn thêm nhiều vị trí khi phù hợp.** | |

Đề xuất gom **1.300–1.500 câu ứng viên** từ nguồn có giấy phép phù hợp, sau đó lọc và bổ sung theo từng nhóm. Ưu tiên các phần nền tảng và tình huống ngắn, nhất là trong nguồn có cả câu Senior. Nhóm Fullstack lấy câu hỏi về sự phối hợp giữa các lớp; các câu Frontend hoặc Backend dùng chung giữ nguyên ID và gắn thêm nhãn Fullstack.

## Nguồn có giấy phép công bố

| Nguồn | Phần nên lấy | Giấy phép repo công bố |
| --- | --- | --- |
| [The Learning Hub — Interview Question Bank](https://github.com/TheLearningHubOrg/learn-interview-questions) | Bắt đầu ở `tracks/`. README công bố hơn 1.800 câu trên nhiều chủ đề và cấp độ. Lọc kỹ Frontend, API, SQL, Python, Fullstack, AI và kiểm thử trước khi đưa vào VMI. | MIT |
| [h5bp — Front-end Developer Interview Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions) | Các tệp câu hỏi trong `src/questions/`. Ưu tiên câu hỏi chung, HTML, CSS, JS, mạng, kiểm thử, hiệu năng và accessibility. | MIT |
| [Duyet — Vietnamese Frontend Interview Questions](https://github.com/duyet/vietnamese-frontend-interview-questions) | Câu hỏi tiếng Việt trong README. So trùng ý với h5bp trước khi nhập. | MIT |
| [Lydia Hallie — JavaScript Questions](https://github.com/lydiahallie/javascript-questions) | Có bản `vi-VI/`. Chọn những câu nền tảng có thể trả lời bằng lời. | MIT |
| [AS Backend Institute — Backend Interview Questions](https://github.com/AS-Backend-Institute/backend-interview-questions) | Câu hỏi Node.js, Express, REST, MySQL, MongoDB và Redis trong README. | MIT |
| [Ali Talha Çoban — Backend Interview Questions](https://github.com/alitalhacoban/backend-interview-questions-2026) | Repo công bố 337 câu. Xem `docs/`, bắt đầu với DBMS, Java, Spring và design patterns cơ bản. | MIT |
| [Amit Shekhar — Android Interview Questions](https://github.com/amitshekhariitbhu/android-interview-questions) | Android, Kotlin, vòng đời, coroutine, Jetpack và kiểm thử trong README. | Apache-2.0 |
| [RaiTechLabs — iOS & Swift Interview Questions](https://github.com/raitechlabs/ios-interview-questions) | Swift, SwiftUI, UIKit, concurrency và Core Data. | MIT |
| [Alexey Grigorev — Data Science Interviews](https://github.com/alexeygrigorev/data-science-interviews) | `theory.md`, `technical.md` và mục xác suất trong `contrib/`. | CC BY 4.0 |

Dùng tệp Markdown tại revision cụ thể của repo khi lấy số lượng lớn. Ghi revision, đường dẫn và giấy phép theo từng nguồn. Với câu được dịch hoặc biên tập, giữ thông tin ghi công và ghi rõ thay đổi theo điều kiện của giấy phép tương ứng.

## Nguồn tham khảo cách hỏi

| Nguồn | Dùng để tham khảo |
| --- | --- |
| [Khải Zin AM — Bài kể lại phỏng vấn Backend Node.js/TypeScript](https://www.khaizinam.com/ke-chuyen-phong-van-junior-intern-backend-nodejs-typescript-ho-hoi-gi-minh-tra-loi-ra-sao/) | Cách mở đầu và hỏi tiếp trong bài kể lại một buổi phỏng vấn Intern/Junior. |
| [Hello Interview — Design a URL Shortener](https://www.hellointerview.com/learn/system-design/problem-breakdowns/bitly) | Cách dẫn từ yêu cầu sang API, lưu trữ và lựa chọn đánh đổi. |
| [Tech Interview Handbook — Behavioral Questions](https://www.techinterviewhandbook.org/behavioral-interview-questions/) | Các chủ đề về dự án, teamwork, bất đồng và bài học sau sai sót. |
| [PassInterview — Câu hỏi Việt–Anh](https://passinterview.app/vi/c/all) | Tham khảo độ phủ chủ đề. Điều khoản của trang cấm cào tự động, sao chép hàng loạt và dịch lại nội dung. [Điều khoản PassInterview](https://passinterview.app/terms#2-content-and-intellectual-property) |

Dùng các nguồn trong mục này để định hướng chủ đề và cách diễn đạt. Chỉ đưa nguyên văn vào bộ dữ liệu khi đã có quyền sử dụng phù hợp.

## Tiêu chí bàn giao cho VMI

1. **Đếm theo ý hỏi.** Cùng ý ở hai nguồn, hai cách diễn đạt hoặc hai bản Việt–Anh dùng chung một ID. Một câu đào sâu được tính riêng khi nó kiểm tra lập luận, điều kiện hoặc kiến thức khác.
2. **Phù hợp phỏng vấn bằng lời.** Intern tập trung kiến thức nền và cách giải thích. Fresher thêm tình huống thực tế, gỡ lỗi hoặc đánh đổi. Ưu tiên câu hỏi tự đứng được và có thể trả lời trong khoảng 3 phút.
3. **Giữ nguồn từng câu.** Trường tối thiểu gồm ID, nội dung câu hỏi, ngôn ngữ, vị trí, cấp độ, chủ đề, loại câu hỏi và URL nguồn. Với câu lấy từ repo, lưu thêm revision và giấy phép. Với câu tự soạn, đánh dấu nguồn là nội bộ. Có thể thêm bản Việt–Anh, ID câu cha hoặc đáp án mẫu khi có.
4. **Báo số lượng thực nhận.** Khi bàn giao, ghi số câu thô, số câu loại trùng, số câu bị loại vì lệch cấp độ hoặc cần ngữ cảnh còn thiếu, và số câu giữ lại theo từng nhóm.
