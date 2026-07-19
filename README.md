# Báo cáo thực tập AWS

Website báo cáo thực tập được xây dựng bằng Hugo và Markdown, dựa trên giao diện FCJ Workshop. Nội dung trình bày nhật ký thực tập, đề xuất dự án, workshop triển khai RecruitPro trên AWS, tự đánh giá và phản hồi.

- Website: <https://tiennnn1107.github.io/aws-internship-report-site/>
- Repository: <https://github.com/Tiennnn1107/aws-internship-report-site>
- Ngôn ngữ: tiếng Anh và tiếng Việt

## Công nghệ sử dụng

- Hugo Extended `0.137.1`
- Markdown
- Hugo Learn Theme
- Git và GitHub
- GitHub Actions và GitHub Pages cho website báo cáo
- Các dịch vụ AWS được trình bày trong workshop: VPC, EC2, RDS, S3, ALB, CloudFront, CloudWatch và SNS

> GitHub Actions trong repository này chỉ dùng để build và deploy website tài liệu lên GitHub Pages. Ứng dụng RecruitPro hiện vẫn được build và triển khai thủ công; CI/CD cho ứng dụng là hướng phát triển trong tương lai.

## Yêu cầu

Trước khi chạy dự án, cần cài đặt:

- [Git](https://git-scm.com/)
- [Hugo Extended v0.137.1](https://github.com/gohugoio/hugo/releases/tag/v0.137.1)

Kiểm tra phiên bản Hugo:

```powershell
hugo version
```

Kết quả cần có từ khóa `extended` và phiên bản tương thích với `0.137.1`.

## Tải source code

Clone repository cùng theme submodule:

```powershell
git clone --recurse-submodules https://github.com/Tiennnn1107/aws-internship-report-site.git
cd aws-internship-report-site
```

Nếu đã clone repository nhưng chưa tải theme:

```powershell
git submodule update --init --recursive
```

## Chạy website trên máy local

Khởi động Hugo development server:

```powershell
hugo server -D
```

Mở địa chỉ được Hugo hiển thị trong terminal, thông thường là:

```text
http://localhost:1313/aws-internship-report-site/
```

Hugo tự động tải lại trang khi file Markdown, layout hoặc tài nguyên tĩnh thay đổi.

## Build website

Kiểm tra khả năng build mà không ghi kết quả ra thư mục `public`:

```powershell
hugo --renderToMemory
```

Build bản production:

```powershell
hugo --minify
```

Kết quả được tạo trong thư mục `public/`. Đây là dữ liệu sinh tự động và không cần commit.

## Cấu trúc dự án

```text
.
├── .github/workflows/       # Workflow deploy GitHub Pages
├── archetypes/              # Mẫu front matter của Hugo
├── content/                 # Nội dung Markdown song ngữ
├── layouts/                 # Layout và shortcode tùy chỉnh
├── static/                  # Hình ảnh, CSS và tài nguyên tĩnh
├── themes/                  # Hugo theme dạng Git submodule
├── config.toml              # Cấu hình website và ngôn ngữ
└── README.md
```

Các phần nội dung chính:

```text
content/
├── 1-Worklog/               # Nhật ký thực tập
├── 2-Proposal/              # Đề xuất dự án
├── 3-BlogsTranslated/       # Blog đã dịch
├── 4-EventParticipated/     # Sự kiện đã tham gia
├── 5-Workshop/              # Workshop triển khai trên AWS
├── 6-SelfEvaluation/        # Tự đánh giá
└── 7-Feedback/              # Phản hồi
```

## Quy ước nội dung song ngữ

Mỗi trang sử dụng hai file:

- `_index.md`: nội dung tiếng Anh.
- `_index.vi.md`: nội dung tiếng Việt.

Ví dụ:

```text
content/5-Workshop/5.11-Kiem-thu-he-thong/
├── _index.md
└── _index.vi.md
```

Front matter cơ bản:

```yaml
---
title: "System testing"
date: 2026-07-10
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---
```

Lưu ý:

- `title` của `_index.md` phải viết bằng tiếng Anh.
- `title` của `_index.vi.md` phải viết bằng tiếng Việt.
- `weight` quyết định thứ tự hiển thị trong menu.
- `pre` chứa số thứ tự của mục.
- Hai bản ngôn ngữ nên có cùng cấu trúc và số mục.

## Thêm hình ảnh

Đặt hình trong `static/images/` theo đúng cấu trúc nội dung. Ví dụ:

```text
static/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/source-code.png
```

Nhúng hình vào Markdown:

```markdown
![Spring Boot source code](/images/5-Workshop/5.2-Chuan-bi-moi-truong-trien-khai/source-code.png)
```

Nên dùng tên file không dấu, không chứa khoảng trắng và mô tả ảnh đúng ngôn ngữ của trang.

## Nhúng video YouTube

Không commit video dung lượng lớn vào repository. Tải video lên YouTube rồi nhúng bằng mã sau:

```html
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden;">
  <iframe src="https://www.youtube.com/embed/VIDEO_ID"
    title="Testing video"
    style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
    allowfullscreen>
  </iframe>
</div>
```

Thay `VIDEO_ID` bằng mã nằm sau `youtu.be/` hoặc tham số `v=` của URL YouTube.

## Kiểm tra trước khi commit

```powershell
hugo --renderToMemory
git diff --check
git status --short
```

Nếu không có lỗi, commit và push:

```powershell
git add -A
git commit -m "Mô tả thay đổi"
git push origin main
```

## Triển khai GitHub Pages

Workflow tại `.github/workflows/hugo.yml` tự động chạy khi có commit được push lên `main`:

1. Checkout source code và theme submodule.
2. Cài Hugo Extended `0.137.1`.
3. Build website bằng `hugo --minify`.
4. Upload artifact.
5. Deploy lên GitHub Pages.

Có thể theo dõi quá trình deploy trong tab **Actions** của repository.

## Tác giả

**Tiến Trần Tân**

- GitHub: <https://github.com/Tiennnn1107>
- LinkedIn: <https://www.linkedin.com/in/ti%E1%BA%BFn-tr%E1%BA%A7n-t%C3%A2n-752650403/>

## Nguồn giao diện

Dự án được phát triển dựa trên FCJ Workshop Template và Hugo Learn Theme, sau đó được tùy chỉnh cho báo cáo thực tập AWS.
