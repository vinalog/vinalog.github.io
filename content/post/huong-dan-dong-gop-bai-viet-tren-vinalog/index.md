---
author: Tri BUI
title: "Hướng dẫn đóng góp bài viết trên VinaLog"
date: 2021-08-08T13:00:00+07:00
tags:
    - Tutorial
    - Hướng dẫn
categories:
    - Tutorials
draft: false
image: update.jpg
---

Chào mọi người, mình xin phép được chia sẻ cách đăng bài viết trên VinaLog Github như sau:

## Mã nguồn của VinaLog Github

Đây là mã nguồn của VinaLog: https://github.com/vinalog/vinalog.github.io.

### Thông tin về mã nguồn

1. Hugo.

    Blog được xây dựng từ Hugo. Hugo là một framework xây dựng dựa trên ngôn ngữ Golang của Google và sử dụng markdown để tạo bài viết. Trang chủ của Hugo Golang ở đây: https://gohugo.io.

    *Ưu điểm:*
    - Tốc độ xây dựng (build) trang web nhanh.
    - Không cần cơ sở dữ liệu để lưu bài viết
    - Các plugin không yêu cầu cấp quyền, không cần lo về bảo mật

    *Nhược điểm:*
    - Cập nhật...

2. Git, cụ thể là Github.

    Mã nguồn Web được lưu trữ trên Github. Github là một trang để lưu trữ mã nguồn mở, giúp chia sẻ code với nhau và mọi người có thể đóng góp code của mình trên đó.

    Trang chủ của Github ở đây: https://github.com.

### Cách sử dụng mã nguồn

1. Trước tiên, bạn phải cài đặt Git. Tải Git ở đây: https://git-scm.com/downloads.

    Kiểm tra Git đã cài đặt trên máy tính của bạn. Sử dụng lệnh sau:

    ```bash
    git --version
    ```

    ![Như thế này là được.](2021-08-08_091416.png)

2. Tiếp theo, bạn phải có một tài khoản Github. Đăng kí ở đây: https://github.com/signup

    Sau khi đăng ký xong, bạn phải xác nhận một e-mail để xác thực tài khoản. Đăng nhập vào Github.

    ![](2021-08-08_092043.png)

3. Sử dụng một số lệnh để tải xuống và sử dụng mã nguồn

    Bạn truy cập mã nguồn https://github.com/vinalog/vinalog.github.io và fork về tài khoản Github của bạn.

    ![](2021-08-08_092213.png)

    Kết quả sau khi fork.

    ![](2021-08-08_092324.png)

    Tiếp theo, các bạn sử dụng một số lệnh sau:
    ```bash
    # Tạo một thư mục mới tên là source
    mkdir source
    cd source

    # Clone mã nguồn về máy tính
    git clone https://github.com/tribuit003/vinalog.github.io.git
    ```

    > Với mã nguồn này bạn có thể khởi chạy trang VinaLog dưới máy tính của bạn.

4. Để chạy VinaLog dưới máy tính. (Không cần thiết có thể bỏ qua)

    Các bạn phải cài đặt Hugo. Tải và cài đặt Hugo ở đây: https://gohugo.io/getting-started/installing/. Bạn chỉ cần follow cái hướng dẫn trên là cài đặt được Hugo.

    Kiểm tra đã cài đặt Hugo hay chưa.
    ![](2021-08-08_093044.png)

    > Mã nguồn hiện tại vẫn chưa có Themes nên bạn không thể chạy được trang. Các bạn cần sử dụng lệnh sau

    ```bash
    # Truy cập vào thư mục themes trong mã nguồn
    cd themes

    # Tải themes về máy
    git clone https://github.com/CaiJimmy/hugo-theme-stack.git

    # Trở về thư mục chính
    cd ..
    ```

    ![](2021-08-08_093336.png)

    Giờ bạn có thể chạy Web dưới local. Sử dụng lệnh

    ```
    hugo server -D
    ```

    ![](2021-08-08_093454.png)

    ![Truy cập http://localhost:1313 hoặc http://127.0.0.1:1313](2021-08-08_093515.png)

5. Để tạo bài viết mới.

    Mở trình soạn thảo văn bản. Ở đây mình sử dụng Visual Studio Code. Tiếp theo, bạn tạo một thư mục mới trong `content/post/<bai-viet-moi>/index.md`

    ![](2021-08-08_093901.png)

    Sử dụng `markdown` để viết bài viết.

    ```markdown
    ---
    title: "Bài viết mới từ người lạ"
    date: 2021-08-08
    tags:
        - Test
    categories:
        - Test
    image: null
    draft: false
    lastmod: 2021-08-08

    ---

    ## Đây là dòng 1

    Đây là câu văn.

    ## Đây là dòng 2

    ```

    Chạy thử dưới local. Tắt server và chạy lại.
    ```bash
    # Ctrl+C

    hugo server -D
    ```

    ![](2021-08-08_094614.png)

    Sau khi viết xong bài viết và chỉnh sửa xong bài viết. Hãy cùng qua bước tiếp theo.

6. Đẩy bài viết lên Github của bạn.

    Sử dụng các lệnh thao tác với Git như sau:

    ```bash
    git add .
    git commit -m "Add new post from Guest"
    git push
    ```

    ![](2021-08-08_102117.png)

    Sau khi đẩy code lên Github của bạn. Kết quả như thế này!

    ![](2021-08-08_102447.png)

    Tiếp theo, bạn cần tạo một `Pull requests` để đẩy **code về Github của VinaLog**.

    ![](2021-08-08_102736.png)

    ![Comment của bạn ở đây](2021-08-08_104353.png)

    ![Sau khi tạo Pull requests](2021-08-08_104433.png)

    ![Theo dõi quá trình Pull requests](2021-08-08_104555.png)

    Bạn đợi bên VinaLog kiểm duyệt và bài viết của bạn sẽ được đăng lên VinaLog.

## Kết quả

Trang chủ của VinaLog: https://vinalog.github.io

![](2021-08-08_104848.png)

Chúc các bạn thành công!.