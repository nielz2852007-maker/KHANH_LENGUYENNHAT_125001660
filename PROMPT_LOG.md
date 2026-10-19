# PROMPT_LOG.md — Nhật ký Prompt Engineering

**Sinh viên:** Lê Nguyễn Nhật Khánh
**MSSV:** 125001660
**Chủ đề:** Website tri ân Ngày Nhà giáo Việt Nam 20/11
**Công cụ AI:** opencode (big-pickle)

---

## Prompt 1 — Yêu cầu ban đầu

**Prompt người dùng:**
> https://github.com/nielz2852007-maker/KHANH_LENGUYENNHAT_125001660.git

**Phản hồi của AI:** Phân tích URL, xác nhận repository đang trống và hỏi hướng xử lý (clone hay push code từ thư mục本地).

---

## Prompt 2 — Xác định chủ đề

**Prompt người dùng:**
> tôi muốn làm 1 trang web về ngày nhà giáo việt nam

**Phản hồi của AI:** Khởi tạo git repository, tạo cấu trúc dự án:
- `index.html` — trang chính
- `style.css` — stylesheet
- `assets/flower.svg` — hình ảnh hoa tri ân (SVG vector tự vẽ)

---

## Prompt 3 — Yêu cầu chuẩn HTML5

**Prompt người dùng:**
> Website phải sử dụng đúng ngữ nghĩa các thẻ HTML5:
> ● `<header>` (Chứa logo, navigation menu)
> ● `<nav>` (Thanh điều hướng)
> ● `<main>` (Khu vực nội dung chính)
> ● `<section>` hoặc `<article>` (Chia các khối nội dung rõ ràng)
> ● `<footer>` (Chân trang chứa thông tin liên hệ, copyright,...)

**Phản hồi của AI:** Cấu trúc HTML5 được tổ chức:
- `<header class="hero">` chứa logo + `<nav>` menu điều hướng
- `<main>` bao gồm 3 `<section>`: Về ngày lễ, Lời chúc, Lời cảm ơn
- `<footer>` chứa câu danh ngôn, thông tin liên hệ và copyright

---

## Các kỹ thuật Prompt Engineering đã áp dụng

| Kỹ thuật | Áp dụng |
|---|---|
| **Persona** | AI đóng vai lập trình viên web |
| **Constraint** | Bắt buộc dùng thẻ HTML5 semantic |
| **Context** | Cung cấp chủ đề 20/11, tên repo, MSSV |
| **Iterative refinement** | Bổ sung yêu cầu dần: chủ đề → semantic HTML → footer liên hệ/copyright |
| **Output format** | Yêu cầu file cấu trúc chuẩn (index.html, style.css, assets/) |

---

## Kết quả

- [x] Website giao diện responsive, tông đỏ–vàng tri ân
- [x] Đúng ngữ nghĩa thẻ HTML5 (header/nav/main/section/footer)
- [x] Asset SVG tự tạo trong `assets/`
- [x] Push lên GitHub + kích hoạt GitHub Pages
