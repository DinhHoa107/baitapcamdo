# 🏦 Quan Ly Tiem Cam Do - BTVN 02

**Mon hoc:** Phat trien ung dung voi ma nguon mo (TEE0421)  
**Sinh vien:** Dinh Hoa  
**Lop:** 58KTPM  
**Deadline:** 23h59 ngày 09/05/2026  

---

## 📋 Yeu cau de bai

- Thiet ke CSDL cho he thong quan ly tiem cam do
- Xay dung 3 service bang Docker: MariaDB, phpMyAdmin, Django
- Co trang Admin (them/sua/xoa du lieu)
- Co trang liet ke con no den han chua tra
- Public qua Cloudflare Tunnel

---

## 🗄️ Thiet ke CSDL

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

## ⚙️ Cac buoc thuc hien

### Buoc 1: Tao cau truc thu muc
```bash
mkdir -p camdo_project/django_app/camdo
mkdir -p camdo_project/django_app/templates
cd camdo_project
```
> 📸 **[Chen anh terminal sau khi tao thu muc]**

---

### Buoc 2: Tao docker-compose.yml (3 service)
```bash
nano docker-compose.yml
```
- Service **db**: MariaDB 11.2
- Service **phpmyadmin**: cong 8080
- Service **web**: Django build tu Dockerfile

> 📸 **[Chen anh noi dung docker-compose.yml]**

---

### Buoc 3: Tao Dockerfile
```bash
nano django_app/Dockerfile
```
> 📸 **[Chen anh noi dung Dockerfile]**

---

### Buoc 4: Tao requirements.txt
