**“Sơ đồ tư duy toàn bộ website bsliem.github.io”** (dạng kiến trúc hệ thống) để bác giữ như **tài liệu kỹ thuật lâu dài của project.**codes mde please

```
# Sơ đồ tư duy toàn bộ website `bsliem.github.io`
*Tài liệu kiến trúc hệ thống – phiên bản nền tảng*

---

## 1. Mục tiêu tổng quát

Website `bsliem.github.io` là website cá nhân – học thuật – chuyên môn của **BS.CK2. Đỗ Thanh Liêm**, được xây dựng để phục vụ đồng thời 3 mục tiêu:

### 1.1. Hồ sơ chuyên môn
- Giới thiệu bác sĩ
- Trình bày quá trình đào tạo
- Trình bày kinh nghiệm nghề nghiệp
- Xây dựng uy tín học thuật và chuyên môn

### 1.2. Kênh chia sẻ học thuật
- Đăng bài viết chuyên môn
- Chia sẻ nội dung nghiên cứu
- Lưu trữ các công trình, bài báo, liên kết học thuật
- Tạo nền tảng phát triển nội dung lâu dài

### 1.3. Kênh thông tin phòng khám
- Cung cấp thông tin liên hệ
- Hướng dẫn đặt lịch khám
- Chỉ đường bằng Google Maps
- Hỗ trợ người bệnh tiếp cận thông tin chính thức

---

# 2. Tư tưởng thiết kế hệ thống

## 2.1. Nền tảng kỹ thuật
Website sử dụng:

- **Quarto** để viết nội dung và dựng website
- **Git** để quản lý phiên bản
- **GitHub** để lưu trữ source code
- **GitHub Pages** để xuất bản website
- **CSS tùy chỉnh** để thiết kế giao diện riêng

## 2.2. Tư tưởng kiến trúc
Website được tổ chức theo mô hình:

- **Trang tĩnh cốt lõi** ở thư mục gốc
- **Bài viết động** trong thư mục `posts/`
- **Biến dùng chung** trong `_variables.yml`
- **Cấu hình website** trong `_quarto.yml`
- **Giao diện** trong `styles.css`
- **HTML xuất bản** trong `docs/`

Đây là mô hình:
- dễ đọc
- dễ mở rộng
- dễ bảo trì
- phù hợp cho phát triển nội dung lâu dài

---

# 3. Kiến trúc tổng thể website

```text
Người dùng
   ↓
Truy cập bsliem.github.io
   ↓
GitHub Pages đọc thư mục docs/
   ↓
docs/ được tạo ra bởi Quarto render
   ↓
Quarto render từ các file .qmd + _variables.yml + styles.css + _quarto.yml
   ↓
Source code được quản lý bằng Git và lưu trên GitHub
```

------

# 4. Kiến trúc thư mục dự án

```
bsliem.github.io/
│
├── _quarto.yml
├── _variables.yml
├── styles.css
├── .nojekyll
├── README.md
│
├── index.qmd
├── about.qmd
├── research.qmd
├── posts.qmd
├── booking.qmd
├── contact.qmd
│
├── posts/
│   ├── 2026-03-14-bai-viet-dau-tien.qmd
│   ├── ...
│
├── hinh/
│   ├── bs_liem_ava.webp
│   ├── ...
│
├── my_md/
│   ├── 01_gioi_thieu.qmd
│   ├── 02_ho_so.qmd
│   ├── ...
│
└── docs/
    ├── index.html
    ├── about.html
    ├── research.html
    ├── posts.html
    ├── booking.html
    ├── contact.html
    ├── site_libs/
    └── ...
```

------

# 5. Vai trò của từng thành phần

## 5.1. `_quarto.yml`

### Vai trò

Là file cấu hình trung tâm của toàn bộ website.

### Chức năng

- Khai báo project kiểu website
- Xác định thư mục xuất bản là `docs/`
- Tạo thanh điều hướng `navbar`
- Cấu hình theme / css / toc / smooth-scroll
- Điều phối cách Quarto render toàn site

### Ý nghĩa

Đây là **bộ khung kiến trúc** của website.

------

## 5.2. `_variables.yml`

### Vai trò

Chứa các biến dùng chung cho toàn website.

### Biến tiêu biểu

- `name`
- `subtitle`
- `hospital`
- `clinic`
- `email`
- `phone`
- `phone_tel`
- `website_url`
- `youmed_url`
- `cambridge_url`
- `address`
- `google_maps_url`

### Ý nghĩa

Giúp:

- thống nhất thông tin trên toàn site
- giảm lặp lại nội dung
- sửa một nơi, đổi toàn bộ website
- dễ quản lý lâu dài

------

## 5.3. `styles.css`

### Vai trò

Điều khiển giao diện website.

### Phạm vi tác động

- màu sắc
- font chữ
- navbar
- hero section
- card box
- button
- spacing
- giao diện mobile
- bóng đổ, bo góc, nền

### Ý nghĩa

Đây là thành phần quyết định:

- website có “đẹp” hay không
- website có “ra chất bác sĩ / học thuật” hay không

------

## 5.4. `index.qmd`

### Vai trò

Trang chủ của website.

### Mục tiêu

- tạo ấn tượng đầu tiên
- giới thiệu ngắn gọn về bác sĩ
- định hướng người dùng đến các phần quan trọng
- làm “landing page” chứ không chỉ là tài liệu đọc

### Thành phần nên có

- tên bác sĩ
- phụ đề chuyên môn
- mô tả ngắn
- nút dẫn đến:
  - Giới thiệu
  - Bài viết
  - Đặt lịch khám
- các khối:
  - chuyên môn
  - định hướng website
  - truy cập nhanh

------

## 5.5. `about.qmd`

### Vai trò

Trang hồ sơ chuyên môn.

### Nội dung cốt lõi

- quá trình đào tạo
- kinh nghiệm chuyên môn
- hướng nghiên cứu
- đơn vị công tác
- định hướng nghề nghiệp

### Ý nghĩa

Trang xây dựng **uy tín và chân dung nghề nghiệp**.

------

## 5.6. `research.qmd`

### Vai trò

Trang nghiên cứu học thuật.

### Nội dung có thể chứa

- hướng nghiên cứu chính
- bài báo khoa học
- công trình đã công bố
- liên kết bài báo quốc tế
- dữ liệu / dự án / hội nghị

### Ý nghĩa

Giúp website không chỉ là website phòng khám, mà còn là **website học thuật cá nhân**.

------

## 5.7. `posts.qmd`

### Vai trò

Trang tổng hợp bài viết.

### Chức năng

- lấy nội dung từ thư mục `posts/`
- liệt kê các bài viết mới
- sắp xếp theo ngày
- có thể lọc theo category nếu mở rộng

### Ý nghĩa

Đây là “cổng vào” của hệ thống blog / bài viết.

------

## 5.8. `posts/`

### Vai trò

Thư mục chứa từng bài viết riêng lẻ.

### Quy ước đặt tên

```
YYYY-MM-DD-ten-bai-viet.qmd
```

### Ví dụ

```
posts/2026-03-14-bai-viet-dau-tien.qmd
posts/2026-03-20-sa-sut-tri-tue-som.qmd
posts/2026-03-28-mat-ngu-o-nguoi-cao-tuoi.qmd
```

### Ý nghĩa

Giúp:

- dễ viết bài mới
- dễ quản lý theo thời gian
- mở rộng số lượng bài mà không rối thư mục gốc

------

## 5.9. `booking.qmd`

### Vai trò

Trang đặt lịch khám.

### Nội dung

- dịch vụ khám chữa bệnh
- thời gian khám
- hướng dẫn liên hệ trước
- điện thoại / Zalo
- địa chỉ
- Google Maps
- nút gọi điện / mở bản đồ

### Ý nghĩa

Đây là trang chuyển đổi thực tế nhất của website.

------

## 5.10. `contact.qmd`

### Vai trò

Trang liên hệ.

### Nội dung

- bệnh viện công tác
- phòng khám
- email
- điện thoại
- website
- YouMed
- địa chỉ
- bản đồ

### Ý nghĩa

Là nơi chuẩn hóa và xác nhận các kênh liên hệ chính thức.

------

## 5.11. `docs/`

### Vai trò

Thư mục xuất bản HTML.

### Chức năng

- chứa các file `.html` sau khi render
- GitHub Pages lấy nội dung ở đây để public website

### Ý nghĩa

Là **cầu nối giữa source code và website online**.

------

# 6. Sơ đồ logic nội dung website

```
Website bsliem.github.io
│
├── Trang chủ
│   ├── Giới thiệu ngắn
│   ├── Nút điều hướng nhanh
│   ├── Chuyên môn
│   ├── Mục tiêu website
│   └── Truy cập nhanh
│
├── Giới thiệu / Hồ sơ
│   ├── Đào tạo
│   ├── Kinh nghiệm
│   ├── Sở trường nghiên cứu
│   └── Hồ sơ chuyên môn
│
├── Nghiên cứu
│   ├── Hướng nghiên cứu
│   ├── Bài báo
│   ├── Dự án
│   └── Liên kết học thuật
│
├── Bài viết
│   ├── Danh sách bài viết
│   └── Từng bài riêng trong posts/
│
├── Đặt lịch khám
│   ├── Dịch vụ
│   ├── Giờ khám
│   ├── Hướng dẫn liên hệ
│   ├── Địa chỉ
│   └── Bản đồ
│
└── Liên hệ
    ├── Bệnh viện công tác
    ├── Phòng khám
    ├── Email
    ├── Điện thoại
    ├── Website
    └── YouMed
```

------

# 7. Sơ đồ dòng chảy làm việc (workflow)

## 7.1. Workflow biên tập nội dung

```
Sửa file .qmd / _variables.yml / styles.css
   ↓
quarto render
   ↓
Kiểm tra local trong docs/
   ↓
git add .
   ↓
git commit -m "..."
   ↓
git push
   ↓
GitHub Pages tự deploy
   ↓
Website online cập nhật
```

------

## 7.2. Workflow viết bài mới

```
Tạo file mới trong posts/
   ↓
Viết YAML + nội dung bài viết
   ↓
quarto render
   ↓
Kiểm tra posts.html và bài viết riêng
   ↓
git add . && git commit && git push
   ↓
Website cập nhật bài mới
```

------

## 7.3. Workflow sửa thông tin chung

```
Sửa _variables.yml
   ↓
quarto render
   ↓
Toàn site cập nhật các biến liên quan
```

Ví dụ:

- đổi số điện thoại
- đổi email
- đổi tên phòng khám
- đổi link YouMed

------

# 8. Quan hệ giữa các file

## 8.1. Quan hệ cấu hình

- `_quarto.yml` điều phối toàn website
- `_variables.yml` cung cấp dữ liệu nội dung dùng chung
- `styles.css` cung cấp diện mạo

## 8.2. Quan hệ nội dung

- `index.qmd`, `about.qmd`, `research.qmd`, `booking.qmd`, `contact.qmd`, `posts.qmd`
   đều là các node nội dung chính
- `posts/` là nguồn cấp nội dung cho `posts.qmd`

## 8.3. Quan hệ xuất bản

- tất cả `.qmd` được render thành `.html` trong `docs/`
- GitHub Pages chỉ đọc `docs/`

------

# 9. Hệ thống biến dùng chung – triết lý vận hành

## 9.1. Mục tiêu

Không hard-code các thông tin lặp lại nhiều lần.

## 9.2. Ví dụ thông tin cần biến hóa

- tên bác sĩ
- đơn vị công tác
- phòng khám
- email
- điện thoại
- website
- Google Maps
- link YouMed

## 9.3. Lợi ích

- nhất quán
- dễ cập nhật
- giảm sai sót
- giúp site chuyên nghiệp hơn

------

# 10. Hệ thống giao diện – triết lý thẩm mỹ

## 10.1. Định hướng thẩm mỹ

Website cần:

- sạch
- sáng
- đáng tin
- chuyên nghiệp
- không rối
- không quá màu mè

## 10.2. Tông màu phù hợp

- xanh y khoa
- xanh đậm tin cậy
- xanh sáng hiện đại
- xanh ngọc nhẹ gợi cảm giác chữa lành
- nền sáng, dễ đọc

## 10.3. Ngôn ngữ thị giác

- hero section
- card box
- nút bấm rõ
- icon nhẹ
- khoảng trắng hợp lý
- giao diện mobile thân thiện

------

# 11. Các vấn đề kỹ thuật từng gặp và bài học

## 11.1. Render nhầm chỉ ra `index.html`

### Hiện tượng

Quarto có lúc chỉ báo:

```
Output created: docs\index.html
```

### Bài học

Cần nhìn log đầy đủ để chắc rằng toàn site đã render, hoặc đảm bảo cấu hình website đúng.

------

## 11.2. Xem nhầm trang

### Hiện tượng

Sửa `booking.qmd` nhưng lại mở `index.html`.

### Bài học

Phải xem đúng trang tương ứng với file đang sửa.

------

## 11.3. Dùng nhầm code block trong `.qmd`

### Hiện tượng

Bọc nội dung trong:

````
```markdown
...
```
````

### Bài học

`.qmd` là file nội dung thật, không cần code fence cho phần nội dung trang.

------

## 11.4. Git identity lỗi

### Hiện tượng

```
Author identity unknown
```

### Cách sửa

```
git config --global user.name "bsliem"
git config --global user.email "liem20k@gmail.com"
```

------

## 11.5. Cache trình duyệt

### Hiện tượng

GitHub đã cập nhật nhưng website vẫn hiện bản cũ.

### Bài học

Phải nghĩ đến:

- Chrome cache
- hard reload
- tab ẩn danh
- thêm `?v=2` vào URL

------

# 12. Tầm nhìn phát triển tương lai

## 12.1. Giai đoạn ngắn hạn

- hoàn thiện nội dung trang chính
- hoàn thiện CSS
- đồng bộ toàn bộ biến
- làm trang chủ đẹp hơn

## 12.2. Giai đoạn trung hạn

- viết bài đều đặn trong `posts/`
- hiển thị bài mới trên trang chủ
- cải thiện SEO
- thêm ảnh chân dung / ảnh phòng khám

## 12.3. Giai đoạn dài hạn

- biến website thành hồ sơ nghề nghiệp chính thức
- là cổng học thuật cá nhân
- là nơi chia sẻ kiến thức cho cộng đồng
- là kênh thông tin chính thức của phòng khám

------

# 13. Nguyên tắc vận hành lâu dài

## 13.1. Nội dung thật viết trong `.qmd`

Không sửa trực tiếp `.html` trong `docs/`

## 13.2. Mọi thay đổi đều đi theo chu trình

```
source → render → kiểm tra → git → publish
```

## 13.3. Biến dùng chung để trong `_variables.yml`

Không lặp lại thủ công ở nhiều trang nếu không cần

## 13.4. Giao diện tập trung ở `styles.css`

Không sửa linh tinh từng trang nếu có thể gom về CSS

## 13.5. Giữ thư mục gốc sạch

- trang chính ở root
- bài viết ở `posts/`
- ảnh ở `hinh/`
- HTML trong `docs/`

------

# 14. Kết luận kiến trúc hệ thống

Website `bsliem.github.io` được thiết kế như một hệ thống gồm 5 lớp:

## Lớp 1: Nội dung

- `.qmd`
- `posts/`

## Lớp 2: Dữ liệu dùng chung

- `_variables.yml`

## Lớp 3: Cấu hình

- `_quarto.yml`

## Lớp 4: Giao diện

- `styles.css`

## Lớp 5: Xuất bản

- `docs/`
- GitHub Pages

Tóm lại:

```
Nội dung + Biến + Cấu hình + Giao diện
→ Quarto render
→ docs/
→ GitHub Pages
→ Website online
```

------

# 15. Ghi chú định hướng cá nhân

Website này không chỉ là một sản phẩm kỹ thuật.

Nó là:

- hồ sơ nghề nghiệp số
- kênh học thuật cá nhân
- bộ mặt chuyên môn trên Internet
- nền tảng để phát triển bài viết, nghiên cứu, và hoạt động phòng khám trong tương lai

Vì vậy định hướng đúng là:

**làm chậm, chắc, sạch, đẹp, dễ quản lý, và có thể phát triển lâu dài.**