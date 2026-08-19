# Reflection — Lab 19

**Tên:** Phạm Quốc Bảo
**Cohort:** K4
**Path đã chạy:** docker

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

**Trả lời:**

- **Hybrid thắng trung bình** (78.6% vs 77.8% BM25, 73.2% semantic) nhờ robust trên mọi loại query.
- **Exact queries:** BM25 và Hybrid cùng 96.7%, vector 88.7% — keyword đủ mạnh khi có exact term.
- **Paraphrase queries:** Tất cả đều thấp (24-33%), nhưng BM25 33.3% > Hybrid 32.0% > Vector 24.0% — do bge-small-en yếu trên tiếng Việt paraphrase.
- **Mixed queries:** Hybrid 100% > Semantic 98.5% > BM25 97.0% — đây là case hybrid tỏa sáng.

**Khi nào KHÔNG dùng hybrid:**
- Query quá ngắn, chỉ có 1 từ khóa → BM25 đủ, hybrid thêm overhead RRF.
- Latency cực kỳ nghiêm ngặt (<10ms) → dùng 1 retriever thay vì 2.
- Khi semantic model yếu trên corpus (như bge-small-en với tiếng Việt) → hybrid kéo xuống thay vì đẩy lên.

---

## Điều ngạc nhiên nhất khi làm lab này

Semantic (vector) chỉ đạt 73.2% — thấp hơn cả BM25 77.8% trên tiếng Việt. Điều này cho thấy embedding model có impact lớn nhất, không phải search algorithm.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
