# Bộ Skills cho Business Analyst (BA)

Bộ skills hoàn chỉnh cho công việc Business Analyst, phù hợp cho cả **solo developer** tự BA cho dự án của mình lẫn **BA chuyên nghiệp** trong team/agency.

## Cấu trúc bộ skills

10 skills bao trùm toàn bộ vòng đời BA, từ discovery → design → validate → handoff → UAT:

| # | Skill | Giai đoạn | Mô tả |
|---|-------|-----------|-------|
| 1 | `requirement-elicitation` | Discovery | Phỏng vấn, workshop, observation để thu thập yêu cầu thật |
| 2 | `stakeholder-analysis` | Discovery | Phân tích bên liên quan, RACI, communication plan |
| 3 | `brd-writer` | Define | Tài liệu Business Requirements — cấp cao, ngôn ngữ business |
| 4 | `bpmn-process-flow` | Define | Vẽ quy trình nghiệp vụ, As-Is vs To-Be |
| 5 | `srs-writer` | Define | Software Requirements Specification — FR + NFR chi tiết |
| 6 | `use-case-specification` | Design | Kịch bản sử dụng chi tiết với main/alternative/exception flow |
| 7 | `user-story-writing` | Design | User Story Agile/Scrum với AC, INVEST, story points |
| 8 | `data-modeling-erd` | Design | Entity-Relationship Diagram + Data Dictionary |
| 9 | `wireframe-mockup` | Design | Wireframe lo/mid/hi-fi, IA, user flow mapping |
| 10 | `uat-test-planning` | Validate | UAT plan, test cases, defect tracking, sign-off |

## Workflow điển hình áp dụng các skills

```
Phase 1: DISCOVERY (Khám phá)
  ├── stakeholder-analysis     → Hiểu ai liên quan
  └── requirement-elicitation  → Thu thập yêu cầu thật

Phase 2: DEFINE (Định nghĩa)
  ├── brd-writer               → Tài liệu nghiệp vụ cấp cao
  ├── bpmn-process-flow        → Vẽ As-Is / To-Be
  └── srs-writer               → Spec kỹ thuật-chức năng

Phase 3: DESIGN (Thiết kế)
  ├── use-case-specification   → Kịch bản chi tiết
  ├── user-story-writing       → Story Agile cho sprint
  ├── data-modeling-erd        → Thiết kế data
  └── wireframe-mockup         → Thiết kế UI

Phase 4: VALIDATE (Xác nhận)
  └── uat-test-planning        → Test với user thật, sign-off
```

## Cách sử dụng

### Với Claude
Mỗi skill là 1 thư mục có file `SKILL.md`. Claude sẽ tự động kích hoạt skill phù hợp dựa trên ngữ cảnh hỏi:

- Hỏi "viết user story cho feature X" → kích hoạt `user-story-writing`
- Hỏi "vẽ ERD cho app Y" → kích hoạt `data-modeling-erd`
- Hỏi "phỏng vấn user thế nào" → kích hoạt `requirement-elicitation`

### Cài đặt vào Claude
1. Mỗi thư mục trong `ba-skills/` là 1 skill độc lập
2. Upload từng skill như user skill (tùy môi trường Claude bạn dùng)
3. Hoặc giữ làm reference template để paste khi cần

### Đọc trực tiếp như tài liệu
Mỗi `SKILL.md` là 1 cheatsheet/checklist hoàn chỉnh — đọc khi cần làm task BA tương ứng.

## Đặc điểm chung của bộ skills

- ✅ **Tiếng Việt** — phù hợp ngữ cảnh thị trường Việt Nam
- ✅ **Có template** copy-paste được ngay
- ✅ **Anti-patterns** rõ ràng — học từ sai lầm thường gặp
- ✅ **Áp dụng cho solo developer** — mỗi skill có section "Áp dụng cho solo dev" với phiên bản gọn
- ✅ **Ví dụ thực tế** — dùng cùng 1 use case "Ăn Gì Hôm Nay" / "đặt món" xuyên suốt để dễ liên hệ
- ✅ **Quote dạng Vietnamese context** — Nghị định 13/2023, VNPay/MoMo/ZaloPay, Misa, Viettel SMS...

---

**Phiên bản**: 1.0
**Ngôn ngữ**: Tiếng Việt
**License**: Sử dụng tự do cho mục đích cá nhân/công việc
