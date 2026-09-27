Bài này khó hơn 2 bài trước ở chỗ **không được chỉ ra sẵn lỗi**. Phải đọc toàn bộ và bắt cả lỗi cấu trúc lẫn lỗi chất lượng requirement. Tôi sẽ chấm theo kiểu peer review, không bỏ qua mấy lỗi “nhìn có vẻ hợp lý”.

# Bước 1 — Bảng lỗi phát hiện

|   STT | Nội dung lỗi                                                                                                                           | Phân loại lỗi                            | Vị trí đúng / Cách khắc phục                                                                                                                                           |
| ----: | -------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1** | `2.4 Constraints` đang chứa **Actor + Use Case**                                                                                       | **Sai vị trí IEEE 830**                  | Actor và Use Case tổng thể nên đặt ở **Chương 2 — Overall Description → Product Functions / User Classes and Characteristics**, không phải Constraints.                |
| **2** | `1.3 Definitions` chứa **ERD**                                                                                                         | **Sai vị trí IEEE 830**                  | ERD nên đặt ở **Chương 3 — Specific Requirements → Data Requirements / Logical Database Requirements**. `Definitions` chỉ dùng để định nghĩa thuật ngữ, từ viết tắt... |
| **3** | REQ-21: “phản hồi ... **một cách nhanh chóng**”                                                                                        | **Vi phạm Verifiable**                   | Thay “nhanh chóng” bằng chỉ số đo được, ví dụ thời gian phản hồi ≤ X giây trong điều kiện tải xác định.                                                                |
| **4** | REQ-22 chỉ mô tả trường hợp thanh toán đủ 100% nhưng chưa quy định rõ xử lý khi thanh toán **thiếu, thất bại hoặc chưa được xác nhận** | **Vi phạm Complete**                     | Bổ sung các trường hợp thanh toán không đủ/thất bại và trạng thái tương ứng.                                                                                           |
| **5** | REQ-23 và REQ-24 quy định **hai hành vi trái ngược nhau** sau khi thanh toán                                                           | **Vi phạm Consistent**                   | Phải thống nhất thành **một Business Rule duy nhất** về quyền chỉnh sửa báo giá sau khi thanh toán.                                                                    |
| **6** | REQ-23 có cụm “**bất kỳ lúc nào**”                                                                                                     | **Vi phạm Unambiguous / Verifiable**     | Xác định rõ thời điểm và điều kiện được chỉnh sửa, tránh từ tuyệt đối không có phạm vi.                                                                                |
| **7** | REQ-25: “**có thể được cân nhắc**”, “**tùy nguồn lực**”                                                                                | **Vi phạm Verifiable + Unambiguous**     | Không thể xác định yêu cầu có bắt buộc hay không. Phải xác định Priority rõ ràng, ví dụ `Must Have` hoặc `Should Have`.                                                |
| **8** | REQ-25 không có **mức độ ưu tiên**                                                                                                     | **Thiếu thông tin yêu cầu / Incomplete** | Bổ sung `Priority: Should Have` chẳng hạn, và xác định phạm vi thực hiện.                                                                                              |
| **9** | ERD được đặt ở `Definitions` nhưng không có mô tả quan hệ dữ liệu trong phần yêu cầu                                                   | **Incomplete / sai cấu trúc**            | Đưa ERD vào phần Data Requirements và mô tả các thực thể/quan hệ mà hệ thống phải quản lý nếu cần.                                                                     |

### Tối thiểu 3 đặc tính vàng đã bắt được

Bài yêu cầu ít nhất 3, ở đây có:

* **Verifiable** → REQ-21, REQ-25
* **Complete** → REQ-22
* **Consistent** → REQ-23 ↔ REQ-24
* **Unambiguous** → REQ-23, REQ-25

Như vậy phần này **đủ yêu cầu bài**.

---

# Bước 2 — Bản chỉnh sửa hoàn chỉnh

## 1. Sửa cấu trúc IEEE 830

### `[1.2 Scope]`

Phần này **đúng vị trí**.

Có thể giữ:

> **1.2 Scope**
> Hệ thống hỗ trợ khách hàng doanh nghiệp đặt tour trọn gói cho nhóm từ 10 người trở lên.

---

## 2. Sửa `[2.4 Constraints]`

Bản cũ:

> Actor chính: Nhân viên đặt tour...
> Use Case: Tạo yêu cầu đặt tour...

Đây **không phải Constraints**.

Nên chuyển thành:

> **2.x User Classes and Characteristics / Product Functions**
>
> **Actor chính:**
>
> * Nhân viên đặt tour — phía khách hàng doanh nghiệp.
> * Điều phối viên RikkeiTravel.
>
> **Các Use Case chính:**
>
> * Tạo yêu cầu đặt tour.
> * Duyệt báo giá.
> * Xác nhận thanh toán.

Còn `Constraints` chỉ nên chứa các **ràng buộc** thực sự, ví dụ:

> **2.4 Constraints**
>
> * Chỉ khách hàng doanh nghiệp có nhu cầu đặt tour theo nhóm từ 10 người trở lên thuộc phạm vi của phân hệ.
> * Việc xác nhận thanh toán phải dựa trên kết quả xác thực giao dịch từ hệ thống thanh toán.

---

# 3. Sửa `[1.3 Definitions]`

Bản cũ:

> Sơ đồ ERD lưu trữ Yêu cầu đặt tour - Báo giá - Hợp đồng.

Sai bản chất.

`Definitions` phải là kiểu:

> **1.3 Definitions, Acronyms and Abbreviations**
>
> * **Đặt tour trọn gói:** hình thức khách hàng doanh nghiệp đặt một tour bao gồm các dịch vụ được xác định trong báo giá/hợp đồng.
> * **Báo giá:** tài liệu thể hiện chi phí dự kiến của tour và các điều kiện áp dụng.
> * **Hợp đồng:** thỏa thuận giữa khách hàng doanh nghiệp và RikkeiTravel về dịch vụ tour.
> * **Điều phối viên:** nhân sự RikkeiTravel chịu trách nhiệm xử lý và điều phối yêu cầu đặt tour.

Còn ERD chuyển xuống:

> **3.x Data Requirements / Logical Database Requirements**
>
> **ERD — Yêu cầu đặt tour, Báo giá, Hợp đồng**
>
> Sơ đồ mô tả các thực thể dữ liệu chính và mối quan hệ giữa `Yêu cầu đặt tour`, `Báo giá` và `Hợp đồng`.

---

# 4. Viết lại REQ-21

Bản cũ:

> Hệ thống phải phản hồi báo giá cho khách hàng doanh nghiệp một cách nhanh chóng sau khi nhận yêu cầu.

Lỗi nằm ở **“nhanh chóng”**.

### Bản đạt chuẩn:

> **REQ-21:** Sau khi hệ thống nhận thành công yêu cầu đặt tour hợp lệ, hệ thống phải hiển thị báo giá cho khách hàng doanh nghiệp trong thời gian **không quá 5 giây đối với ít nhất 95% số yêu cầu**, trong điều kiện hệ thống có tối đa **100 yêu cầu đặt tour được xử lý đồng thời**.

Bây giờ QA có thể test:

```text
Gửi yêu cầu hợp lệ
       ↓
Đo thời gian
       ↓
Hiển thị báo giá
       ↓
≤ 5 giây ?
       ↓
95% request đạt?
```

Đây mới là **Verifiable**.

---

# 5. Xử lý REQ-23 ↔ REQ-24

Đây là lỗi quan trọng nhất bài.

### REQ-23 nói:

> Điều phối viên **được chỉnh sửa** báo giá sau khi khách thanh toán.

### REQ-24 nói:

> Báo giá **bị khóa**, không ai được chỉnh sửa sau khi khách thanh toán.

Hai câu này **đấm nhau trực diện**.

Không thể để cả hai cùng tồn tại.

## Quy tắc nghiệp vụ thống nhất đề xuất

Ta chọn một Business Rule:

> **BR-01 — Khóa báo giá sau khi thanh toán**
>
> Khi hệ thống xác nhận khách hàng đã thanh toán đủ 100% giá trị hợp đồng, báo giá tương ứng phải được chuyển sang trạng thái **“Đã khóa”**. Sau thời điểm này, không actor nào được phép chỉnh sửa nội dung hoặc giá trị của báo giá.

Sau đó sửa hai requirement:

> **REQ-23:** Điều phối viên có thể chỉnh sửa báo giá khi báo giá chưa ở trạng thái **“Đã khóa”**. Sau khi báo giá được khóa, hệ thống phải từ chối mọi yêu cầu chỉnh sửa báo giá từ điều phối viên.

> **REQ-24:** Khi hệ thống xác nhận khách hàng đã thanh toán đủ 100% giá trị hợp đồng, hệ thống phải chuyển báo giá sang trạng thái **“Đã khóa”** và không cho phép bất kỳ actor nào chỉnh sửa báo giá đó.

Như vậy:

```text
Báo giá chưa thanh toán đủ
        │
        ▼
Điều phối viên được sửa
        │
        │ Thanh toán đủ 100%
        ▼
   [ĐÃ KHÓA]
        │
        ▼
Không actor nào được sửa
```

REQ-23 và REQ-24 giờ **không còn mâu thuẫn**.

---

# 6. Xử lý REQ-25

Bản cũ:

> Tính năng xuất báo giá ra file PDF có thể được cân nhắc bổ sung sau, tùy nguồn lực đội phát triển.

Câu này cực kỳ tệ về mặt SRS vì Dev/QA không biết:

> **Có phải làm không?**

“Có thể được cân nhắc” = chưa phải requirement rõ ràng.

“Tùy nguồn lực” = đẩy quyết định sang lúc triển khai.

## Bản sửa

Ví dụ xác định đây là tính năng **không bắt buộc ở phiên bản đầu**:

> **REQ-25:** Hệ thống nên hỗ trợ chức năng xuất báo giá thành file PDF để khách hàng doanh nghiệp tải xuống.
>
> **Priority: Should Have**
>
> **Release:** Phiên bản 1.1.

Nếu muốn coi nó là bắt buộc ngay phiên bản đầu thì dùng:

> **Priority: Must Have**

Nhưng đề bài yêu cầu **bổ sung mức độ ưu tiên**, chứ không cho dữ kiện để khẳng định business muốn Must hay Should. Vì vậy **Should Have** là một phương án hợp lý để thể hiện đây là tính năng được mong muốn nhưng có thể triển khai sau.

---

# Bản cuối cùng có thể nộp

## Bước 1 — Bảng lỗi

| STT | Nội dung lỗi                                        | Phân loại                    | Cách khắc phục                                                           |
| --: | --------------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------ |
|   1 | Actor/Use Case đặt trong `2.4 Constraints`          | Sai vị trí IEEE 830          | Chuyển sang `2.x User Classes and Characteristics / Product Functions`   |
|   2 | ERD đặt trong `1.3 Definitions`                     | Sai vị trí IEEE 830          | Chuyển sang Chương 3 → Data Requirements / Logical Database Requirements |
|   3 | REQ-21 dùng “nhanh chóng”                           | **Verifiable**               | Quy định thời gian phản hồi cụ thể                                       |
|   4 | REQ-22 thiếu xử lý thanh toán không đủ/thất bại     | **Complete**                 | Bổ sung các trường hợp ngoại lệ và trạng thái tương ứng                  |
|   5 | REQ-23 và REQ-24 mâu thuẫn                          | **Consistent**               | Xây dựng một Business Rule duy nhất về việc khóa báo giá                 |
|   6 | REQ-23 dùng “bất kỳ lúc nào”                        | **Unambiguous / Verifiable** | Quy định rõ điều kiện/thời điểm được sửa                                 |
|   7 | REQ-25 dùng “có thể được cân nhắc”, “tùy nguồn lực” | **Unambiguous / Verifiable** | Xác định rõ requirement và priority                                      |
|   8 | REQ-25 chưa có Priority                             | **Complete**                 | Bổ sung `Priority: Should Have`                                          |

## Bước 2 — Các bản sửa chính

**REQ-21:**

> Sau khi hệ thống nhận thành công yêu cầu đặt tour hợp lệ, hệ thống phải hiển thị báo giá cho khách hàng doanh nghiệp trong thời gian không quá **5 giây đối với ít nhất 95% số yêu cầu**, trong điều kiện tối đa **100 yêu cầu đặt tour được xử lý đồng thời**.

**BR-01:**

> Khi hệ thống xác nhận khách hàng đã thanh toán đủ 100% giá trị hợp đồng, báo giá tương ứng phải được chuyển sang trạng thái **“Đã khóa”**. Sau thời điểm này, không actor nào được phép chỉnh sửa báo giá.

**REQ-23:**

> Điều phối viên có thể chỉnh sửa báo giá khi báo giá chưa ở trạng thái **“Đã khóa”**. Sau khi báo giá được khóa, hệ thống phải từ chối mọi yêu cầu chỉnh sửa báo giá.

**REQ-24:**

> Khi hệ thống xác nhận khách hàng đã thanh toán đủ 100% giá trị hợp đồng, hệ thống phải chuyển báo giá sang trạng thái **“Đã khóa”** và không cho phép bất kỳ actor nào chỉnh sửa báo giá đó.

**REQ-25:**

> Hệ thống nên hỗ trợ chức năng xuất báo giá thành file PDF để khách hàng doanh nghiệp tải xuống.
> **Priority: Should Have**
> **Release: 1.1**

### Nếu thầy hỏi “đâu là 4 lỗi vàng nổi bật nhất?”

Trả lời thẳng:

> **REQ-21 → Verifiable** vì “nhanh chóng” không đo được.
> **REQ-22 → Complete** vì thiếu các trường hợp thanh toán không đủ/thất bại.
> **REQ-23 ↔ REQ-24 → Consistent** vì hai requirement mâu thuẫn trực tiếp.
> **REQ-25 → Unambiguous + Verifiable** vì “có thể cân nhắc” và “tùy nguồn lực” không xác định được đây có phải requirement bắt buộc hay không.
