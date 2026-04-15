[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23572409&assignment_repo_type=AssignmentRepo)
# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** nguyenduyminhhoang@gmail.com
**Name:** Nguyễn Duy Minh Hoàng

---

## Mô tả

Bài lab Day 10 xây dựng một ETL Pipeline tự động xử lý dữ liệu sản phẩm từ file JSON. Pipeline thực hiện 4 bước: Extract (đọc file JSON), Validate (loại bỏ records có giá âm hoặc category rỗng), Transform (giảm giá 10%, chuẩn hóa category, thêm timestamp), và Load (lưu ra file CSV). Ngoài ra, bài lab còn có phần Stress Test để quan sát tác động của dữ liệu rác lên kết quả của AI Agent.

---

## Cach chay (How to Run)

### Prerequisites
```bash
pip install pandas
```

### Chay ETL Pipeline
```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)
```bash
python agent_simulation.py

Testing with CLEAN data:
Agent: Based on my data, the best choice is Laptop at $1200.

Testing with GARBAGE data:
Agent: Based on my data, the best choice is Nuclear Reactor at $999999.
```

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Kết quả

- Tổng records đọc được: **5**
- Records hợp lệ (đã lưu vào CSV): **3**
- Records bị loại: **2** (1 record giá âm, 1 record category rỗng)
- Columns trong output: `id`, `product`, `price`, `category`, `discounted_price`, `processed_at`
- **Stress Test:** Clean data → Agent trả lời chính xác (Laptop $1200). Garbage data → Agent bị đánh lừa bởi outlier (Nuclear Reactor $999999).
