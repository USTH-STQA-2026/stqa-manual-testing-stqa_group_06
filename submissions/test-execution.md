># Test Execution — Kết quả thực thi kiểm thử

> **Hướng dẫn**: Chạy từng TC trên hệ thống https://stqa.rbc.vn, ghi lại kết quả thực tế.
> Kết luận: **Pass** (kết quả đúng), **Fail** (kết quả sai → tạo bug report), **Blocked** (không thực hiện được vì lỗi khác chặn), **Not Run** (chưa chạy).

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_06 |
| **Ngày thực thi** | 19/05/2026 |
| **Trình duyệt** | Chrome 148 |
| **Hệ điều hành** | macOS |

---

## Kết quả chi tiết

| TC ID | Functional Group | Expected Result (Summary) | Actual Result | Conclusion | Evidence | Bug |
|---|---|---|---|---|---|---|
| TC-01 | Login | User logs in successfully with valid credentials | Login successful and dashboard displayed | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/7b3eab0a-11a3-424d-8a8d-dc5aa68ef0ba" />| None |
| TC-02 | Login | Display "Member not found" message | Correct error message displayed | Pass |<img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/9f3eddd4-6bb7-46cc-a96b-a8de6ca86432" />| None |
| TC-03 | Login | Display "Incorrect password" message | Correct error message displayed | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/f9bab5d2-eff6-4b3b-b000-e54bc6254cc1" />| None |
| TC-04 | Login Validation | Display validation for empty fields | Validation message displayed correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/4a5c3c51-778c-499e-aa3e-5e6d81401cef" />| None |
| TC-05 | Book Management | Book list displayed successfully | Book list loaded correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/96a697a6-c595-45a3-83e0-5a4c556335f6" />| None |
| TC-06 | View Book Details | Display complete book information correctly | Book details displayed with title, author, category, publication year, and status | Pass | Screenshot of book detail information | None |
| TC-07 | Book Management | Book status updates immediately after borrow/return | Status updated correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/407080ca-e416-46c7-a2fd-f0abeba07b53" /><img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/46c67ae4-ba74-4c1d-9174-1e1d7a4e100a" />| None |
| TC-08 | Search | Correct book displayed when searching by title | BOOK001 displayed correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/c3557336-c064-45c5-a742-eb1c61cf00c1" />| None |
| TC-09 | Search | Correct book displayed when searching by author | BOOK002 displayed correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/3437c49a-2430-426f-b78c-f1c176f60764" />| None |
| TC-10 | Search & Filter | Correct filtered result displayed | BOOK002 displayed correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/a015a9a6-f44a-41b1-a08f-9bf25a600d22" />| None |
| TC-11 | Search | Search is case-insensitive | Same result returned for "Python" and "python" | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/05fc073f-6970-4784-a35d-cdb4c2f6c292" /><img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/472deb64-585f-4320-90a6-a6fc8266b1a0" />| None |
| TC-12 | Search | No result displayed for non-existent keyword | No results shown | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/c36abf64-96db-4f1c-af19-53e06d2c0c4b" />| None |
| TC-13 | Search | System supports search without Vietnamese accents | No book displayed  | Fail | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/c64349ef-47b9-4427-8845-83a2652444e1" />| BUG-01 |
| TC-14 | Borrow Book | Borrow request succeeds | Book borrowed successfully | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/1db2d749-1f67-4377-8f7c-9856bdc50feb" />| None |
| TC-15 | Borrow Book | Reject borrowing already borrowed book | Borrow rejected correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/ec7a8444-bfc9-41a4-be95-e0c246c3274d" />| None |
| TC-16 | Borrow Book | Reject borrowing lost book | Cannot borrow book with status "Lost" | Pass | Screenshot showing lost book borrowed | None |
| TC-17 | Borrow Limit | Allow borrowing the 3rd book | Borrow successful | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/de0b2dff-e8d6-40a2-82af-737fa18e82fd" />| None |
| TC-18 | Borrow Limit | Reject borrowing the 4th book | Borrow successfully | Fail | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/01dd3928-33eb-47ba-84e4-059729ac5cfa" />| None |
| TC-19 | Session Security | Redirect expired session to login page | User redirected correctly | Pass | <img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/42632d1e-3bd6-4646-8318-37923b8983e6" />| None |
| TC-20 | Member Validation | Notify expired member account | Correct notification displayed | Pass |<img width="1911" height="153" alt="image" src="https://github.com/user-attachments/assets/4fcf696e-af48-4384-af9c-5e10cb5b7743" />| None |
| TC-21 | Member Validation | Notify suspended member account | Correct notification displayed | Pass | <img width="1911" height="162" alt="image" src="https://github.com/user-attachments/assets/b630df41-3ecf-43cf-a5c7-e3cdf7457018" />| None |
| TC-22 | Return Book | Return succeeds and book becomes available | Return processed correctly | Pass | <img width="1913" height="442" alt="image" src="https://github.com/user-attachments/assets/093e6664-2fff-475b-bfb8-d1beca863898" />| None |
| TC-22 | Return Book | Reject invalid return request | Return rejected correctly | Pass |<img width="1899" height="141" alt="image" src="https://github.com/user-attachments/assets/f65021df-2454-4841-b5d9-e276984b48dc" />| None |
| TC-24 | Overdue Handling | Display overdue warning | Warning displayed correctly | Pass | <img width="1907" height="247" alt="image" src="https://github.com/user-attachments/assets/78cca06f-c24f-43a1-a3bd-59887b3a7f46" />| None |
| TC-25 | Overdue Check | Record  marked "Overdue" when dueDate = today | System correctly marks record as Overdue | Pass | Screenshot of overdue status | None |
| TC-26 | Authorization | Librarian can view all "Overdue" records | All overdue records displayed | Pass |<img width="1917" height="263" alt="image" src="https://github.com/user-attachments/assets/44a59bb3-506f-403b-8459-eb774cd29b5e" />| None |
| TC-27 | Authorization | Member only views own "Overdue" records | Only member records displayed | Pass | Screenshot of member overdue page | None |
| TC-28 | Member Management | Member created successfully | Display "Invalid Email" | Fail | Screenshot of invalid email message | BUG-03 |
| TC-29 | Member Management | Display email validation error | Member added successfully | Fail | Screenshot of validation message | BUG-04 |
| TC-30 | Member Management | Reject duplicate email | Display "Invalid Email" | Pass | Screenshot of error message | None |
| TC-31 | Borrow Records | Librarian views all borrow records | All records displayed correctly | Pass | <img width="1919" height="702" alt="image" src="https://github.com/user-attachments/assets/fcadc47e-f9d7-4c6d-be0b-59078189b8e0" />| None |
| TC-32 | Authorization | Reject unauthorized record access | Some member can see other member borrow records | Fail | Screenshot showing unauthorized access to borrow records | BUG-05 |
| TC-33 | Authorization | Prevent members from accessing and modifying other members' borrow records | Member MEM002 can view and directly update borrow record of MEM003 | Fail | Screenshot showing unauthorized access and modification of another member's borrow record | BUG-06 |
| TC-35 | Record Status | Display correct borrowing status based on existing borrow records | Book status is displayed as "Borrowing" but no corresponding borrow record exists in the system | Fail | Screenshot showing book status and missing borrow record | BUG-07 |
| TC-36 | Record Status | Display status "Returned" correctly | Status displayed correctly | Pass | <img width="1913" height="468" alt="image" src="https://github.com/user-attachments/assets/c2e41cb2-113d-43ce-b9d0-b4d2b44471e0" />| None |
| TC-37 | Record Status | Display status "Overdue" correctly | Status displayed correctly | Pass |<img width="1919" height="776" alt="image" src="https://github.com/user-attachments/assets/18579df7-ad16-489d-b04a-14d9f61453b4" />| None |


## Tổng hợp kết quả

| Chỉ số | Giá trị |
|--------|---------|
| Tổng số test case | 37 |
| Pass | 30 |
| Fail | 7 |
| Blocked | 0 |
| Not Run | 0 |
| **Tỷ lệ Pass** | 81.08% |

### Kết quả theo nhóm chức năng

| Functional Group | Total TC | Pass | Fail | Pass Rate |
|---|---|---|---|---|
| Login | 4 | 4 | 0 | 100% |
| Book Management | 3 | 3 | 0 | 100% |
| Search | 6 | 5 | 1 | 83.33% |
| Borrow Book | 8 | 7 | 1 | 87.5% |
| Return Book | 3 | 3 | 0 | 100% |
| Overdue Management | 3 | 2 | 1 | 66.7% |
| Member Management | 3 | 1 | 2 | 33.3% |
| Borrow Records | 7 | 4 | 3 | 57.1% |
| Total | 37 | 30 | 7 | 81.08% |
