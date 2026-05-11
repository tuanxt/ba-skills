---
name: uat-test-planning
description: Use this skill for planning and executing User Acceptance Testing (UAT) — defining test scenarios, writing test cases, organizing UAT sessions, tracking defects, and managing sign-off. Triggers on phrases like "UAT", "User Acceptance Testing", "kiểm thử nghiệp vụ", "kiểm thử chấp nhận", "test case", "test scenario", "test plan", "kế hoạch test", "go-live readiness", "sign-off", "defect tracking", "bug log". Use proactively before any production release, especially when there are external stakeholders or end users who need to validate the product matches their needs.
---

# UAT — User Acceptance Testing

UAT là **bài kiểm tra cuối** trước go-live, do **user thật** (không phải QA chuyên nghiệp) thực hiện, để xác nhận sản phẩm đáp ứng nhu cầu nghiệp vụ. BA thường chủ trì UAT vì hiểu yêu cầu rõ nhất.

## UAT vs các loại test khác

| Loại test | Ai làm | Mục đích | Stage |
|---|---|---|---|
| **Unit test** | Dev | Function/component chạy đúng | Lúc code |
| **Integration test** | Dev | Các module nối với nhau OK | Sau code |
| **System test** | QA | Toàn hệ thống đúng spec | Pre-release |
| **UAT** | **End user / BA** | **Đáp ứng nhu cầu nghiệp vụ** | **Trước go-live** |
| **Smoke test** | QA | Major function OK sau deploy | Sau deploy |
| **Regression test** | QA | Bug cũ không quay lại | Mỗi release |

→ UAT khác QA testing ở chỗ: QA test theo **spec**, UAT test theo **mục tiêu kinh doanh** + **kịch bản thực tế**.

## Quy trình UAT chuẩn

### Phase 1: Planning (Trước UAT 2-3 tuần)

#### 1.1 UAT Plan Document

```markdown
# UAT Plan: [Tên dự án]

## 1. Mục tiêu UAT
- Xác nhận hệ thống đáp ứng BR1-BR15
- Validate UX với user thật
- Identify gap so với spec
- Sign-off cho go-live

## 2. Scope
**In-scope**:
- Module Đặt món (full flow)
- Module Thanh toán (VNPay, COD)
- Module Theo dõi đơn

**Out-of-scope**:
- Module Admin (sẽ UAT phase 2)
- Báo cáo BI

## 3. Phương pháp
- Scenario-based testing (kịch bản thực tế)
- 10 user tham gia (5 KH cá nhân, 3 NV nhà hàng, 2 admin)
- Test trên môi trường UAT (production-like)
- 5 ngày làm việc

## 4. Entry Criteria (điều kiện BẮT ĐẦU UAT)
- [ ] Hoàn thành System Testing với pass rate > 95%
- [ ] Không có Critical/Blocker bug open
- [ ] UAT environment ready & stable
- [ ] Test data đã được prepare
- [ ] User account UAT đã tạo
- [ ] Training cho UAT participant đã xong

## 5. Exit Criteria (điều kiện KẾT THÚC UAT)
- [ ] Tất cả test case đã chạy
- [ ] Pass rate ≥ 95%
- [ ] Không có Critical/High defect chưa fix
- [ ] Stakeholder sign-off

## 6. Roles & Responsibilities
| Role | Người | Trách nhiệm |
|---|---|---|
| UAT Lead | BA Linh | Coordinate, viết report |
| UAT Tester | 10 user | Execute test, log defect |
| Dev Support | Tech Lead Khoa | Fix defect, hotline |
| QA Support | QA Mai | Verify defect fix |
| Sponsor | Anh Hùng | Final sign-off |

## 7. Tools
- Test management: TestRail / Jira / Google Sheet
- Defect tracking: Jira
- Communication: Slack channel #uat-project-x
- Recording: Loom (cho complex bug)

## 8. Schedule
| Tuần | Hoạt động |
|---|---|
| W-2 | Viết test scenario, prepare data |
| W-1 | Train UAT participants, dry run |
| W1 (M-F) | Execute UAT |
| W2 Mon-Wed | Fix defect, re-test |
| W2 Thu-Fri | Final regression, sign-off |
```

#### 1.2 Test Scenarios & Test Cases

**Test Scenario** = kịch bản nghiệp vụ end-to-end
**Test Case** = bước cụ thể trong scenario

```markdown
## Scenario UAT-S01: Khách lần đầu đặt món

**Persona**: Chị Lan, 32t, nội trợ, lần đầu dùng app
**Goal**: Đặt 1 đơn cơm trưa cho gia đình
**Pre-condition**: 
- App đã cài
- Chưa có tài khoản
- Có điện thoại nhận OTP

### Test Cases:

#### TC-001: Đăng ký tài khoản mới
- Steps:
  1. Mở app
  2. Bấm "Đăng ký"
  3. Nhập SĐT: 0901234567
  4. Bấm "Gửi OTP"
  5. Nhập OTP nhận được
  6. Hoàn tất thông tin: tên, ngày sinh
- Expected:
  - SĐT validate đúng format
  - OTP nhận trong < 30s
  - Tài khoản được tạo, tự động đăng nhập
  - Chuyển sang màn Onboarding
- Actual: [user/BA điền sau khi test]
- Status: Pass / Fail / Blocked
- Defect ID: [nếu fail]

#### TC-002: Tìm nhà hàng gần
- Steps:
  1. Cho phép quyền vị trí
  2. Xem danh sách nhà hàng
- Expected:
  - Hiển thị 10+ nhà hàng trong bán kính 5km
  - Sắp xếp theo khoảng cách tăng dần
  - Mỗi card hiện: tên, hình, rating, khoảng cách
- ...

#### TC-003 → TC-010: ... (đặt món, thanh toán VNPay, xem trạng thái...)

### Acceptance Criteria for Scenario:
- ✅ Hoàn thành toàn bộ flow trong < 5 phút
- ✅ User không cần hỏi BA câu nào
- ✅ Không có lỗi UX nghiêm trọng (không tìm thấy button, nhầm flow)
```

### Phase 2: Preparation (1 tuần trước)

- [ ] **Test data**: Tạo data như production (10 nhà hàng thật, 50+ món, có giá thật, có hình thật)
- [ ] **UAT environment**: Deploy code mới nhất, smoke test
- [ ] **User accounts**: Tạo cho mỗi UAT tester
- [ ] **Training session** (1-2 tiếng):
  - Demo nhanh hệ thống
  - Hướng dẫn log defect (format chuẩn)
  - Phân chia scenario cho từng người
- [ ] **Test devices**: iOS + Android + Web, các size màn hình khác nhau
- [ ] **Dry run**: BA tự chạy 1 lần để verify environment

### Phase 3: Execution (UAT Week)

#### Daily UAT cycle

```
9:00  Daily UAT standup (15p)
       - Hôm qua test gì, pass/fail
       - Hôm nay test gì
       - Blocker?

9:15  Execute test
12:00 Lunch
13:30 Continue test
16:00 Defect triage với dev team
17:00 Update test status
```

#### Defect Log Template

| ID | Date | Reporter | Severity | Priority | Title | Steps | Expected | Actual | Screenshot | Status | Assignee | Fixed in |
|----|------|----------|----------|----------|-------|-------|----------|--------|------------|--------|----------|----------|
| D-001 | 11/05 | Lan | Critical | P1 | App crash khi click "Thanh toán" | 1.Login 2.Add món 3.Click pay | Mở cổng VNPay | App crash | [link] | Open | Khoa | - |

**Severity** (mức độ nghiêm trọng kỹ thuật):
- **Critical**: System down, data loss, security breach
- **High**: Major function broken, không có workaround
- **Medium**: Function lỗi nhưng có workaround
- **Low**: Cosmetic, typo, minor UX

**Priority** (mức độ gấp về business):
- **P1**: Fix ngay, block UAT
- **P2**: Fix trước go-live
- **P3**: Fix khi có thời gian
- **P4**: Backlog cho phase sau

### Phase 4: Triage & Fix

Họp Defect Triage hàng ngày:
- Review defect mới
- Confirm severity/priority
- Assign cho dev
- Set ETA

Sau fix:
- Dev báo "Fixed in build X"
- QA verify trên UAT env
- UAT tester re-test
- Close hoặc Reopen

### Phase 5: Sign-off

#### UAT Summary Report

```markdown
# UAT Summary Report: [Project]

## Tổng quan
- Tổng test case: 120
- Pass: 115 (95.8%)
- Fail: 5 (4.2%)
- Blocked: 0

## Defect
- Critical: 0 open, 2 closed
- High: 1 open (P3, fix sau go-live), 5 closed
- Medium: 3 open (P3-P4), 8 closed
- Low: 4 open (P4 — cosmetic, list ra để fix dần)

## Go-live recommendation
✅ **APPROVED** — Sẵn sàng go-live với note:
- Fix 1 High open trong sprint sau go-live
- Cosmetic defect có thể release later

## Sign-off

| Role | Name | Signature | Date |
|---|---|---|---|
| Sponsor | Anh Hùng | ✓ | 11/05/2026 |
| PO | Chị Lan | ✓ | 11/05/2026 |
| BA | Linh | ✓ | 11/05/2026 |
| Tech Lead | Khoa | ✓ | 11/05/2026 |
```

## Test Scenarios — Cách thiết kế tốt

### 1. Cover Happy Path TRƯỚC
80% test scenarios → happy path (đúng quy trình)
20% → edge case, error case

### 2. Đa dạng persona
Khác nhau về: tuổi, tech-savvy, device, vị trí, mục đích

### 3. Realistic data
Đừng dùng "Test User", "Lorem ipsum" → dùng tên Việt thật, địa chỉ thật, giá hợp lý

### 4. End-to-end > Unit
UAT test **journey**, không test từng button. 1 scenario nên cover 5-15 steps.

### 5. Bao gồm Negative test
- Nhập SĐT sai format
- Đặt món khi nhà hàng đóng
- Mất mạng giữa chừng
- Hết tiền trong tài khoản
- Voucher hết hạn

### 6. Test mọi điểm tích hợp
- Thanh toán (VNPay, MoMo, ZaloPay)
- SMS OTP
- Push notification
- Google Maps
- Email

## Chọn UAT participants

**Số lượng**: 5-15 người là sweet spot
- < 5: không đủ diverse, bias cao
- > 15: khó coordinate, diminishing return

**Tiêu chí chọn**:
- ✅ Đại diện target user (đúng persona)
- ✅ Sẵn sàng dành thời gian (cam kết 1-2 buổi)
- ✅ Sẵn sàng phản hồi thẳng (không nịnh)
- ❌ KHÔNG phải dev/QA của dự án (bias)
- ❌ KHÔNG phải người đã thấy product nhiều lần

**Pro tip**: Mời 1-2 người **không ưa dự án** (skeptical stakeholder). Họ sẽ tìm ra bug mà champion bỏ qua.

## Mẹo facilitate UAT session

### Trước session
- Email reminder 1 ngày trước
- Gửi link UAT environment, account, hướng dẫn
- Confirm device họ sẽ dùng

### Trong session
- **Đừng dạy quá nhiều** — để họ tự khám phá (mục đích test UX)
- **Không bias** — đừng nói "thử nút màu xanh" → nói "đặt 1 đơn cơm gà"
- **Quan sát hành vi** — họ click sai? phân vân ở đâu? thở dài ở bước nào?
- **Ghi chú quote** — "Em không biết nút này để làm gì" → quote nguyên văn
- **Record screen** nếu họ cho phép

### Sau session
- Debrief ngay (15 phút) — họ thấy thế nào? Điểm nào bực bội nhất?
- Cảm ơn họ! Tặng voucher nhỏ
- Tổng hợp finding trong 24h

## Anti-patterns

❌ **UAT do dev/QA chạy** → mất ý nghĩa, họ biết hệ thống quá rõ
❌ **UAT 1 ngày trước go-live** → không kịp fix
❌ **Không có exit criteria** → UAT kéo dài vô tận hoặc rush
❌ **Bỏ qua negative test** → user thật sẽ tìm ra cách break system
❌ **Sign-off bằng miệng** → khi có issue sau go-live, ai chịu?
❌ **UAT trên môi trường dev** → data không thật, không reproducible
❌ **Không document defect chuẩn** → dev không reproduce được
❌ **Treat UAT như formality** → check box, không thật sự test

## Áp dụng cho solo developer

Solo dev "không có UAT" — sai. Vẫn cần:

**Mini-UAT cho solo dev:**

1. **Tìm 3-5 beta tester** từ target audience (Facebook Group, bạn bè đúng persona)
2. **Tạo Google Form** với scenarios:
   - "Hãy thử đặt 1 đơn cơm trưa"
   - "Hãy thử thanh toán VNPay"
   - "Hãy thử huỷ đơn"
3. **Gửi TestFlight (iOS) / Internal track (Android)**
4. **Schedule 30 phút call** với mỗi tester
5. **Quan sát qua share screen** — họ click đâu? phân vân ở đâu?
6. **Tổng hợp top 10 issue** → fix trước go-live

**Quy tắc 5 user**: Nielsen research → 5 user phát hiện 80% UX issue. Đừng đợi 50 user.

**Tool gọn cho solo dev:**
- **TestFlight** + **Maze** (UX testing)
- **Notion** làm bug tracker
- **Loom** record session
- **Google Form** survey post-test

## Output cuối: UAT Sign-off Email

```
Subject: [Project X] UAT Sign-off — Approved for Go-live

Kính gửi anh/chị,

Chúng ta đã hoàn tất UAT cho [Project X] với kết quả:
- Pass rate: 95.8% (115/120 test cases)
- 0 Critical defect open
- Approval cho go-live ngày 15/05/2026

Chi tiết trong báo cáo: [link]

Risk cần lưu ý sau go-live:
1. 1 High defect (P3) — sẽ fix trong sprint 1 sau go-live
2. 4 Cosmetic issue — backlog

Xin xác nhận sign-off bằng cách reply email này.

Trân trọng,
BA Team
```
