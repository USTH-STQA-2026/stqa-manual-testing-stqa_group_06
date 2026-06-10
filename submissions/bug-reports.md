# Bug Reports — Báo cáo lỗi

| Thông tin | |
|---|---|
| **Nhóm** | STQA_Group_06 |
| **Ngày báo cáo** | 22/05/2026 |


## BUG-01

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-01 |
| **TC liên quan** | TC-13 |
| **REQ liên quan** | REQ-03 |
| **Mức độ** | Medium |
| **Người phát hiện** | Nguyễn Khắc Trường |
| **Ngày phát hiện** | 22/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System does not display books when searching without Vietnamese accents

**Môi trường:**
- Browser: Chrome 148
- Operating System: Window
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User has successfully logged into the system
- Search function is available
- Book: BOOK001 – "Lập trình Flutter cơ bản" exists in the database

**Bước tái hiện:**
1. Log into the Library Management System
2. Navigate to the Search Book function
3. Enter the keyword: lap trinh flutter
4. Press Search or Enter

**Kết quả mong đợi:**
- The system should display: BOOK001 – “Lập trình Flutter cơ bản”
- The search function should support searching without Vietnamese accents

**Kết quả thực tế:**
- No book is displayed
- The search result list is empty even though BOOK001 – “Lập trình Flutter cơ bản” exists in the database

**Tác động:**
- Users cannot search books using keywords without Vietnamese accents
- This reduces search usability and negatively affects user experience, especially for users who type without Vietnamese input methods

**Mức độ**
- Medium

**Minh chứng:**
<img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/c64349ef-47b9-4427-8845-83a2652444e1" />

**Đề xuất xử lý:**
- Implement accent-insensitive search processing
- Normalize Vietnamese accented characters before comparing search keywords
- Example:Lập trình Flutter → lap trinh flutter
---

## BUG-02

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-02 |
| **TC liên quan** | TC-18 |
| **REQ liên quan** | REQ-04 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Mạnh Tú |
| **Ngày phát hiện** | 22/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System allows borrowing books beyond the maximum borrowing limit instead of rejecting the request

**Môi trường:**
- Browser: Chrome 148
- Operating System: Window
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User has logged into the system successfully
- Member MEM006 has already borrowed 3 books: BOOK001, BOOK002, BOOK005
- BOOK008 – “Computer Networks” is currently in Available status

**Bước tái hiện:**
1. Log into the Library Management System
2. Navigate to the Borrow Book function
3. Verify that the member has already borrowed 3 books
4. Select BOOK008 – “Computer Networks”
5. Click the Borrow button

**Kết quả mong đợi:**
- The system should reject the borrowing request and display the message:
“Maximum borrow limit reached (3 books)”
- No new borrowing transaction should be created.

**Kết quả thực tế:**
- The system still allows the member to borrow the 4th book successfully
- No warning or error message is displayed

**Tác động:**
- This issue violates the core business rule of the library system regarding the maximum borrowing limit.
- Users can borrow more books than permitted, causing inaccurate borrowing records and reducing control over library resources.

**Mức độ**
- High

**Minh chứng:**
<img width="2435" height="1600" alt="image" src="https://github.com/user-attachments/assets/01dd3928-33eb-47ba-84e4-059729ac5cfa" />

**Đề xuất xử lý:**
- Add validation before creating a borrowing transaction.
- If the current borrowed book count is greater than or equal to the maximum limit, the borrowing request should be rejected.

---

## BUG-03

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-03 |
| **TC liên quan** | TC-28 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Đình Thi |
| **Ngày phát hiện** | 19/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System displays “Invalid Email” for valid email format during member creation

**Môi trường:**
- Browser: Chrome 148
- Operating System: Window
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User is logged into the system as Librarian
- Member creation page is accessible

**Bước tái hiện:**
1. Log into the Library Management System as Librarian
2. Access Add Member
3. Enter valid member information
4. Input email: user@domain.com 
5. Click Add Member.

**Kết quả mong đợi:**
- The system should create the member successfully
- No validation error should be displayed

**Kết quả thực tế:**
- The system displays: “Invalid Email”
- The member account is not created

**Tác động:**
- Valid member data cannot be added to the system
- This prevents librarians from creating new members and affects member management functionality

**Mức độ**
- Medium

**Minh chứng:**
<img width="2530" height="1380" alt="image" src="https://github.com/user-attachments/assets/7cfb2c6a-f517-4c71-b0c0-a2f72a17b6a6" />

**Đề xuất xử lý:**
- Review email validation logic.
- The system should accept valid email formats such as: user@domain.com  and reject only invalid formats

---

## BUG-04

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-04 |
| **TC liên quan** | TC-29 |
| **REQ liên quan** | REQ-07 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Minh Quang |
| **Ngày phát hiện** | 19/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System allows member creation with email missing “.” in domain instead of displaying validation error

**Môi trường:**
- Browser: Chrome 148
- Operating System: Window
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User is logged into the system as Librarian
- Member creation page is accessible

**Bước tái hiện:**
1. Log into the Library Management System as Librarian
2. Access Add Member
3. Enter valid member information
4. Input email: user@domaincom 
5. Click Add Member

**Kết quả mong đợi:**
- The system should reject the input and display an email validation message such as: “Invalid Email”
- The member account should not be created

**Kết quả thực tế:**
- The system creates the member successfully
- No validation message is displayed

**Tác động:**
- Invalid email data can be stored in the system
- This affects data quality and may cause failures in notifications and member communication

**Mức độ**
- Medium

**Minh chứng:**
<img width="2536" height="1392" alt="image" src="https://github.com/user-attachments/assets/60fee26a-97ae-4799-b444-99a02d9835c6" />
<img width="2546" height="1393" alt="image" src="https://github.com/user-attachments/assets/591abe73-759d-492f-a2d4-b3aa0bd34352" />

**Đề xuất xử lý:**
- Add email format validation before member creation
- The system should verify the existence of: @ and . in the domain part


## BUG-05

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-05 |
| **TC liên quan** | TC-32 |
| **REQ liên quan** | REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Đức Anh Tuấn |
| **Ngày phát hiện** | 19/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System allows members to view other members’ borrowing records instead of denying access

**Môi trường:**
- Browser: Chrome 148
- Operating System: macOS
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User is logged into the system as Member MEM002
- Borrow records exist for MEM003
- Borrow record query function is accessible

**Bước tái hiện:**
1. Log into the system as MEM002
2. Navigate to Borrow Records.
3. Search or access borrowing records of MEM003
4. Open the displayed borrowing records.

**Kết quả mong đợi:**
- The system should deny access and display a message such as: “Access Denied”
- MEM002 should only be allowed to view their own borrowing records

**Kết quả thực tế:**
- MEM002 can view borrowing records belonging to MEM004 successfully
- No authorization restriction is applied

**Tác động:**
- This issue violates access control rules and exposes other users’ borrowing information
- Unauthorized users can access data that should be private, affecting confidentiality and system security

**Mức độ**
- High

**Minh chứng:**
<img width="1919" height="869" alt="image" src="https://github.com/user-attachments/assets/ddebbaaf-e29c-4f17-9fdd-ea5e20574870" />

**Đề xuất xử lý:**
- Implement authorization validation before displaying borrowing records
- Rule:
    Member → view own records only
    Librarian → view all records
- If the logged-in member attempts to access another member’s records, the system should reject the request

## BUG-06

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-06 |
| **TC liên quan** | TC-33 |
| **REQ liên quan** | REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Đình Thi |
| **Ngày phát hiện** | 19/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System allows members to access and modify other members’ borrowing records

**Môi trường:**
- Browser: Chrome 148
- Operating System: Window
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- User is logged into the system as MEM006
- Borrow records exist for MEM003
- Borrow record management function is accessible

**Bước tái hiện:**
1. Log into the system as MEM006
2. Open the borrow record URL belonging to MEM003
3. Access the record details page
4. Attempt to edit the borrow record or return the borrowed book.

**Kết quả mong đợi:**
- The system should deny access
- The user should receive a message such as: “Access Denied”
- No modification, update, or return operation should be allowed

**Kết quả thực tế:**
- MEM006 successfully accesses MEM003’s borrowing record
- The member can directly modify record information and perform update operations

**Tác động:**
- This issue violates authorization rules and allows unauthorized modification of another member’s borrowing data
- It affects:
    + Data confidentiality
    + Data integrity
    + System security
- Users can alter records that do not belong to them.

**Mức độ**
- High

**Minh chứng:**
<img width="1919" height="926" alt="image" src="https://github.com/user-attachments/assets/45538c62-555c-44a3-bfca-8eaca023df2c" />

**Đề xuất xử lý:**
- Implement authorization validation before displaying and updating records
- Rules:
    Member:
    + View own records only
    + Modify own records only

    Librarian:
    + Full access
    + If the logged-in member attempts to access another member’s records, the system should reject the request
- Any attempt to access another member’s record should be blocked

---
## BUG-07

| Thuộc tính | Chi tiết |
|-----------|---------|
| **Mã lỗi** | BUG-07 |
| **TC liên quan** | TC-35 |
| **REQ liên quan** | REQ-08 |
| **Mức độ** | High |
| **Người phát hiện** | Nguyễn Đức Anh Tuấn |
| **Ngày phát hiện** | 19/05/2026 |
| **Trạng thái** | Open |

**Tiêu đề:**
System displays book status as “Borrowing” but no corresponding borrow record exists

**Môi trường:**
- Browser: Chrome 148
- Operating System: macOS
- Interface Language: Vietnamese

**Điều kiện tiên quyết:**
- Book BOOK006 exists in the system.
- Book status is displayed as: “Borrowing”
- Borrow record list is accessible

**Bước tái hiện:**
1. Open Book Details of BOOK006.
2. Verify the displayed book status.
3. Open Borrow Records list.
4. Search for records corresponding to BOOK006.
5. Compare the displayed book status with existing borrow records.

**Kết quả mong đợi:**
- The system should display a corresponding borrow record for BOOK006 when the book status is: “Borrowing”
- Borrow status and borrow records must remain consistent.

**Kết quả thực tế:**
- Book BOOK006 is displayed with status: “Borrowing”
- However, no corresponding borrow record exists in the system.

**Tác động:**
- TThe system contains inconsistent borrowing data.
- Book inventory status indicates the book is borrowed, but the transaction record is missing.
- This affects:
    + Borrow history tracking
    + Inventory management
    + Data consistency and auditing

**Mức độ**
- High

**Minh chứng:**
<img width="1888" height="131" alt="image" src="https://github.com/user-attachments/assets/5d50a834-7a27-42f0-b818-fea0bbd9d2e3" />
<img width="1919" height="822" alt="image" src="https://github.com/user-attachments/assets/0a840fe7-85ae-498b-a395-7cbbafce7851" />

**Đề xuất xử lý:**
- Verify synchronization logic between book status and borrowing records 
- Rule:
    Book status = Borrowing
    → Corresponding borrow record must exist

