# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600155
**Name:** Nguyễn Duy Minh Hoàng
**Date:** 2026-04-15

---

## 1. Kết quả thí nghiệm

Chạy `agent_simulation.py` với 2 bộ dữ liệu và ghi lại kết quả:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Kết quả hợp lý, sản phẩm đúng, giá chính xác |
| Garbage Data (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Kết quả sai hoàn toàn do outlier giá trị cực đoan |

---

## 2. Phân tích & nhận xét

### Tại sao Agent trả lời sai khi dùng Garbage Data?

Khi sử dụng bộ dữ liệu "rác" (`garbage_data.csv`), Agent đã trả về kết quả hoàn toàn sai lệch. Có nhiều nguyên nhân dẫn đến điều này:

1. **Outlier cực đoan (Extreme Outlier):** Bản ghi "Nuclear Reactor" có giá $999,999 — một giá trị phi thực tế nhưng vẫn được Agent chấp nhận vì nó nằm trong cột `price`. Logic của Agent chỉ tìm sản phẩm có giá cao nhất trong category "electronics", nên nó chọn đúng bản ghi lỗi này.

2. **Duplicate IDs:** Có 2 bản ghi có `id=1` (Laptop và Banana), gây ra sự nhầm lẫn và không nhất quán trong dữ liệu, làm cho kết quả phân tích trở nên không đáng tin cậy.

3. **Wrong Data Types:** Bản ghi "Broken Chair" có trường `price = "ten dollars"` — kiểu chuỗi thay vì số. Nếu Agent có lúc cần tính toán số học, điều này sẽ gây lỗi runtime.

4. **Null Values:** Bản ghi "Ghost Item" có `id=None` và `category=None`, điều này có thể làm hỏng các phép lọc và groupby khi xử lý dữ liệu.

Kết luận: Dữ liệu rác không chỉ gây lỗi kỹ thuật mà còn dẫn Agent đến các quyết định sai lệch — nguy hiểm hơn là Agent vẫn trả lời "tự tin" dù kết quả là phi lý.

---

## 3. Kết luận

**Quality Data > Quality Prompt?** Đồng ý.

Dù prompt có chính xác và rõ ràng đến đâu, nếu dữ liệu đầu vào chứa outlier, giá trị null, hoặc sai kiểu dữ liệu, Agent vẫn sẽ cho ra kết quả sai. Chất lượng dữ liệu là nền tảng của mọi hệ thống AI — không có pipeline ETL tốt, không thể có AI tốt.
