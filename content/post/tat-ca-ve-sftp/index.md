---
author: Ethan BUI
title: "Tất cả về sFTP, SSH và FTP"
date: 2021-08-11T10:50:00+07:00
tags:
    - SSH
    - FTP
    - sFTP
categories:
    - Learn
draft: false
image: sftp.jpg
---

## Giới thiệu tổng quan

### sFTP là gì?

sFTP là một giao thức mạng giúp người dùng có thể upload và download dữ liệu trên máy chủ. sFTP dùng SSH để kết nối nên dữ liệu được di chuyển sẽ bảo mật (mã hoá) hơn.

Thông tin thêm để tìm hiểu:
* Các kiểu mã hoá của SSH

### SSH là gì?

SSH là một giao thức mạng giúp người dùng có thể điều khiển máy tính từ xa qua Internet. SSH sinh ra để thay thế cho Telnet vốn không có mã hoá. SSH sử dụng port là 22.

### FTP là gì?

FTP là một giao thức giúp người dùng có thể chuyển dữ liệu từ máy tính này sang máy tính khác. FTP sử dụng 2 port là 20 và 21.

### Đăng nhâp

Để sử dụng được sFTP, bạn phải có tài khoản được lưu trữ trên máy chủ.

- Đăng nhập trên Windows

    - Sử dụng phần mềm Filezilla

- Đăng nhập trên Linux

    - Sử dụng phần mềm Filezilla


    - Sử dụng command line

        ```
        sftp user@ip_domain_localhost
        ```


- Đăng nhập trên MacOS

## Cách sử dụng

1. Tạo người dùng trên máy chủ

Sử dụng một số lệnh để tạo người dùng
```
sudo useradd usersftp
sudo passwd usersftp
```

2. Tạo thư mục để lưu trữ

Sử dụng một số lệnh để tạo thư mục
```
mkdir -p /var/sftp/uploads
```

3. Cấu hình với giới hạn cho người dùng và thư mục

Sử dụng một số lệnh để giới hạn người dùng
```
sudo chown root:root /var/sftp
sudo chmod 755 /var/sftp

sudo chown usersftp:usersftp /var/sftp/uploads
```

Hạn chế quyền truy cập vào thư mục
```
vi /etc/ssh/sshd_config
```

```
Match User usersftp
        ForceCommand internal-sftp -d sftp
        PasswordAuthentication yes
        ChrootDirectory /var/sftp
        X11Forwarding no
        AllowTcpForwarding no
```

Sau khi thay đổi, chúng ta sẽ khởi động lại dịch vụ SSH
```
systemctl status sshd
systemctl restart sshd
```

Đăng nhập thử
```
ssh
sftp
```

4. Một số lệnh thường dùng

* SSH

  - Đăng nhập

    ```
    ssh -p userssh@your_server_ip_or_remote_hostname
    ```

  - Debug

    ```
    ssh -v userssh@your_server_ip_or_remote_hostname
    ```

  - Tạo SSK key

    ```
    ssh-keygen
    ```
  
  - Copy SSH key

    ```bash
    ssh-copy-id username@remote_host

    # or
    cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

    ```

* sFTP
  
  - Đăng nhập

    ```bash
    sftp -oPort=custom_port usersftp@your_server_ip_or_remote_hostname
    ```

  - Debug

    ```bash
    sftp -o LogLevel=DEBUG1 usersftp@your_server_ip_or_remote_hostname
    ```

## Một số trường hợp cụ thể

### Chỉ 1 người dùng

```
groupadd sftponly

systemctl restart sshd
```

```
Match Group sftponly
    ChrootDirectory /home/%u
    ForceCommand internal-sftp
    AllowTcpForwarding no
    PasswordAuthentication yes
    X11Forwarding no
```

```
useradd -G sftponly -s /sbin/nologin user1
chown root /home/user1
chmod g+rx /home/user1
```

```
mkdir /home/user1/data
chown user1:user1 /home/user1/data
```

Chứng thực qua SSH keys.

```
chown user1:user1 /home/user1/data
chown user1:user1 /home/user1/.ssh
chmod 0700 /home/user1/.ssh 
```

Kiểm tra
```
sftp user1@ip_domain_localhost
sftp -o LogLevel=DEBUG1 user1@ip_domain_localhost
```

### Nhiều người dùng

```bash
#Create okchakela group
groupadd okchakela
#Add members and specify the home directory
useradd Codeeer -d /mnt/data1/Private/Codeeer -s /sbin/nologin -G okchakela
useradd Ridesky -d /mnt/data1/Private/Ridesky -s /sbin/nologin -G okchakela
useradd Dorothy -d /mnt/data1/Private/Dorothy -s /sbin/nologin -G okchakela
 
#Create ftpaccess group
groupadd ftpaccess
#Add member
useradd py -s /sbin/nologin -G ftpaccess
```

```bash
#For matching okchakela group
chown root:root /
chown root:root /mnt
chown root:root /mnt/data1
chown root:root /mnt/data1/Private
#Set the owner of the user's private directory
chown -R Codeeer /mnt/data1/Private/Codeeer
chown -R Ridesky /mnt/data1/Private/Ridesky
chown -R Dorothy /mnt/data1/Private/Dorothy
#Set up permissions that other people cannot access (700)
chmod -R 700 /mnt/data1/Private/Codeeer
chmod -R 700 /mnt/data1/Private/Ridesky
chmod -R 700 /mnt/data1/Private/Dorothy
 
#Used to match ftpaccess group
chown root:root /home
#Set the owner of the user's private directory
chown py /home/py
#Set up permissions that other people cannot access (700)
chmod 700 /home/py
```

## Tham khảo

1. https://blog.tinned-software.net/setup-sftp-only-account-using-openssh-and-ssh-key/
2. https://www.programmersought.com/article/24614931803/
3. https://www.digitalocean.com/community/tutorials/how-to-use-sftp-to-securely-transfer-files-with-a-remote-server
4. https://vi.wikipedia.org/wiki/SSH
5. https://vi.wikipedia.org/wiki/FTP