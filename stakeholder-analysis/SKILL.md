---
name: stakeholder-analysis
description: Use this skill for identifying, mapping, and managing stakeholders — including stakeholder discovery, power/interest matrix, RACI charts, communication planning, and influence strategies. Triggers on phrases like "stakeholder", "stakeholder analysis", "phân tích bên liên quan", "RACI", "power interest grid", "ma trận quyền lực", "communication plan", "kế hoạch giao tiếp", "ai là người quyết định", "buy-in", "alignment", "engage stakeholder". Use proactively at project kickoff and whenever the project has multiple decision-makers or there's misalignment — knowing WHO decides and HOW to engage them prevents projects from stalling.
---

# Stakeholder Analysis

Dự án thất bại thường không vì lý do kỹ thuật — mà vì **không quản lý được kỳ vọng của người liên quan**. Skill này giúp identify đúng người, hiểu họ muốn gì, và lên kế hoạch giao tiếp hiệu quả.

## Stakeholder là ai?

Bất kỳ ai **ảnh hưởng đến** hoặc **bị ảnh hưởng bởi** dự án. Bao gồm:

### Internal stakeholders (trong tổ chức)
- **Sponsor**: Người phê duyệt budget (thường là exec)
- **Steering Committee**: Hội đồng quyết định cấp cao
- **Product Owner / Product Manager**: Quyết định feature
- **Business Owner**: Trưởng phòng nghiệp vụ
- **End users**: Người dùng cuối
- **IT/Tech team**: Architect, dev, QA, DevOps, Security
- **Operations**: Support, training, vận hành sau go-live
- **Finance, Legal, HR**: Hỗ trợ ngang

### External stakeholders (ngoài tổ chức)
- **Khách hàng cuối** (nếu B2C)
- **Vendor/Supplier**: Đối tác tích hợp (VNPay, vendor giao hàng)
- **Regulator**: Cơ quan quản lý nhà nước
- **Competitor** (gián tiếp)
- **Cộng đồng**: User community, KOL, báo chí

## Quy trình Stakeholder Analysis

### Bước 1: Identify (Liệt kê)

Brainstorm tất cả người có liên quan. Đừng bỏ sót — sót 1 stakeholder = surprise sau này.

**Câu hỏi giúp identify:**
- Ai bỏ tiền ra?
- Ai sẽ dùng?
- Ai bị thay đổi bởi dự án này?
- Ai có quyền veto?
- Ai cung cấp resource (people, tools, data)?
- Ai sẽ vận hành sau khi go-live?
- Có ràng buộc pháp lý/compliance nào không?

### Bước 2: Analyze (Phân loại)

Đánh giá mỗi stakeholder trên 2 trục: **Quyền lực** và **Mức độ quan tâm**.

#### Power/Interest Matrix

```
   Cao  ┌─────────────────────┬─────────────────────┐
        │                     │                     │
        │   KEEP SATISFIED    │   MANAGE CLOSELY    │
Quyền   │   (Sponsor cấp cao, │   (PO, Sponsor      │
lực     │    Regulator)       │    trực tiếp,       │
        │                     │    Tech Lead)       │
        │                     │                     │
        ├─────────────────────┼─────────────────────┤
        │                     │                     │
        │   MONITOR           │   KEEP INFORMED     │
        │   (Stakeholder      │   (End users,       │
        │    xa, cộng đồng)   │    Operations team) │
        │                     │                     │
   Thấp └─────────────────────┴─────────────────────┘
        Thấp     Mức quan tâm     Cao
```

**Chiến lược 4 góc:**

| Vùng | Chiến lược |
|---|---|
| **Manage Closely** (quyền cao + quan tâm cao) | Họp 1-1 thường xuyên, involve trong quyết định, transparency tối đa |
| **Keep Satisfied** (quyền cao + quan tâm thấp) | Update định kỳ, không spam, đảm bảo không bất ngờ |
| **Keep Informed** (quyền thấp + quan tâm cao) | Newsletter, demo, gather feedback, dùng làm champion |
| **Monitor** (quyền thấp + quan tâm thấp) | Update tối thiểu, theo dõi xem họ có thay đổi vị trí không |

### Bước 3: Plan (Lập kế hoạch)

#### Stakeholder Register Template

| ID | Tên | Vai trò | Quyền lực | Quan tâm | Vị thế | Mong muốn chính | Mối quan tâm | Chiến lược engage | Tần suất |
|----|-----|---------|-----------|----------|--------|------------------|---------------|---------------------|----------|
| S1 | Anh Hùng | CEO/Sponsor | Cao | Trung | Champion | Tăng doanh thu | ROI rõ ràng | 1-1 monthly, dashboard | Hàng tháng |
| S2 | Chị Lan | PM | Cao | Cao | Champion | On-time, on-budget | Risk visibility | Daily standup, weekly status | Hàng ngày |
| S3 | Anh Khoa | Tech Lead | Cao | Cao | Neutral | Code quality, không over-engineering | Tech debt | Tech review, decision logs | Hàng tuần |
| S4 | Cô Mai | Trưởng CSKH | Trung | Cao | Skeptical | UI dễ dùng cho nhân viên | Training cost | Demo sớm, co-design | 2 tuần/lần |
| S5 | Phòng kế toán | Stakeholder phụ | Thấp | Trung | Neutral | Báo cáo đầy đủ | Tích hợp Misa | Email update tháng | Tháng |

**Vị thế (Stance) — Cực kỳ quan trọng:**
- **Champion** 🟢 — ủng hộ tích cực, có thể nhờ vận động hộ
- **Supporter** 🟢 — đồng thuận, không chủ động
- **Neutral** 🟡 — chưa có ý kiến
- **Skeptical** 🟠 — hoài nghi, cần thuyết phục bằng evidence
- **Blocker** 🔴 — chống đối, cần xử lý đặc biệt

→ **Goal của BA**: Đẩy mọi stakeholder lên ít nhất Neutral, ideal là Supporter+.

## RACI Matrix — Ai làm gì?

RACI = **R**esponsible, **A**ccountable, **C**onsulted, **I**nformed

| Activity | Sponsor | PM | BA | Tech Lead | Dev | QA | PO |
|---|---|---|---|---|---|---|---|
| Approve budget | **A** | C | I | I | I | I | C |
| Define requirements | I | C | **R** | C | I | I | **A** |
| Approve requirements | **A** | C | R | C | I | I | R |
| Design solution | I | I | C | **R/A** | C | I | I |
| Develop | I | I | I | A | **R** | I | I |
| Test | I | I | C | A | C | **R** | I |
| Sign-off go-live | **A** | R | C | C | I | C | R |
| Production support | I | A | I | R | **R** | C | I |

**Nguyên tắc:**
- Mỗi hàng có **đúng 1 A** (Accountable — chịu trách nhiệm cuối cùng)
- Có thể có nhiều R, nhưng càng ít càng rõ ràng
- C (Consulted) = hỏi ý kiến trước khi quyết
- I (Informed) = báo sau khi đã quyết

## Communication Plan Template

```markdown
| Stakeholder | Thông tin cần biết | Hình thức | Tần suất | Người gửi |
|---|---|---|---|---|
| Sponsor | Status, risk, budget | Email + dashboard | Tháng | PM |
| PO | Detailed progress, blocker | Standup + Jira | Hàng ngày | Scrum Master |
| End users | Tính năng mới, training | Newsletter + demo | Phase | BA |
| Vendor (VNPay) | Integration plan | Họp + email | Khi cần | Tech Lead |
| All-hands | Major milestones | Town hall | Quý | Sponsor |
```

## Quản lý stakeholder khó tính

### Loại 1: "Người hay đổi ý"
**Triệu chứng**: Mỗi tuần một ý tưởng mới, scope phình to.
**Cách xử lý**:
- Lock requirement bằng sign-off chính thức
- Mọi thay đổi qua Change Request có cost/timeline ước lượng
- Show impact: "Nếu thêm cái này, X bị delay 2 tuần"

### Loại 2: "Người mất tích"
**Triệu chứng**: Không tham gia họp, không feedback, đến cuối project mới phản đối.
**Cách xử lý**:
- Forced check-in 1-1 hàng tuần (15 phút thôi)
- Document mọi giả định, gửi cho họ "im lặng = đồng ý"
- Escalate lên sếp họ nếu cần

### Loại 3: "Người siêu chi tiết"
**Triệu chứng**: Soi từng dấu phẩy, slow down team.
**Cách xử lý**:
- Cho họ vai trò review chính thức (chứ không phải ad-hoc commenter)
- Set deadline cứng cho mỗi review (3 ngày → mặc định approve)
- Tách "must-fix" vs "nice-to-have" feedback

### Loại 4: "Người chống đối"
**Triệu chứng**: Phản đối ngay từ đầu, lo bị thay thế bởi hệ thống mới.
**Cách xử lý**:
- Hiểu nguyên nhân thật (thường là sợ hãi, không phải logic)
- Cho họ vai trò trong dự án (co-design, user testing lead)
- Show how it helps THEM (less repetitive work → more time for higher-value tasks)

### Loại 5: "Sếp ra lệnh từ trên trời"
**Triệu chứng**: Sponsor có ý tưởng, push xuống mà không tham vấn ai.
**Cách xử lý**:
- Đừng đối đầu trực tiếp
- Đưa data: "Ý này tuyệt, em thử với 5 user → kết quả X"
- Đưa option: "Có 3 cách làm ý này — em recommend cách B vì..."

## Stakeholder Engagement Plan

Với mỗi stakeholder quan trọng, lên kế hoạch riêng:

```markdown
## Engagement Plan: Anh Hùng (CEO/Sponsor)

**Vị thế hiện tại**: Champion (đã ủng hộ)
**Vị thế mục tiêu**: Giữ Champion

**Mong muốn của họ**:
- ROI 3x trong 18 tháng
- Không có sự cố compliance
- Báo cáo gọn 1 slide/tháng

**Mối lo của họ**:
- Dự án delay làm trễ board meeting Q4
- Tech debt từ MVP gây issue lâu dài

**Engagement strategy**:
- Monthly 1-1 30 phút, sáng thứ Hai đầu tháng
- Email update mỗi thứ Sáu (3 bullet: progress, blocker, ask)
- Live dashboard trên Notion
- Surprise good news (early wins) → email ngay
- Bad news → mặt đối mặt, có proposal kèm theo

**Watch out**:
- Tránh deep tech jargon
- Nói budget bằng VND chứ không phải "story point"
```

## Áp dụng cho solo developer

Solo dev "không có stakeholder" — sai. Stakeholder gồm:

- **Bản thân bạn** ở tương lai (3-6 tháng nữa)
- **Co-founder/partner** (nếu có)
- **Investor/người ủng hộ tài chính**
- **Beta user**
- **Cộng đồng** (Twitter/X, Threads, FB Group)
- **App Store reviewer** (gián tiếp ảnh hưởng launch)

**Mini stakeholder plan cho solo dev:**

```markdown
| Người | Cần gì từ tôi | Tôi cần gì từ họ | Engage thế nào |
|---|---|---|---|
| Beta users (5) | App chạy được, feedback channel | Bug report, testimonial | Group Zalo, weekly update |
| Co-founder | Transparency, status | Marketing support | Daily standup 15p |
| Mentor | Update tháng | Feedback chiến lược | Email cuối tháng |
| Audience | Build-in-public content | Engagement, idea | 3 post/tuần trên Threads |
```

## Anti-patterns

❌ **"Chúng ta sẽ làm cho ai cũng vui"** — không thể, phải prioritize
❌ **Treat all stakeholders equally** — quyền lực khác nhau, attention khác nhau
❌ **Lập stakeholder list 1 lần rồi quên** — phải update mỗi quarter (người chuyển vị trí, mất quyền)
❌ **Bỏ qua stakeholder ngoài** (vendor, regulator) — cuối project mới phát hiện compliance issue
❌ **Communication 1 chiều** — chỉ broadcast, không lắng nghe → mất signal sớm về vấn đề
❌ **Không có buy-in từ end user** — họ là người dùng thật, ý kiến sponsor có thể sai
