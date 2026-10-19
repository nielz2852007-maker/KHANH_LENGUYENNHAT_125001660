# NHẬT KÝ PROMPT ENGINEERING (VIBE CODING LOG)

- **Họ và tên:** Lê Nguyễn Nhật Khánh
- **MSSV:** 125001660
- **Tên đề tài Website:** Landing Page Tri Ân Thầy Cô 20/11 — Ngày Nhà giáo Việt Nam
- **Công cụ AI đã sử dụng:** Antigravity và GEMINI ( KHÁM PHÁ )
- **Phương pháp làm việc:** Vibe Coding — trao đổi bằng ngôn ngữ tự nhiên với AI, code được sinh ra và tinh chỉnh theo từng vòng lặp (iteration), SV đóng vai trò người review & ra ràng buộc.

---

## 1. Yêu cầu ban đầu (System/Initial Prompt)

> "tôi muốn làm 1 trang web về ngày nhà giáo việt nam"

**Bối cảnh gửi kèm cho AI:** repository GitHub đã tạo sẵn `KHANH_LENGUYENNHAT_125001660` (đang trống), thư mục làm việc local, và yêu cầu sản phẩm phải gồm:

- File mã nguồn website: `index.html`, `style.css`, thư mục `assets/`...
- File `PROMPT_LOG.md` (nhật ký Prompt Engineering)
- Kích hoạt GitHub Pages để giảng viên xem trực tiếp giao diện live

**Ý nghĩa của prompt này:** thay vì mô tả kỹ thuật (giả lập requirements kỹ thuật), SV đặt vấn đề bằng **ngôn ngữ đời thường** — AI tự suy luận stack phù hợp (HTML/CSS thuần, không framework), tự đề xuất cấu trúc dự án và quy trình đẩy Git. Đây là đặc trưng của Vibe Coding: **mục tiêu + ràng buộc**, chi tiết kỹ thuật để AI đề xuất.

---

## 2. Quá trình tinh chỉnh & Giải quyết sự cố (Iteration)

### Lần 1: Dự khung dự án & Semantic HTML5

- **Prompt đã dùng:**
  > "Website phải sử dụng đúng ngữ nghĩa các thẻ HTML5:
  > ● `<header>` (Chứa logo, navigation menu)
  > ● `<nav>` (Thanh điều hướng)
  > ● `<main>` (Khu vực nội dung chính)
  > ● `<section>` hoặc `<article>` (Chia các khối nội dung rõ ràng)
  > ● `<footer>` (Chân trang chứa thông tin liên hệ, copyright,...)"

- **Kết quả AI tạo ra:**
  - Cấu trúc trang: Hero (`<header>` + `<nav>` menu 3 mục) → `<main>` chứa 3 `<section>` (Về ngày lễ / Lời chúc / Lời cảm ơn) → `<footer>`.
  - Nội dung 3 thẻ card (Lịch sử, Ý nghĩa, Hoạt động), 4 `blockquote` lời chúc, thư cảm ơn.
  - Asset `assets/flower.svg` do AI vẽ vector (bông hoa tri ân) — không dùng ảnh bên ngoài.

- **Nhận xét & Tinh chỉnh của SV:**
  - Ban đầu AI dùng nhiều `<div>` cho khối card → yêu cầu chuyển sang `<article>`, khối tiêu đề mỗi section dùng `<header>` cho đúng ngữ nghĩa.
  - Footer chưa đủ thông tin → yêu cầu bổ sung email liên hệ + dòng copyright `(© 2026 ...)` đúng yêu cầu đề bài.

---

### Lần 2: CSS Variables, Layout hiện đại & Tích hợp thư viện hiệu ứng

- **Prompt đã dùng:**
  > "2. Kỹ thuật CSS & CSS Variables
  > ● Sử dụng CSS Variables (`:root { --primary-color: ...; }`) để quản lý phối màu, font chữ và spacing nhất quán cho toàn bộ trang.
  > ● Áp dụng Layout hiện đại: CSS Flexbox hoặc CSS Grid để căn chỉnh responsive cơ bản.
  > 3. Tương tác & Hiệu ứng (Libraries)
  > ● Tích hợp Animate.css: áp dụng hiệu ứng động cho Text tiêu đề, Hero Section, Button CTA.
  > ● Tích hợp AOS (Animate On Scroll): tạo hiệu ứng xuất hiện cuộn trang sinh động cho các section.
  > ● Hiệu ứng `:hover`, `:focus` tự viết bằng CSS cho nút bấm và các thẻ bài viết (cards)."

- **Kết quả AI tạo ra:**
  - `:root` khai báo biến theo nhóm: màu (`--color-primary`, `--color-accent`...), font (`--font-heading`, `--font-body`), spacing (`--sp-1 ÷ --sp-6`), radius, transition — toàn trang chỉ dùng biến.
  - **Flexbox:** `.nav`, `.hero`, `.hero-actions`, `.footer` · **CSS Grid:** `.cards` và `.quotes` với `repeat(auto-fit, minmax(...))` — tự responsive.
  - Nhúng CDN: Animate.css 4.1.1 + AOS 2.3.4; gắn class `animate__fadeInDown/fadeUp/zoomIn` kèm `animate__delay-*` cho Hero; gắn `data-aos="fade-up|zoom-in|flip-up"` cho section/cards/thư cảm ơn, khởi tạo `AOS.init({ duration: 800, once: true })`.
  - Hover/focus tự viết: nút CTA (nâng + đổi bóng + outline `:focus-visible`), card (translateY + viền vàng), blockquote, nav-link, footer link.

- **Thách thức gặp phải:**
  1. Nút CTA không thấy rõ trạng thái khi dùng bàn phím (thiếu `:focus-visible`).
  2. Sợ AOS "chặn" nội dung nếu JS lỗi → nội dung biến mất khi cuộn.

- **Cách sửa prompt (Debug prompt):**
  > "hiệu ứng focus bàn phím cho nút và link chưa rõ, thêm outline chuẩn; đồng thời đảm bảo nếu AOS/JS không load thì nội dung vẫn hiển thị bình thường (không bị ẩn)."

  → AI thêm `:focus-visible` outline cho mọi phần tử tương tác và rule an toàn cho AOS.

---

### Lần 3: Tinh chỉnh typography & thẩm mỹ giao diện

- **Prompt đã dùng:**
  > "tôi muốn nó đẹp hơn và chữ phải ngăn nắp hơn được không"

- **Kết quả AI tạo ra (thiết kế lại gần như toàn bộ giao diện):**
  - Google Fonts: **Playfair Display** (tiêu đề, chữ nghiêng sang trọng) + **Be Vietnam Pro** (nội dung, hiển thị tiếng Việt chuẩn).
  - Chữ "ngăn nắp": `line-height: 1.75`, `text-wrap: balance` cho heading, `text-wrap: pretty` cho đoạn văn, container cố định `1080px` căn giữa, hệ thống spacing nhất quán.
  - Chi tiết thẩm mỹ: viền vàng mảnh quanh Hero, thẻ card đánh số 01/02/03, thanh gradient ẩn/hiện khi hover, thư cảm ơn kiểu giấy viết tay có bó hoa SVG, footer 2 cột (thương hiệu + thông tin liên hệ).

- **Thách thức gặp phải:** Chữ ban đầu bị dày, khối chữ trái phải không đều, nhiều `div` trung gian vô nghĩa.

- **Cách sửa prompt (Debug prompt):**
  > Rà theo tiêu chí: "không lạm dụng `<div>` vô nghĩa" → yêu cầu AI dùng `<article>`, `<header>` thay div bọc nội dung; kiểm tra lại toàn bộ độ rộng dòng và khoảng cách giữa các khối.

- **Nhận xét & Tinh chỉnh của SV:** Giao diện sau lần này đạt mức "hoàn thiện cao" — kiểm tra trên cả desktop và mobile đều không vỡ layout.

---

### Lần 4: Kiểm tra theo rubric & hoàn thiện chi tiết nhỏ

- **Prompt đã dùng:**
  > Rà giúp tôi theo bảng tiêu chí chấm: thẻ ngữ nghĩa, `<div>` vô nghĩa, CSS Variables cho color/font, cân đối Flexbox/Grid, UI/UX thẩm mỹ, Animate.css/AOS đúng cách, hiệu ứng mượt không lạm dụng. Còn gì chưa đạt thì sửa luôn.

- **Kết quả AI tạo ra / sửa trực tiếp:**
  - Thêm `<meta name="description">` + thẻ Open Graph (OG title/description/type) để link chia sẻ đẹp.
  - Thêm **skip-link** ("Bỏ qua điều hướng") trỏ tới `#main-content` cho hỗ trợ bàn phím.
  - Sửa logo link `href="#"` → `href="#top"` (đúng chuẩn, không nhảy lung tung).
  - Thêm `@media (prefers-reduced-motion: reduce)` — tắt animation cho người nhạy cảm với chuyển động → chuyển động "mượt mà, không lạm dụng".
  - Tạo `README.md` giới thiệu cấu trúc dự án + hướng dẫn chạy local + link Pages.

- **Nhận xét & Tinh chỉnh của SV:** Các chi tiết nhỏ này thường bị quên nhưng lại là điểm cộng khi GV chấm "tính hoàn thiện".

---

### Lần 5: Triển khai thật & xử lý sự cố Git/GitHub Pages

- **Prompt đã dùng:**
  > "đẩy code lên GitHub repository và bật GitHub Pages để giảng viên xem live"

- **Thách thức gặp phải (sự cố thật):**
  1. `git push` bị **rejected** với lỗi `fetch first` — vì SV đã sửa file trực tiếp trên web GitHub → có commit mới hơn ở remote.
  2. Cần bật GitHub Pages nhưng công cụ CLI chưa đăng nhập.
  3. Email trong footer ban đầu do AI đặt là email mẫu, có thể sai chính tả.

- **Cách sửa prompt (Debug prompt):**
  > "push bị lỗi fetch first, xử lý giúp tôi mà không mất commit của tôi hay của AI"

  → AI chạy `git pull --rebase origin main` → gộp lịch sử gọn gàng (không commit trùng), giữ nguyên cả thay đổi trên web lẫn thay đổi local, push thành công. Hướng dẫn SV bật **Settings → Pages → Deploy from branch → main/root**, SV tự bật và AI kiểm tra lại bằng cách fetch URL Pages để xác nhận trang live hiển thị đủ nội dung.

- **Kết quả:** Website live tại
  `https://nielz2852007-maker.github.io/KHANH_LENGUYENNHAT_125001660/`

---

### Lần 6: Sản phẩm bổ sung — file thuyết trình 7 slide

- **Prompt đã dùng:**
  > "làm cho 7 slide đi"

- **Kết quả AI tạo ra:** File `slides/Bai_Tap_20_11_LNNKhanh.pptx` (7 slide 16:9, cùng tông màu với website) bằng script `python-pptx`: bìa → giới thiệu đề tài → cấu trúc HTML5 → CSS Variables/Layout → hiệu ứng/thư viện → nhật ký prompt (phần này) → kết quả + link live.

---

## 3. Bảng kỹ thuật Prompt Engineering đã áp dụng

| Kỹ thuật | Cụ thể trong dự án |
|---|---|
| **Context / Bối cảnh** | Gửi link repo trống, mô tả sản phẩm phải có (index.html, PROMPT_LOG.md, Pages) |
| **Constraint (Ràng buộc)** | Liệt kê đúng 5 nhóm thẻ HTML5; nêu tên thư viện Animate.css/AOS; cấm lạm dụng `<div>` |
| **Persona (Vai trò)** | AI đóng vai lập trình viên web senior làm việc với khách hàng không rành kỹ thuật |
| **Iterative refinement** | 6 lần tinh chỉnh, mỗi lần 1 vấn đề cụ thể thay vì một prompt dài duy nhất |
| **Debug prompt** | Mô tả *triệu chứng* (ví dụ "push bị fetch first", "focus chưa rõ") thay vì chỉ định lệnh — AI tự chọn cách sửa |
| **Self-check / Review prompt** | "Rà giúp tôi theo bảng tiêu chí..." — ép AI đối chiếu rubric với code đã sinh |
| **Output format** | Yêu cầu cấu trúc file rõ ràng, trả về mô tả ngắn gọn để SV dễ review |

---

## 4. Đánh giá cá nhân về quá trình Vibe Coding

- **AI đã giúp bạn tiết kiệm thời gian ở phần nào nhất?**
  1. **Dự khung HTML + CSS hệ thống:** dựng semantic HTML, bộ CSS Variables, layout Flexbox/Grid responsive chỉ mất vài prompt — phần này nếu code tay mất nhiều ngày, đặc biệt là chỉnh breakpoint mobile.
  2. **Tích hợp thư viện & animation stagger:** gắn class Animate.css/AOS kèm delay theo thứ tự từng phần tử — việc căn timing thủ công rất dễ sai.
  3. **Xử lý sự cố Git:** nhờ AI giải thích và chạy `rebase` khi push bị từ chối, tránh được lỗi mất commit thường gặp với người mới.
  4. **Sinh sản phẩm kèm theo:** nhật ký báo cáo, README, file slide 7 trang — đều được tạo nhanh từ đúng dữ liệu dự án.

- **Bài học rút ra khi đặt câu hỏi (Prompt) cho AI trong thiết kế web:**
  1. **Ràng buộc rõ thắng kết quả rõ:** prompt chung chung ("làm cho đẹp") cho kết quả mong lung; prompt nêu đích danh thẻ HTML5, tên biến CSS, tên thư viện thì AI trả về đúng thứ cần dùng.
  2. **Chỉnh lặp lại (iterative) tốt hơn một prompt dài:** mỗi vòng chỉ nêu 1 vấn đề ("chữ chưa ngăn nắp", "focus chưa thấy") — AI sửa đúng chỗ, không phá chỗ khác.
  3. **Mô tả triệu chứng, không chỉ lệnh:** khi debug, nói "trang bị ẩn khi AOS lỗi" hiệu quả hơn "tắt AOS đi" — AI còn đề xuất hướng fix bền hơn.
  4. **Không tin 100% AI:** luôn tự mở trang, kéo thử trên mobile, kiểm tra tab bàn phím, đọc lại commit trước khi push. AI viết email mẫu, tạo `div` thừa, đặt `href="#"` — những lỗi nhỏ này đều do SV phát hiện khi review.
  5. **Prompt yêu cầu AI tự rà rubric** ("rà giúp tôi theo tiêu chí chấm") là cách rất hiệu quả để bắt lỗi trước khi nộp bài.
