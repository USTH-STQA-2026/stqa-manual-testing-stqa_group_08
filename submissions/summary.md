# Test Summary Report
---

## 1. Group Information

| Field | Details |
|-----|----------|
| **Group** | GROUP 8 |
| **Class** | ICT |
| **Report Date** | 06/06/2026 |
| **System Under Test** | https://stqa.rbc.vn — v1.0 |

---

## 2. Results Overview

| Metric | Value |
|--------|-------|
| Total Test Cases | 48 |
| Pass | 36 |
| Fail | 11 |
| Blocked | 1 |
| Not Run | 0 |
| **Pass Rate** | **75%** |
| **Total bugs found** | **7** |

### Distribution by Functional Group

| Functional Group | TCs | Pass | Fail | Blocked | Bug IDs | Pass Rate | Rating |
|-----------------|-----|------|------|---------|---------|-----------|--------|
| Login | 6 | 6 | 0 | 0 | — | 100% | Good |
| View Book List | 2 | 2 | 0 | 0 | — | 100% | Good |
| Search & Filter Books | 6 | 5 | 1 | 0 | BUG-01 | 83.33% | Minor issue |
| Borrow Book | 7 | 5 | 2 | 0 | BUG-02, BUG-03 | 71.43% | Needs fixing |
| Return Book | 4 | 2 | 2 | 0 | BUG-04 | 50% | Needs fixing |
| Overdue Handling | 4 | 4 | 0 | 0 | — | 100% | Good |
| Member Management | 10 | 5 | 4 | 1 | BUG-05, BUG-06 | 50% | Critical issues |
| Borrow Record Lookup | 9 | 8 | 1 | 0 | BUG-07 | 88.89% | Needs fixing |
| **Total** | **48** | **36** | **11** | **1** | | **75%** | |

### Bug Distribution by Severity
 
| Severity | Count | Bug IDs |
|----------|-------|---------|
| High | 5 | BUG-02, BUG-03, BUG-05, BUG-06, BUG-07 |
| Medium | 1 | BUG-01 |
| Low | 1 | BUG-04 |

---

## 3. Test Design Techniques Used

| Technique | Applied to | No. of TCs | How it was applied |
|-----------|-----------|------------|-------------------|
| Equivalence Partitioning (EP) | REQ-01 to REQ-08 (all) | 46 | Inputs were partitioned into valid/invalid classes (e.g., valid email vs. unregistered email vs. empty). One representative value was tested per partition to avoid redundancy. |
| Boundary Value Analysis (BVA) | REQ-04, REQ-05, REQ-06, REQ-08 | 5 | Tested at the exact borrow limit boundary (2 books = allowed, 3 books = blocked), at the due date boundary (dueDate = currentDate per REQ-06), and at the edge of empty/single/multiple record counts for borrow record lookup. |
| Decision Table | REQ-04 | 1 | All combinations of borrow conditions (suspended, expired, book availability, borrow limit) were mapped into a decision table with 5 rules to ensure no condition combination was missed. |

---

## 4. Software Quality Analysis

### 4.1. Strengths
- **Login** is fully functional and correctly handles all error cases (empty fields, wrong email, wrong password) with accurate, specific error messages.
- **View Book List** works correctly for both roles, displays all 20 books with accurate information, and reflects borrow/return state changes in real time without a page refresh.
- **Search by title and author** works correctly and is properly case-insensitive as required by the SRS.
- **Overdue Handling** correctly identifies and updates overdue records when triggered by the librarian, and correctly limits member visibility to their own records.
- **Core return flow** (on-time return) works correctly — record status and book status both update as expected.
- **Role-based access control** for the Member tab is correctly enforced — members do not see the "Add Member" button.

### 4.2. Weaknesses
- **Member Management is the most defective module** (44.44% pass rate). BUG-06 causes the email validator to misfire on valid, empty, and duplicate emails alike, blocking member creation entirely and cascading into a Blocked state for phone validation (TC-07).
- **Privacy control in Borrow Record Lookup is broken** (BUG-07) — a logged-in member can query and read another member's full borrow history simply by entering their Member ID, which is a direct violation of REQ-08.
- **The 3-book borrow limit is not enforced** (BUG-02) — members can borrow a 4th book without any error, violating a core business rule defined in REQ-04.
- **Suspended and expired account statuses are conflated** (BUG-03) — the system shows the "expired" message for suspended accounts, which would mislead users and generate incorrect support requests.
- **Category filter is case-sensitive** (BUG-01) — contradicts the SRS requirement, silently returning no results for valid input.
- **No overdue warning on return** (BUG-04) — returning a late book gives no feedback to the user, making it impossible for librarians or members to know a return was overdue.

---

## 5. Bug Fix Priority Recommendations

| Order | Bug ID | Severity | Reason |
|-------|--------|----------|--------|
| 1 | BUG-06 | High | Completely blocks member creation — a core librarian workflow — and cascades to make 4 test cases untestable. Must be fixed first to unblock BUG-05 and TC-07 retesting. |
| 2 | BUG-07 | High | Active privacy breach: any member can read any other member's borrow history. Violates data privacy requirements and poses reputational risk. |
| 3 | BUG-02 | High | The 3-book borrow limit is a core business rule (REQ-04). Allowing a 4th borrow corrupts borrow state and undermines inventory control. |
| 4 | BUG-05 | High | Invalid emails (missing domain dot) pass validation and are written to the system, causing dirty data. Fix is dependent on BUG-06 being resolved first. |
| 5 | BUG-03 | High | Suspended accounts receive the "expired" error message — misleading but borrowing is still correctly rejected, so operational impact is limited to user confusion. |
| 6 | BUG-01 | Medium | Case-sensitive category filter degrades usability but does not block any workflow. |
| 7 | BUG-04 | Low | Overdue warning is missing on return. The return itself succeeds correctly, so operational impact is limited. |

---

## 6. Conclusion

**The system is not ready for release in its current state.**
 
Of the 7 bugs found, 5 are High severity. Two bugs in particular are hard blockers:
 
- **BUG-07** is a privacy violation — members can access other members' personal borrow data — which would be unacceptable in any production environment.
- **BUG-06** completely prevents the librarian from adding new members, disabling a core administrative function of the system.
Additionally, **BUG-02** undermines the integrity of the borrowing system by allowing the 3-book limit to be bypassed.

Additionally, **BUG-02** undermines the integrity of the borrowing system by allowing the 3-book limit to be bypassed.
