# Test Cases — Bảng trường hợp kiểm thử

> **Hướng dẫn**: Viết tối thiểu **20 TC** phủ đủ các chức năng chính (REQ-01 → REQ-08).
> Xem [examples/sample-test-case.md](../examples/sample-test-case.md) để hiểu cách viết TC tốt.
> Tự tổ chức và phân nhóm test case theo cách hợp lý nhất.

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_06 |
| **Ngày tạo** | 19/05/2026 |
| **Hệ thống** | https://stqa.rbc.vn |
| **Tham chiếu** | SRS v1.0 |

---

## Bước 1: Mô hình hóa miền đầu vào — Input Domain Modeling (IDM)

> 📖 **Textbook:** Chương 6 — *Input Domain Modeling*, Paul Ammann & Jeff Offutt.
>
> **Trước khi viết Test Case**, nhóm **phải** phân tích miền đầu vào bằng bảng IDM bên dưới.
> Mỗi chức năng cần xác định: **Đặc tính (Characteristic)**, **Phân vùng (Block/Partition)**, và **Giá trị đại diện (Value)**.

### IDM — Đăng nhập (REQ-01)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Email có tồn tại trong DB? | Có | `librarian@library.com` | Đăng nhập thành công |
| | Không | `noone@email.com` | Thông báo lỗi |
| Mật khẩu có đúng? | Đúng | `admin123` | Đăng nhập thành công |
| | Sai | `wrongpass` | Thông báo lỗi |
| Ô nhập có rỗng? | Không rỗng | (giá trị bất kỳ) | Xử lý bình thường |
| | Rỗng | `""` | Thông báo "Vui lòng nhập..." |

### IDM — Tìm kiếm sách (REQ-03)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Từ khóa có tồn tại trong DB? | Có (tên sách) | `"Flutter"` | Hiển thị sách chứa "Flutter" |
| | Có (tên tác giả) | `"Nguyễn"` | Hiển thị sách của tác giả Nguyễn |
| | Không | `"XYZ123"` | Danh sách rỗng |
| Phân biệt HOA/thường? | Chữ thường | `"flutter"` | Kết quả giống "Flutter" |
| | Chữ HOA | `"FLUTTER"` | Kết quả giống "Flutter" |

### IDM — Mượn sách (REQ-04)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Trạng thái sách? | Có sẵn | BOOK001 | Cho phép mượn |
| | Đang mượn | BOOK003 | Không cho phép |
| | Thất lạc | BOOK007 | Không cho phép |
| Trạng thái thành viên? | Hoạt động | MEM002 | Cho phép mượn |
| | Tạm ngưng | MEM004 | Từ chối, thông báo lỗi |
| | Hết hạn | MEM005 | Từ chối, thông báo lỗi |
| Số sách đang mượn? | < 3 (BVA: 0, 1, 2) | MEM006 (0 sách) | Cho phép mượn |
| | = 3 (BVA: giới hạn) | MEM đã mượn 3 sách | Từ chối, thông báo vượt giới hạn |

### IDM — Return & Overdue Check (REQ-05, REQ-06)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| Borrowing relationship | Borrowing member(valid) | MEM001 is borrowing BOOK003 | Allow book return |
| | Member did not borrow this book | MEM001 returns BOOK007 | Do not allow return |
| | Book was already returned previously | BOOK005 is "Available" | Do not allow return |
| Book return status | Returned on time | return Date < dueDate | Return successfully |
| | Returned on due date | return Date = dueDate | Return successfully |
| | Returned overdue | return Date > dueDate | Display overdue warning |
| Book Status After Return  | Book is Borrowed | BOOK003 | After return → change to "Available" |
| Overdue Checkn  | dueDate < currentDate | dueDate = 20/06, currentDate = 24/06 | Mark as "Overdue" |
| | dueDate = currentDate (Boundary) | dueDate = 20/06, currentDate = 20/06 | Mark as "Overdue" |
| | dueDate > currentDate (Boundary) | dueDate = 20/06, currentDate = 19/06 | Not Overdue |
| User Role  | Librarian | LIB001 | View all overdue records |
| | Member views their own record | MEM007 | Only view their own overdue records |
| | Member views another member's record | MEM002 xem MEM007 | Not allowed to view |

### IDM — Member & Borrow record (REQ-07, REQ-08)

| Đặc tính (Characteristic) | Phân vùng (Block) | Giá trị đại diện (Value) | Kết quả mong đợi |
|---|---|---|---|
| User Role for Adding Member | Librarian (Valid) | LIB001 | Allow member creation |
| | Regular Member | MEM001 | Do not allow adding member  |
| Full Name | Not empty | "Nguyen Van A" | Accept |
| | Empty | "" | Reject and require input |
| Email format | Contains '@' and '.' in domain (Valid) | user@domain.com | Create successfully |
| | Missing "." in domain | user@domaincom | Display error |
| | Missing "@" | userdomain.com | Display error |
| | MIssing domain | user@.com | Display error |
| Duplicate Email  | Email does not exist yet | newuser@domain.com | Allow creation |
| | Email already exists | existing@domain.com | Display error |
| Phone Number | Correct format | 0987665432 | Accept |
| | Incorrect format | abc123 | Display error |
| View Borrow Record Permission | Librarian | LIB001 | View all records |
| | Member views their own record | MEM001 | Only allowed to view records of MEM001 |
| | Member views another member's records | MEM001 views MEM004 | Do not allow |
| Borrow Record Status | Borowwing | BR001 | Display status correctly |
| | Returned | BR002 | Display status correctly |
| | Overdue | BR003 | Display status correctly |

---

## Bước 2: Test Cases

## REQ-01: Log In
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-01 | Login successfully with valid account | Account exists | 1. Open login screen 2. Enter email/password 3. Click Login | ba.nguyen@email.com / password123 | Login successfully | REQ-01 | EP |
| TC-02 | Login with non-existent account | Account does not exist | Execute login | binh.pham12@email.com / password123 | Display "Member not found" | REQ-01 | EP |
| TC-03 | Login with incorrect password | Account exists | Execute login | binh.pham@email.com / passwork123 | Display "Incorrect password" | REQ-01 | EP |
| TC-04 | Check empty inputs | None | Leave email/password blank then login | " " / " " | Display "Please enter email and password" | REQ-01 | EP |

## REQ-02: View Books
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-05 | Display all books list | Logged in |None | None | Book list is displayed | REQ-02 | Functional |
| TC-06 | Display complete book information | User is logged in | 1. Open Book List page</br> 2. Select a book | BOOK001 | System displays book title, author, category, publication year, and status (Available/Borrowed) correctly | REQ-02 | Functional |
| TC-07 | Book status update on borrow/return | Logged in | 1.Select button + on BOOK001 "Lập trình Flutter cơ bản"</br>2.Confirm "Borrow"</br>3.Go to Borrow/Return and click "Return book" | Logged in with "Active" member | Status updates from "Borrowing" to "Returned" immediately | REQ-02 | Functional |

## REQ-03: Search Books
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-08 | Search book by title | Logged in (MEM002 or LIB001) (Nguyễn Học Bá or Nguyễn Thủ Thư) | 1. Enter keyword in the search box</br> 2. Observe displayed book list | Keyword = "Flutter" | List displays BOOK001 "Lập trình Flutter cơ bản" | REQ-03 | EP |
| TC-09 | Search book by author's name | Logged in | 1. Enter keyword in the search box</br> 2. Observe displayed book list | Keyword = "Hùng" | List displays BOOK002 "Cấu trúc dữ liệu và giải thuật" | REQ-03 | EP |
| TC-10 | Search book by combining search + category filter | Logged in  | 1. Enter keyword "Hùng" in the search box<br>2. Select category "Công nghệ" | Keyword = "Hùng", "Công nghệ" | List displays BOOK002 "Cấu trúc dữ liệu và giải thuật" | REQ-03 | EP |
| TC-11 | Search is case-insensitive | Logged in  | 1. Enter keyword "Python" in the search box<br>2. Clear and enter keyword "python" in the search box | Keyword = "Python", "python" | List displays BOOK009 "Nhập môn lập trình Python" | REQ-03 | EP |
| TC-12 | Search for non-existent book | Logged in | Search book | “ABCXYZ” | No results found | REQ-03 | EP |
| TC-13 | Search without Vietnamese accents | Logged in | Search book | “lap trinh flutter” | List displays BOOK001 "Lập trình Flutter cơ bản" | REQ-03 | EP |

## REQ-04: Borrow Books
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-14 | Borrow book successfully | Logged in with Active member, Available book | Select Borrow | MEM001 + BOOK001 | Borrow successfully | REQ-04 | EP |
| TC-15 | Reject borrowing already Borrowed book | BOOK003 is currently borrowed | Borrow BOOK003 | MEM001 + BOOK003 | Reject borrowing | REQ-04 | EP |
| TC-16 | Verify borrow rejection for "Lost" book | Logged in as MEM002 | Locate "BOOK007" (Status: Lost) | Book: "BOOK007" | The "+" borrow button is completely hidden/disabled and status is "Lost" | REQ-04 | EP |
| TC-17 | Borrow 3rd book | Member has borrowed 2 books | Click "Borrow" on BOOK005 "Trí tuệ nhân tạo đại cương" | Books borrowed before test: 2<br>Test borrow book: BOOK005 | Borrow successfully | REQ-04 | BVA |
| TC-18 | Borrow 4th book | Member MEM006 borrow 3 books BOOK001, BOOK002, BOOK005 | Click "Borrow" on BOOK008 "Mạng máy tính" | Books borrowed before test: 3<br>Test borrow book: BOOK008 | Display message: "Maximum borrow limit reached (3 books)" | REQ-04 | EP |
| TC-19 | Borrow book with member status "Expired" | Logged in as MEM005 | Borrow "Available" book | Member expired | Notify member account expired | REQ-04 | EP |
| TC-20 | Borrow book with member status "Suspended" | Logged in as MEM004 | Borrow "Available" book | Member suspended | Notify member account suspended | REQ-04 | EP |
| TC-21 | Borrow book after session timeout | Session expired | Borrow book | BOOK001 | User is redirected to login page | REQ-04 | Security Testing |

## REQ-05 & REQ-06: Return & Overdue Check
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-22 | Return book successfully | Member is borrowing the book | Select Return | MEM003 return BOOK003 | Return successfully, book becomes Available | REQ-05 | EP |
| TC-23 | Return book not belonging to member | Member did not borrow that book | Return book | MEM001 returns BOOK007 | Reject book return | REQ-05 | EP |
| TC-24 | Return overdue book | Overdue book | Return book | returnDate > dueDate | Display overdue warning | REQ-05 | BVA |
| TC-25 | Check overdue with dueDate = currentDate | Borrow record exists | Click “Check Overdue” | dueDate = today | Record is marked as Overdue | REQ-06 | BVA |
| TC-26 | Librarian views all overdue records | Logged in as Librarian | Check Overdue | LIB001 | Display all overdue records | REQ-06 | Authorization |
| TC-27 | Member only views their own overdue records | Logged in as Member | Check Overdue | MEM002 | Only display overdue records of MEM002 | REQ-06 | Authorization |

## REQ-07: Member Record
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-28 | Add member with valid email | Logged in as Librarian | Add Member | user@domain.com | Create member successfully | REQ-07 | EP |
| TC-29 | Add member with email missing '.' | Logged in as Librarian | Add Member | user@domaincom | Display email error | REQ-07 | EP |
| TC-30 | Add member with duplicate email | Email already exists | Add Member | existing@gmail.com | Display duplicate email error | REQ-07 | EP |

## REQ-08: Borrow Record
| Test Case ID | Test Objective | Pre-condition | Test Steps | Test Data | Expected Result | Requirement | Test Technique |
| ----- | ------------------------------------------ | ----------------------------- | ------------------------------------------------------------ | ----------------------------------------------- | --------------------------------- | ------ | -------------- |
| TC-31 | Librarian views all borrow records | Logged in as Librarian | Open Borrow Records | LIB001 | Display all records | REQ-08 | Authorization |
| TC-32 | Member views another member's borrow record | Logged in as Member | Query record | MEM002 views MEM004 | Access denied | REQ-08 | Authorization |
| TC-33 | Prevent members from accessing and modifying other members' borrow records | Logged in as MEM006 | 1. Open another member's borrow record URL<br>2. Attempt to edit or return the borrowed book | MEM003 accesses borrow record of MEM006 | Access denied and no modification allowed | REQ-08 | Authorization Testing |
| TC-34 | Display correct record status "Borrowing" | "Borrowing" record exists | Open borrow record | BR003 | Display "Borrowing" | REQ-08 | State Testing |
| TC-35 | Verify consistency between book status and borrow records | Book status = "Borrowing" | 1. Open book details<br>2. Open borrow records list<br>3. Compare book status with borrow records | BOOK006 | System displays a corresponding borrow record for the book with status "Borrowing" | REQ-08 | Consistency Testing |
| TC-36 | Display correct record status "Returned" | "Returned" record exists | Open borrow record | BR004 | Display “Returned” | REQ-08 | State Testing |
| TC-37 | Display correct record status "Overdue" | "Overdue" record exists | Open borrow record | BR005 | Display “Overdue” | REQ-08 | State Testing |



---

## Tổng hợp

| Functional Group | Number of TCs | REQs Covered | Applied IDM Techniques |
| ------------------------ | ------ | ------------------- | ------------------------------------------------------------------------ |
| System Login | 4 | REQ-01 | EP, BVA |
| View Book List | 3 | REQ-02 | Functional Testing |
| Book Search & Filter | 6 | REQ-03 | EP, Decision Table |
| Book Borrowing | 8 | REQ-04 | EP, BVA, Security Testing |
| Book Returning | 3 | REQ-05 | EP, BVA, State Transition |
| Overdue Check & Handling | 3 | REQ-06 | BVA, Authorization |
| Member Management | 3 | REQ-07 | EP, Validation Testing |
| Borrow Record Query | 7 | REQ-08 | Authorization, State Testing, Consistency Testing |

| **Total** | **37** | **REQ-01 → REQ-08** | **EP, BVA, Decision Table, Authorization, State Transition, Validation, Security Testing, Consistency Testing** |
