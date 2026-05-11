---
name: brd-writer
description: Use this skill for writing Business Requirements Documents (BRD) — high-level documents capturing business needs, objectives, scope, stakeholders, and success criteria before any technical design. Triggers on phrases like "BRD", "Business Requirements Document", "tài liệu yêu cầu nghiệp vụ", "viết BRD", "business case", "scope document", "project charter", "tài liệu đề xuất dự án", "định nghĩa yêu cầu nghiệp vụ". Use proactively at project kickoff or when business stakeholders need to sign off on what will be built — BEFORE writing SRS, user stories, or design.
---

# BRD — Business Requirements Document

BRD là tài liệu **cấp cao nhất** trong dự án, viết bằng ngôn ngữ nghiệp vụ (không kỹ thuật). Mục đích: align tất cả stakeholder về **WHY** và **WHAT**, chưa nói **HOW**.

## BRD vs SRS vs FRD — Đừng nhầm lẫn

| Tài liệu | Đối tượng | Trả lời câu hỏi | Người viết chính |
|---|---|---|---|
| **BRD** (Business Requirements) | Stakeholder, sponsor, exec | **Tại sao** làm và **đạt được gì** | BA / PM |
| **FRD** (Functional Requirements) | Team thiết kế, BA, PM | Hệ thống **phải làm gì** | BA |
| **SRS** (Software Requirements Spec) | Dev, QA, architect | Phần mềm **phải làm như thế nào** | BA + Tech Lead |

→ Thứ tự thông thường: **BRD → FRD → SRS → User Stories**

## Template BRD chuẩn

```markdown
# Business Requirements Document
**Tên dự án**: [Tên]
**Phiên bản**: 1.0
**Ngày**: [DD/MM/YYYY]
**Tác giả**: [Tên BA]
**Sponsor**: [Tên người chịu trách nhiệm cao nhất]
**Status**: Draft / In Review / Approved

---

## 1. Tóm tắt điều hành (Executive Summary)
[1-2 đoạn ngắn gọn: vấn đề, giải pháp đề xuất, lợi ích kỳ vọng, ngân sách dự kiến]

## 2. Bối cảnh kinh doanh (Business Context)

### 2.1 Vấn đề hiện tại
[Mô tả pain point hiện tại, có số liệu kèm theo nếu có]
- Hiện trạng: ...
- Tác động: ... (mất bao nhiêu doanh thu/thời gian/khách hàng)
- Lý do cần giải quyết ngay: ...

### 2.2 Cơ hội
[Cơ hội kinh doanh nếu giải quyết được vấn đề]

### 2.3 Bối cảnh thị trường (nếu có)
[Competitor, xu hướng, regulation mới]

## 3. Mục tiêu dự án (Business Objectives)

Sử dụng nguyên tắc **SMART**:
- **S**pecific — Cụ thể
- **M**easurable — Đo được
- **A**chievable — Khả thi
- **R**elevant — Liên quan
- **T**ime-bound — Có deadline

**Ví dụ:**
- **BO1**: Giảm thời gian xử lý đơn hàng từ 15 phút xuống 5 phút trong vòng Q2/2026
- **BO2**: Tăng tỷ lệ giữ chân khách hàng từ 40% lên 60% sau 6 tháng go-live
- **BO3**: Giảm chi phí vận hành 30% so với hệ thống hiện tại trong năm đầu

## 4. Phạm vi dự án (Scope)

### 4.1 Trong phạm vi (In-Scope)
- ✅ Tính năng A: ...
- ✅ Tính năng B: ...
- ✅ Tích hợp với hệ thống X

### 4.2 Ngoài phạm vi (Out-of-Scope)
- ❌ Tính năng C (làm trong phase 2)
- ❌ Mobile app (chỉ web phase 1)
- ❌ Báo cáo BI nâng cao

> **Quan trọng**: Mục Out-of-Scope thường bị bỏ qua nhưng cực kỳ giá trị — chống scope creep.

### 4.3 Giả định (Assumptions)
- Khách hàng có internet ổn định
- Hệ thống ERP hiện tại sẽ duy trì hoạt động
- Team có đủ kiến thức về React/Node.js

### 4.4 Ràng buộc (Constraints)
- Budget tối đa: 500 triệu VNĐ
- Deadline cứng: Q3/2026 (do regulation mới)
- Phải tuân thủ Nghị định 13/2023 về bảo vệ dữ liệu cá nhân
- Phải tương thích với hệ thống kế toán Misa hiện tại

## 5. Stakeholder

| Vai trò | Tên / Phòng ban | Trách nhiệm | Mức ảnh hưởng |
|---|---|---|---|
| Sponsor | Giám đốc kinh doanh | Phê duyệt budget, scope | Cao |
| Product Owner | Trưởng phòng SP | Quyết định feature ưu tiên | Cao |
| End user | Nhân viên CSKH (20 người) | Người dùng cuối | Trung bình |
| Stakeholder phụ | Phòng kế toán | Cung cấp yêu cầu báo cáo | Thấp |

## 6. Yêu cầu nghiệp vụ cấp cao (Business Requirements)

Viết ở mức **business**, không kỹ thuật. Đánh số để truy vết.

- **BR1**: Hệ thống phải cho phép khách hàng tự đặt món và thanh toán online 24/7
- **BR2**: Nhà hàng phải nhận đơn ngay khi khách thanh toán thành công
- **BR3**: Admin phải xem được báo cáo doanh thu theo ngày/tuần/tháng
- **BR4**: Khách hàng phải tra cứu được lịch sử đơn hàng tối thiểu 2 năm
- **BR5**: Hệ thống phải hỗ trợ tiếng Việt và tiếng Anh

## 7. Phân tích lợi ích (Benefits / Business Case)

### 7.1 Lợi ích hữu hình (Tangible)
| Lợi ích | Năm 1 | Năm 2 | Năm 3 |
|---|---|---|---|
| Tăng doanh thu | 500tr | 1.2 tỷ | 2 tỷ |
| Giảm chi phí nhân sự | 200tr | 250tr | 300tr |
| **Tổng** | 700tr | 1.45 tỷ | 2.3 tỷ |

**Investment**: 500tr (one-time) + 50tr/năm vận hành
**ROI**: ~330% sau 3 năm
**Payback period**: ~8 tháng

### 7.2 Lợi ích vô hình (Intangible)
- Tăng trải nghiệm khách hàng
- Tăng độ nhận diện thương hiệu
- Dữ liệu để phân tích hành vi khách hàng

## 8. Tiêu chí thành công (Success Criteria / KPI)

Cách đo lường sau khi go-live:

| KPI | Baseline (hiện tại) | Target (sau 6 tháng) | Đo bằng cách |
|---|---|---|---|
| Số đơn/ngày | 50 | 200 | Dashboard hệ thống |
| Tỷ lệ huỷ đơn | 15% | < 5% | Dashboard |
| NPS khách hàng | N/A | > 50 | Survey hàng quý |
| Uptime | N/A | > 99.5% | Monitoring tool |

## 9. Phân tích rủi ro (Risks)

| ID | Rủi ro | Khả năng | Tác động | Mitigation |
|---|---|---|---|---|
| R1 | Khách hàng không quen công nghệ | Cao | Trung bình | Onboarding video + hotline support |
| R2 | Tích hợp VNPay không ổn định | Trung bình | Cao | Có fallback sang MoMo + COD |
| R3 | Vendor giao hàng huỷ giữa chừng | Thấp | Cao | Ký hợp đồng SLA, có vendor backup |

## 10. Roadmap & Timeline (cấp cao)

| Phase | Thời gian | Nội dung chính | Deliverable |
|---|---|---|---|
| Discovery | Tháng 1 | Phỏng vấn, BRD, FRD | BRD approved |
| Design | Tháng 2 | UI/UX, kiến trúc | Mockup + SRS |
| Build MVP | Tháng 3-4 | Core features | App chạy được |
| UAT | Tháng 5 | Test với khách thật | Sign-off |
| Go-live | Tháng 6 | Rollout dần | Production |

## 11. Phê duyệt (Sign-off)

| Vai trò | Tên | Chữ ký | Ngày |
|---|---|---|---|
| Sponsor | | | |
| Product Owner | | | |
| BA | | | |
| Tech Lead | | | |
```

## Mẹo viết BRD hiệu quả

### 1. Ngôn ngữ business, không kỹ thuật

❌ **Tệ**: "Hệ thống dùng React Native + Supabase với JWT auth"
✅ **Tốt**: "Khách hàng phải đăng nhập an toàn và sử dụng được trên cả iOS và Android"

### 2. Truy vết được (Traceability)

Đánh số rõ ràng (BR1, BR2...) để sau này từ Story/Test ngược về được BRD.

### 3. Quantify khi có thể

❌ "Tăng doanh thu" → ✅ "Tăng doanh thu 30% trong 12 tháng"
❌ "Khách hài lòng hơn" → ✅ "NPS từ 30 lên 50"

### 4. Cẩn thận với Assumptions

Assumption sai = dự án thất bại. Ví dụ: "Khách có smartphone" — đúng với Gen Z, sai với khách 60+ tuổi ở quê.

### 5. Out-of-Scope rất quan trọng

Stakeholder thường mặc định "chắc làm cả cái này nữa". List rõ những gì KHÔNG làm trong scope này.

## Quy trình tạo BRD

1. **Pre-work**: Đọc tài liệu cũ, research industry
2. **Stakeholder interview** (xem skill `requirement-elicitation`)
3. **Draft v0.1**: Viết theo template
4. **Internal review**: Tech lead, PM review
5. **Stakeholder review**: Họp duyệt với sponsor
6. **Revise** dựa trên feedback
7. **Sign-off**: Có chữ ký formal (hoặc email confirmation)
8. **Baseline**: Lock version, mọi thay đổi sau đó phải qua Change Request

## Áp dụng cho solo developer

Solo dev thường skip BRD vì "tôi tự hiểu". Nhưng:

- **Viết BRD nhẹ (2-3 trang)** vẫn cực kỳ giá trị → ép bản thân clarify mục tiêu kinh doanh
- Đặc biệt khi pitch cho investor, đăng ký funding, hoặc tuyển co-founder
- Lưu trong `docs/BRD.md` của repo
- Format gọn: chỉ cần section 1, 3, 4, 6, 8 — bỏ qua các phần formal

**Template gọn cho solo dev:**
```markdown
# Mini BRD: [Tên app]

## Vấn đề
[1 đoạn]

## Giải pháp
[1 đoạn]

## Target user
[Persona ngắn]

## Mục tiêu 6 tháng (SMART)
- ...

## Trong scope MVP
- ...

## Ngoài scope (phase sau)
- ...

## Success criteria
- ...
```
