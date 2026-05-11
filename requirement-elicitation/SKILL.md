---
name: requirement-elicitation
description: Use this skill for gathering, eliciting, and refining business/software requirements from stakeholders, users, or your own product idea. Triggers on phrases like "thu thập yêu cầu", "phỏng vấn user", "requirement gathering", "elicitation", "discovery", "user interview", "stakeholder workshop", "đặt câu hỏi cho khách hàng", "hỏi gì khi gặp khách", "khám phá nhu cầu", "user research", "validation". Use proactively when user is starting a new project or feature and hasn't clarified what users actually need — even if they only describe a vague idea ("tôi muốn làm app X"), recognize the intent and help elicit real requirements before jumping to design.
---

# Requirement Elicitation (Thu thập yêu cầu)

Đây là bước **đầu tiên và quan trọng nhất** của BA. Sai ở đây = build sai sản phẩm. Skill này hướng dẫn cách khai thác yêu cầu thực sự từ stakeholder/user, không phải yêu cầu họ tự nói ra trên bề mặt.

## Nguyên tắc cốt lõi

1. **Hỏi "Tại sao" trước "Làm gì"** — User nói "tôi muốn nút export Excel" → đào sâu lý do → có thể họ chỉ cần dashboard tốt hơn
2. **Phân biệt nhu cầu (need) vs mong muốn (want) vs giải pháp (solution)** — User thường nói giải pháp, BA phải lần ngược ra nhu cầu gốc
3. **Lắng nghe nhiều hơn nói** — Tỷ lệ 80/20 (80% lắng nghe)
4. **Không phán xét** — Mọi yêu cầu đều có lý do, dù nghe vô lý
5. **Ghi chép có cấu trúc** — Không chỉ "user nói gì" mà còn "tại sao họ nói vậy"

## Chọn kỹ thuật phù hợp

| Tình huống | Kỹ thuật phù hợp |
|---|---|
| 1-3 stakeholder, cần đào sâu | **Interview 1-1** |
| 5-15 người, cần align ý kiến | **Workshop** |
| Quy trình hiện tại phức tạp | **Observation** (quan sát tại chỗ) |
| Đã có user dùng app | **Survey** + **Interview** |
| Tài liệu cũ, hệ thống legacy | **Document analysis** |
| Cần ý tưởng mới | **Brainstorming** / **Design thinking** |
| Validate giả định nhanh | **Prototype + feedback** |

## Quy trình phỏng vấn 1-1 (User Interview)

### Trước khi phỏng vấn (Prep)

1. **Định nghĩa mục tiêu rõ ràng**: "Sau buổi này tôi cần biết gì?"
2. **Chuẩn bị 10-15 câu hỏi mở** (không trả lời được bằng yes/no)
3. **Research trước về người được phỏng vấn** (role, context, painpoint giả định)
4. **Gửi lịch + agenda** 1-2 ngày trước
5. **Chuẩn bị recording** (xin phép trước khi record)

### Trong buổi phỏng vấn (45-60 phút)

**Phần 1 — Warm-up (5 phút)**: Giới thiệu, tạo không khí, nói rõ mục đích
**Phần 2 — Background (10 phút)**: Hỏi về vai trò, công việc hàng ngày, context
**Phần 3 — Đào sâu vấn đề (25-30 phút)**: Painpoint, workflow hiện tại, workaround
**Phần 4 — Tương lai (10 phút)**: Mong muốn, ưu tiên, success criteria
**Phần 5 — Wrap-up (5 phút)**: Tóm tắt, hỏi "còn gì tôi nên hỏi mà chưa hỏi?"

### Bộ câu hỏi mẫu (template)

**Khám phá painpoint:**
- "Một ngày làm việc bình thường của anh/chị diễn ra như thế nào?"
- "Đâu là phần mất nhiều thời gian nhất trong công việc này?"
- "Lần gần nhất anh/chị bực mình với hệ thống/quy trình hiện tại là khi nào? Chuyện gì đã xảy ra?"
- "Nếu có một cây đũa thần, anh/chị muốn thay đổi điều gì?"

**Đào sâu workflow:**
- "Anh/chị có thể chỉ cho tôi xem cách làm hiện tại không?" (kết hợp observation)
- "Sau bước này thì làm gì tiếp theo?"
- "Khi có lỗi/exception thì xử lý sao?"
- "Ai là người tiếp theo trong quy trình này?"

**5 Whys (đào sâu nguyên nhân gốc):**
- "Tại sao điều đó lại quan trọng với anh/chị?"
- "Tại sao quy trình lại làm theo cách đó?"
- Hỏi "Tại sao" 5 lần liên tiếp để chạm tới root cause

### Sau buổi phỏng vấn

- Tổng hợp note trong vòng 24h (trí nhớ phai nhanh)
- Phân loại insight theo: **Pain**, **Need**, **Want**, **Solution proposed**, **Constraint**
- Highlight quote nguyên văn quan trọng (để dùng trong tài liệu)
- Gửi follow-up email tóm tắt + xin confirmation

## Workshop Facilitation

Khi cần align nhiều stakeholder (5-15 người). Format phổ biến:

**Discovery Workshop (3-4 giờ):**
1. **Set context** (15 phút) — Tại sao chúng ta ở đây
2. **Stakeholder mapping** (30 phút) — Ai liên quan, ai quyết định
3. **Goal alignment** (45 phút) — Mục tiêu chung là gì
4. **Current state** (45 phút) — Quy trình hiện tại, painpoint
5. **Future state** (45 phút) — Mong muốn, success metrics
6. **Prioritization** (30 phút) — MoSCoW hoặc Impact/Effort matrix
7. **Next steps** (15 phút) — Ai làm gì, khi nào

Công cụ: **Miro / FigJam** cho remote, **sticky notes thật** cho offline.

## Áp dụng cho solo developer

Khi bạn là solo dev làm app cho thị trường Việt Nam, bạn vẫn cần elicitation, nhưng "stakeholder" có thể là:
- **Bạn bè, người thân** trong target audience
- **Cộng đồng Facebook Group, Reddit, Threads** của niche đó
- **Comment trên app competitor** (App Store, CH Play reviews)
- **Bản thân bạn** — nhưng cẩn thận vì bạn không phải user trung bình

**Mẹo cho solo dev:**
- Phỏng vấn ít nhất 5 người target trước khi viết code
- Đừng hỏi "anh có dùng app X không?" → hỏi "lần gần nhất anh cần Y, anh đã làm gì?"
- Quan sát hành vi thật quan trọng hơn câu trả lời (people lie, behavior doesn't)
- Sử dụng "Mom Test" — tránh câu hỏi mà mẹ bạn cũng sẽ trả lời "ý hay đó con"

## Output mong đợi

Sau elicitation, BA cần produce:

1. **Stakeholder list** với role, mức độ ảnh hưởng
2. **Painpoint inventory** — danh sách vấn đề, có dẫn chứng quote
3. **As-Is process** — quy trình hiện tại (kèm BPMN nếu phức tạp)
4. **Initial requirements list** — yêu cầu thô, chưa ưu tiên
5. **Open questions** — câu hỏi cần làm rõ thêm
6. **Assumptions & risks** — giả định và rủi ro phát hiện được

## Anti-patterns (tránh làm)

- ❌ Hỏi câu yes/no ("Anh có thấy hệ thống chậm không?") → thay bằng "Anh đánh giá tốc độ hệ thống thế nào?"
- ❌ Dẫn dắt câu trả lời ("Chắc anh muốn nút này màu xanh đúng không?")
- ❌ Giải thích giải pháp giữa chừng → user sẽ adapt theo, mất insight thật
- ❌ Bỏ qua những điều "ai cũng biết" — đó thường là nơi giả định sai
- ❌ Chỉ phỏng vấn người trên cao (CEO, manager) — bỏ qua người dùng cuối
- ❌ Tin tưởng 100% vào lời nói — luôn cross-check với hành vi/số liệu
