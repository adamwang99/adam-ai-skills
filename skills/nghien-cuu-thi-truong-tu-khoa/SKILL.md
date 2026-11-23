---
name: "nghien-cuu-thi-truong-tu-khoa"
description: "Dùng khi cần chọn ngách, chọn hướng nội dung, dựng cây chuyên mục, kiểm một chủ đề có đáng làm không, hoặc chọn sản phẩm và góc video ngắn làm affiliate (Amazon US, sàn VN) cho adamusesai, 3a, ai-world và mạng web tin: đo từ khoá, trending, đối thủ, review, luật, rồi chấm điểm ra quyết định."
---

# Nghiên cứu thị trường, từ khoá, trending → ra quyết định hướng đi

Mục tiêu: mọi đề xuất hướng đi phải có SỐ từ công cụ, không trả lời bằng cảm giác. Kết quả cuối luôn là một bảng chấm điểm + một quyết định + kế hoạch thử 6 tuần.

## Luật cứng
- Chỉ dùng công cụ miễn phí hoặc tài khoản bạn đã có (ví dụ Wriai). Không tự mua, không tự tạo tài khoản, không nhập mật khẩu, không thanh toán.
- Không vượt chặn bot, không đọc trang robots cấm; trang không đọc được thì chấm theo tiêu đề SERP và ghi rõ.
- Không in khoá. Khoá API (SerpApi, DataForSEO, Google Ads) do chủ tài khoản tạo và cất trong kho bí mật, không dán vào chat.
- Gắn nhãn mọi số liệu: [Đo] = từ công cụ, [Suy luận] = AI tính, [Chưa biết].
- Số tăng trưởng % và CPC của Wriai KHÔNG tin cậy → tăng trưởng lấy từ Google Trends.

## Bước 0. Chốt câu hỏi
Ghi 1 dòng: chọn ngách mới / mở chuyên mục / kiểm 1 chủ đề / lập cây trang / chọn sản phẩm và góc video affiliate. Ghi site hoặc kênh đích và thị trường (mặc định VN, tiếng Việt; affiliate Amazon thì US, tiếng Anh).
Câu hỏi là sản phẩm affiliate hay video ngắn: làm theo mục "Nhánh B" cuối skill, dùng lại Bước 3 (Trends) và Bước 7 (luật).

## Bước 1. Mở rộng hạt giống (30–50 từ)
- Lấy từ: gợi ý Google, People Also Ask, related queries của Trends, tiêu đề đối thủ, GSC của site mình.
- Có thể dùng skill seo-cluster (claude-seo) để mở rộng và gom cụm theo trùng SERP.
- Mẫu đuôi hay ra cơ hội: "<x> là gì", "<x> github", "cách dùng <x>", "<x> miễn phí", "<x> giá", "so sánh <x> <y>", "<x> tiếng việt".

## Bước 2. Đo lượng tìm + độ khó (Wriai Keyword Explorer, trình duyệt của bạn)
1. wriai.com/dashboard/keyword-explorer.
2. Nút vị trí → gõ "Việt" → chọn Việt Nam. Nút ngôn ngữ → gõ "Vietnam" → chọn Tiếng Việt.
3. Bấm vào ô hạt giống và nút Search bằng ref (cuộn lên đầu trước; bấm toạ độ hay trượt vào bảng).
4. Mỗi lần tìm tốn 2.000 credit; kết quả lưu 24h xem lại miễn phí → gom hạt giống, không tìm lặt vặt.
5. Nếu hiện popup nâng cấp: KHÔNG bấm "Để sau" (nó chuyển sang trang thanh toán); đóng popup.
6. Ghi: volume, KD, ý định (thông tin/mua), 10 từ liên quan lớn nhất.
Phương án dự phòng: Google Keyword Planner chỉ chạy khi bạn có tài khoản khách hàng Google Ads (seo-google: /seo google volume).

## Bước 3. Đo xu hướng (Google Trends)
- URL: https://trends.google.com/trends/explore?date=today%2012-m&geo=VN&q=A,B,C,D,MOC&hl=vi
- Mỗi lô tối đa 5 từ, LUÔN có 1 từ mốc chung (ví dụ "xe máy điện" hoặc một từ AI ổn định) để so giữa các lô.
- Đọc bằng get_page_text sau khi cuộn. Không bấm banner cookie.
- Ghi: điểm trung bình 12 tháng, xu hướng 3 tháng gần (lên/ngang/xuống), đỉnh đột biến (spike rồi về 0 = chủ đề sóng, không xây hub dài hạn), truy vấn "Đột phá".
- Thêm khung 5 năm (date=today%205-y) cho ngách định đầu tư dài.
- Thị trường US: `geo=US`, từ khoá tiếng Anh, bỏ `hl=vi`. Sản phẩm theo mùa hoặc mới nổi: thêm khung 90 ngày (`date=today%203-m`).
- So các tên gọi khác nhau của cùng một thứ trong 1 lô (ví dụ "portable blender", "mini blender", "personal blender") để chọn đúng chữ người dùng gõ.
- Đọc "Cụm từ tìm kiếm có liên quan" (Related queries), cả tab Gia tăng lẫn Hàng đầu, để lấy từ khoá phụ và góc nội dung.
- Trends chỉ là mức quan tâm TƯƠNG ĐỐI, không phải lượt tìm hay số đơn hàng. Cần số tuyệt đối thì dùng Wriai (Bước 2).

## Bước 4. Tín hiệu trending ngoài Google (mảng công nghệ/AI)
Không cần khoá:
- Hugging Face: https://huggingface.co/api/models?sort=trendingScore&limit=20
- OSS Insight: https://api.ossinsight.io/v1/trends/repos/?period=past_week&language=All
- GitHub search API (giới hạn tốc độ; sort=stars, created:>ngày).
- Nếu đã cài skill last30days: chạy cho Reddit, Hacker News, GitHub, Polymarket, YouTube (các nguồn không cần khoá). Bỏ qua X/TikTok nếu chưa có khoá.
Quy tắc: trending ngoài Google chỉ là tín hiệu SỚM; chỉ thành chủ đề khi Trends VN hoặc Wriai có lượng tìm.

## Bước 5. Soi đối thủ trên SERP
- 10 kết quả đầu cho 5–10 từ chính: loại site (báo, sàn, blog, docs), độ sâu bài, ngày cập nhật, có bảng/giá/so sánh không.
- Có thể dùng competitor-profiling / seo-competitor-pages / competitive-brief để dựng hồ sơ.
- Chấm "khe hở": SERP toàn diễn đàn/bài cũ/bài dịch máy = khe lớn; toàn báo lớn + hãng = khe nhỏ.

## Bước 6. Kiểm trùng trong hệ thống của mình
- Tải sitemap mọi site của bạn (mỗi ngôn ngữ); tìm slug/tiêu đề cùng từ khoá.
- Luật trùng gợi ý: chuyên mục được phép chồng lấn; chỉ tránh CÙNG từ khoá chính + CÙNG ý định cùng lúc; sổ từ khoá ghi lịch sử, không ghi "quyền sở hữu"; để GSC quyết sau 8–12 tuần; không sao chép/viết lại cùng một bài sang site khác.
- Google Search Console: xem site mình đã có hiển thị cho cụm này chưa.

## Bước 7. Kiểm luật và rủi ro
- Nghị định 147/2024: không đăng lại tin đã đăng trên báo VN ("thông tin tổng hợp") nếu không có giấy phép trang tổng hợp. Nguồn phải là nguồn gốc (hãng, repo, văn bản nhà nước, nghiên cứu).
- Chính sách spam Google: không nội dung hàng loạt, không lạm dụng uy tín site, link tài trợ gắn rel="sponsored".
- Ngành nhạy cảm (tài chính, y tế, pháp lý) ghi cảnh báo E-E-A-T.

## Bước 8. Chấm điểm và quyết định
Bảng mỗi ngách/cụm, thang 0–5 mỗi cột:
| Cột | Trọng số | Nguồn |
|---|---|---|
| Lượng tìm VN | 2 | Wriai [Đo] |
| Xu hướng 12 tháng | 2 | Trends [Đo] |
| Độ khó / khe hở SERP | 2 | Wriai KD + Bước 5 |
| Ý định mua / kiếm tiền (tài trợ, banner, affiliate) | 2 | Wriai intent + đối thủ có quảng cáo |
| Hợp năng lực đội viết và nguồn gốc sẵn có | 1 | [Suy luận] |
| Rủi ro luật/spam (điểm cao = rủi ro thấp) | 1 | Bước 7 |
Tổng tối đa 50. ≥30 làm ngay; 22–29 thử nhỏ; <22 để sau.
Ghi rõ điểm nào là [Suy luận].

## Bước 9. Đầu ra
1. Bảng chấm điểm + 3 hướng xếp hạng + 1 khuyến nghị.
2. Cây chuyên mục / hub-spoke (dùng site-architecture hoặc seo-cluster nếu cần).
3. 10–20 tiêu đề bài đầu (từ khoá chính, ý định, volume, KD), không trùng luật Bước 6.
4. Kế hoạch thử 6 tuần: số bài/tuần, mốc đo GSC (tuần 2, 4, 6), ngưỡng dừng/tăng.
5. Lưu báo cáo thành tệp `seo-<dd-mm>-<chu-de>.md`. Chỉ giao việc viết sau khi người quyết định chốt.

## Theo dõi sau quyết định
- Mốc 2/4/6 tuần: GSC hiển thị, vị trí, CTR cho cụm. Có thể dùng seo-drift để theo dõi thay đổi trang.
- 8–12 tuần: xem trang nào trong hệ thống được Google chọn cho từ khoá trùng, rồi mới gộp/điều chỉnh.

## Nhánh B. Chọn sản phẩm affiliate và góc video ngắn
Dùng cho affiliate Amazon US và làm tương tự cho sàn VN (Shopee, TikTok Shop, Lazada).
Nguyên tắc: tìm sản phẩm trước, làm video sau. Nhiều view chưa chắc ra đơn; mục tiêu là đúng người đang cần mua.

### B1. Tìm sản phẩm (5–10 ứng viên mỗi ngách)
- Amazon Best Sellers theo ngành hàng: sản phẩm đang bán chạy.
- Amazon Movers & Shakers: sản phẩm tăng hạng bán chạy nhanh nhất trong 24 giờ.
- Chọn 1 ngành hàng (ví dụ Home & Kitchen), lấy 5–10 sản phẩm. Ghi: tên, giá, hạng, số đánh giá, ngày xem.
- Đọc review 1–3 sao, không chỉ 5 sao: ghi 3–5 lời phàn nàn lặp lại (ví dụ máy hút bụi mini: khó vệ sinh, pin yếu, hút lông thú kém). Mỗi lời phàn nàn là một ý video so sánh hoặc kiểm chứng.
- Chỉ xem trang công khai như người dùng; Amazon chặn bot hay yêu cầu đăng nhập thì dừng, không vượt, ghi [Chưa biết].

### B2. Kiểm xu hướng tại thị trường đích
- Google Trends theo Bước 3: US, 90 ngày và 12 tháng, tên sản phẩm tiếng Anh, so các tên gọi trong 1 lô, đọc Related queries.
- Loại sản phẩm chỉ có 1 đỉnh rồi về 0 (hàng sóng) nếu định làm lâu dài.

### B3. Soi video đối thủ (YouTube Shorts, TikTok, Reels)
- Tìm theo tên sản phẩm VÀ theo vấn đề người mua gặp (ví dụ "best amazon kitchen gadgets", "amazon finds under $20", "kitchen gadgets you actually need").
- Chọn 3–5 kênh cùng ngách, ghi cho từng video đáng chú ý:
  - View so với mặt bằng của kênh (video vượt trung bình kênh nhiều lần mới đáng học). Video 100 nghìn view trên kênh thường vài nghìn view đáng nghiên cứu hơn video 1 triệu view trên kênh vốn lớn.
  - Mới đăng hay đăng lâu.
  - Câu nói hoặc hình ảnh 3 giây đầu.
  - Góc chính: công dụng, so sánh, hay giải quyết vấn đề.
  - Bình luận đang hỏi gì về sản phẩm.
- Học lý do chủ đề thu hút rồi làm cách thể hiện riêng. Không chép video, kịch bản hay hình của người khác.

### B4. Một sản phẩm thành nhiều góc
Mỗi sản phẩm đưa ra ít nhất 4 góc, ví dụ:
- Có đáng giá [giá] không.
- 3 điều cần xem trước khi mua.
- Rẻ và đắt khác nhau ở đâu.
- Kiểm chứng một lời phàn nàn từ review 1–3 sao (ví dụ "có hút được lông thú không").
Câu lệnh mẫu cho AI (dán kèm tóm tắt video và bình luận đã thu thập):
"Phân tích các video và bình luận mình cung cấp về sản phẩm [tên sản phẩm]. Đề xuất 10 ý tưởng YouTube Shorts cho người xem [Mỹ/Việt Nam], mỗi ý gồm câu mở đầu bằng [tiếng Anh/tiếng Việt], vấn đề người xem quan tâm, nội dung video 30 giây và lời kêu gọi hành động. Không bịa công dụng sản phẩm."
Kiểm lại mọi công dụng AI đưa ra với trang sản phẩm và review thật trước khi dùng.

### B5. Thử nhỏ rồi mới nhân
- Không làm 30 video ngay. Thử 3–5 góc khác nhau trước.
- Đo: tỉ lệ người chọn xem thay vì lướt qua, thời gian xem, lượt bấm vào link sản phẩm. Góc nào thắng mới làm thêm.

### B6. Luật riêng cho affiliate
- Ghi rõ link affiliate theo luật nền tảng và sàn (Amazon Associates yêu cầu câu công bố; trên web gắn rel="sponsored").
- Không bịa trải nghiệm, không review giả, không đánh giá sao giả, không hứa công dụng hãng không công bố.
- Hàng sức khoẻ, làm đẹp, trẻ em: kiểm thêm điều khoản nền tảng trước khi làm.

### B7. Đầu ra nhánh B
| Sản phẩm | Giá | Hạng/nguồn (ngày xem) | Trends 90 ngày/12 tháng | 3 lời phàn nàn chính | Video đối thủ vượt trung bình kênh | 4 góc đề xuất | Chọn thử? |
|---|---|---|---|---|---|---|---|
Kèm: 3–5 góc thử đầu tiên, chỉ số đo, ngày xem lại kết quả. Lưu thành tệp `aff-<dd-mm>-<nganh>.md`.

