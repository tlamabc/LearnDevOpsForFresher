# LearnDevOpsForFresher


# Hướng Dẫn Cấu Hình Hệ Thống Linux

## Mục lục
1. [Giới thiệu](#giới-thiệu)
2. [Yêu cầu hệ thống](#yêu-cầu-hệ-thống)
3. [Bước 1: Cài đặt Web Server](#bước-1-cài-đặt-web-server)
    - [Cài đặt Nginx](#cài-đặt-nginx)
    - [Cài đặt Apache](#cài-đặt-apache)
4. [Bước 2: Cài đặt Cơ Sở Dữ Liệu](#bước-2-cài-đặt-cơ-sở-dữ-liệu)
    - [Cài đặt MySQL](#cài-đặt-mysql)
    - [Cài đặt PostgreSQL](#cài-đặt-postgresql)
5. [Bước 3: Triển khai các ứng dụng khác](#bước-3-triển-khai-các-ứng-dụng-khác)
    - [Cài đặt Node.js](#cài-đặt-nodejs)
    - [Cài đặt PHP](#cài-đặt-php)
    - [Cài đặt Python](#cài-đặt-python)
6. [Bước 4: Đảm bảo bảo mật](#bước-4-đảm-bảo-bảo-mật)
    - [Cài đặt và cấu hình Firewall](#cài-đặt-và-cấu-hình-firewall)
    - [Cài đặt Fail2ban](#cài-đặt-fail2ban)
    - [Cấu hình SSH an toàn](#cấu-hình-ssh-an-toàn)
7. [Bước 5: Triển khai và kiểm tra](#bước-5-triển-khai-và-kiểm-tra)
    - [Triển khai ứng dụng](#triển-khai-ứng-dụng)
    - [Giám sát và theo dõi](#giám-sát-và-theo-dõi)

## Giới thiệu
Tài liệu này hướng dẫn cách cấu hình hệ thống Linux từ cơ bản đến nâng cao, bao gồm việc cài đặt và cấu hình Web Server, cơ sở dữ liệu, các ứng dụng khác và đảm bảo bảo mật cho hệ thống.

## Yêu cầu hệ thống
- Hệ điều hành: Ubuntu, CentOS, hoặc Debian.
- Quyền truy cập `sudo`.
- Kết nối internet.

## Bước 1: Cài đặt Web Server

### Cài đặt Nginx
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt Nginx:
    ```bash
    sudo apt install nginx -y
    ```
3. Kiểm tra trạng thái Nginx:
    ```bash
    sudo systemctl status nginx
    ```
4. Cấu hình Nginx:
    - Tạo file cấu hình cho website:
    ```bash
    sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com
    sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
    sudo nginx -t
    sudo systemctl reload nginx
    ```

### Cài đặt Apache
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt Apache:
    ```bash
    sudo apt install apache2 -y
    ```
3. Kiểm tra trạng thái Apache:
    ```bash
    sudo systemctl status apache2
    ```
4. Cấu hình Apache:
    - Tạo Virtual Host cho website:
    ```bash
    sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/example.com.conf
    sudo a2ensite example.com.conf
    sudo apache2ctl configtest
    sudo systemctl reload apache2
    ```

## Bước 2: Cài đặt Cơ Sở Dữ Liệu

### Cài đặt MySQL
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt MySQL:
    ```bash
    sudo apt install mysql-server -y
    ```
3. Cấu hình bảo mật MySQL:
    ```bash
    sudo mysql_secure_installation
    ```
4. Tạo cơ sở dữ liệu và người dùng:
    ```bash
    sudo mysql -u root -p
    CREATE DATABASE example_db;
    CREATE USER 'example_user'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON example_db.* TO 'example_user'@'localhost';
    FLUSH PRIVILEGES;
    EXIT;
    ```

### Cài đặt PostgreSQL
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt PostgreSQL:
    ```bash
    sudo apt install postgresql postgresql-contrib -y
    ```
3. Tạo cơ sở dữ liệu và người dùng:
    ```bash
    sudo -i -u postgres
    psql
    CREATE DATABASE example_db;
    CREATE USER example_user WITH ENCRYPTED PASSWORD 'password';
    GRANT ALL PRIVILEGES ON DATABASE example_db TO example_user;
    \q
    exit
    ```

## Bước 3: Triển khai các ứng dụng khác

### Cài đặt Node.js
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt Node.js và npm:
    ```bash
    sudo apt install nodejs npm -y
    ```
3. Cài đặt các gói cần thiết:
    ```bash
    npm install
    ```

### Cài đặt PHP
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt PHP:
    ```bash
    sudo apt install php libapache2-mod-php php-mysql -y
    ```
3. Kiểm tra phiên bản PHP:
    ```bash
    php -v
    ```

### Cài đặt Python
1. Cập nhật hệ thống:
    ```bash
    sudo apt update
    ```
2. Cài đặt Python3 và pip:
    ```bash
    sudo apt install python3 python3-pip -y
    ```

## Bước 4: Đảm bảo bảo mật

### Cài đặt và cấu hình Firewall
1. Cài đặt `ufw`:
    ```bash
    sudo apt install ufw -y
    ```
2. Cấu hình tường lửa:
    ```bash
    sudo ufw allow OpenSSH
    sudo ufw allow 'Nginx Full' # Thay bằng 'Apache Full' nếu sử dụng Apache
    sudo ufw enable
    sudo ufw status
    ```

### Cài đặt Fail2ban
1. Cài đặt Fail2ban:
    ```bash
    sudo apt install fail2ban -y
    ```
2. Khởi động và kích hoạt Fail2ban:
    ```bash
    sudo systemctl start fail2ban
    sudo systemctl enable fail2ban
    ```
3. Cấu hình Fail2ban tại `/etc/fail2ban/jail.local`.

### Cấu hình SSH an toàn
1. Chỉnh sửa tệp cấu hình SSH:
    ```bash
    sudo nano /etc/ssh/sshd_config
    ```
2. Khuyến nghị:
    - Thay đổi cổng SSH mặc định (Port 22).
    - Vô hiệu hóa đăng nhập root (`PermitRootLogin no`).
    - Cho phép đăng nhập bằng khóa SSH, vô hiệu hóa mật khẩu (`PasswordAuthentication no`).
3. Tải lại cấu hình SSH:
    ```bash
    sudo systemctl reload sshd
    ```

## Bước 5: Triển khai và kiểm tra

### Triển khai ứng dụng
- Sử dụng các công cụ CI/CD như Jenkins, GitLab CI, hoặc GitHub Actions để tự động triển khai ứng dụng.

### Giám sát và theo dõi
- Cài đặt và cấu hình các công cụ giám sát như Prometheus, Grafana, hoặc Zabbix để theo dõi trạng thái và hiệu suất của hệ thống.

---

**Chú ý:** Hãy kiểm tra kỹ lưỡng mọi cấu hình trước khi triển khai trên hệ thống sản xuất.
