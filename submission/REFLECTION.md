# Reflection — Lab 19

**Tên:** Ngô Văn Kiệt
**Cohort:** _<A20-K3 / A20-K3>_
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 truy vấn, hybrid đạt Precision@10 cao nhất tổng thể (78,6%), nhỉnh
hơn BM25 (77,8%) và vector (73,2%). Với `exact`, BM25 và hybrid cùng đạt
96,7% vì từ khóa đặc trưng đã là tín hiệu đủ mạnh. Với `mixed`, hybrid đạt
100%, cao hơn BM25 97,0% và vector 98,5%, cho thấy RRF tận dụng tốt cả khớp
từ khóa lẫn ngữ nghĩa.

Ở `paraphrase`, kết quả thực nghiệm không giống kỳ vọng lý thuyết: BM25 đạt
33,3%, hybrid 32,0% và vector 24,0%. Nguyên nhân hợp lý là Lite dùng
`bge-small-en-v1.5`, model thiên tiếng Anh nên biểu diễn paraphrase tiếng Việt
chưa tốt. Vì vậy, lựa chọn retriever phải dựa trên benchmark đúng ngôn ngữ và
corpus, không chỉ dựa trên mặc định.

Tôi chọn pure BM25 cho truy vấn mã lỗi, tên riêng hoặc exact-match khi cần độ
trễ và chi phí thấp. Pure vector phù hợp với truy vấn khái niệm khi đã kiểm
chứng một embedding đa ngữ tốt. Hybrid hợp với traffic hỗn hợp, nhưng phải trả
thêm chi phí chạy hai retriever và vận hành fusion.

---

## Điều ngạc nhiên nhất khi làm lab này

Model embedding không phù hợp ngôn ngữ có thể khiến semantic search thua cả
BM25; kiến trúc “hiện đại hơn” không tự động tạo ra kết quả tốt hơn.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
