---
name: srs-writer
description: Use this skill for writing Software Requirements Specifications (SRS) — detailed technical-functional documents covering functional requirements, non-functional requirements (performance, security, scalability), system interfaces, data requirements, and constraints. Triggers on phrases like "SRS", "Software Requirements Specification", "tài liệu đặc tả phần mềm", "viết SRS", "functional requirement", "non-functional requirement", "NFR", "system spec", "tài liệu kỹ thuật cho dev". Use proactively when a project moves from business approval (BRD) into design/development and dev team needs detailed specifications.
---

# SRS — Software Requirements Specification

SRS là tài liệu **chi tiết kỹ thuật-chức năng**, cầu nối giữa BRD (nghiệp vụ) và Implementation (code). Theo chuẩn **IEEE 830**, SRS phải đảm bảo: đúng, rõ ràng, đầy đủ, nhất quán, kiểm thử được, và có thể truy vết.

## Cấu trúc SRS theo IEEE 830 (rút gọn cho thực tế)

```markdown
# Software Requirements Specification
**Sản phẩm**: [Tên]
**Phiên bản SRS**: 1.0
**Ngày**: [DD/MM/YYYY]
**Tác giả**: [Tên]

---

## 1. Giới thiệu (Introduction)

### 1.1 Mục đích
[Tài liệu này dùng để làm gì, ai đọc]

### 1.2 Phạm vi sản phẩm
[Sản phẩm này là gì, làm gì, không làm gì]

### 1.3 Định nghĩa & Viết tắt
| Thuật ngữ | Định nghĩa |
|---|---|
| BR | Business Requirement |
| FR | Functional Requirement |
| NFR | Non-Functional Requirement |
| KH | Khách hàng |
| ... | ... |

### 1.4 Tài liệu tham chiếu
- BRD v1.2 (link)
- UI Design v0.5 (Figma link)
- Architecture Document (link)

### 1.5 Tổng quan tài liệu
[Cấu trúc tài liệu]

---

## 2. Mô tả tổng thể (Overall Description)

### 2.1 Bối cảnh sản phẩm
[Sản phẩm đứng độc lập hay là module của hệ thống lớn?]

### 2.2 Chức năng chính (high-level)
- Đặt món
- Thanh toán
- Theo dõi đơn
- ...

### 2.3 User Class & Đặc điểm
| User Class | Số lượng | Tần suất dùng | Đặc điểm |
|---|---|---|---|
| Khách hàng cá nhân | ~10,000 | Hằng ngày | 18-45 tuổi, dùng mobile |
| Nhân viên nhà hàng | ~200 | Hằng ngày | Dùng tablet tại quầy |
| Admin nội bộ | ~5 | Hằng tuần | Dùng web desktop |

### 2.4 Môi trường vận hành
- **Mobile**: iOS 14+, Android 9+
- **Web**: Chrome 100+, Safari 15+, Firefox 100+
- **Server**: Linux Ubuntu 22.04, Node.js 20+
- **Database**: PostgreSQL 15+
- **Mạng**: Internet, hỗ trợ 3G/4G

### 2.5 Ràng buộc thiết kế & triển khai
- Bắt buộc dùng React Native cho mobile (tận dụng team hiện tại)
- Bắt buộc tích hợp VNPay (regulation)
- Database không được host ngoài Việt Nam (Nghị định 13/2023)

### 2.6 Giả định & Phụ thuộc
- API VNPay sẵn sàng và stable
- Người dùng có smartphone với GPS

---

## 3. Yêu cầu chức năng (Functional Requirements)

### 3.1 FR — Module Đăng ký/Đăng nhập

#### FR-001: Đăng ký bằng số điện thoại
- **Mô tả**: Khách hàng đăng ký tài khoản bằng số điện thoại + OTP
- **Ưu tiên**: MUST
- **Input**: Số điện thoại VN (10 số, format 0xxx)
- **Output**: Tài khoản được tạo, user đăng nhập tự động
- **Business Rules**:
  - BR-001.1: SĐT phải duy nhất, nếu trùng → báo lỗi "SĐT đã đăng ký"
  - BR-001.2: OTP có hiệu lực 5 phút, tối đa 3 lần resend trong 1 giờ
  - BR-001.3: Sau 5 lần nhập OTP sai → khoá SĐT này 30 phút
- **Truy vết về BRD**: BR2 (yêu cầu đăng ký dễ dàng)
- **Acceptance Criteria**: [xem use case UC-001]

#### FR-002: Đăng nhập bằng OTP
[...]

### 3.2 FR — Module Đặt món

#### FR-010: Xem danh sách nhà hàng theo vị trí
- **Mô tả**: Hệ thống hiển thị nhà hàng trong bán kính X km từ vị trí khách
- **Ưu tiên**: MUST
- **Input**: Lat/Long của khách (lấy từ GPS hoặc nhập)
- **Output**: Danh sách nhà hàng sắp xếp theo khoảng cách tăng dần
- **Business Rules**:
  - BR-010.1: Default X = 5km, có thể chỉnh 1-20km
  - BR-010.2: Chỉ hiện nhà hàng đang mở cửa
  - BR-010.3: Nếu không có GPS → cho nhập địa chỉ thủ công
[...]

(Liệt kê tất cả FR theo module)

---

## 4. Yêu cầu phi chức năng (Non-Functional Requirements)

### 4.1 Performance (Hiệu năng)
- **NFR-P1**: 95% request API trả về < 500ms ở môi trường production
- **NFR-P2**: Trang chủ load < 2s trên 4G
- **NFR-P3**: Hệ thống chịu được 1,000 user đồng thời
- **NFR-P4**: Database query < 100ms cho 90% query
- **NFR-P5**: Search nhà hàng trả kết quả < 1s với 10,000 nhà hàng

### 4.2 Security (Bảo mật)
- **NFR-S1**: Mật khẩu lưu dạng hash bcrypt (cost factor ≥ 12)
- **NFR-S2**: Mọi giao tiếp client-server qua HTTPS (TLS 1.3+)
- **NFR-S3**: Dữ liệu nhạy cảm (số thẻ, CCCD) phải mã hoá AES-256
- **NFR-S4**: Tuân thủ Nghị định 13/2023 về dữ liệu cá nhân
- **NFR-S5**: Audit log mọi hành động admin, lưu tối thiểu 2 năm
- **NFR-S6**: Rate limit: 100 request/phút/IP

### 4.3 Reliability (Độ tin cậy)
- **NFR-R1**: Uptime ≥ 99.5% (tối đa downtime ~3.6h/tháng)
- **NFR-R2**: Backup database hàng ngày, lưu 30 ngày
- **NFR-R3**: Recovery Time Objective (RTO) ≤ 2 giờ
- **NFR-R4**: Recovery Point Objective (RPO) ≤ 1 giờ

### 4.4 Usability (Dễ dùng)
- **NFR-U1**: User mới đặt món thành công lần đầu trong < 3 phút
- **NFR-U2**: Tuân thủ WCAG 2.1 level AA (accessibility)
- **NFR-U3**: Hỗ trợ tiếng Việt + tiếng Anh
- **NFR-U4**: Mọi thao tác phá hoại (xoá, huỷ) phải có confirm

### 4.5 Scalability (Khả năng mở rộng)
- **NFR-SC1**: Thiết kế hỗ trợ scale lên 100,000 user trong 2 năm
- **NFR-SC2**: Database hỗ trợ sharding khi cần
- **NFR-SC3**: Stateless backend để horizontal scale dễ dàng

### 4.6 Compatibility (Tương thích)
- **NFR-C1**: Mobile: iOS 14+, Android 9+ (API 28+)
- **NFR-C2**: Web responsive: 320px - 1920px
- **NFR-C3**: Tương thích thanh toán: VNPay, MoMo, ZaloPay

### 4.7 Maintainability (Dễ bảo trì)
- **NFR-M1**: Code coverage unit test ≥ 70%
- **NFR-M2**: Tài liệu API auto-generated (OpenAPI/Swagger)
- **NFR-M3**: Tuân thủ ESLint + Prettier rules đã định

### 4.8 Localization
- **NFR-L1**: Tất cả text UI dùng i18n key, không hardcode
- **NFR-L2**: Định dạng tiền: 1,000,000₫ (separator dấu phẩy, ký hiệu ₫ ở sau)
- **NFR-L3**: Định dạng ngày: dd/mm/yyyy

---

## 5. Yêu cầu giao diện (Interface Requirements)

### 5.1 User Interface
[Link Figma + key screen descriptions]

### 5.2 Hardware Interface
- Camera (để scan QR code thanh toán)
- GPS (để xác định vị trí)

### 5.3 Software Interface (Tích hợp với hệ thống khác)
| Hệ thống | Mục đích | Protocol | Format |
|---|---|---|---|
| VNPay API | Thanh toán | HTTPS REST | JSON |
| Firebase Cloud Messaging | Push notification | HTTPS | JSON |
| Google Maps API | Hiển thị bản đồ | HTTPS REST | JSON |
| SMS Gateway (Viettel) | Gửi OTP | HTTPS | JSON |

### 5.4 Communication Interface
- HTTPS REST API (chính)
- WebSocket cho real-time (theo dõi đơn hàng)

---

## 6. Yêu cầu dữ liệu (Data Requirements)

### 6.1 Entity chính
- User
- Restaurant
- MenuItem
- Order
- Payment
- Review
[Xem ERD chi tiết trong skill data-modeling-erd]

### 6.2 Khối lượng dữ liệu dự kiến (Year 1)
| Entity | Số lượng | Growth/tháng |
|---|---|---|
| User | 10,000 | +1,000 |
| Order | 100,000 | +10,000 |
| MenuItem | 5,000 | +200 |

### 6.3 Data retention
- Order: lưu 5 năm (theo luật kế toán)
- Audit log: 2 năm
- Session: 30 ngày

### 6.4 Data privacy
- Tuân thủ Nghị định 13/2023
- User có quyền request xoá dữ liệu (right to be forgotten)

---

## 7. Phụ lục (Appendix)

### 7.1 Glossary mở rộng
### 7.2 Use Case Diagrams
### 7.3 Wireframes
### 7.4 Traceability Matrix

| BR | FR | Test Case | Status |
|---|---|---|---|
| BR1 | FR-001, FR-002 | TC-001, TC-002 | Approved |
| BR2 | FR-010, FR-011 | TC-010 | In Progress |
```

## Phân biệt 3 loại yêu cầu

### Functional (FR) — Hệ thống làm GÌ
- "Khách phải đăng ký được bằng SĐT"
- "Admin phải xuất được báo cáo Excel"
- → Kiểm thử bằng test case input-output

### Non-Functional (NFR) — Hệ thống làm NHƯ THẾ NÀO
- "API phải < 500ms"
- "Hệ thống chịu 1000 user đồng thời"
- → Kiểm thử bằng performance test, security audit

### Business Rules (BR) — Quy tắc nghiệp vụ
- "Đơn < 30k không cho đặt"
- "Khách VIP free ship > 100k"
- → Một phần của FR, nhưng nên tách ra để dễ thay đổi sau

## Phân loại ưu tiên — MoSCoW

| Mức | Ý nghĩa | Tỷ lệ khuyến nghị |
|---|---|---|
| **MUST** | Bắt buộc, không có thì product fail | ~60% |
| **SHOULD** | Quan trọng, nhưng có thể delay | ~20% |
| **COULD** | Có thì tốt (nice-to-have) | ~20% |
| **WON'T** | Không làm phase này | (phase sau) |

## Đặc tính SRS chất lượng cao

| Tiêu chí | Cách kiểm tra |
|---|---|
| **Correct** | Yêu cầu đúng với BRD, không bịa thêm |
| **Unambiguous** | Mỗi câu chỉ hiểu được 1 cách. Tránh "user-friendly", "fast", "good" |
| **Complete** | Đủ FR, NFR, error case, edge case |
| **Consistent** | Không có yêu cầu mâu thuẫn nhau |
| **Verifiable** | Kiểm thử được. "Nhanh" → không verifiable. "< 2s" → verifiable |
| **Modifiable** | Cấu trúc tốt để dễ update, có ID truy vết |
| **Traceable** | Mỗi FR map ngược về BR, mỗi test map về FR |

## Từ ngữ TRÁNH dùng trong SRS

❌ "user-friendly", "intuitive", "easy to use" → ✅ Đo bằng metric (NFR-U)
❌ "fast", "quick", "performant" → ✅ "< X ms"
❌ "robust", "reliable" → ✅ "uptime ≥ 99.5%"
❌ "v.v.", "etc.", "..." → ✅ Liệt kê đầy đủ
❌ "thường", "đôi khi" → ✅ Số liệu cụ thể
❌ "nếu cần", "có thể" → ✅ Quyết định rõ MUST/SHOULD/COULD

## Anti-patterns

❌ **Trộn yêu cầu với giải pháp**: "Dùng Redux để quản lý state" → đó là implementation, không phải requirement.
❌ **NFR quá ít** — chỉ tập trung FR, quên performance/security → product chậm, dễ hack.
❌ **Không có traceability** — sau 6 tháng không biết tại sao có FR này.
❌ **Quá chi tiết về UI** — Figma đã có, SRS không cần mô tả từng pixel.
❌ **SRS một lần xong là thôi** — phải maintain, mỗi change request update SRS.

## Áp dụng cho solo developer

SRS đầy đủ là overkill cho solo dev. Phiên bản gọn:

```markdown
# Mini SRS: [Feature name]

## Functional
- FR1: ...
- FR2: ...

## Non-Functional (chỉ cần liệt kê những gì matter)
- Performance: API < 500ms
- Security: Hash password, HTTPS only

## Out of scope
- ...

## Open questions
- ?
```

Lưu trong `docs/specs/[feature].md` cùng repo, update theo PR.
