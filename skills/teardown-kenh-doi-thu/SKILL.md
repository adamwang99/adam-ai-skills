---
name: "teardown-kenh-doi-thu"
description: "Mổ xẻ (teardown) một kênh đối thủ hoặc kênh mẫu trên Instagram, TikTok, YouTube, Facebook rồi dựng báo cáo HTML 13 mục có nhãn Xác nhận / Suy luận / Chưa biết. Dùng khi anh nói 'teardown', 'mổ kênh', 'bóc kênh', 'phân tích đối thủ', 'học kênh mẫu', hoặc đưa link một kênh và muốn biết họ làm gì để làm theo. Cần AI điều khiển được trình duyệt."
---

# Teardown kênh đối thủ

**Vào**: một kênh cần mổ xẻ (link hoặc @handle) trên Instagram, TikTok, YouTube
hoặc Facebook.

**Ra**: một **báo cáo HTML 13 mục** mở bằng trình duyệt — ảnh chụp có khoanh đỏ
kèm chú thích từng vùng, bảng số liệu theo nhóm bài, điểm gãy của đường tăng
trưởng, mổ video từng giây kèm prompt viết ngược, phễu bán hàng và giá, cộng
một bản tóm tắt chữ và file CSV dữ liệu thô.

Khác hẳn việc "nhờ AI phân tích đối thủ" thông thường: ở đây mọi nhận định đều
có **nhãn nguồn gốc** — Xác nhận (thấy tận mắt trên kênh), Suy luận (rút ra từ
số liệu), Chưa biết (chưa quét được). Không có chỗ cho AI đoán bừa rồi nói như
thật.

## Chạy được ở đâu — đọc trước khi bắt đầu

| Công cụ | Làm được không |
|---|---|
| **Claude Code / Codex có bật công cụ trình duyệt** (browser MCP, Playwright MCP, hoặc tiện ích điều khiển Chrome) | **Có** — đây là đường chính. AI tự mở kênh, cuộn, chụp màn hình, cắt khung video, chạy script |
| app ChatGPT / Claude bản tải về, có chạy lệnh + điều khiển trình duyệt | Có |
| ChatGPT web, Gemini (chỉ trả lời chữ) | **Không tự quét được.** Vẫn dùng được quy trình và khuôn báo cáo, nhưng người dùng phải tự chụp màn hình và tự điền số liệu |

Ngoài ra cần **Python 3** cho ba script tính số liệu (AI tự cài giúp nếu chưa có).

Chưa có quyền điều khiển trình duyệt thì nhắn thẳng cho AI: *"bật công cụ điều
khiển trình duyệt cho bạn giúp tôi"* — Claude Code và Codex hiện đại tự tra tài
liệu và tự cài được.

## Lấy bộ mẫu về máy (1 lệnh)

Bộ mẫu gồm khung báo cáo HTML sẵn CSS, ba script Python đã kiểm thử, và **một
báo cáo mẫu thật đã làm xong** để nhìn trước thành phẩm:

```bash
git clone https://github.com/PhongMenly/teardown-kenh-doi-thu.git
```

Mở `vi-du/zara/bao-cao-teardown-zara.html` bằng trình duyệt để xem một báo cáo
hoàn chỉnh trông ra sao trước khi bắt tay làm kênh của mình.

Muốn gọi bằng `/teardown-kenh-doi-thu` ở mọi dự án thì chép thư mục đó vào
`~/.claude/skills/` (Windows: `%USERPROFILE%\.claude\skills\`).

## Hỏi người dùng ba điều này trước khi làm

1. **Kênh nào, nền tảng nào?** (link hoặc @handle)
2. **Mổ để làm gì?** Dựng kênh mới, so với kênh đang có, hay tìm khuôn nội dung
   để bắt chước — quyết định mục 13 viết gì.
3. **Nhân vật/kênh của người dùng là gì?** Để phần cuối báo cáo đề xuất đúng
   thứ tự thử cho họ, không nói chung chung.

Thiếu cái nào thì hỏi đúng cái đó. Đủ rồi thì làm luôn, đừng hỏi vòng vo.

## Thời gian thật

Một kênh cỡ 150–200 bài: **3–5 giờ** cho bản đầy đủ (kiểm kê bài, mổ 5–10
video, dựng báo cáo). Bản rút gọn (định vị + đường tăng trưởng + 3 video):
khoảng 1 giờ. Nói trước con số này với người dùng, đừng hứa "vài phút".

---

Một lần teardown ra: báo cáo HTML 13 mục có ảnh khoanh đỏ, một file chữ tóm tắt, dữ liệu thô các bài, và thứ tự thử cho nhân vật của bạn. Làm theo skill này thì lần sau không phải nghĩ lại cách làm.

Bản mẫu thật: `vi-du/zara/bao-cao-teardown-zara.html` trong chính skill này (kênh @iamfacelesszara, quét 03/10/2026; ảnh ở `vi-du/zara/img/`). Mở thẳng bằng trình duyệt hoặc qua máy chủ cục bộ ở cuối file này. Làm kênh mới thì xem bản mẫu này trước để biết một báo cáo xong trông ra sao.

## Khi nào dùng

- Người dùng đưa một kênh (tên, handle hoặc link) và nói "teardown", "mổ kênh", "xem kênh này làm gì".
- Cần học khuôn nội dung, công cụ, phễu bán của một kênh để dựng nội dung cho nhân vật của người dùng.

Không dùng khi chỉ cần liệt kê ý tưởng nội dung (đó là việc khác, không cần cả quy trình này).

## Đầu vào cần

1. Kênh cần mổ (link hoặc handle) và nền tảng.
2. Mục đích (ví dụ: dựng kênh cho nhân vật của mình, so với kênh của bạn).
3. Nhân vật của bạn để so sánh ở mục 13.

Thiếu cái nào thì chỉ hỏi đúng cái đó. Đã có đủ thì làm luôn, không hỏi thêm.

## Quy tắc an toàn (đọc trước khi làm)

- Chỉ đọc nội dung công khai. Không nhập mật khẩu, không đăng nhập hộ. Nếu cần đăng nhập thì nhờ người dùng tự làm.
- **Không** nhắn tin, bình luận, theo dõi, mua hàng, đăng ký form của đối thủ. Việc nào cần thì ghi vào mục 12 và hỏi người dùng trước.
- Không tải video về máy khi chưa xin phép. Chỉ vẽ khung đang phát lên lớp phủ rồi chụp.
- Ẩn danh người bình luận. Không ghi email, số điện thoại, mật khẩu, tên cá nhân.
- Làm việc ở **một tab riêng** do AI tự mở, không dùng chung tab người dùng đang xem; mỗi lệnh trình duyệt phải ghi rõ tab nào. Thao tác cách nhau vài giây như người thật.
- Khi người dùng đang xem cùng tab, trang có thể tự cuộn lệch. Làm ở tab riêng và chụp màn hình ngay trước khi bấm.

## Quy trình 8 bước

Chi tiết từng bước, kèm cách lấy dữ liệu: **Phụ lục A**.

1. **Định vị**: trang cá nhân, bio, highlight, trang bán hàng. Họ bán gì cho ai.
2. **Kiểm kê toàn bộ bài**: đủ ngày đăng, lượt xem, thích, bình luận, caption vào `bai-viet.csv`. Giờ đăng giải mã từ mã bài bằng `scripts/giai-ma-shortcode.py`.
3. **Đo hiệu quả**: chạy `scripts/phan-tich-so-lieu.py` ra trung vị, bảng nhóm bài, top 10, nhịp đăng.
4. **Tìm điểm gãy**: lúc đường lượt xem đổi, và họ đã đổi cái gì.
5. **Phân loại tuyến nội dung**: gán tay cột `tuyen`, chạy lại script.
6. **Mổ video** 5–10 video hay nhất + 1 bài thất bại: ảnh 12 khung (**Phụ lục C**), prompt viết ngược theo công thức Seedance ở **Phụ lục B**.
7. **Lần theo tiền**: link, giá, sản phẩm của ai, CTA qua các đời, bằng chứng họ khoe.
8. **Đọc khán giả** và so 3–4 kênh cùng ngách.

Cuối cùng phân ba cột: **xác nhận / suy luận / chưa biết**.

## Dựng báo cáo

1. Tạo thư mục `<thư-muc-du-an>/teardown-<ten-kenh>/` có `img/`.
2. Chép `assets/mau-bao-cao.html` thành `bao-cao-teardown-<ten-kenh>.html`, thay mọi `{{...}}`, điền 13 mục theo **Phụ lục B**.
3. Chụp ảnh đặt vào `img/`, khoanh đỏ theo toạ độ phần trăm.
4. Tạo bản một file (ảnh nhúng base64) để gửi đi, và `teardown-<ten-kenh>.md` tóm tắt chữ.

Xem báo cáo trên máy: thêm một mục vào cấu hình chạy của dự án:

```json
{ "name": "teardown-<ten-kenh>", "runtimeExecutable": "python",
  "runtimeArgs": ["-m", "http.server", "<cong>", "--directory", "<thư-muc-du-an>/teardown-<ten-kenh>"], "port": <cong> }
```

Mở `http://localhost:<cong>/bao-cao-teardown-<ten-kenh>.html#s1`. Cổng bản Zara là 8791, chọn cổng khác nếu đã dùng.

## Giao kết quả

Trả lời ngắn trong chat, theo thứ tự:

1. Hai ba dòng: kênh này thắng nhờ đâu.
2. Đường dẫn báo cáo (localhost và file).
3. Điểm gãy và thứ tự thử cho nhân vật của bạn.
4. Việc cần người dùng quyết hoặc cho phép (mục 12 và 13).

## Rà soát trước khi giao

- Chính tả tiếng Việt, dấu, thuật ngữ nhất quán ("teardown" viết một từ).
- Số trong chữ khớp bảng và script.
- Mọi ảnh hiện được, khoanh đỏ đúng chỗ (mở báo cáo ra xem từng ảnh).
- Mỗi mục có nhãn Xác nhận / Suy luận / Chưa biết.
- Mọi việc cần xin phép đã nằm trong mục 12.
- Không có dữ liệu riêng tư.

## Sau khi xong (bắt buộc, để lần sau nhanh hơn)

1. Ghi một dòng vào sổ `nhat-ky-teardown.md` trong thư mục làm việc: ngày, kênh,
   nền tảng, đường dẫn báo cáo, điều rút ra, việc còn dang dở. Lần sau mổ kênh
   khác, đọc sổ này trước để khỏi vấp lại.
2. Lưu lại 3–5 điều rút ra vào bộ nhớ của AI (nếu AI có bộ nhớ), kèm đường dẫn
   báo cáo — để lần sau nhắc tên kênh là nó nhớ đã mổ rồi.
3. Vấp chỗ nào mới (trang đổi cấu trúc, cách lấy số liệu mới, công cụ mới) thì
   ghi thêm vào sổ, và sửa lại quy trình nếu cần.
4. Chạy `scripts/dong-goi-1-file.py` trong bộ mẫu để gộp báo cáo + ảnh thành
   một tệp HTML duy nhất, gửi cho người khác xem được ngay.

## Chỗ đã có người vấp — tránh sẵn

| Vấp | Cách tránh |
|---|---|
| Dùng chung tab với người dùng, trang tự cuộn lệch, bấm nhầm | Làm ở tab riêng do AI tự mở, chụp màn hình ngay trước khi bấm |
| Cửa sổ đăng nhập hiện lên chặn thao tác | Nhờ người dùng đóng, không cố vượt |
| Video không hiện khung khi tab ở nền | Đưa tab lên trước, chờ khoảng 2 giây rồi mới chụp |
| Nhầm giờ đăng do múi giờ | Giờ giải mã từ mã bài là UTC, giờ Việt Nam cộng 7 |
| Đo thiếu bài nhưng nói như đã đo hết | Luôn ghi rõ đã đo bao nhiêu trên tổng số |

---

# Phụ lục A — Quy trình teardown chi tiết

Làm đúng thứ tự. Cuối mỗi bước ghi vào sổ tạm (một file `ghi-chu.md` trong thư mục teardown) những gì **xác nhận**, **suy luận**, **chưa biết**. Cuối cùng báo cáo chỉ là sổ tạm được trình bày lại.

Nguyên tắc chung: chỉ đọc nội dung công khai, không đăng nhập thay người dùng, mỗi thao tác cách nhau vài giây như người thật, dùng một tab riêng (không phải tab của agent khác).

## Bước 1. Định vị

Mở trang cá nhân. Chụp màn hình (đặt tên `01-profile.jpg`). Ghi:

- Số follower, số đang theo dõi, có tick xanh không, số bài.
- Bio từng dòng: lời hứa, từ khoá kêu gọi (ví dụ "222 To Start"), link.
- Highlight: tên từng cái, cái nào là bằng chứng bán hàng, cái nào dạy quy trình.
- Họ bán gì, cho ai, định vị trong một câu.

Với kênh có trang bán hàng/link trong bio: mở trang đó, chụp (`02-shop.jpg`), ghi từng sản phẩm, giá, sản phẩm của ai.

## Bước 2. Kiểm kê toàn bộ bài

Mục tiêu: có đủ danh sách bài, ngày đăng, lượt xem, thích, bình luận, caption để chạy script.

Cách lấy dữ liệu, thử lần lượt:

1. **Lưới trang cá nhân**: cuộn hết lưới, mỗi ô Reels hiện lượt xem. Ghi lại số lượt xem của từng ô theo thứ tự.
2. **Mở từng bài ở chế độ chưa đăng nhập** (hoặc trang bài công khai): thẻ `og:description` thường có số thích, bình luận và caption. Có thể lấy bằng cách tải trang bài rồi đọc thẻ meta, không cần đăng nhập.
3. **Giờ đăng**: giải mã từ mã bài bằng `scripts/giai-ma-shortcode.py` (giờ UTC, cộng 7 là giờ Việt Nam). Không cần mở từng bài.
4. Điền vào CSV theo mẫu `assets/mau-posts-gia-dinh.csv` (cột: shortcode, posted_at, views, likes, comments, tuyen, caption).

Nếu kênh có hàng trăm bài mà chỉ lấy được một phần: ghi rõ đã đo bao nhiêu trên tổng số, đừng nói như đã đo hết.

## Bước 3. Đo hiệu quả và đường tăng trưởng

Chạy:

```bash
python scripts/phan-tich-so-lieu.py bai-viet.csv --nhom 21
```

Lấy từ kết quả: tổng quan (trung vị, số bài vượt ngưỡng), bảng nhóm bài theo thời gian, top 10, nhịp đăng, tỉ lệ tương tác, giờ đăng hay gặp. Dán vào mục 3 và 8 của báo cáo.

Số liệu follower theo mốc: tìm các highlight/bài ghi mốc ("1K followers", "2K in 24h") và chụp làm bằng chứng.

## Bước 4. Tìm điểm gãy

Điểm gãy là lúc đường lượt xem đổi hẳn (trung vị nhảy lên, hoặc xuất hiện bài vượt trội đầu tiên). Cách tìm:

1. Nhìn bảng nhóm bài: nhóm nào trung vị tăng gấp đôi trở lên so với nhóm trước.
2. Mở các bài quanh thời điểm đó, ghi **cái gì khác** so với các bài trước: định dạng, nhịp đăng, chủ đề, caption, nhạc.
3. Viết kết luận trong khung `.box` ở mục 3: "trước điểm gãy làm X, sau điểm gãy làm Y".

## Bước 5. Phân loại tuyến nội dung

Gán tay cột `tuyen` trong CSV cho từng bài (chỉ cần cho các bài đo được). Chạy lại script để có bảng theo tuyến. Một bài thuộc một tuyến. Tên tuyến ngắn, nhất quán. Ghi tuyến nào mạnh, tuyến nào luôn yếu, tuyến nào bán hàng nhưng ít xem.

## Bước 6. Mổ video

Chọn 5–10 video hay nhất, cộng 1 bài thất bại cùng khuôn để đối chiếu. Với mỗi video (xem **Phụ lục C**):

1. Cắt 12 khung đều theo thời lượng, ghi thời điểm mỗi khung.
2. Đánh dấu khung ngay sau mỗi lần cắt cảnh (viền đỏ).
3. Ghi: độ dài, số cảnh, thời điểm cắt, cảnh mở, cảnh kết, chữ trên hình, âm thanh, bối cảnh, nhân vật mặc gì.
4. **Prompt viết ngược**: viết prompt Seedance theo công thức của người dùng (xem **Phụ lục B**, mục 5) để tái tạo video đó. Gắn nhãn "Suy luận, chưa chạy thử".

## Bước 7. Lần theo tiền

Mọi link, giá, sản phẩm, của ai, CTA qua các đời. Ghi mỗi CTA đổi vào lúc nào (đối chiếu ngày đăng). Ghi bằng chứng họ khoe (ảnh người mua, con số). Ghi rõ cái gì là của chính họ, cái gì họ chỉ làm affiliate.

Tuyệt đối không mua hàng, không đăng ký, không nhắn tin cho họ trong bước này. Nếu cần để hiểu phễu, ghi vào mục "Việc chưa làm được" và hỏi người dùng.

## Bước 8. Đọc khán giả

Đọc bình luận của 5–10 bài lớn nhất. Ghi: ai bình luận (tệp nào, nước nào), họ hỏi gì, tương tác thật hay chéo giữa các kênh cùng ngách. **Ẩn danh**: không ghi tên người bình luận, không ghi thông tin cá nhân.

So 3–4 kênh cùng ngách (chọn từ danh sách đề xuất/bình luận): cái gì là công thức chung của ngách, cái gì là riêng của kênh này.

## Kết thúc

1. Điền mục "Ba việc chưa làm được" cho mọi việc bị chặn (cần đăng nhập, cần mua, cần nhắn tin).
2. Viết kết luận: 5 điều rút ra, thứ tự thử cho nhân vật của người dùng, các việc cần quyết.
3. Cuối cùng chia ba cột: **xác nhận / suy luận / chưa biết**.

## Kênh không phải Instagram

- **TikTok**: lượt xem hiện trên lưới; giờ đăng thường suy được từ ID bài (số nguyên 64 bit, 32 bit cao là mốc giây Unix; cần kiểm lại với một bài đã biết giờ); caption, nhạc, hashtag ở trang bài.
- **YouTube**: lượt xem, ngày đăng, thời lượng ở tab Video; mô tả, thẻ, chương ở trang video; Shorts ở tab Shorts.
- **Facebook**: số tương tác ở bài; hạn chế quyền xem nên ghi rõ phần không lấy được.

Phần "giải mã giờ đăng từ mã bài" chỉ áp dụng cho Instagram; với nền tảng khác đọc ngày hiển thị.

---

# Phụ lục B — Cấu trúc và cách viết báo cáo

Báo cáo là một file HTML một trang (CSS, nhãn, khung khoanh đỏ, mục lục). Bản này không kèm mẫu HTML: AI tự dựng theo cấu trúc dưới đây.

## Bố cục thư mục đầu ra

```
teardown-<ten-kenh>/
  bao-cao-teardown-<ten-kenh>.html      báo cáo chính, ảnh gọi từ img/
  bao-cao-teardown-<ten-kenh>-1-file.html   bản một file (ảnh nhúng base64) để gửi đi
  teardown-<ten-kenh>.md                tóm tắt chữ để lưu và tìm lại
  bai-viet.csv                          dữ liệu thô các bài
  img/                                  01-profile.jpg, 02-shop.jpg, v01.jpg ...
```

Đặt tên ảnh: `01-` đến `0x-` cho ảnh trang; `v01`, `v02`... cho tấm 12 khung của từng video; `t01-` cho ảnh quy trình/công cụ; `fail-` cho bài thất bại.

## 13 mục

| # | Mục | Nội dung |
|---|---|---|
| 1 | Hồ sơ và định vị | Ảnh trang cá nhân khoanh A/B/C, số liệu, bio, highlight, họ bán gì cho ai |
| 2 | Phễu bán hàng và giá | Bảng nguồn tiền: sản phẩm, giá, của ai; CTA; bằng chứng họ khoe |
| 3 | Đường tăng trưởng | Bảng nhóm bài theo thời gian, điểm gãy trong khung `.box` |
| 4 | Các tuyến nội dung và hiệu quả | Bảng tuyến: độ dài, lượt xem trung vị, cao nhất, ghi chú |
| 5 | Mổ video từng giây + prompt viết ngược | Mỗi video: ảnh 12 khung, chú thích, ảnh trang bài khoanh đỏ, prompt trong `<pre>` |
| 6 | Bài thất bại | 1 bài thất bại để đối chiếu, các kiểu bài luôn thấp |
| 7 | Công cụ và tính năng họ chọn | Công cụ, quy trình tạo, lựa chọn tạo cảm giác "thật" |
| 8 | Caption, CTA, hashtag, giờ đăng, âm thanh | Khuôn caption, CTA qua các đời, giờ đăng, tỉ lệ tương tác |
| 9 | Khán giả quan tâm điều gì | Ai bình luận, hỏi gì, tương tác thật hay chéo |
| 10 | So với cả ngách | Công thức chung của ngách và điểm riêng của kênh |
| 11 | Nền tảng khác của cùng chủ kênh | TikTok, Threads, YouTube... |
| 12 | Việc chưa làm được | Bảng: việc, tình trạng, cần gì |
| 13 | Kết luận và việc cần quyết | 5 điều rút ra, thứ tự thử cho nhân vật của người dùng, việc cần quyết |

Mục nào không có dữ liệu thì giữ mục đó và viết một dòng "Chưa quét được vì ..." với nhãn Chưa biết. Không xoá mục.

## Nhãn bắt buộc

- `<span class="tag t-ok">Xác nhận</span>`: thấy trực tiếp trên kênh.
- `<span class="tag t-inf">Suy luận</span>`: rút ra từ dữ liệu, chủ kênh chưa nói thẳng.
- `<span class="tag t-unk">Chưa biết</span>`: chưa quét được.

Mỗi nhận định quan trọng phải có một nhãn. Số liệu thì ghi nguồn (đo từ lưới, từ thẻ meta, từ mã bài).

## Ảnh khoanh đỏ

Mỗi ảnh chụp có các ô viền đỏ đánh chữ A, B, C và chú thích bên dưới giải thích từng ô.

```html
<figure>
  <div class="shot"><img src="img/01-profile.jpg" alt="Trang cá nhân">
    <div class="b" style="left:43%;top:8.5%;width:14.5%;height:4.5%"><i>A</i></div>
  </div>
  <figcaption><b>A</b> Nội dung ô A. <b>B</b> Nội dung ô B.</figcaption>
</figure>
```

Toạ độ `left/top/width/height` tính theo phần trăm kích thước ảnh. Cách xác định: mở ảnh, đo vị trí vùng cần chỉ, chia cho kích thước ảnh. Sau khi dựng, mở báo cáo trong trình duyệt và kiểm từng ô có nằm đúng chỗ không.

Hai ảnh cạnh nhau dùng `<div class="grid2">...</div>`.

## Prompt viết ngược (mục 5)

Dùng công thức dưới đây, viết **hoàn toàn bằng tiếng Anh**:

```
[Thời lượng][Thể loại],[Nhân vật],[Âm thanh],[Ánh sáng, chất liệu, bối cảnh]

Character: based on @Image1, ...

[Shot 1, 0-3s: ...]
[Shot 2, 3-6s: ...]
[Shot 3, 6-8s: ...]
```

Quy ước: @Image1 là ảnh nhân vật, @Image2 là ảnh trang phục (flat-lay), @Image3 là ảnh bối cảnh. Mỗi video một prompt. Gắn nhãn Suy luận và ghi "chưa chạy thử". Ưu tiên góc cận và cảm xúc, sang trọng, đẳng cấp.

## Văn phong

- Tiếng Việt có dấu đầy đủ, câu ngắn, số liệu cụ thể. Xưng hô theo đúng cách người dùng vẫn dùng (hỏi một lần rồi giữ nguyên cả báo cáo).
- Số Việt hoá: 1,6 triệu; 19,8 nghìn; viết tắt trong bảng N (nghìn), Tr (triệu).
- Thuật ngữ nhất quán: "teardown", "điểm gãy", "tuyến nội dung", "prompt viết ngược", "một cảnh quay liền".
- Không phóng đại. Nói rõ số mẫu (đã đo bao nhiêu trên tổng).
- Không để lộ thông tin riêng tư của người bình luận (tên, tài khoản cá nhân).

## Rà soát trước khi giao

1. Chính tả tiếng Việt: dấu, "teardown" (một từ), tên kênh, tên công cụ (Seedance, Topview, GPT Image).
2. Mọi số trong chữ khớp với bảng và với script.
3. Mọi ảnh hiện được, khoanh đỏ đúng chỗ.
4. Mỗi mục có ít nhất một nhãn Xác nhận/Suy luận/Chưa biết.
5. Mục 12 liệt kê đủ việc cần xin phép.
6. Không chứa mật khẩu, email, số điện thoại hay tên người bình luận.

---

# Phụ lục C — Kỹ thuật cắt khung video

Mục đích: với mỗi video cần mổ, có một ảnh 12 khung đều theo thời lượng, khung ngay sau mỗi lần cắt cảnh có viền đỏ, kèm thời điểm. Ảnh đặt tên `v01.jpg`, `v02.jpg`...

Không tải video về máy. Chỉ vẽ khung đang phát trong trang lên một lớp phủ rồi chụp màn hình lớp phủ đó. (Nếu bắt buộc phải tải video, xin phép người dùng trước và nói rõ tên file, nguồn, dung lượng.)

## Điều kiện để chạy được

1. Mở trang bài trong **tab riêng**, đưa tab lên phía trước (tab nền thường không tải video).
2. Chờ trang tải xong, bấm phát một lần để video có dữ liệu, rồi tạm dừng.
3. Sau mỗi lần dựng lớp phủ, **chờ khoảng 2 giây** rồi mới chụp.
4. Mỗi video một lần dựng, kiểm tra ảnh chụp có đủ 12 khung trước khi sang video khác.

## Mã mẫu chạy trong trang (công cụ chạy JavaScript của trình duyệt)

Trạng thái: **mã mẫu viết lại**. Chạy thử trên một video, chỉnh nếu trang đổi cấu trúc. Nếu video khác nguồn (cross-origin) làm vải vẽ bị khoá thì bước phát hiện cắt cảnh sẽ không chạy, khung vẫn vẽ được và khi đó phải đánh dấu cú cắt bằng mắt.

```js
(async () => {
  const v = document.querySelector('video');
  if (!v) return 'không thấy video';
  v.pause();
  const dur = v.duration;
  const N = 12, W = 270, H = Math.round(W * v.videoHeight / v.videoWidth);
  const seek = t => new Promise(r => { v.onseeked = r; v.currentTime = Math.min(t, dur - 0.05); });

  // 1) phát hiện cắt cảnh: lấy mẫu mỗi 0,1 giây, so mức thay đổi hình ảnh
  const cuts = [];
  try {
    const s = document.createElement('canvas'); s.width = 32; s.height = 32;
    const sc = s.getContext('2d', { willReadFrequently: true });
    let prev = null;
    for (let t = 0; t < dur; t += 0.1) {
      await seek(t);
      sc.drawImage(v, 0, 0, 32, 32);
      const d = sc.getImageData(0, 0, 32, 32).data;
      if (prev) {
        let diff = 0;
        for (let i = 0; i < d.length; i += 4) diff += Math.abs(d[i] - prev[i]) + Math.abs(d[i + 1] - prev[i + 1]) + Math.abs(d[i + 2] - prev[i + 2]);
        if (diff / (32 * 32 * 3) > 40) cuts.push(+t.toFixed(2));   // ngưỡng 40, chỉnh nếu bắt sai
      }
      prev = d;
    }
  } catch (e) { cuts.push('KHÔNG_ĐO_ĐƯỢC: ' + e.message); }

  // 2) vẽ 12 khung đều theo thời lượng, khung ngay sau cú cắt có viền đỏ
  const cols = 6, rows = 2, c = document.createElement('canvas');
  c.width = cols * (W + 6) + 6; c.height = rows * (H + 6) + 30;
  const g = c.getContext('2d');
  g.fillStyle = '#fff'; g.fillRect(0, 0, c.width, c.height);
  const numCuts = cuts.filter(x => typeof x === 'number');
  for (let i = 0; i < N; i++) {
    const t = (dur * (i + 0.5)) / N;
    await seek(t);
    const x = 6 + (i % cols) * (W + 6), y = 30 + Math.floor(i / cols) * (H + 6);
    g.drawImage(v, x, y, W, H);
    const prevT = (dur * (i - 0.5)) / N;
    if (numCuts.some(ct => ct > prevT && ct <= t)) { g.strokeStyle = '#e00000'; g.lineWidth = 5; g.strokeRect(x, y, W, H); }
    g.fillStyle = 'rgba(0,0,0,.75)'; g.fillRect(x, y, 64, 18);
    g.fillStyle = '#fff'; g.font = 'bold 12px Arial'; g.fillText((i + 1) + ' · ' + t.toFixed(1) + 's', x + 4, y + 13);
  }
  g.fillStyle = '#000'; g.font = 'bold 14px Arial';
  g.fillText('dài ' + dur.toFixed(1) + 's | cắt cảnh tại: ' + (numCuts.join(', ') || 'không có (1 cảnh liền)'), 8, 20);

  // 3) hiện lớp phủ phủ kín trang để chụp
  c.style.cssText = 'position:fixed;left:0;top:0;z-index:2147483647;max-width:100vw;background:#fff';
  document.body.appendChild(c);
  return { dai_giay: +dur.toFixed(1), cat_canh: cuts };
})()
```

Sau khi chụp xong, xoá lớp phủ: `document.querySelector('canvas[style*="2147483647"]')?.remove()`.

## Chú thích từng video trong báo cáo

Dưới mỗi ảnh ghi: số cảnh, thời điểm cắt, cảnh mở, cảnh kết, chữ trên hình, âm thanh, bối cảnh, nhân vật mặc gì. Ví dụ: "3 cảnh, cắt tại 3,05s và 6,35s. Cảnh 1: cận cực gần một mắt... Cảnh 3 (2 giây cuối): lùi ra chính diện, lộ kết quả."

Nếu video quá dài hoặc không dựng được khung (ví dụ cùng khuôn với video khác), nói rõ trong mục 5 thay vì bỏ qua âm thầm.