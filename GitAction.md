# Git Action để triển khai CI/CD

## CI/CD là gì?

**CI/CD** là viết tắt của **Continuous Integration/Continuous Delivery** (Tích hợp liên tục/Phân phối liên tục) và **Continuous Deployment** (Triển khai liên tục). Đây là một phương pháp phát triển phần mềm giúp tự động hóa các giai đoạn xây dựng, kiểm thử và triển khai ứng dụng.

* **Continuous Integration (CI):** Tự động hợp nhất các thay đổi mã nguồn từ nhiều nhà phát triển vào một kho lưu trữ chung. Mỗi lần hợp nhất sẽ kích hoạt một quy trình xây dựng và kiểm thử tự động để phát hiện lỗi sớm.
* **Continuous Delivery (CD):** Tự động hóa việc phát hành các thay đổi mã nguồn đã được kiểm thử thành công đến môi trường staging hoặc production.
* **Continuous Deployment (CD):** Tự động triển khai các thay đổi đã qua kiểm thử lên môi trường production mà không cần sự can thiệp của con người.

## GitHub Actions là gì?

**GitHub Actions** là một nền tảng CI/CD được tích hợp sẵn trong GitHub. Nó cho phép bạn tự động hóa các quy trình phát triển phần mềm của mình, chẳng hạn như:

* Xây dựng và kiểm thử mã nguồn
* Đóng gói ứng dụng
* Triển khai ứng dụng lên các môi trường khác nhau
* Gửi thông báo
* Và nhiều hơn nữa

## Cách hoạt động của GitHub Actions

GitHub Actions sử dụng các tệp YAML để định nghĩa các quy trình làm việc (workflows). Mỗi workflow bao gồm một hoặc nhiều công việc (jobs), và mỗi job bao gồm một hoặc nhiều bước (steps).

* **Workflows:** Được định nghĩa trong các tệp `.yml` trong thư mục `.github/workflows` của kho lưu trữ.
* **Events:** Các sự kiện kích hoạt workflow, chẳng hạn như `push` (đẩy mã nguồn), `pull_request` (yêu cầu kéo), `schedule` (lịch trình),...
* **Jobs:** Các công việc được thực thi trên một máy ảo (runner).
* **Steps:** Các lệnh hoặc hành động được thực thi trong một job.
* **Actions:** Các đoạn mã có thể tái sử dụng để thực hiện các tác vụ phổ biến.

## Ví dụ về workflow CI/CD đơn giản

```yaml
name: CI/CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

  deploy:
    needs: build
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Deploy to production
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```

## Lợi ích của việc sử dụng GitHub Actions cho CI/CD

* **Tích hợp liền mạch:** Được tích hợp sẵn trong GitHub, không cần sử dụng dịch vụ của bên thứ ba.
* **Dễ sử dụng:** Cú pháp YAML đơn giản, dễ học và dễ sử dụng.
* **Linh hoạt:** Hỗ trợ nhiều ngôn ngữ lập trình, hệ điều hành và nền tảng đám mây.
* **Miễn phí:** Cung cấp gói miễn phí cho các kho lưu trữ công khai và riêng tư.
* **Cộng đồng lớn:** Có một cộng đồng lớn và nhiều actions có sẵn để tái sử dụng.
