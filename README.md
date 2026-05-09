#  Quan Ly Tiem Cam Do - BTVN 02

**Mon hoc:** Phat trien ung dung voi ma nguon mo 
**Sinh vien:** Tạ Phạm Đình Hòa
**Lop:** 58KTPM  
**Deadline:** 23h59 ngày 09/05/2026  

---

##  Yeu cau de bai

- Thiet ke CSDL cho he thong quan ly tiem cam do
- Xay dung 3 service bang Docker: MariaDB, phpMyAdmin, Django
- Co trang Admin (them/sua/xoa du lieu)
- Co trang liet ke con no den han chua tra
- Public qua Cloudflare Tunnel

---

##  Thiet ke CSDL

<img width="1184" height="1631" alt="image" src="https://github.com/user-attachments/assets/89d7a25f-2eae-4eb9-8e0a-d9d05efaaaf6" />


### Cac bang:

| Bang | Mo ta |
|---|---|
| NhanVien | Nhan vien xu ly phieu cam |
| KhachHang | Khach hang cam do (con no) |
| TaiSan | Tai san duoc dem cam |
| PhieuCamDo | Phieu ghi nhan giao dich cam |
| ThanhToan | Lich su thanh toan cua phieu |

---

## 🐳 Cau truc thu muc
```
camdo_project/
├── docker-compose.yml
└── django_app/
    ├── Dockerfile
    ├── requirements.txt
    ├── manage.py
    ├── config/
    │   ├── settings.py
    │   └── urls.py
    ├── camdo/
    │   ├── models.py
    │   ├── views.py
    │   ├── admin.py
    │   └── apps.py
    └── templates/
        └── home.html
```
---

##  Cac buoc thuc hien

### Buoc 1: Tao cau truc thu muc
```bash
mkdir -p camdo_project/django_app/camdo
mkdir -p camdo_project/django_app/templates
cd camdo_project
```
<img width="1478" height="758" alt="image" src="https://github.com/user-attachments/assets/19fae3cf-2f8e-4716-a123-1458a64034d8" />


---

### Buoc 2: Tao docker-compose.yml (3 service)
```bash
nano docker-compose.yml
```
- Service **db**: MariaDB 11.2
- Service **phpmyadmin**: cong 8080
- Service **web**: Django build tu Dockerfile

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/44ec1479-f9fd-4e0c-ac50-a99b163b40b4" />

<img width="1480" height="759" alt="image" src="https://github.com/user-attachments/assets/00f05c19-81d6-4448-8335-e6f238582fe8" />

---

### Buoc 3: Tao Dockerfile
```bash
nano django_app/Dockerfile
```
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/b05a98f7-36dc-48d6-997f-6f95026bc284" />

---

### Buoc 4: Tao requirements.txt
Django==4.2.11
mysqlclient==2.2.4
python-decouple==3.8

<img width="1480" height="758" alt="image" src="https://github.com/user-attachments/assets/bedffe62-538a-4db4-8999-e5cca920fe6b" />

---

### Buoc 5: Tao Django project
```bash
pip3 install django --break-system-packages
export PATH=$PATH:/home/dinhhoa/.local/bin
django-admin startproject config .
```
<img width="1486" height="762" alt="image" src="https://github.com/user-attachments/assets/37a9e4cf-dfa3-44ad-aa1e-3e922ee92295" />

---

### Buoc 6: Viet models.py (5 bang)
```bash
nano camdo/models.py
```
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/866aaa9a-86c6-466b-98ea-2093a59f83d9" />

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/11769111-2c24-4384-aff5-f40094e40fca" />

---

### Buoc 7: Viet admin.py
```bash
nano camdo/admin.py
```
<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/dc532b7a-af77-4fae-87e3-87edbcbfd9c7" />


---

### Buoc 8: Viet views.py - trang con no qua han
```bash
nano camdo/views.py
```
<img width="1477" height="757" alt="image" src="https://github.com/user-attachments/assets/8acccc3a-bee7-42d8-98d0-9582cac59ca4" />

---

### Buoc 9: Build va chay Docker
```bash
docker compose up --build -d
```
<img width="1485" height="762" alt="image" src="https://github.com/user-attachments/assets/e4ac2270-930d-443a-8d2e-89bc2373bf44" />


---

### Buoc 10: Migrate database
```bash
docker exec camdo_web python manage.py makemigrations camdo
docker exec camdo_web python manage.py migrate
```
<img width="1477" height="758" alt="image" src="https://github.com/user-attachments/assets/64a6c2ed-24e5-4366-a6e9-00a4208a5a0d" />


---

### Buoc 11: Tao tai khoan admin
```bash
docker exec -it camdo_web python manage.py createsuperuser
```
<img width="1917" height="1075" alt="image" src="https://github.com/user-attachments/assets/6ee9e692-dfc9-4cbd-a8d9-3204891b0499" />

---

### Buoc 12: Cai Cloudflare Tunnel
```bash
docker exec -it mycloudflared cloudflared tunnel login
docker exec -it mycloudflared cloudflared tunnel create camdo
docker exec -it mycloudflared cloudflared tunnel route dns camdo camdo.taphamdinhhoa.io.vn
docker exec -it mycloudflared cloudflared tunnel run --url http://camdo_web:8000 camdo
```
<img width="1478" height="765" alt="image" src="https://github.com/user-attachments/assets/8daa157d-479f-41c8-a246-d6338e88d0db" />


---

## Ket qua

| Trang | Link |
|---|---|
| Trang chu (con no qua han) | https://camdo.taphamdinhhoa.io.vn |
| Trang Admin | https://camdo.taphamdinhhoa.io.vn/admin |
| phpMyAdmin | http://192.168.123.115:8080 |

<img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/672a9acf-481f-4495-b820-095205e2a92e" />

><img width="1918" height="1078" alt="image" src="https://github.com/user-attachments/assets/7a8b65d7-6484-477d-8694-26f7fb831c99" />

<img width="1918" height="1077" alt="image" src="https://github.com/user-attachments/assets/f2619046-bbf1-4842-80fb-fe5ef459992f" />

---

##  Cong nghe su dung

- **Python** 3.11
- **Django** 4.2.11
- **MariaDB** 11.2
- **Docker** + Docker Compose
- **Cloudflare Tunnel**
- **phpMyAdmin**
