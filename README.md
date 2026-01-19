# 📋 Task Board - N-Tier Architecture (Week 6)

## 🏗️ Architecture

## 🚀 Quick Start

```bash
# Start all services
./scripts/start-all.sh

# Access
https://taskboard.local
```

## 📁 Project Structure
```
week6-ntier/
├── src/           # Backend source code
├── public/        # Frontend files
├── database/      # SQL scripts
├── nginx/         # Nginx config
└── scripts/       # Helper scripts
```
## 🛠️ Technologies

<img width="284" height="159" alt="Screenshot 2569-01-19 at 13 45 56" src="https://github.com/user-attachments/assets/dfbdf2a5-4785-40a7-a82d-b3ca96b9eb0a" />


---
## 👨‍💻 Author
[นางสาว วริศรา สรรพกรพิเศษ] - ENGSE207 Week 6

## 🛠️ แก้ปัญหาเบื้องต้น
```
1. ไม่สามารถรันไฟล์ SQL ได้ (No such file or directory)

ปัญหา:รันคำสั่ง psql -f database/init.sql แล้วระบบแจ้งว่าไม่พบไฟล์
สาเหตุ:รันคำสั่งจาก directory ที่ไม่ตรงกับตำแหน่งของไฟล์
วิธีแก้ไข:เข้าไปยังโฟลเดอร์ database ก่อน หรือระบุ path ให้ถูกต้อง cd database psql -h localhost -U taskboard -d taskboard_db -f init.sql

2. ทดสอบ API ผ่าน HTTPS ไม่ผ่าน (curl option -k is unknown)

ปัญหา:สคริปต์ test-api.sh แจ้ง error เกี่ยวกับ curl -k
สาเหตุ:ส่ง option -k รวมกับ URL ทำให้ curl อ่านคำสั่งผิด
วิธีแก้ไข:แยก -k เป็น option ของ curl ไม่ใส่รวมกับ URL curl -k https://taskboard.local/api/health

3. เข้าเว็บ taskboard.local ไม่ได้ (DNS_PROBE_FINISHED_NXDOMAIN)

ปัญหา:Browser ไม่สามารถเข้าถึง taskboard.local
สาเหตุ:ยังไม่ได้กำหนด DNS หรือ host name ในเครื่อง client
วิธีแก้ไข:เพิ่ม mapping ในไฟล์ /etc/hosts 192.168.56.2 taskboard.localจากนั้นสามารถ ping และเข้าเว็บได้ตามปกติ

```
### PostgreSQL
```bash
# ตรวจสอบ status
sudo systemctl status postgresql

# ดู logs
sudo tail -50 /var/log/postgresql/postgresql-*-main.log

# Reset password
sudo -u postgres psql -c "ALTER USER taskboard PASSWORD 'taskboard123';"
```

## Nginx
```
# Test config
sudo nginx -t

# ดู logs
sudo tail -f /var/log/nginx/taskboard_error.log

# Restart
sudo systemctl restart nginx
```

## Node.js
```
# ดู PM2 logs
pm2 logs taskboard-api

# Restart
pm2 restart taskboard-api

# ดู process
pm2 show taskboard-api
```
