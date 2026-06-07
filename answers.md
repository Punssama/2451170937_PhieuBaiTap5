# BÀI LÀM — PBT 05

## PHẦN A — KIỂM TRA ĐỌC HIỂU

### Câu A1 — Viewport & Mobile-First

1. Thẻ `<meta viewport>` chuẩn:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

**Giải thích:**

- `width=device-width`: đặt chiều rộng layout bằng đúng chiều rộng màn hình thiết bị.
- `initial-scale=1.0`: trang được hiển thị ở mức zoom ban đầu là 100%.

2. Nếu thiếu thẻ này, iPhone sẽ thường render trang theo kiểu desktop width (thường khoảng 980px), sau đó thu nhỏ lại để vừa màn hình. Kết quả là chữ nhỏ, layout nhìn bị zoom out và khó dùng trên mobile.

3. Mobile-First và Desktop-First:

**Mobile-First**: viết CSS mặc định cho mobile trước, rồi mở rộng dần bằng `min-width`.

```css
.container {
  width: 100%;
}

@media (min-width: 768px) {
  .container {
    width: 720px;
  }
}
```

**Desktop-First**: viết CSS mặc định cho desktop, rồi thu nhỏ bằng `max-width`.

```css
.container {
  width: 1200px;
}

@media (max-width: 767px) {
  .container {
    width: 100%;
  }
}
```

**Vì sao Mobile-First được khuyên dùng:**

- Phù hợp xu hướng người dùng mobile nhiều hơn.
- CSS gốc đơn giản, nhẹ hơn.
- Dễ mở rộng dần cho màn hình lớn.
- Hạn chế ghi đè CSS phức tạp.

---

### Câu A2 — Breakpoints

| Breakpoint | Kích thước | Thiết bị đại diện | Gợi ý lưới sản phẩm |
| ---------- | ---------: | ----------------- | ------------------- |
| `xs`       |  `< 576px` | Mobile nhỏ        | 1 cột               |
| `sm`       |  `≥ 576px` | Mobile lớn        | 1 - 2 cột           |
| `md`       |  `≥ 768px` | Tablet            | 2 cột               |
| `lg`       |  `≥ 992px` | Laptop nhỏ        | 3 cột               |
| `xl`       | `≥ 1200px` | Desktop           | 4 cột               |
| `xxl`      | `≥ 1400px` | Desktop lớn       | 4 - 6 cột           |

**Ghi chú:** `xs` thường là mặc định, không cần viết media query riêng.

---

### Câu A3 — Media Queries

| Chiều rộng màn hình | `.container` width |
| ------------------- | ------------------ |
| 375px (iPhone SE)   | `100%`             |
| 600px               | `540px`            |
| 800px               | `720px`            |
| 1000px              | `960px`            |
| 1400px              | `1140px`           |

**Lý do:** trình duyệt áp dụng rule theo `min-width` gần nhất thỏa điều kiện.

---

### Câu A4 — SCSS Basics

1. **Variables**

   Dùng biến để tái sử dụng giá trị như màu sắc, font, spacing.

   ```scss
   $primary-color: #2f80ed;

   .btn {
     background: $primary-color;
   }
   ```

2. **Nesting**

   Viết CSS lồng nhau để thể hiện rõ quan hệ cha - con.

   ```scss
   .card {
     .title {
       font-weight: 700;
     }
   }
   ```

3. **Mixins**

   Tạo khối CSS tái sử dụng, có thể truyền tham số.

   ```scss
   @mixin flex-center {
     display: flex;
     justify-content: center;
     align-items: center;
   }

   .box {
     @include flex-center;
   }
   ```

4. **`@extend` / Inheritance**

   Cho phép một selector kế thừa style từ selector khác.

   ```scss
   .btn-base {
     padding: 10px 16px;
     border-radius: 8px;
   }

   .btn-primary {
     @extend .btn-base;
     background: #2f80ed;
     color: #fff;
   }
   ```

**Vì sao trình duyệt không đọc trực tiếp `.scss`:**

- SCSS là ngôn ngữ tiền xử lý, không phải CSS thuần.
- Trình duyệt chỉ hiểu file CSS đã biên dịch.
- Cần bước **compile SCSS → CSS** bằng Sass compiler trước khi chạy trang.

---

## PHẦN B — THỰC HÀNH CODE

### Bài B1 — Responsive Product Page

- File: [responsive.html](responsive.html)
- File: [responsive.css](responsive.css)

**Đã làm đúng yêu cầu chính:**

- Mobile-first, CSS mặc định 1 cột.
- `@media (min-width: 768px)` cho tablet.
- `@media (min-width: 1024px)` cho desktop.
- Navigation hamburger trên mobile, menu ngang trên tablet/desktop.
- Sidebar ẩn trên mobile, hiện lại từ tablet.
- 8 product cards.
- Ảnh responsive với `max-width: 100%; height: auto;`.

### Bài B2 — CSS Transitions & Animations

- File: [animations.html](animations.html)
- File: [animations.css](animations.css)

**Đã làm đủ 5 hiệu ứng:**

- Card hover: `translateY(-8px)` + shadow.
- Button hover: đổi màu + scale nhẹ.
- Image zoom: ảnh phóng to khi hover.
- Loading spinner: `@keyframes spin`.
- Fade-in: `@keyframes fadeIn`.

### Bài B3 — SCSS Refactor

- Folder: [scss](scss)
- File: [scss/\_variables.scss](scss/_variables.scss)
- File: [scss/\_mixins.scss](scss/_mixins.scss)
- File: [scss/\_components.scss](scss/_components.scss)
- File: [scss/style.scss](scss/style.scss)
- File output: [scss/style.css](scss/style.css)

**Lệnh compile:**

```bash
npx -y sass scss/style.scss scss/style.css
```

---

## PHẦN C — PHÂN TÍCH

### Câu C1 — Phân tích trang web thực

**Em chọn trang Shopee** để phân tích responsive ở 3 kích thước màn hình.

#### 1) Mobile — 375px

- Navigation thu gọn, ưu tiên nút menu/hamburger.
- Thanh tìm kiếm vẫn có nhưng bố cục nhỏ gọn hơn.
- Số cột sản phẩm ít, thường là 1 - 2 cột.
- Một số banner hoặc sidebar phụ bị ẩn để tiết kiệm diện tích.
- Font size nhỏ hơn và nội dung được xếp theo chiều dọc.

#### 2) Tablet — 768px

- Menu hiển thị nhiều hơn so với mobile.
- Grid sản phẩm tăng lên 2 - 3 cột.
- Banner và các block nội dung có thể hiển thị đầy đủ hơn.
- Các phần phụ trợ như gợi ý danh mục bắt đầu xuất hiện rõ.

#### 3) Desktop — 1440px

- Navigation đầy đủ, menu ngang rõ ràng.
- Grid sản phẩm rộng hơn, thường 4 cột hoặc nhiều hơn.
- Sidebar, banner, khối khuyến mãi và danh mục đều hiển thị đồng thời.
- Font size và khoảng trắng được tối ưu cho màn hình lớn.

#### 4) Media queries thường thấy trong DevTools

- `@media (min-width: 768px)` — chuyển từ mobile lên tablet.
- `@media (min-width: 1024px)` hoặc `@media (min-width: 1200px)` — tối ưu cho desktop.
- Một số layout còn dùng `max-width` để ẩn/hiện thành phần ở mobile.

---

### Câu C2 — Thiết kế Responsive Strategy

## 1. Wireframe theo 3 kích thước

### Mobile

- Header: logo + nút đặt bàn + icon menu.
- Hero image chiếm toàn chiều ngang.
- Grid món ăn: 1 cột.
- Form đặt bàn: nằm dưới grid món ăn.
- Bản đồ: đặt dưới form.
- Footer: cuối trang.

```text
┌──────────────────────┐
│ Header               │
├──────────────────────┤
│ Hero image           │
├──────────────────────┤
│ Grid món ăn (1 cột)  │
├──────────────────────┤
│ Form đặt bàn         │
├──────────────────────┤
│ Google Maps          │
├──────────────────────┤
│ Footer               │
└──────────────────────┘
```

### Tablet

- Header vẫn giữ gọn nhưng đầy đủ hơn mobile.
- Grid món ăn: 2 cột.
- Form đặt bàn và bản đồ vẫn xếp dọc để dễ thao tác.

```text
┌────────────────────────────────┐
│ Header                         │
├────────────────────────────────┤
│ Hero image                     │
├────────────────────────────────┤
│ Grid món ăn (2 cột)            │
├────────────────────────────────┤
│ Form đặt bàn                   │
├────────────────────────────────┤
│ Google Maps                    │
├────────────────────────────────┤
│ Footer                         │
└────────────────────────────────┘
```

### Desktop

- Layout 2 cột tổng thể.
- Cột trái: hero + grid món ăn.
- Cột phải: form đặt bàn + bản đồ, có thể đặt sticky.
- Grid món ăn: 3 hoặc 4 cột tùy chiều rộng.

```text
┌────────────────────────────────────────────────────┐
│ Header                                             │
├───────────────────────────────┬────────────────────┤
│ Hero + Grid món ăn            │ Form đặt bàn       │
│ (3-4 cột)                     │ + Google Maps      │
├───────────────────────────────┴────────────────────┤
│ Footer                                             │
└────────────────────────────────────────────────────┘
```

## 2. CSS skeleton Mobile-First

```css
/* Base - Mobile */
.page {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

.header,
.hero,
.menu-grid,
.booking-form,
.map,
.footer {
  width: 100%;
}

.menu-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

/* Tablet */
@media (min-width: 768px) {
  .menu-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .page {
    gap: 24px;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  .page {
    grid-template-columns: 2fr 1fr;
    align-items: start;
  }

  .main-content {
    display: grid;
    gap: 24px;
  }

  .menu-grid {
    grid-template-columns: repeat(3, 1fr);
  }

  .sidebar {
    display: grid;
    gap: 24px;
  }
}
```

**Kết luận:**

- Mobile: ưu tiên nội dung chính, 1 cột.
- Tablet: mở rộng thành 2 cột cho gallery.
- Desktop: chia layout rõ ràng, tận dụng không gian lớn bằng Grid + sidebar.

---

## Ghi chú screenshots

- Chụp 3 màn hình: 375px, 768px, 1440px.
- Chụp thêm DevTools để thấy `@media` rules của trang đã chọn.
