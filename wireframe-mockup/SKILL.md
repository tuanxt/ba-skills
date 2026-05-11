---
name: wireframe-mockup
description: Use this skill for designing wireframes and mockups at low/mid/high fidelity — sketching UI layout, defining information architecture, mapping user flows to screens, annotating interactions. Triggers on phrases like "wireframe", "mockup", "phác thảo UI", "vẽ giao diện", "low-fi", "hi-fi", "prototype", "Figma", "Balsamiq", "screen design", "thiết kế màn hình", "user flow screen", "information architecture", "IA". Use proactively whenever user is moving from requirements to visual design — even a rough wireframe is more useful than a wall of text when discussing UI with stakeholders.
---

# Wireframe & Mockup

Wireframe là **bản phác thảo cấu trúc UI**, không quan tâm màu sắc/typography. Mockup là wireframe được "đẹp hoá" với màu, font, hình ảnh thật. Skill này hướng dẫn cách thiết kế đúng fidelity, đúng giai đoạn.

## 3 mức độ Fidelity

| Mức | Khi dùng | Công cụ | Thời gian |
|---|---|---|---|
| **Low-fi (Lo-fi)** | Brainstorm, early discovery | Giấy, Balsamiq, Excalidraw | Phút |
| **Mid-fi** | Review chi tiết với stakeholder | Figma, Sketch | Giờ |
| **Hi-fi** | Trước khi handoff cho dev | Figma + interaction | Ngày |

### Lo-fi: Vẽ tay hoặc Balsamiq
- Khối hộp, đường thẳng, scribble cho ảnh
- **Mục đích**: Test ý tưởng nhanh, không bám víu vào chi tiết
- Sai lầm: làm lo-fi quá đẹp → stakeholder tưởng final, không dám critique

### Mid-fi: Figma không màu
- Khung xám đen trắng
- Có text thật, button, icon đơn giản
- **Mục đích**: Validate flow + layout

### Hi-fi: Figma đầy đủ
- Đầy đủ màu, font, ảnh thật
- Có interaction (prototype clickable)
- **Mục đích**: Handoff cho dev, demo investor

> **Quy tắc vàng**: Đừng nhảy thẳng lên hi-fi. Mỗi lần nâng fidelity = chi phí thay đổi tăng x10.

## Quy trình thiết kế (từ idea → wireframe)

### Bước 1: Information Architecture (IA)

Trước khi vẽ, định nghĩa cấu trúc thông tin:

```
App "Ăn Gì Hôm Nay"
├── Trang chủ
│   ├── Gợi ý hôm nay (carousel)
│   ├── Theo mood (grid 4 mood)
│   └── Lịch sử ăn gần đây
├── Khám phá
│   ├── Theo món
│   ├── Theo nhà hàng
│   └── Theo bộ lọc
├── Yêu thích
└── Profile
    ├── Khẩu vị
    ├── Lịch sử
    └── Cài đặt
```

**Card sorting**: phỏng vấn user, đưa họ list feature → họ nhóm theo cách họ nghĩ → có IA tự nhiên.

### Bước 2: User Flow → Screens

Map từng bước user → màn hình tương ứng:

```
[Onboarding] → [Setup khẩu vị] → [Trang chủ]
                                    ↓
                               [Chi tiết món]
                                    ↓
                               [Xác nhận] → [Đặt món thành công]
```

Mỗi mũi tên = 1 transition cần thiết kế.

### Bước 3: Sketch lo-fi từng màn

**Mỗi màn cần xác định:**
1. **Mục đích chính** (1 câu): "Màn này giúp user làm gì?"
2. **Primary action** (CTA chính): Nút quan trọng nhất, kích thước lớn nhất
3. **Secondary actions**: Nút phụ
4. **Thông tin hiển thị**: Bắt buộc vs nice-to-have
5. **Trạng thái**: Empty / Loading / Success / Error

### Bước 4: Nâng cấp lên mid-fi → hi-fi

Chỉ làm sau khi flow đã được validate.

## Anatomy của một wireframe màn hình

```
┌─────────────────────────────────────┐
│  [←]    Tên màn       [⋮]          │  ← Header (nav)
├─────────────────────────────────────┤
│                                      │
│  Tiêu đề chính                       │
│  Mô tả phụ                           │
│                                      │
│  ┌──────────────────────────────┐   │
│  │  Card content                │   │  ← Main content
│  │                              │   │
│  └──────────────────────────────┘   │
│                                      │
│  ┌──────────────────────────────┐   │
│  │  Card content                │   │
│  └──────────────────────────────┘   │
│                                      │
├─────────────────────────────────────┤
│  [🏠]  [🔍]  [♥]  [👤]              │  ← Tab bar
└─────────────────────────────────────┘
```

## Checklist mỗi wireframe phải có

- [ ] **Header** với tên màn + nút back (nếu không phải tab gốc)
- [ ] **Primary CTA** rõ ràng, không bị che bởi keyboard
- [ ] **Empty state** (khi không có data)
- [ ] **Loading state** (skeleton hoặc spinner)
- [ ] **Error state** (mất mạng, server lỗi, validation lỗi)
- [ ] **Touch targets ≥ 44x44px** (chuẩn iOS) / 48dp (Android)
- [ ] **Hierarchy rõ ràng** (cái nào quan trọng to/đậm hơn)
- [ ] **Spacing nhất quán** (4, 8, 16, 24, 32 — bậc 8)
- [ ] **Note ghi chú** explain logic không thấy trên màn

## Annotation (Ghi chú) — Phần BA hay quên

Wireframe không tự nói được. BA phải annotate:

```
┌──────────────────────────────┐
│  [Email input]               │ ← (1) Validate real-time RFC 5322,
│                              │     hiển thị lỗi dưới field
│  [Password]               👁  │ ← (2) Min 8 ký tự, có toggle show/hide
│                              │
│  [☑ Nhớ tôi]                │ ← (3) Lưu refresh token 30 ngày
│                              │
│  [   Đăng nhập   ]           │ ← (4) Disable nếu form invalid
│                              │     Loading state khi submit
│                              │
│  [Quên mật khẩu?]            │ ← (5) Mở màn /forgot-password
└──────────────────────────────┘

Notes:
(1) Email regex: /^[^\s@]+@[^\s@]+\.[^\s@]+$/
(2) Password ẩn mặc định
(3) Token expire sau 30 ngày inactive
(4) Show error: "Email hoặc mật khẩu không đúng"
(5) Edge case: nếu account chưa verify email → message khác
```

## User Flow Mapping (link wireframes)

Trong Figma/Miro, nối các màn bằng arrow:

```
[Login] ─────── login OK ────────► [Home]
   │
   ├── forgot pwd ────► [Forgot] ────► [Reset success] ────► [Home]
   │
   └── register ──────► [Register] ─── verify OTP ──► [Onboarding] ─► [Home]
```

Mỗi mũi tên = 1 transition + condition (login OK, OTP đúng, etc.)

## Component Library — Khi dự án lớn

Khi có 30+ màn, định nghĩa **design system**:

| Component | Variants | States |
|---|---|---|
| Button | Primary, Secondary, Ghost, Link | Default, Hover, Pressed, Disabled, Loading |
| Input | Text, Email, Password, Number, Date | Default, Focus, Error, Disabled |
| Card | Default, Highlighted, Compact | Static, Interactive |
| Modal | Center, Bottom Sheet, Toast | - |

→ Trong Figma dùng **Component + Auto-layout + Variants** → đổi 1 chỗ, cập nhật tất cả.

## Mobile vs Web — Khác biệt cốt lõi

| Yếu tố | Mobile | Web |
|---|---|---|
| Layout | 1 cột, scroll dọc | Multi-column, grid |
| Touch target | ≥ 44x44px | Click chuột nhỏ hơn OK |
| Navigation | Bottom tab / hamburger | Top nav / sidebar |
| Input | Bàn phím che màn dưới | Có chuột + bàn phím |
| Action | Bottom CTA, swipe | Top right CTA, hover |
| Density | Cao (ít info/màn) | Thấp (nhiều info/màn) |

## Responsive Breakpoints (cho web)

```
Mobile:   320 - 767px   (1 column)
Tablet:   768 - 1023px  (2 columns)
Desktop:  1024 - 1439px (3 columns)
Wide:     1440px+       (4 columns)
```

Vẽ wireframe 3 size: mobile (375), tablet (768), desktop (1440).

## Anti-patterns trong wireframe

❌ **Lorem ipsum** → dùng text thật tiếng Việt, dài ngắn ảnh hưởng layout
❌ **Logo placeholder** ở mọi nơi → distract khỏi flow chính
❌ **Bỏ qua error/empty state** → khi build mới phát hiện thiếu
❌ **Không có annotation** → handoff dev → dev đoán → bug
❌ **Quá nhiều CTA** trên 1 màn → user paralysis. Quy tắc: 1 màn = 1 primary CTA
❌ **Wireframe không scrollable** → quên rằng mobile content dài
❌ **Đẹp quá ở giai đoạn lo-fi** → stakeholder không dám phê bình

## Công cụ recommend

| Mục đích | Công cụ | Cost |
|---|---|---|
| Lo-fi nhanh | **Excalidraw** | Free |
| Lo-fi pro | **Balsamiq** | $9/mo |
| Mid + Hi-fi | **Figma** | Free tier OK |
| Prototype interactive | **Figma** / **ProtoPie** | Free / $15/mo |
| Code-based design | **TLDraw** / **Penpot** | Free |
| Vẽ tay | **Giấy A4 + bút** | Free |

**Recommend cho solo dev Việt Nam**: Figma (free) cho mọi thứ.

## Mẹo từ thực tế

1. **Vẽ trên giấy trước** — bao giờ cũng nhanh hơn mở Figma
2. **Crazy 8s** — chia giấy 8 ô, mỗi ô vẽ 1 ý tưởng trong 1 phút (8 phút có 8 ý tưởng)
3. **Steal like an artist** — screenshot UI hay của Grab, Shopee, Foody → adapt cho mình
4. **Show your work early** — wireframe xấu nhưng review sớm > wireframe đẹp review trễ
5. **Test với user thật** — đưa wireframe trên điện thoại, bảo họ "đặt một đơn" → quan sát

## Áp dụng cho solo developer

- Skip BRD/SRS dài → nhưng **đừng skip wireframe**
- Wireframe = đi trước code 1 ngày = tiết kiệm 1 tuần refactor
- Vẽ tay lo-fi 30 phút → mở Figma 1-2h cho hi-fi
- Hi-fi xong → Figma Dev Mode → copy CSS/measurements thẳng vào code
