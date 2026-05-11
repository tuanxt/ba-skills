---
name: user-story-writing
description: Use this skill for writing Agile user stories with proper format (As a... I want... So that...), acceptance criteria, story points estimation, and backlog grooming. Triggers on phrases like "user story", "viết user story", "story Agile", "Scrum backlog", "acceptance criteria", "AC", "Given When Then", "story point", "backlog grooming", "refinement", "viết yêu cầu cho dev", "ticket Jira", "epic", "feature breakdown". Use proactively whenever user is planning features for an Agile/Scrum project — even if they just describe a feature ("tôi muốn user đăng nhập bằng Google"), convert it into properly structured stories.
---

# User Story Writing

User Story là cách viết yêu cầu phổ biến nhất trong Agile/Scrum. Skill này hướng dẫn viết story rõ ràng, có acceptance criteria đầy đủ, dev đọc xong là code được mà không cần hỏi thêm.

## Cấu trúc User Story chuẩn

```
As a [persona/role],
I want [action/goal],
So that [benefit/value]
```

**Ví dụ tốt:**
> As a khách hàng đặt món, I want lưu địa chỉ giao hàng yêu thích, So that tôi không phải nhập lại địa chỉ mỗi lần đặt món.

**Ví dụ tệ (thiếu giá trị):**
> As a user, I want a save button — *thiếu lý do, không biết save cái gì, save xong làm gì*

## Tiêu chuẩn INVEST

Story tốt thoả mãn 6 tiêu chí INVEST:

| Tiêu chí | Ý nghĩa | Cách kiểm tra |
|---|---|---|
| **I**ndependent | Độc lập, không phụ thuộc story khác | Có thể làm sau hoặc trước story khác không? |
| **N**egotiable | Có thể thương lượng chi tiết | Không khoá cứng cách làm |
| **V**aluable | Có giá trị cho user/business | Trả lời được "So that" |
| **E**stimable | Ước lượng được effort | Dev có hình dung được scope không? |
| **S**mall | Đủ nhỏ để làm trong 1 sprint | Tối đa 1-3 ngày dev |
| **T**estable | Kiểm thử được | Có acceptance criteria rõ ràng |

## Acceptance Criteria (AC) — Quan trọng nhất

AC là **điều kiện chấp nhận** — story chỉ "done" khi tất cả AC pass. Có 2 format phổ biến:

### Format 1: Given-When-Then (BDD style)

```
Scenario: Khách hàng lưu địa chỉ giao hàng mới
  Given khách đã đăng nhập và đang ở màn checkout
  When khách nhập địa chỉ mới và bấm "Lưu địa chỉ này"
  Then địa chỉ được lưu vào profile
  And lần đặt món tiếp theo, địa chỉ xuất hiện trong dropdown
```

Dùng khi: behavior phức tạp, nhiều bước, cần test tự động.

### Format 2: Checklist

```
Acceptance Criteria:
- [ ] Có nút "Lưu địa chỉ này" dưới form nhập địa chỉ
- [ ] Khi bấm, hiển thị toast "Đã lưu" trong 2s
- [ ] Địa chỉ được lưu vào bảng user_addresses
- [ ] Tối đa lưu 5 địa chỉ/user (nếu đã 5, hỏi user replace cái nào)
- [ ] Lần checkout tiếp theo, địa chỉ default = địa chỉ vừa lưu
```

Dùng khi: yêu cầu đơn giản, nhiều rule rời rạc.

## Template chuẩn (copy-paste để dùng)

```markdown
## [ID] — [Tên ngắn gọn của story]

**Story:**
As a [persona],
I want [hành động],
So that [giá trị].

**Background/Context:**
[1-2 câu giải thích tại sao có story này, bối cảnh]

**Acceptance Criteria:**
- [ ] AC1: ...
- [ ] AC2: ...
- [ ] AC3: ...

**Out of scope (KHÔNG làm trong story này):**
- ...
- ...

**Dependencies:**
- Cần [API X] hoạt động trước
- Phụ thuộc story [#123]

**Mockup/Design:**
[Link Figma hoặc paste ảnh]

**Technical Notes:** (BA có thể bỏ qua, dev thêm vào)
- ...

**Estimation:** [story points hoặc giờ]
```

## Story Points — Ước lượng tương đối

Dùng dãy Fibonacci: **1, 2, 3, 5, 8, 13, 21**. Không phải giờ, mà là độ phức tạp tương đối so với một story "chuẩn" (baseline) của team.

| Points | Ý nghĩa thực tế |
|---|---|
| 1 | Trivial, vài giờ (đổi text, đổi màu) |
| 2 | Đơn giản, nửa ngày (form đơn giản) |
| 3 | Vừa, 1 ngày (CRUD cơ bản) |
| 5 | Phức tạp, 2-3 ngày (logic nghiệp vụ, nhiều case) |
| 8 | Lớn, gần 1 tuần (cần research, nhiều unknown) |
| 13 | Quá lớn → **split thành nhiều story** |
| 21 | Đây là Epic, không phải Story |

**Planning Poker**: cả team estimate cùng lúc, nếu lệch nhau nhiều → discuss → estimate lại.

## Cách split story khi quá lớn

Story 13+ điểm cần chia nhỏ. Các pattern phổ biến:

| Pattern | Ví dụ |
|---|---|
| **Theo workflow** | Story 1: Tạo đơn → Story 2: Thanh toán → Story 3: Xác nhận |
| **Theo data variant** | Story 1: Thanh toán bằng VNPay → Story 2: Thanh toán bằng MoMo |
| **Happy path trước** | Story 1: Đăng ký thành công → Story 2: Xử lý lỗi/edge cases |
| **CRUD tách rời** | Story 1: Tạo → Story 2: Sửa → Story 3: Xoá → Story 4: List |
| **Theo persona** | Story 1: Customer xem đơn → Story 2: Admin duyệt đơn |
| **Simple → Complex** | Story 1: Search by name → Story 2: Search + filter nâng cao |

## Epic, Feature, Story, Task — Phân biệt

```
Epic (vài tuần - vài tháng)
  └── Feature (1-2 sprint)
       └── Story (vài ngày, nằm gọn trong 1 sprint)
            └── Task (vài giờ, kỹ thuật, dev tự chia)
```

**Ví dụ thực tế (app "Ăn Gì Hôm Nay"):**
- **Epic**: Onboarding & Personalization
- **Feature**: Setup khẩu vị ban đầu
- **Story**: As a user mới, I want chọn 5 món yêu thích trong onboarding, So that gợi ý lần đầu phù hợp với tôi
- **Task** (dev tự chia): Tạo API GET /foods → Tạo screen ChọnMón → Lưu vào local DB → Track event

## Anti-patterns thường gặp

❌ **Story kỹ thuật không có giá trị user**:
> "As a developer, I want refactor database schema, so that code dễ maintain"
> → Đây là **Task kỹ thuật**, không phải Story. Đưa vào tech debt backlog.

❌ **Story quá to (Epic giả danh Story)**:
> "As a user, I want quản lý đơn hàng" → đây là feature, phải chia ra: tạo / xem / huỷ / sửa đơn

❌ **AC quá mơ hồ**:
> "Hệ thống phải nhanh" → bao nhiêu giây? "User-friendly" → đo bằng gì?

❌ **Thiếu "So that" (giá trị)**:
> "As a user, I want có dark mode" → tại sao? Để dễ đọc ban đêm? Để tiết kiệm pin? Lý do khác nhau dẫn đến giải pháp khác nhau.

❌ **Quá nhiều AC trong 1 story** (10+):
> Dấu hiệu cần split. AC lý tưởng: 3-7 cái/story.

❌ **Trộn nhiều persona trong 1 story**:
> "As an admin and user, I want..." → tách 2 story riêng.

## Áp dụng cho solo developer

Khi bạn là solo dev, vẫn nên viết story vì:

1. **Self-discipline** — Buộc bản thân clarify trước khi code
2. **Future you** — Đọc lại sau 3 tháng vẫn hiểu tại sao làm
3. **Async communication** — Nếu sau này thuê freelancer, có sẵn spec
4. **Đo lường progress** — Burn down chart dù chỉ 1 mình

**Mẹo gọn cho solo dev:**
- Dùng GitHub Issues hoặc Linear thay vì Jira (đỡ overhead)
- Story format có thể rút gọn: bullet list AC + 1 dòng "Why"
- Không cần story points — dùng T-shirt size (S/M/L) hoặc giờ ước lượng

## Workflow chuẩn

1. **Capture idea** → ghi nhanh vào backlog (rough story)
2. **Refinement/Grooming** → viết đủ AC, ước lượng, làm rõ với team
3. **Definition of Ready** (DoR) → story đạt chuẩn để vào sprint:
   - Có persona rõ
   - Có AC đầy đủ
   - Có mockup nếu cần UI
   - Đã estimate
   - Không có dependency block
4. **Sprint Planning** → commit vào sprint
5. **Definition of Done** (DoD) → khi nào coi là xong:
   - Code review pass
   - Test pass (unit + integration)
   - Đã deploy lên staging
   - PO/BA accept
   - Documentation update
