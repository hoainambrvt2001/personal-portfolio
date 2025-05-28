# Braxton Personal Portfolio – Project Context (for GitHub Copilot)

> **Mục tiêu**: Cung cấp Copilot (và mọi AI khác được tích hợp vào VS Code) bức tranh toàn cảnh về cấu trúc, công nghệ và quy ước mã của dự án. Nội dung này _không_ được đóng gói lên production; chỉ dùng cho trợ lý mã.

---

## 1 – Tên & mô tả ngắn
- **Tên** : *Braxton Personal Portfolio & Résumé* (fork tuỳ chỉnh).
- **Chức năng chính**: Trang portfolio một trang (one-page) với phần trình bày cá nhân, gallery, testimonials, tải CV, form liên hệ Ajax.
- **Thiết kế gốc**: Template HTML5 của **mix_design** (ThemeForest) – version `1.0.1` (18-04-2025).

---

## 2 – Kiến trúc thư mục gốc
```
/ (root)
│  index.html          # trang chính (hoặc demo_xxx.html -> index.html)
│  mail.php            # Ajax contact (UniMail)
│  .htaccess           # cache rules
│
├─ css/
│   ├─ loaders/loader.css
│   ├─ plugins.css      # ↓ compile sẵn: Bootstrap 5 grid, FontAwesome 6.7.2, Phosphor 2.1.2,
│   ├─ main.css         # biến CSS, theme switch, layout.
│   └─ custom.css       # **<- chỗ ghi đè style** (không bị template update xoá).
│
├─ js/
│   ├─ libs.min.js      # gộp: jQuery 3.x, GSAP 3.12.7 (+ScrollTrigger), Lenis 1.2.3,
│   │                   # Modernizr, imagesLoaded, Swiper 11.2.6, PhotoSwipe v5.
│   ├─ gallery-init.js  # khởi tạo PhotoSwipe.
│   └─ app.js           # Swiper init, GSAP parallax & gradient, form Ajax.
│
├─ img/                # ảnh, favicon, background .webp/.png
├─ fonts/              # Webfonts Syne, FontAwesome, Phosphor
└─ source-files/       # CSS + JS không nén (tham khảo/gỡ lỗi)
```

> **Ghi chú Copilot**: Khi gợi ý đường dẫn, ưu tiên chuỗi tương đối tính từ file hiện hành; không hard-code domain.

---

## 3 – Thư viện & phiên bản chính
| Mục | Phiên bản | Nguồn |
| --- | --- | --- |
| HTML/CSS framework | **Bootstrap 5.3.5** | CDN / gói nội bộ (đã gộp) |
| Animation engine | **GSAP 3.12.7** + ScrollTrigger | libs.min.js |
| Slider | **Swiper 11.2.6** | "swiper-testimonials" trong `index.html` |
| Lightbox | **PhotoSwipe 5** | gallery-init.js |
| Smooth scroll | **Lenis 1.2.3** | libs.min.js |
| Icon fonts | FontAwesome 6.7.2 + Phosphor 2.1.2 | plugins.css |
| Build tool (optional) | **Gulp 5 + Sass** (BraxtonGULP) | `app/`, `dist/` |

---

## 4 – Build & Dev workflow _(tuỳ chọn khi dùng BraxtonGULP)_
```bash
# Cài đặt
npm install   # thiết lập node_modules

# Phát triển có live-reload
gulp          # alias default (Browsersync + Sass + watch)

# Đóng gói production -> dist/
gulp build    # minify HTML, CSS, JS, optimize images
```

> Nếu **không** dùng Gulp: chỉnh sửa trực tiếp trong `css/main.css`, `js/app.js`, và mở `index.html` bằng Live Server.

---

## 5 – Quy ước tuỳ chỉnh nhanh
- **CSS**: Thêm/ghi đè trong `css/custom.css`; không chỉnh trực tiếp `plugins.css`/`main.css` để tránh merge conflict khi update.
- **JS**: Đính kèm script mới ở cuối `<body>` ngay sau `app.js`. Tuân thủ IIFE hoặc ES6 modules.
- **Ảnh**: Lưu trong `img/`; background `.webp` ưu tiên; đường dẫn tương đối.
- **Theme**: Biến CSS màu nằm ở `:root` trong `main.css` (cả dark & light). Thêm biến màu mới => khai báo ở cả hai khối.
- **Form**: `#contact-form` gửi Ajax POST → `mail.php`; thay `admin_email` ẩn trong HTML.

---

## 6 – Các vùng mã quan trọng (Copilot highlight)
1. **Swiper init** (dòng ~20–35 trong `js/app.js`) – gợi ý tham số `slidesPerView`, breakpoints.
2. **GSAP Parallax** (`[data-speed]`) – có thể extend để animate opacity.
3. **Gradient Blur animation** – tham khảo hàm `random()` cuối `index.html`.
4. **Theme switcher** – nút `.color-switch` trong header, thao tác class `dark-theme`/`light-theme` trên `<html>`.
5. **Gulp config** – `gulpfile.js`: tasks `styles`, `scripts`, `images`, `serve`.

Copilot nên giữ nhất quán: **tab = 2 spaces**, **UTF-8**, **line-break LF**.

---

## 7 – Liên hệ & ghi chú
- Template gốc © mix_design (Envato). Mọi bản quyền hình ảnh giữ nguyên.
- Nếu thêm thư viện mới, cập nhật bảng Thư viện ở mục 3.
- Để bật Copilot Chat hiểu konteks, bảo đảm VS Code mở đồng thời file này với mã nguồn.

> *End of context. Updated: 28 May 2025.*
