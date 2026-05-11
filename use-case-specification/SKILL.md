---
name: use-case-specification
description: Use this skill for writing detailed use case specifications with actors, preconditions, main flow, alternative flows, exceptions, and post-conditions. Triggers on phrases like "use case", "viết use case", "kịch bản sử dụng", "actor flow", "main flow", "alternative flow", "exception flow", "use case diagram", "scenario chi tiết", "luồng nghiệp vụ". Use proactively when behavior is complex (multi-step, many branches, exception handling) and a simple user story isn't enough — especially for backend processes, financial transactions, multi-actor workflows, or safety-critical features.
---

# Use Case Specification

Use Case mô tả **kịch bản tương tác giữa actor và hệ thống** một cách chi tiết, đầy đủ flow chính + flow phụ + exception. Phù hợp khi User Story quá ngắn để diễn tả hết, ví dụ: thanh toán, đặt chỗ, quy trình duyệt nhiều cấp.

## Khi nào dùng Use Case thay vì User Story?

| Tình huống | Nên dùng |
|---|---|
| Feature đơn giản, 1-2 bước | **User Story** |
| Quy trình nhiều bước, nhiều branch | **Use Case** |
| Cần verify chi tiết với khách hàng | **Use Case** (dễ review hơn) |
| Agile sprint planning | **User Story** |
| Dự án Waterfall, fixed scope | **Use Case** |
| Có nhiều exception/error case | **Use Case** |
| Cần training tài liệu cho user | **Use Case** |

→ Trong thực tế, **Use Case + User Story bổ sung cho nhau**: Use Case ở giai đoạn discovery/design, User Story khi vào sprint.

## Cấu trúc Use Case chuẩn

```
─────────────────────────────────────
Use Case ID:        UC-001
Use Case Name:      Đặt món ăn
Actor (chính):      Khách hàng đã đăng nhập
Actor (phụ):        Hệ thống thanh toán (VNPay), Nhà hàng
Mô tả tóm tắt:      Khách hàng chọn món từ menu nhà hàng,
                    thanh toán, và gửi đơn cho nhà hàng

Trigger:            Khách bấm "Đặt món" từ trang nhà hàng
Frequency:          ~500 lần/ngày trên toàn hệ thống

Preconditions:
  - Khách đã đăng nhập
  - Khách đã chọn nhà hàng đang hoạt động
  - Nhà hàng có ít nhất 1 món còn hàng

Postconditions (Success):
  - Đơn hàng được tạo với status "Chờ nhà hàng xác nhận"
  - Nhà hàng nhận notification
  - Khách trừ tiền (nếu thanh toán online)
  - Khách thấy màn "Đang xử lý"

Postconditions (Failure):
  - Không có đơn hàng nào được tạo
  - Tiền không bị trừ
  - Khách nhận thông báo lỗi cụ thể

─────────────────────────────────────
MAIN FLOW (Happy Path):

1. Khách xem menu, chọn món và bấm "Thêm vào giỏ"
2. Hệ thống thêm món vào giỏ, hiển thị tổng tiền tạm tính
3. Khách bấm "Đặt món" từ giỏ hàng
4. Hệ thống hiển thị màn xác nhận: địa chỉ, danh sách món, tổng tiền
5. Khách chọn phương thức thanh toán (COD / VNPay / MoMo)
6. Khách bấm "Xác nhận đặt món"
7. Hệ thống validate giỏ hàng (món còn không, nhà hàng còn mở)
8. Hệ thống tạo đơn hàng với status "Chờ thanh toán"
9. [Nếu thanh toán online] Hệ thống redirect sang cổng thanh toán
10. Khách hoàn tất thanh toán
11. Hệ thống cập nhật status thành "Chờ nhà hàng xác nhận"
12. Hệ thống gửi notification cho nhà hàng
13. Hệ thống hiển thị màn "Đang xử lý đơn hàng"
14. Use case kết thúc

─────────────────────────────────────
ALTERNATIVE FLOWS:

A1. Thanh toán COD (tại bước 5)
  5a. Khách chọn COD
  5b. Bỏ qua bước 9-10
  5c. Tiếp tục bước 11 với status "Chờ nhà hàng xác nhận"
  
A2. Áp dụng voucher (trước bước 6)
  - Khách nhập mã voucher
  - Hệ thống validate và tính lại tổng tiền
  - Tiếp tục main flow

─────────────────────────────────────
EXCEPTION FLOWS:

E1. Món hết hàng (tại bước 7)
  7a. Hệ thống phát hiện 1+ món hết hàng
  7b. Hiển thị thông báo "Món X đã hết, vui lòng chọn món khác"
  7c. Cho phép khách xoá món đó và tiếp tục, hoặc huỷ
  7d. Nếu khách huỷ → use case kết thúc, không tạo đơn

E2. Nhà hàng đóng cửa (tại bước 7)
  7a. Hệ thống phát hiện nhà hàng đã đóng
  7b. Hiển thị "Nhà hàng đã đóng, vui lòng đặt sau X giờ"
  7c. Use case kết thúc, không tạo đơn

E3. Thanh toán thất bại (tại bước 10)
  10a. Cổng thanh toán trả về fail
  10b. Hệ thống cập nhật đơn thành "Thanh toán thất bại"
  10c. Hiển thị "Thanh toán không thành công, thử lại?"
  10d. Cho phép retry (về bước 9) hoặc đổi phương thức (về bước 5)

E4. Mất kết nối mạng (bất kỳ bước nào)
  - Hệ thống giữ giỏ hàng trong local storage
  - Khi mạng phục hồi, tiếp tục từ bước đang dở

─────────────────────────────────────
BUSINESS RULES (BR):
BR1. Tối thiểu giá trị đơn: 30,000 VNĐ
BR2. Thanh toán online phải hoàn tất trong 15 phút, sau đó đơn tự huỷ
BR3. Khách hàng VIP miễn phí ship cho đơn > 100,000 VNĐ
BR4. Nhà hàng có 5 phút để xác nhận, sau đó đơn tự huỷ và hoàn tiền

─────────────────────────────────────
NON-FUNCTIONAL REQUIREMENTS:
- Bước 1-8 phải hoàn tất trong < 3 giây
- Hệ thống chịu được 1000 đơn đồng thời vào giờ cao điểm
- Lịch sử đơn lưu tối thiểu 2 năm
─────────────────────────────────────
```

## Use Case Diagram (UML)

Sơ đồ tổng quan, dùng tool **draw.io / Lucidchart / PlantUML**:

```
┌─────────────────────────────────────┐
│           Hệ thống đặt món          │
│                                      │
│    ┌─────────────┐                  │
│    │  Đặt món    │◄────┐            │
│    └─────────────┘     │            │
│                        │            │
│    ┌─────────────┐     │            │
│    │ Huỷ đơn     │◄────┤            │
│    └─────────────┘     │            │
│                        │            │
│    ┌─────────────┐     │            │
│    │ Theo dõi đơn│◄────┤            │
│    └─────────────┘     │            │
└────────────────────────┼────────────┘
                         │
                    ╔════╧═════╗
                    ║  Khách   ║
                    ║  hàng    ║
                    ╚══════════╝
```

Quan hệ chính:
- **Association**: actor — use case (đường thẳng)
- **<<include>>**: use case A luôn bao gồm B (vd: "Đặt món" luôn <<include>> "Đăng nhập" nếu chưa login)
- **<<extend>>**: use case B mở rộng A trong điều kiện cụ thể (vd: "Áp voucher" <<extend>> "Đặt món")
- **Generalization**: actor con kế thừa actor cha

## Mức độ chi tiết (Levels)

Use case có 3 mức:

| Level | Khi dùng | Đặc điểm |
|---|---|---|
| **Brief** | Early discovery | 1-2 câu mô tả, chưa có flow |
| **Casual** | High-level review | Main flow dạng narrative, không đánh số |
| **Fully Dressed** | Implementation | Đầy đủ template như trên |

Đừng viết "fully dressed" cho mọi use case — chỉ làm cho các use case quan trọng/phức tạp.

## Cách viết flow hiệu quả

**Quy tắc viết bước:**
1. Mỗi bước là 1 câu, bắt đầu bằng **subject + verb**
2. Chỉ subject là **Actor** hoặc **Hệ thống** (không nhập nhằng)
3. Không nói **cách làm** (đó là việc của dev), chỉ nói **làm gì**
4. Tránh từ mơ hồ: "xử lý", "kiểm tra" → phải nói rõ kiểm tra cái gì

**Ví dụ tốt:**
> 3. Hệ thống validate email theo định dạng RFC 5322

**Ví dụ tệ:**
> 3. Hệ thống xử lý email

## Anti-patterns

❌ **Viết flow theo UI** (nút này, click kia) → khi UI thay đổi, use case lỗi thời. Viết theo **intent** của user.
❌ **Trộn flow chính và phụ** → khó đọc. Tách riêng "Alternative" và "Exception".
❌ **Thiếu Preconditions** → reader không biết khi nào use case này áp dụng.
❌ **Quá nhiều actor trong 1 use case** → tách ra. 1 use case = 1 actor chính + actor phụ hỗ trợ.
❌ **Use case quá to** (50+ bước) → đó là **business process**, không phải use case. Chia nhỏ.
❌ **Mỗi click 1 use case** → quá nhỏ, không có giá trị nghiệp vụ. Use case phải có **goal** rõ ràng.

## Use Case vs User Story — Chuyển đổi qua lại

Từ Use Case → User Stories (khi vào Agile):
```
UC-001: Đặt món
  ├── Story 1: Thêm món vào giỏ
  ├── Story 2: Xem giỏ hàng + chỉnh số lượng
  ├── Story 3: Chọn phương thức thanh toán
  ├── Story 4: Thanh toán COD
  ├── Story 5: Thanh toán online (VNPay)
  ├── Story 6: Áp dụng voucher
  └── Story 7: Xử lý lỗi thanh toán (E3)
```

## Áp dụng cho solo developer

- Solo dev thường không cần fully dressed use case
- Nhưng với **flow phức tạp** (thanh toán, đặt chỗ, multi-step wizard) → viết casual use case **ít nhất** để track edge cases
- Đặc biệt hữu ích để liệt kê **tất cả error case** trước khi code → tránh quên handle
- Lưu trong file `docs/use-cases/UC-XXX.md` trong repo
