# Test Summary — Báo cáo tổng hợp kiểm thử

## 1. Thông tin nhóm

| Mục | Thông tin |
|-----|----------|
| **Nhóm** | STQA_Group_06 |
| **Lớp** | 252ICT2012.L1 |
| **Ngày báo cáo** | 19/05/2026 |
| **Hệ thống kiểm thử** | https://stqa.rbc.vn — v1.0 |

---

## 2. Tổng quan kết quả

| Chỉ số | Giá trị |
| ----- | ----- |
| Total Test Cases | 37 |
| Pass | 30 |
| Fail | 7 |
| Blocked | 0 |
| Not Run | 0 |
| Pass Rate | 81.08% |
| Bugs Detected | 7 |

### Phân bổ theo nhóm chức năng

| Nhóm chức năng | TC | Pass | Fail | Bug | Đánh giá |
| ----- | :---: | :---: | :---: | :---: | ----- |
| REQ-01: System Login | 4 | 4 | 0 | 0 | Functions smoothly, correctly blocks invalid accounts. |
| REQ-02: View Book List | 3 | 3 | 0 | 0 | Displays the complete book list and statuses accurately. |
| REQ-03: Book Search & Filter | 6 | 5 | 1 | 1 | Fails to search when using Vietnamese keywords without accents. |
| REQ-04: Book Borrowing | 8 | 7 | 1 | 1 | Logic flaw allows borrowing a 4th book exceeding the limit. |
| REQ-05: Book Returning | 3 | 3 | 0 | 0 | Successfully processes returns and updates book status. |
| REQ-06: Overdue Check & Handling | 3 | 2 | 1 | 1 | Miscalculates the overdue status when dueDate equals currentDate. |
| REQ-07: Member Management | 3 | 1 | 2 | 2 | Poor data validation infrastructure allows corrupted profile processing. |
| REQ-08: Borrow Record Query | 7 | 4 | 3 | 2 | Critical authorization leak exposes private member logs to cross-user access. |

### Phân bổ bug theo mức độ

| Mức độ | Số lượng | Bug IDs |
| ----- | :---: | ----- |
| High | 4 | BUG-02, BUG-05, BUG-06, BUG-07 |
| Medium | 3 | BUG-01, BUG-03, BUG-04 |
| Low | 0 | None |

---

## 3. Kỹ thuật thiết kế đã sử dụng

| Kỹ thuật | Áp dụng cho REQ nào? | Số TC sử dụng | Giải thích cách áp dụng |
| ----- | ----- | :---: | ----- |
| Equivalence Partitioning (EP) | REQ-01, REQ-03, REQ-04, REQ-05, REQ-07 | 21 | Segmented the input domain into valid and invalid partitions  |
| Boundary Value Analysis (BVA) | REQ-01, REQ-04, REQ-05, REQ-06 | 5 | Tested critical edge boundaries including maximum concurrent borrow quantities  and date equality (dueDate = currentDate) |
| Functional Testing | REQ-02, REQ-07 | 3 | Ensured comprehensive metadata display of catalog books and strict validation behaviors for newly generated member profiles |
| Authorization Testing | REQ-06, REQ-08 | 4 | Validated multi-role permission layers to ensure proper data isolation between the Librarian and regular Members |
| State Transition Testing | REQ-05, REQ-08 | 4 | Audited status alterations of transactional records switching across "Borrowing", "Returned", and "Overdue" lifetimes |
| Security Testing | REQ-04 | 1 | Verified system behavior and safety actions when a user session expires suddenly |

---

## 4. Phân tích chất lượng phần mềm
### 4.1. Điểm mạnh
----Authentication Security: The login infrastructure functions properly, securely authorizing credentials and catching blank inputs.
----Basic Catalog Integrity: Basic browsing operations, database loading, detailed item summaries, and standard keyword queries operate with consistent stability.
----Standard Operational Flow: The standard processes for straightforward borrowing checkouts and timely book returns run reliably without system interruption.

### 4.2. Điểm yếu
----Broken Authorization Framework: Regular member profiles can easily cross-reference, view, and directly edit or trigger book returns on records belonging to foreign accounts.----Business Rule Bypass: Lack of strict back-end enforcement regarding the maximum loan ceiling allows users to check out a 4th book completely undetected.
----Flawed Boundary Logic: The automated calculation tool contains arithmetic errors that flag loans as overdue on the exact day they are due.
----String Normalization Flaws: The search algorithm does not strip accent markers, preventing users from pulling up results using un-accented keywords.

---

## 5. Đề xuất ưu tiên sửa lỗi

| Thứ tự | Bug | Mức độ | Lý do ưu tiên |
|--------|-----|--------|---------------|
| 1 | BUG-06 | High | Security vulnerability allowing users to modify or return transactions belonging to other members, potentially corrupting transaction history and audit logs. |
| 2 | BUG-05 | High | Privacy and authorization issue where regular members can access sensitive information of other users. |
| 3 | BUG-02 | High | Core business logic failure allowing users to borrow more than the maximum limit of 3 books, causing inventory inconsistencies. |
| 4 | BUG-07 | High | Data Desynchronization: Causes a mismatch between the current book status schema and the underlying loan transactional logs. |
| 5 | BUG-03 | Medium | Validation logic incorrectly rejects valid email addresses, preventing users from completing registration or update operations. |
| 6 | BUG-04 | Medium | Validation Logic Failure: Locks out correct operational inputs while accidentally processing malformed or corrupted parameters into the database. |
| 7 | BUG-01 | Medium | UX Usability Bottleneck: Harms ease-of-use by yielding completely empty results when searching without explicit Vietnamese text accents. |

---

## 6. Kết luận

- The system is not ready for release!

Although the software demonstrates reliable performance across fundamental workflows like secure logins and data catalog indexing, it contains major high-risk functional defects. The platform suffers from broken cross-user authorization barriers, missing server-side data validations, and flawed date calculation algorithms. Deploying the system in its present form would trigger massive data leaks and a total failure of library inventory governance. The development cycle must remain open to implement hot-fixes addressing all High and Medium severity items before entering re-verification.

---

## 7. Bài học rút ra (Tùy chọn)
- Proactive Boundary Mapping: Discovered that analytical engineering requires mapping edge equations explicitly during design to avoid logical code bugs .
- Defensive Back-End Isolation: Realized that access rights must be evaluated strictly through server-side authorization structures rather than safely relying on UI modifications or component hiding.

---

## 8. Khai báo sử dụng AI (Tùy chọn)
| Công cụ AI | Dùng cho phần nào | Bạn đã kiểm tra/chỉnh sửa thế nào |
| ----- | ----- | ----- |
| Gemini, ChatGPT | Data aggregation from test-executions | Checking data. |