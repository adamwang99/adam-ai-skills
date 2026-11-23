---
name: "seo-va-do-luong-ux-web"
description: "Dùng khi làm SEO kỹ thuật, SEO cho AI search, hoặc đo UX/chuyển đổi cho adamusesai.com và site song ngữ tương tự: audit, thêm trang mới, trước khi đổi ảnh/giao diện, theo dõi thay đổi trang sau deploy."
---

# SEO kỹ thuật, SEO cho AI search và đo UX cho web song ngữ

Tổng hợp từ việc đọc các repo claude-seo (AgriciDaniel, đọc lại bản v2.5.0 ngày 08/11/2026,
chỉ đọc mã, không cài), geo-seo-claude, seo-audit (southwellmedia), rampstackco/claude-skills,
superseo-skills, cộng bài học từ các lần soát adamusesai.com (Adam Uses AI). Điều chỉnh cho site song ngữ
VI/EN chạy SSR (TanStack Start + Cloudflare Workers + Supabase).

## Nguyên tắc số 1: HTML thô mới là sự thật
Bot AI (GPTBot, ClaudeBot, PerplexityBot) phần lớn KHÔNG chạy JavaScript. Google có chạy
nhưng chậm, và không dựng trang trả mã khác 200. Vì vậy mọi thẻ SEO (title, description,
canonical, robots, hreflang, og:*, JSON-LD) phải có trong HTML do máy chủ trả về, nằm trong
2 MB đầu (Googlebot chỉ đọc chừng đó). Bản HTML thô và bản sau khi chạy JS phải khớp nhau.
Cấm sửa SEO hay nội dung bằng useEffect/DOM ở trình duyệt rồi báo là xong. Kiểm bằng HTML
thô (curl user-agent Googlebot), không kiểm bằng trình duyệt.

## Nguyên tắc số 2: luật Google khác với ngưỡng kinh nghiệm
Ghi rõ trong báo cáo mỗi con số là luật của Google hay ngưỡng kinh nghiệm. Luật Google:
canonical, noindex, hreflang hai chiều, giới hạn sitemap, Core Web Vitals, chính sách spam.
Ngưỡng kinh nghiệm (không phải luật): độ dài title/meta, số từ tối thiểu, điểm Flesch,
mật độ link, tỉ lệ anchor, đoạn trả lời 130-170 từ, điểm E-E-A-T. Chỉ chấm điểm phần đã
đo; phần chưa đo ghi "chưa đo", không đoán.

## Cách báo cáo mỗi phát hiện
Mỗi dòng gồm: (1) quan sát đo được, kèm trang và số; (2) mức FAIL / WARN / PASS;
(3) phụ thuộc: sửa cái này trước cái nào; (4) cách biết đã sửa đúng (phép thử cụ thể);
(5) chỉ số theo dõi sau khi sửa. Xếp ưu tiên theo tác động chia công sức, chia nhóm
P0 (ngay) / P1 (trong tuần) / P2 (trong tháng) / P3.
FAIL = chặn bán hoặc chặn index: số điện thoại sai, nút mua chết, trang mua lỗi 500,
link đối tác/affiliate ra 404, trang staging bị index, sai ngôn ngữ.
Luôn kèm phần "Đã ổn, không cần làm" để người sửa khỏi kiểm lại.

## Phần 1: Checklist SEO kỹ thuật
1. title riêng từng trang, đúng ngôn ngữ của trang, từ khoá chính đặt đầu, thương hiệu ở
   cuối. Ngưỡng kinh nghiệm 50-60 ký tự. Nếu phần chính đã dài quá 55 ký tự thì bỏ đuôi
   thương hiệu (bài học 08/11: đuôi " · Adam Uses AI" đẩy ~190 title quá 70 ký tự).
2. meta description riêng từng trang, khoảng 120-160 ký tự, không mở đầu bằng cách lặp
   title, không dùng câu kêu gọi đóng khuôn. Kiểm trùng giữa các trang (kể cả cặp gói gần
   giống nhau).
3. Đúng một H1, không nhảy cấp tiêu đề (H2 rồi H4).
4. canonical tự trỏ trên mọi trang, không vừa canonical sang trang khác vừa noindex.
   Trang có tham số (?ref=, ?utm_) phải canonical về bản sạch.
5. hreflang (xem Phần 3).
6. Chuyển hướng: tối đa 1 bước, dùng 301 (không 302/307) cho chuyển cố định. www → apex và
   http → https đặt bằng Cloudflare Redirect Rules (không có .htaccess trên Workers), chạy
   trước Worker. Link ngắn đã phát ra ngoài (affiliate, QR, quảng cáo) phải 301 về trang
   đích và giữ query, không bao giờ để 404 (bài học /299k?ref= 08/11).
7. robots.txt hợp lệ, trỏ sitemap. Chặn tổ hợp tham số lọc/phân trang và trang thanh toán
   để không phí lượt thu thập (bài học 08/11: 260 URL noindex do ?khac=&sap-ra-mat=).
   Nút lọc dùng JS hoặc rel="nofollow"; mục nội dung vẫn phải là `<a href>` thật.
   Phân trang dùng `<a href>` bò được (Google không dùng rel=next/prev nữa).
8. Trang quan trọng cách trang chủ tối đa 3 cú bấm. Không trang nào mồ côi.
9. og:title, og:description, og:image 1200x630, og:locale; twitter:card đi kèm ảnh
   (summary_large_image mà không có ảnh là lỗi). Ảnh riêng theo ngôn ngữ.
10. Ảnh: alt 10-125 ký tự, mô tả việc đang diễn ra, đúng ngôn ngữ; WebP/AVIF; khai
    width/height; ảnh LCP dùng fetchpriority="high", không lazy. Cỡ kinh nghiệm: ảnh nhỏ
    dưới 50 KB, ảnh nội dung dưới 100 KB, ảnh hero dưới 200 KB; trên 500 KB là lỗi.
    Ảnh AI gắn IPTC DigitalSourceType = trainedAlgorithmicMedia (hoặc C2PA).
11. Sitemap theo ngôn ngữ: tối đa 50.000 URL hoặc 50 MB mỗi tệp, lastmod đúng thật (Google
    bỏ qua priority và changefreq), có image:image. Không đưa URL noindex, URL chuyển hướng,
    URL không phải canonical vào sitemap. Trang bán chính (khoá học, gói) phải có mặt.
12. Core Web Vitals đo trường p75, mobile và desktop riêng: LCP ≤2,5 s (kém >4 s),
    INP ≤200 ms (kém >500 ms), CLS ≤0,1 (kém >0,25). Chẩn đoán: TTFB dưới 800 ms, DOM dưới
    ~1.500 phần tử, tác vụ luồng chính dưới 50 ms. Nguồn: PageSpeed Insights API + CrUX.
13. Không lẫn ngôn ngữ: quét HTML thô /en tìm chữ có dấu tiếng Việt (cả nhãn badge, chú
    thích ảnh, meta, và dữ liệu nhúng cho hydrate), quét /vi tìm câu tiếng Anh (trừ tên
    riêng, thuật ngữ). Dữ liệu trống bản EN thì báo danh sách, không dịch máy hàng loạt.
14. Bảo mật nhẹ: HTTPS, HSTS là tín hiệu rất nhẹ, không thổi phồng trong báo cáo. Cửa sổ
    che nội dung trên mobile và chặn nút Back là lỗi nặng về trải nghiệm.

## Phần 2: Dữ liệu có cấu trúc (JSON-LD)
1. Dùng JSON-LD trong HTML máy chủ trả. Kiểm @context, @type, không để chữ giữ chỗ,
   URL tuyệt đối, ngày đúng định dạng ISO.
2. Organization (trang chủ, kèm sameAs), Person cho tác giả, Article cho tin (headline,
   datePublished, dateModified thật, author), BreadcrumbList.
3. Product: name, image, offers (Offer, price > 0, priceCurrency ISO 4217 đúng trang: VND
   cho /vi, USD cho /en), hasMerchantReturnPolicy khớp chính sách hoàn tiền; có sku,
   phí giao hàng nếu có. aggregateRating chỉ khi có đánh giá thật của khách, không đánh
   giá tự tạo hay đánh giá đổi quà không công khai.
4. Không dựa vào FAQPage hay HowTo để lấy kết quả nhiều định dạng (Google đã rút). Hỏi
   đáp thật nhiều người trả lời thì dùng QAPage.
5. Kiểm bằng Rich Results Test và Schema Markup Validator.

## Phần 3: hreflang cho site song ngữ
1. Mỗi trang khai chính nó và mọi bản ngôn ngữ khác; các bản trỏ ngược lại nhau đủ vòng.
   Lỗi hay gặp nhất là thiếu link trỏ ngược.
2. Đúng một x-default, trỏ trang mặc định cho khách quốc tế (với site chuyển theo quốc
   gia: gốc `/` hoặc `/en`, không trỏ `/vi`).
3. Mã ngôn ngữ ISO 639-1 (vi, en), vùng nếu có theo ISO 3166-1 (en-GB, không phải en-uk).
4. Chỉ đặt hreflang trên URL canonical; cùng giao thức, cùng kiểu dấu / cuối.
5. Kiểm tương đương nội dung: bản nào cũng tồn tại, cùng khung H2/H3. Bản dịch máy chưa
   duyệt bị coi là nội dung hàng loạt chất lượng thấp.

## Phần 4: Nội dung và E-E-A-T
1. Bài trả lời được câu hỏi "Ai viết, viết thế nào, viết để làm gì" của Google: tác giả
   có trang riêng, có trải nghiệm thật (ảnh chụp, số đo của mình), nguồn chính thức.
2. Từ khoá chính trong title, H1 và 100 chữ đầu; không đặt chỉ tiêu mật độ.
3. Ngưỡng kinh nghiệm (không phải luật): bài blog phủ đủ ý thường từ khoảng 1.500 từ, trang
   sản phẩm 300-400 từ; câu 15-20 từ, đoạn 2-4 câu; khoảng 3-5 link nội bộ mỗi 1.000 từ.
4. Chủ đề thay đổi nhanh (giá, gói, phiên bản AI) chưa cập nhật 12 tháng thì báo.
5. Trên 30 trang địa phương hoặc trang gần giống nhau là dấu hiệu trang cửa ngõ: cảnh báo.

## Phần 5: SEO cho AI search (GEO)
1. robots.txt: tách bot huấn luyện (GPTBot, ClaudeBot) với bot quyết định trích dẫn
   (OAI-SearchBot, Claude-SearchBot, PerplexityBot). Google-Extended không ảnh hưởng
   Google Search hay AI Overviews. Báo cáo riêng từng bot.
2. Google ghi rõ: không cần tệp, markup hay cách chia đoạn riêng để vào AI Overviews và
   AI Mode; chỉ cần trang được index, thu thập được, link nội bộ tốt, chữ thật, schema
   khớp chữ trên trang.
3. Ngưỡng kinh nghiệm cho các máy AI khác: câu trả lời nằm trong 40-60 từ đầu mỗi mục, có
   đoạn trả lời trọn ý khoảng 130-170 từ, H2 dạng câu hỏi, số liệu kèm nguồn và ngày,
   phần quan trọng đặt sớm trong trang.
4. Tên thương hiệu, liên hệ, giá nhất quán ở mọi nơi (web, MCP, mạng xã hội, sameAs).
5. llms.txt: làm cũng không hại nhưng không phải đòn bẩy với Google, xếp ưu tiên thấp.

## Phần 6: Ý định tìm kiếm (SXO)
Trước khi viết hoặc sửa trang cho một từ khoá, xem 10 kết quả đầu: nếu trên 60% cùng một
loại trang (bài hướng dẫn, trang sản phẩm, danh sách) thì làm đúng loại đó. Viết bài blog
cho từ khoá mà Google toàn trả trang sản phẩm là lệch ý định, sửa nội dung không cứu được.

## Phần 7: Theo dõi thay đổi sau deploy (drift)
Chụp mốc mỗi trang quan trọng: mã trạng thái, title, meta description, canonical, meta
robots, H1-H3, JSON-LD (kèm mã băm), og:*, hreflang. So lại sau mỗi lần deploy:
- Nặng (báo ngay): mất schema, đổi hoặc mất canonical, thêm noindex, mất hoặc đổi hẳn
  H1, mất title, trang 2xx thành 4xx/5xx, link đối tác ra 404.
- Cảnh báo: đổi title hoặc description, Core Web Vitals xấu đi trên 20%, mất og.
- Ghi nhận: thêm schema, đổi H2, đổi nội dung.
Lưu mốc trong kho mã hoặc cơ sở dữ liệu của bạn (ví dụ tệp CSV trong `seo/`).

## Phần 8: Backlink và index
1. Chỉ phân tích hồ sơ link, không xây link bằng mạng trao đổi, bài vệ tinh tự động hay
   mua link không gắn sponsored. Link trả tiền và affiliate gắn rel="sponsored".
2. Không chấm điểm khi thiếu dữ liệu (ghi "chưa đủ dữ liệu"). "Link độc hại" là khái
   niệm của nhà cung cấp công cụ; chỉ disavow khi có án phạt thủ công hoặc link trả tiền
   cũ không gỡ được.
3. Google Indexing API chỉ dùng cho JobPosting và BroadcastEvent. Bài thường dùng
   IndexNow (Bing, Yandex, Naver, Seznam), sitemap lastmod đúng, link nội bộ, và nút
   Yêu cầu lập chỉ mục trong Search Console (khoảng 10 URL/ngày).
4. Search Console URL Inspection API: khoảng 2.000 lượt/ngày mỗi property. Cơ hội nhanh:
   truy vấn vị trí 4-20 có nhiều hiển thị.

## Phần 9: Đo UX và chuyển đổi
1. Gắn công cụ đo trước khi đổi bất kỳ thứ gì ảnh hưởng UX: Cloudflare Web Analytics
   hoặc Plausible/Umami. Kết nối Google Search Console để thấy từ khoá, trang được index,
   lỗi index.
2. Đặt tên sự kiện thống nhất, không đổi giữa chừng: view_product, click_buy,
   open_checkout, purchase_success, kèm thuộc tính lang và slug.
3. Phễu chính: xem trang skill, bấm mua, mở thanh toán, đơn thành công. Tách theo
   /vi và /en.
4. Đo nền 2-4 tuần trước khi đổi. Đổi xong đo lại cùng khoảng, cùng chỉ số. Lượng
   khách ít thì đo lâu hơn, và nói rõ số mẫu. Không kết luận "tăng chuyển đổi" khi chưa
   có số trước/sau.
5. Khi traffic tụt: xác nhận tụt thật, khoanh vùng (trang nào, ngôn ngữ nào, thiết bị
   nào), soi trang, soi kỹ thuật, rồi mới xét nguyên nhân bên ngoài.

## Cách soát toàn site (quy trình chuẩn)
1. Lấy mọi URL từ sitemap; curl từng URL với user-agent Googlebot (song song khoảng 12
   luồng): mã trạng thái, URL cuối, title, description, robots, canonical, hreflang, số
   H1, cỡ trang.
2. Tổng hợp: mã khác 200, chuyển hướng, noindex lạc, canonical lệch, thiếu hreflang tự
   trỏ, title/meta thiếu, quá dài, trùng; lẫn ngôn ngữ.
3. Đối chiếu Search Console: Lập chỉ mục trang (từng lý do, xem mẫu URL), Sơ đồ trang web,
   Kiểm tra URL cho trang nghi vấn (xem canonical Google chọn). Dữ liệu báo cáo GSC có thể
   cũ vài tuần, nên kiểm lại trang thật trước khi báo lỗi.
4. Kiểm riêng các link đã phát ra ngoài (affiliate, khoá học, quảng cáo) và bản www/http.

## Ai dùng
Claude lên kế hoạch và nghiệm thu, Hermes thực thi code. Cả hai dùng chung bản này.
Nghiệm thu luôn bằng HTML thô trên toàn sitemap, kèm số trang đã quét và số đo từng trang.
