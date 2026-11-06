# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:**
- **Họ và tên:**
- **SEED** (in ở ô đầu notebook):

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | v |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | v |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | v |

## 2. Kết quả chính

SEED=3331 · thử thách #2
Bộ kiểm tra: 13/14 đạt
  ✅ 1.1 vectorize
  ✅ 1.2 sigmoid / predict_proba
  ✅ 1.3 train_logreg
  ✅ 1.4 metrics
  ✅ 2.1 build_mlp
  ✅ 2.2 train_mlp
  ✅ 3.1–3.2 cosine / top_k_similar
  ✅ 3.3 knn_predict
  ✅ 4.2–4.3 prompt / parse_label
  ✅ tính tay: baseline_accuracy
  ✅ tính tay: sigmoid_0
  ✅ tính tay: f1_example
  ✅ tính tay: cosine_example
  ❌ tính tay: llm_cost_per_day

Dự đoán đã ghi:
  [07:25:13] ml_f1: F1-score: Khoảng 0.85–0.95. Precision có thể cao hơn Recall. Precision cao vì mô hình thường chỉ dự đoán spam khi nhận thấy những từ có dấu hiệu spam khá rõ ràng. - Recall thấp hơn vì một số tin nhắn spam sử dụng ngôn ngữ bình thường hoặc không chứa những từ phổ biến trong vocabulary. Mô hình có thể nhầm chúng thành ham.
  [07:25:55] ml_lr: lr=0.001 thì learning rate quá nhỏ, khiến đường loss giảm từ từ, gần như phẳng. lr=50 thì learning rate quá lớn, khiến đường loss không ổn định, có thể dao động hoặc phân kỳ.
  [07:28:03] dl_curve: Validation Loss không giảm mãi. MLP có thể bằng hoặc nhỉnh hơn Logistic Regression về F1, nhưng không chắc chắn.
  [07:30:50] dl_relu: Nếu xoá nn.ReLU(), hai lớp Linear liên tiếp có thể gộp thành một lớp Linear duy nhất về mặt biểu diễn toán học. Vì vậy, mạng này tương đương với Logistic Regression sau khi áp dụng Sigmoid. Dự đoán F1 có thể giảm hoặc gần như không đổi
  [08:52:36] emb_search: Kết quả gần nhất có thể là Spam, dù truy vấn không chứa các từ khóa spam quen thuộc như free, win, prize, vì khác với Bag-of-Words, Embedding MiniLM biểu diễn câu dựa trên ngữ nghĩa, không chỉ dựa vào từ xuất hiện. Câu truy vấn không chứa từ free, win hay prize, nhưng nội dung vẫn mang ý nghĩa quảng cáo hoặc lừa nhận thưởng.
  [10:22:24] emb_tricky: Dự đoán mô hình 3b. Encoder + Logistic Regression sẽ đoán đúng nhiều hơn BoW.
  [14:55:58] tradeoff: BoW + LogReg (tự code), BoW + MLP (deep learning), Encoder (MiniLM) + kNN có khả năng nằm trên đường Pareto. Cách vượt SLA 50 ms có khả năng là Encoder (MiniLM) + MLP head, Encoder (MiniLM) + kNN.
  [15:29:40] hard_eval: Accuracy với từng model: 1, BoW + LogReg: ~50%; 2, BoW + MLP: ~55%; 3a, Embedding + kNN: ~65%; 3b, Embedding + LogReg: ~55%; 3c, Embedding + MLP head:	~60%. Nhóm khó nhất với BoW và cả với LLM là: spam giọng tự nhiên.
Thiếu dự đoán: ['llm_models', 'llm_fewshot']

                                     f1  f1_SUB
1. BoW + LogReg (tự code)        0.916   0.919
2. BoW + MLP (deep learning)     0.946   0.974
3a. Encoder (MiniLM) + kNN       0.908   1.000
3b. Encoder (MiniLM) + LogReg    0.937   0.974
3c. Encoder (MiniLM) + MLP head  0.958   0.974

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*
Model tụt nhiều nhất là BoW + MLP, ở nhóm case Spam giọng tự nhiên.

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
