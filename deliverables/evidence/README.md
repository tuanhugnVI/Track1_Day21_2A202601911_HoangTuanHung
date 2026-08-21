# evidence/ — data thô của từng bước eval loop

Mọi số liệu trong `../REPORT.md` đều dẫn được xuống một file trong thư mục này.

## Đầu vào

| File | Là gì |
|---|---|
| `dataset-v1.jsonl` | Dataset nhóm chốt — 27 câu, 3 lane, đầu vào của mọi lần chạy |
| `dataset-sc1x-loan-draft.jsonl` · `dataset-sc2x-hung-draft.jsonl` | Lane nháp trước khi gộp (lane `sc-3x` của Phương được gộp thẳng) |

## Đầu ra tutor

| File | Là gì |
|---|---|
| `results-v1.jsonl` | Output tutor trên 27 câu: `output` JSON, `tool_calls`, `usage`, `latency_s`, `raw_content`. 0 row lỗi |

## Nhãn người

| File | Là gì |
|---|---|
| `labels-hung.csv` · `labels-loan.csv` · `labels-phuong.csv` | Ba vòng chấm độc lập (Phương chấm 10 câu lane của mình) |
| `labels.csv` | **Nhãn vàng** sau khi nhóm chốt R3 theo nghĩa chặt — 18 fail / 8 pass / 1 uncertain |
| `labels-hung-review.md` | Ghi chú chấm của Hưng: đối chiếu từng quote với corpus, lý do từng case |
| `b4-disagreement-analysis.md` | Phân tích bất đồng do Loan chuẩn bị cho phiên B4 |

## Judge

| File | Là gì |
|---|---|
| `judge-prompt-v1.md` · `judge-prompt-v2.md` | Prompt judge từng vòng. Diff giải thích ở mục 5 REPORT |
| `verdicts-v1.jsonl` | Vòng 1 — agreement 13/27 = 48% |
| `verdicts-v2.jsonl` | Vòng 2 — agreement 21/27 = 77%, bắt đúng 83% output xấu |
| `verdicts-v1-truncated.jsonl` | **Vòng 0 bị huỷ** — 17/27 row `uncertain` do `max_tokens=500` cắt cụt JSON. Giữ lại làm bằng chứng cho bài học ở mục 5 |

## Tracing

| File | Là gì |
|---|---|
| `braintrust-link.md` | Link project Braintrust + ghi chú quyền truy cập |
| `braintrust-screenshots.md` | Nội dung quan sát trên giao diện Braintrust (128 trace) + giải thích vì sao cột Duration/Tokens hiện 0 |
| `trace-summary.md` | Bảng đầy đủ từng row: `tool_calls`, tokens, latency — bản sao cục bộ của dữ liệu trace |

## Code

| File | Là gì |
|---|---|
| `code_checks.py` | Làn Code, bản đã thêm 2 check của Hưng: `followup_count` và `scope_match` |
| `verify-report-numbers.py` | Script đối chiếu số trong REPORT với evidence. **Phải chạy trong repo chung của nhóm** vì nó `import tutor` để đọc corpus — chạy trong gói nộp này sẽ báo `ModuleNotFoundError: No module named 'tutor'` |

Repo chung: https://github.com/tuanhugnVI/K3-Track1-Day20-21-AI-Evaluation
