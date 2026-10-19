# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Lê Nguyễn Nhật Khánh
- **MSSV:** 125001660
- **Tên đề tài Website:** Landing Page Tri Ân Thầy Cô 20/11 — Ngày Nhà giáo Việt Nam
- **Công cụ AI đã sử dụng:** opencode (mô hình big-pickle) — CLI agent lập trình trên terminal

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> "tôi muốn làm 1 trang web về ngày nhà giáo việt nam"

Prompt tổng quan ban đầu: xác định chủ đề (tri ân thầy cô 20/11), yêu cầu AI tạo cấu trúc dự án chuẩn gồm `index.html`, `style.css`, thư mục `assets/` và đẩy lên GitHub repository đã có sẵn (`KHANH_LENGUYENNHAT_125001660`).

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration)

### Lần 1: Dự Semantic HTML5 & cấu trúc nội dung ban đầu

- **Prompt đã dùng:**
  > "Website phải sử dụng đúng ngữ nghĩa các thẻ HTML5: `<header>` (logo, navigation menu), `<nav>` (thanh điều hướng), `<main>` (khu vực nội dung chính), `<section>` hoặc `<article>` (chia các khối nội dung rõ ràng), `<footer>` (chân trang chứa thông tin liên hệ, copyright,...)."
- **Kết quả AI tạo ra:** Trang web 3 section (Về ngày lễ, Lời chúc, Lời cảm ơn) đúng chuẩn semantic: `<header class="hero">` chứa logo + `<nav>`, `<main>` bọc các `<section>`, `<footer>` có copyright; asset SVG tự vẽ trong `assets/flower.svg`.
- **Nhận xét & Tinh chỉnh của SV:** Cấu trúc thẻ tốt, nhưng footer chưa đủ thông tin liên hệ — đã yêu cầu bổ sung email và copyright đầy đủ.

### Lần 2: Tích hợp CSS Variables, Layout hiện đại & Thư viện hiệu ứng

- **Prompt đã dùng:**
  > "Sử dụng CSS Variables (`:root { --primary-color: ...; }`) để quản lý phối màu, font chữ và spacing nhất quán. Áp dụng Layout hiện đại: Flexbox hoặc Grid responsive. Tích hợp Animate.css cho tiêu đề/Hero/Button CTA. Tích hợp AOS (Animate On Scroll) cho các section nội dung. Hiệu ứng `:hover`, `:focus` tự viết cho nút bấm và cards."
- **Kết quả AI tạo ra:** Bộ CSS Variables đầy đủ (color/font/spacing/radius/transition), Flexbox cho nav–hero–footer, Grid cho cards và quotes; nhúng Animate.css + AOS qua CDN kèm `AOS.init()`; hiệu ứng hover/focus cho btn, card, blockquote, nav-link.
- **Thách thức gặp phải:** Ban đầu code dùng nhiều `div` trung gian, chữ trên trang hơi dày và thiếu khoảng thở; hiệu ứng AOS có thể "đỡ" nội dung nếu không init đúng.
- **Cách sửa prompt (Debug prompt):**
  > "tôi muốn nó đẹp hơn và chữ phải ngăn nắp hơn được không"

  Yêu cầu AI thiết kế lại typography (Google Fonts Playfair Display + Be Vietnam Pro), thêm `line-height`, `text-wrap: balance/pretty`, container cố định, giảm số `div` vô nghĩa (dùng `<article>`, `<header>` cho block nội dung), và giữ hiệu ứng vừa phải không rối mắt.

### Lần 3: Hoàn thiện UI/UX & kiểm tra theo rubric

- **Prompt đã dùng:** Rà lại theo bảng tiêu chí chấm điểm: thẻ `<div>` vô nghĩa, CSS Variables cho color/font, cân đối Flexbox/Grid, UI/UX thẩm mỹ, Animate.css/AOS đúng cách, chuyển động mượt không lạm dụng.
- **Kết quả AI tạo ra:** Bổ sung `prefers-reduced-motion`, scroll hint tinh tế, card gradient mảnh ẩn/hiện khi hover, thư cảm ơn kiểu giấy viết tay, footer 2 cột thông tin — đạt yêu cầu thẩm mỹ và không lạm dụng animation.
- **Nhận xét & Tinh chỉnh của SV:** Giao diện hiện tại đạt yêu cầu; đã commit và push lên GitHub, chuẩn bị bật GitHub Pages để giảng viên xem live.

---

## 3. Đánh giá cá nhân về quá trình Vibe Coding

- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**
  Dựng nhanh khung HTML semantic + CSS đầy biến (variables) và tích hợp thư viện hiệu ứng chỉ vài dòng prompt — phần mất nhiều ngày nếu code tay, đặc biệt là responsive layout và animation stagger.

- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web?**
  1. Prompt nên **gắn ràng buộc cụ thể** (thẻ HTML5 nào, biến CSS tên gì, thư viện nào) thay vì chung chung "làm cho đẹp".
  2. **Chỉnh sửa lặp lại (iterative)** hiệu quả hơn một prompt dài: mỗi lần chỉ nêu 1 vấn đề (ví dụ "chữ ngăn nắp hơn") sẽ cho kết quả chính xác hơn.
  3. Luôn **tự kiểm tra lại code** (kiểm tra thẻ div thừa, animation có chạy, mobile có vỡ layout không) thay vì tin 100% kết quả AI.
