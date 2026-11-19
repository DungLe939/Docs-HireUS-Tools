# Benchmark STT/TTS cho Voice Mock Interview

Đo ngày 19/11/2026 trên Intel Core i5-12500H, 16 luồng logic, RAM 15 GiB và
swap 8 GiB. CPU có `avx_vnni`, không thấy `avx512_vnni`. Máy này không có GPU
NVIDIA cho phép đo, nên không chạy GPU/vLLM hoặc ghi VRAM. Node v24.22.3;
các venv đo dùng Python 3.12.16. Các model chạy tuần tự. Trạng thái RAM và
tải nền của máy trong phiên có thể ảnh hưởng độ trễ.

Quy trình chạy lại ở `backend/scripts/bench/README.md`. Dữ liệu thô trong
`backend/scripts/bench/out/` trên máy đo gồm `results.csv`, `compare.html`,
`compare.md`, log từng adapter và CSV/WAV TTS. Report chia sẻ chỉ chứa số liệu
tổng hợp, không chứa clip hoặc bản chép giọng thật.

## Phương pháp

- ASR dùng 7 MP3 giọng thật trong Downloads, 4 clip tiếng Việt và 2 clip tiếng
  Anh có đáp án. Clip Việt còn lại dài 79,66 giây, nhãn `NATURAL`. Ánh xạ
  được người dùng xác nhận trước khi đo. Kết quả thử Whisper small chỉ dùng
  để gợi ý nhãn lúc chuẩn bị. Không có clip thuộc nhóm 45–60 giây.
- Baseline faster-whisper small/medium/large-v3-turbo dùng HTTP loopback, CPU
  int8, 4 luồng, beam 5, VAD tắt và giữ ngữ cảnh đoạn trước. PhoWhisper
  Transformers dùng CPU FP32, cắt cửa sổ 30 giây. Thử thêm CTranslate2 int8.
  Qwen dùng gói `qwen-asr` 0.0.6, CPU BF16, hai chế độ ngôn ngữ cố định theo
  clip (`forced`) và tự nhận diện (`auto`).
- Mỗi chế độ có một lượt làm nóng rồi ba lượt mỗi clip. Qwen 1.7B dùng một
  lượt mỗi clip và chế độ trên CPU. Các điểm chất lượng lấy lượt thành công
  đầu tiên của mỗi clip, sau đó lấy trung bình theo nhóm. p50/p95 và RTF lấy
  các lượt đo hợp lệ. Thời gian load đo từ lúc bắt đầu khởi tạo adapter đến
  khi sẵn sàng; với cache trống có thể bao gồm tải trọng số. RAM là peak RSS
  của tiến trình model, không phải tổng RAM máy.
- WER/CER giữ thuật toán và chuẩn hóa script cũ. `WER_no_num` loại token có
  chữ số và cụm số được nhận dạng theo quy tắc từ vựng; vẫn còn trường hợp
  từ số đa nghĩa hoặc dạng đọc ngoài quy tắc. WER có thể tăng khi bỏ số
  vì số từ tham chiếu trong mẫu số cũng giảm. Recall dùng số lần xuất hiện
  cả cụm đã chuẩn hóa, phân biệt `cache` và `caching`, không gộp hình thái
  số ít/số nhiều. Không chấm WER/CER/recall cho `NATURAL`.
- TTS dùng 8 câu dài 20–40 từ (3 Việt, 2 Anh, 3 trộn) và bốn giọng Hải Đăng,
  Mai Anh, Thiện Minh, Thùy Dung. SDK lấy mẫu đầu từ `infer_stream`; HTTP
  dùng đo trên loopback qua `apps/openai_speech.py`. TTFA HTTP bắt đầu khi
  có mẫu PCM đầu, không tính WAV header là âm thanh. Tổng thời gian và
  RTF kết thúc khi đọc xong body/stream. Vòng TTS đo từng cấu hình với một
  yêu cầu đang chạy tại một thời điểm; API upstream chỉ khởi tạo Turbo.
- VieNeu dùng source revision
  [512de867](https://github.com/pnnbao97/VieNeu-TTS/tree/512de867d49b883d50cc47989c445d070f62362f),
  cài với `uv sync --locked`. Trọng số Turbo
  [61b85e3](https://huggingface.co/pnnbao-ump/VieNeu-TTS-v3-Turbo/tree/61b85e3d937fbbacb387714180e8182823512523),
  Nano [aba295e](https://huggingface.co/pnnbao-ump/VieNeu-TTS-v3-Nano/tree/aba295eb96a6fa6003ebe417cc1f2802a7adc1dc)
  và codec [ceff0d0](https://huggingface.co/OpenMOSS-Team/MOSS-Audio-Tokenizer-Nano-ONNX/tree/ceff0d0749bfb3fa2d61149794ec6feef0d1e1ae).
- MOSS được ghim
  [d930a0b](https://huggingface.co/hynt/MOSS-Transcribe-Diarize-Vietnamese-6000h/tree/d930a0b2d78f47abed5943d240c859c320454828).
  Đã đọc ba tệp Python và so checksum trước khi thử nạp offline. Các tệp
  triển khai phần cấu hình, xử lý tín hiệu và suy luận tensor; không thấy
  lời gọi mạng, shell hay `exec` bất thường trong ba tệp này.

ASR MOSS CausalLM dùng CPU FP32, 4 luồng, chế độ ngôn ngữ của model.
Load time của HTTP TTS gồm thời gian server làm nóng trước khi sẵn sàng.

## ASR theo ngôn ngữ và độ dài

| Model / chế độ | Nhóm | Clip / lượt | WER % | WER_no_num % | CER % | Recall % | p50 s | p95 s | RTF | Peak MiB | Load s |
| --- | --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| faster-whisper-large-v3-turbo / forced | EN ≤20s | 2 / 6 | 2.9 | 2.9 | 2.5 | 100.0 | 5.55 | 6.78 | 0.44 | 2095 | 47.30 |
| faster-whisper-large-v3-turbo / forced | VI 20-45s | 1 / 3 | 16.7 | 17.1 | 11.4 | 85.7 | 6.46 | 6.74 | 0.32 | 2101 | 47.30 |
| faster-whisper-large-v3-turbo / forced | VI ≤20s | 3 / 9 | 28.4 | 22.6 | 17.3 | 61.5 | 5.72 | 7.17 | 0.71 | 2101 | 47.30 |
| faster-whisper-large-v3-turbo / forced | VI >60s | 1 / 3 | — | — | — | — | 26.09 | 26.72 | 0.33 | 2128 | 47.30 |
| faster-whisper-medium / forced | EN ≤20s | 2 / 6 | 3.3 | 3.3 | 0.8 | 80.0 | 4.33 | 4.57 | 0.33 | 2654 | 44.30 |
| faster-whisper-medium / forced | VI 20-45s | 1 / 3 | 21.8 | 21.1 | 13.2 | 85.7 | 8.37 | 8.42 | 0.41 | 2706 | 44.30 |
| faster-whisper-medium / forced | VI ≤20s | 3 / 9 | 29.0 | 25.4 | 21.9 | 84.6 | 5.31 | 7.03 | 0.60 | 2706 | 44.30 |
| faster-whisper-medium / forced | VI >60s | 1 / 3 | — | — | — | — | 36.28 | 36.97 | 0.45 | 2958 | 44.30 |
| faster-whisper-small / forced | EN ≤20s | 2 / 6 | 18.6 | 18.6 | 7.9 | 60.0 | 1.73 | 2.16 | 0.13 | 860 | 2.32 |
| faster-whisper-small / forced | VI 20-45s | 1 / 3 | 34.6 | 35.5 | 21.0 | 85.7 | 3.35 | 3.68 | 0.17 | 864 | 2.32 |
| faster-whisper-small / forced | VI ≤20s | 3 / 9 | 34.3 | 30.3 | 20.0 | 69.2 | 2.05 | 2.37 | 0.23 | 865 | 2.32 |
| faster-whisper-small / forced | VI >60s | 1 / 3 | — | — | — | — | 13.50 | 13.52 | 0.17 | 987 | 2.32 |
| moss-causal / native | EN ≤20s | 2 / 6 | 10.5 | 10.5 | 5.2 | 60.0 | 9.47 | 12.18 | 0.72 | 5299 | 9.10 |
| moss-causal / native | VI 20-45s | 1 / 3 | 14.1 | 14.5 | 10.7 | 100.0 | 16.76 | 18.32 | 0.84 | 5299 | 9.10 |
| moss-causal / native | VI ≤20s | 3 / 9 | 18.8 | 20.2 | 8.8 | 84.6 | 11.13 | 12.51 | 1.20 | 5299 | 9.10 |
| moss-causal / native | VI >60s | 1 / 3 | — | — | — | — | 75.07 | 79.16 | 0.96 | 5299 | 9.10 |
| pho-base / forced | EN ≤20s | 2 / 6 | 138.1 | 138.1 | 73.7 | 0.0 | 4.06 | 4.25 | 0.31 | 971 | 7.07 |
| pho-base / forced | VI 20-45s | 1 / 3 | 43.6 | 44.7 | 32.7 | 0.0 | 6.30 | 6.41 | 0.31 | 971 | 7.07 |
| pho-base / forced | VI ≤20s | 3 / 9 | 38.5 | 43.6 | 24.8 | 0.0 | 4.04 | 4.55 | 0.38 | 972 | 7.07 |
| pho-base / forced | VI >60s | 1 / 3 | — | — | — | — | 46.90 | 47.31 | 0.59 | 986 | 7.07 |
| pho-base-ct2 / forced | EN ≤20s | 2 / 6 | 129.5 | 129.5 | 72.3 | 0.0 | 1.19 | 1.22 | 0.09 | 339 | 0.71 |
| pho-base-ct2 / forced | VI 20-45s | 1 / 3 | 46.2 | 47.4 | 32.7 | 0.0 | 1.48 | 1.51 | 0.07 | 343 | 0.71 |
| pho-base-ct2 / forced | VI ≤20s | 3 / 9 | 44.3 | 50.9 | 27.0 | 0.0 | 0.98 | 1.23 | 0.11 | 343 | 0.71 |
| pho-base-ct2 / forced | VI >60s | 1 / 3 | — | — | — | — | 6.97 | 7.05 | 0.09 | 396 | 0.71 |
| pho-small / forced | EN ≤20s | 2 / 6 | 106.7 | 106.7 | 82.0 | 0.0 | 9.45 | 9.86 | 0.72 | 2073 | 7.23 |
| pho-small / forced | VI 20-45s | 1 / 3 | 33.3 | 32.9 | 31.7 | 0.0 | 17.43 | 18.20 | 0.87 | 2073 | 7.23 |
| pho-small / forced | VI ≤20s | 3 / 9 | 40.1 | 45.4 | 24.3 | 15.4 | 10.95 | 12.15 | 1.06 | 2073 | 7.23 |
| pho-small / forced | VI >60s | 1 / 3 | — | — | — | — | 70.65 | 74.07 | 0.90 | 2073 | 7.23 |
| pho-small-ct2 / forced | EN ≤20s | 2 / 6 | 117.9 | 117.9 | 71.4 | 0.0 | 3.11 | 3.91 | 0.24 | 650 | 0.82 |
| pho-small-ct2 / forced | VI 20-45s | 1 / 3 | 37.2 | 36.8 | 29.5 | 0.0 | 4.85 | 5.11 | 0.23 | 650 | 0.82 |
| pho-small-ct2 / forced | VI ≤20s | 3 / 9 | 40.1 | 45.4 | 22.5 | 15.4 | 3.30 | 3.87 | 0.34 | 650 | 0.82 |
| pho-small-ct2 / forced | VI >60s | 1 / 3 | — | — | — | — | 18.07 | 18.21 | 0.23 | 775 | 0.82 |
| qwen-0.6b / auto | EN ≤20s | 2 / 6 | 10.9 | 10.9 | 5.2 | 60.0 | 14.30 | 16.11 | 1.07 | 2816 | 69.42 |
| qwen-0.6b / auto | VI 20-45s | 1 / 3 | 17.9 | 18.4 | 13.2 | 85.7 | 24.53 | 26.62 | 1.24 | 2816 | 69.42 |
| qwen-0.6b / auto | VI ≤20s | 3 / 9 | 15.0 | 12.8 | 8.5 | 84.6 | 15.86 | 17.95 | 1.32 | 2816 | 69.42 |
| qwen-0.6b / auto | VI >60s | 1 / 3 | — | — | — | — | 118.37 | 126.85 | 1.52 | 2816 | 69.42 |
| qwen-0.6b / forced | EN ≤20s | 2 / 6 | 10.9 | 10.9 | 5.2 | 60.0 | 12.00 | 13.95 | 0.90 | 2398 | 69.42 |
| qwen-0.6b / forced | VI 20-45s | 1 / 3 | 17.9 | 18.4 | 13.2 | 85.7 | 21.06 | 21.63 | 1.04 | 2398 | 69.42 |
| qwen-0.6b / forced | VI ≤20s | 3 / 9 | 15.0 | 12.8 | 9.4 | 84.6 | 13.31 | 14.85 | 1.16 | 2398 | 69.42 |
| qwen-0.6b / forced | VI >60s | 1 / 3 | — | — | — | — | 117.20 | 117.93 | 1.47 | 2816 | 69.42 |
| qwen-1.7b / auto | EN ≤20s | 2 / 2 | 7.9 | 7.9 | 4.9 | 100.0 | 27.15 | 31.01 | 2.02 | 4790 | 147.29 |
| qwen-1.7b / auto | VI 20-45s | 1 / 1 | 5.1 | 5.3 | 3.9 | 100.0 | 49.65 | 49.65 | 2.44 | 4790 | 147.29 |
| qwen-1.7b / auto | VI ≤20s | 3 / 3 | 8.3 | 8.1 | 3.4 | 92.3 | 28.05 | 29.62 | 2.43 | 4790 | 147.29 |
| qwen-1.7b / auto | VI >60s | 1 / 1 | — | — | — | — | 195.61 | 195.61 | 2.46 | 4890 | 147.29 |
| qwen-1.7b / forced | EN ≤20s | 2 / 2 | 7.9 | 7.9 | 4.9 | 100.0 | 28.65 | 31.46 | 2.15 | 4588 | 147.29 |
| qwen-1.7b / forced | VI 20-45s | 1 / 1 | 5.1 | 5.3 | 3.9 | 100.0 | 45.27 | 45.27 | 2.22 | 4588 | 147.29 |
| qwen-1.7b / forced | VI ≤20s | 3 / 3 | 8.3 | 8.1 | 1.9 | 92.3 | 28.04 | 28.41 | 2.35 | 4588 | 147.29 |
| qwen-1.7b / forced | VI >60s | 1 / 1 | — | — | — | — | 213.97 | 213.97 | 2.69 | 4790 | 147.29 |

### Trạng thái lượt chạy ASR

| Model | Trạng thái tiến trình | Lượt thành công / tổng |
| --- | --- | ---: |
| faster-whisper-large-v3-turbo | ok | 21/21 |
| faster-whisper-medium | ok | 21/21 |
| faster-whisper-small | ok | 21/21 |
| moss-causal | ok | 21/21 |
| moss-multimodal | error | 0/0 |
| moss-speech | error | 0/0 |
| pho-base | ok | 21/21 |
| pho-base-ct2 | ok | 21/21 |
| pho-small | ok | 21/21 |
| pho-small-ct2 | ok | 21/21 |
| qwen-0.6b | ok | 42/42 |
| qwen-1.7b | ok | 14/14 |

### Thuật ngữ theo model

| Model / chế độ | Recall theo lượt xuất hiện | Lượt nhận đúng / xuất hiện theo thuật ngữ |
| --- | ---: | --- |
| faster-whisper-large-v3-turbo / forced | 19/25 (76.0%) | ACID 0/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 3/3, Jest 0/1, PostgreSQL 2/2, REST API 2/2, Redis 2/2, cache 0/1, caching 0/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| faster-whisper-medium / forced | 21/25 (84.0%) | ACID 1/1, CI/CD 1/1, GitHub Actions 0/1, GraphQL 3/3, Jest 0/1, PostgreSQL 2/2, REST API 2/2, Redis 1/2, cache 1/1, caching 0/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| faster-whisper-small / forced | 18/25 (72.0%) | ACID 1/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 3/3, Jest 0/1, PostgreSQL 1/2, REST API 2/2, Redis 1/2, cache 0/1, caching 0/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| moss-causal / native | 21/25 (84.0%) | ACID 1/1, CI/CD 0/1, GitHub Actions 1/1, GraphQL 2/3, Jest 0/1, PostgreSQL 2/2, REST API 1/2, Redis 2/2, cache 1/1, caching 1/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| pho-base / forced | 0/25 (0.0%) | ACID 0/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 0/3, Jest 0/1, PostgreSQL 0/2, REST API 0/2, Redis 0/2, cache 0/1, caching 0/1, coverage 0/1, endpoint 0/1, index 0/2, pipeline 0/1, query 0/2, request 0/1, transaction 0/1, unit test 0/1 |
| pho-base-ct2 / forced | 0/25 (0.0%) | ACID 0/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 0/3, Jest 0/1, PostgreSQL 0/2, REST API 0/2, Redis 0/2, cache 0/1, caching 0/1, coverage 0/1, endpoint 0/1, index 0/2, pipeline 0/1, query 0/2, request 0/1, transaction 0/1, unit test 0/1 |
| pho-small / forced | 2/25 (8.0%) | ACID 0/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 0/3, Jest 0/1, PostgreSQL 0/2, REST API 0/2, Redis 0/2, cache 0/1, caching 0/1, coverage 1/1, endpoint 0/1, index 1/2, pipeline 0/1, query 0/2, request 0/1, transaction 0/1, unit test 0/1 |
| pho-small-ct2 / forced | 2/25 (8.0%) | ACID 0/1, CI/CD 0/1, GitHub Actions 0/1, GraphQL 0/3, Jest 0/1, PostgreSQL 0/2, REST API 0/2, Redis 0/2, cache 0/1, caching 0/1, coverage 1/1, endpoint 0/1, index 1/2, pipeline 0/1, query 0/2, request 0/1, transaction 0/1, unit test 0/1 |
| qwen-0.6b / auto | 20/25 (80.0%) | ACID 1/1, CI/CD 0/1, GitHub Actions 1/1, GraphQL 3/3, Jest 1/1, PostgreSQL 1/2, REST API 2/2, Redis 1/2, cache 1/1, caching 0/1, coverage 0/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| qwen-0.6b / forced | 20/25 (80.0%) | ACID 1/1, CI/CD 0/1, GitHub Actions 1/1, GraphQL 3/3, Jest 1/1, PostgreSQL 1/2, REST API 2/2, Redis 1/2, cache 1/1, caching 0/1, coverage 0/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| qwen-1.7b / auto | 24/25 (96.0%) | ACID 1/1, CI/CD 1/1, GitHub Actions 1/1, GraphQL 3/3, Jest 1/1, PostgreSQL 1/2, REST API 2/2, Redis 2/2, cache 1/1, caching 1/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |
| qwen-1.7b / forced | 24/25 (96.0%) | ACID 1/1, CI/CD 1/1, GitHub Actions 1/1, GraphQL 3/3, Jest 1/1, PostgreSQL 1/2, REST API 2/2, Redis 2/2, cache 1/1, caching 1/1, coverage 1/1, endpoint 1/1, index 2/2, pipeline 1/1, query 2/2, request 1/1, transaction 1/1, unit test 1/1 |

## TTS theo cấu hình và đường gọi

| Engine | Đường gọi | Normalizer backend | Lượt đạt / tổng | TTFA p50/p95 ms | Tổng p50/p95 s | RTF p50 | Peak MiB | Load s |
| --- | --- | --- | ---: | ---: | ---: | ---: | ---: | ---: |
| vieneu-nano | sdk wav | Không | 8/32 | 1106.07 / 1284.55 | 1.79 / 2.09 | 0.20 | 505 | 1.26 |
| vieneu-nano | sdk wav | Có | 3/12 | 780.49 / 1095.06 | 1.89 / 1.90 | 0.20 | 505 | 1.26 |
| vieneu-turbo-fp32 | api pcm | Không | 32/32 | 309.53 / 348.09 | 3.17 / 4.36 | 0.43 | 1451 | 3.89 |
| vieneu-turbo-fp32 | api wav | Không | 32/32 | 336.71 / 423.07 | 3.42 / 4.98 | 0.47 | 1449 | 3.89 |
| vieneu-turbo-fp32 | sdk wav | Không | 32/32 | 325.48 / 364.74 | 3.44 / 4.51 | 0.46 | 1410 | 2.90 |
| vieneu-turbo-fp32 | sdk wav | Có | 12/12 | 341.77 / 367.40 | 3.72 / 4.03 | 0.46 | 1410 | 2.90 |
| vieneu-turbo-int8 | api pcm | Không | 32/32 | 192.20 / 225.95 | 2.52 / 3.47 | 0.32 | 865 | 3.10 |
| vieneu-turbo-int8 | api wav | Không | 32/32 | 189.95 / 233.02 | 2.52 / 3.24 | 0.32 | 863 | 3.10 |
| vieneu-turbo-int8 | sdk wav | Không | 32/32 | 181.46 / 227.18 | 2.41 / 3.38 | 0.32 | 824 | 2.32 |
| vieneu-turbo-int8 | sdk wav | Có | 12/12 | 198.53 / 227.15 | 2.58 / 3.02 | 0.31 | 824 | 2.32 |
| zonos | api — | Không | 0/1 | — | — | — | — | — |

## Kết quả chạy và điểm cần lưu ý

- Hai checkpoint PhoWhisper xuất được sang CTranslate2 int8 với tokenizer
  riêng và chạy đủ clip qua faster-whisper. Lần đầu dùng Transformers gặp lỗi
  tương thích PyAV `metadata_errors` khi đọc MP3. Adapter đo chuyển sang FFmpeg
  PCM mono 16 kHz rồi đo lại. Bản CTranslate2 nhanh hơn trên bộ này, nhưng
  chênh lệch WER phụ thuộc cả đường giải mã. WER lớn hơn 100% là kết quả hợp lệ
  khi có nhiều từ chèn.
- Các bản Qwen 0.6B và 1.7B cho cùng WER theo hai chế độ trên 6 clip có đáp án
  trong lần đo này. Đặt ngôn ngữ hay tự nhận diện vẫn cần thử lại trên bộ nhiều
  ca trộn Việt/Anh hơn. Bản 1.7B thử một lượt mỗi clip và chế độ vì chi phí
  CPU, đặc biệt trên clip dài.
- MOSS `AutoModelForSpeechSeq2Seq` không nhận `MossTranscribeDiarizeConfig`.
  `AutoModelForMultimodalLM` đi qua lớp Transformers tích hợp nhưng lỗi
  `embed_dim=1024` không chia hết cho 6 attention heads. Bảng tách riêng đường
  `AutoModelForCausalLM` theo `auto_map` của checkpoint.
- Turbo FP32 và int8 chạy đủ SDK, HTTP WAV và HTTP PCM. Nano có Mai Anh trong
  bốn giọng yêu cầu, nên các hàng thiếu giọng được tính là không có mẫu.
  API đã ghim chỉ khởi tạo Turbo. Thu được **227 WAV** có số frame, sample width
  và payload hợp lệ. Tỷ lệ mẫu gần clipping cao nhất của int8 là khoảng
  0,0017% ở một mẫu HTTP WAV; phép kiểm tra này không thay thế nghe thực tế.
- Zonos trả lỗi kết nối từ `127.0.0.1:1919`, nên chưa có baseline Zonos.
  Gemini là lựa chọn tùy chọn và không chạy trong đợt đo cục bộ này.
- API VieNeu gửi WAV streaming 48 kHz với độ dài chưa biết trong header,
  còn adapter Zonos hiện xác thực WAV mono PCM16 44,1 kHz với kích thước hữu
  hạn. Benchmark đóng gói lại body thành WAV chuẩn để nghe. Nếu chọn VieNeu
  ở bước sau, cần kiểm tra cách tích hợp PCM/WAV và cả đường đi từ trình duyệt.

## Chuẩn hóa số và nghe đối chiếu

So sánh pipeline text ở cả ba câu trộn cho thấy sea-g2p đã đổi `180 giây` thành
“một trăm tám mươi giây” và `10%` thành “mười phần trăm”, giống output qua
normalizer backend. Có chồng lấn ở bước đọc số. Cả ba cặp lại tạo dãy phoneme
khác nhau ở từ viết tắt: sea-g2p gắn cách đọc tiếng Anh cho `API`/`SQL`,
còn backend đưa cách đọc Việt hóa của `REST API` và `SQL` vào đầu vào.
Các tệp WAV gốc và `-norm` dùng cùng engine, giọng, câu để nghe sự khác biệt.
Tỷ lệ mẫu gần ngưỡng clipping trong CSV chỉ kiểm tra biên độ, không đánh giá
được méo giọng, ngữ điệu, chất lượng đọc tiếng Anh hay mức dễ nghe.

## Hạn chế và cách dùng kết quả

Chỉ có **6 clip có đáp án**. Các số đo mang tính tham khảo, chưa đại diện cho
nhiều giọng, tiếng ồn, độ dài và từ vựng IT khác nhau. Không có clip đã gắn
nhãn im lặng, chỉ tiếng ồn hoặc khoảng ngắt để đếm từ sinh khi không có lời.
Clip `NATURAL` chỉ dùng để nghe và kiểm tra cờ lặp, trống hoặc độ dài khác thường.
Phân vị trên nhóm ít clip và lượt đơn Qwen 1.7B chỉ mô tả lượt quan sát.

Nên nghe các lỗi thuật ngữ và ba cặp WAV gốc/`-norm` trước khi kết luận về
chất lượng. Với cấu hình muốn đánh giá tiếp, bổ sung clip thật ở các dải
45–60 giây, clip ngắt dài hoặc nhiễu, rồi đo lại trên máy mục tiêu. Mốc 10 giây
trong ngữ cảnh VMI là mốc cho từng lần chờ thực tế; SDK/HTTP cục bộ không đo
thời gian gọi AI hay trình duyệt. Báo cáo này để so sánh, chưa chọn model.
