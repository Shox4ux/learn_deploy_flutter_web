# Flutter Web ni Serverga Deploy Qilish (Nginx orqali)

Ushbu qo‘llanmada biz **Flutter Web build fayllarini serverga joylashtirib, Nginx orqali internetga chiqarishni** o‘rganamiz.

Bu bosqichda bizga faqat:

- Ubuntu server
- Nginx
- Flutter Web build fayllari

kerak bo‘ladi.

---

# 1. Serverni yangilash

Serverga ulanganingizdan keyin avval paketlarni yangilaymiz.

```bash
sudo apt update
sudo apt upgrade -y
```

---

# 2. Nginx o‘rnatish

Nginx — bu web server bo‘lib, u foydalanuvchilarga web sahifalarni uzatadi.

```bash
sudo apt install nginx -y
```

Nginx ishlayotganini tekshirish:

```bash
sudo systemctl status nginx
```

Agar ishlamayotgan bo‘lsa:

```bash
sudo systemctl start nginx
```

Server qayta ishga tushganda ham avtomatik ishlashi uchun:

```bash
sudo systemctl enable nginx
```

---

# 3. Web ilova uchun papka yaratish

Web fayllarni joylashtirish uchun `/var/www` ichida yangi papka yaratamiz.

```bash
sudo mkdir -p /var/www/flutter_web
```
Agar build fayllar serverda `/root/flutter_web` ichida bo‘lsa, ularni `/var/www/flutter_web` papkasiga ko‘chiramiz.

```bash
sudo cp -r /root/flutter_web/* /var/www/flutter_web/
```

---

Papka ruxsatlarini o‘zgartiramiz:

```bash
sudo chown -R $USER:$USER /var/www/flutter_web
```

---

# 4. Nginx konfiguratsiya fayli yaratish

Nginx uchun yangi konfiguratsiya fayli yaratamiz.

```bash
sudo nano /etc/nginx/sites-available/flutter_web
```

Ichiga quyidagi konfiguratsiyani yozing:

```nginx
server {
    listen 80;
    server_name _;

    root /var/www/flutter_web;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

---

# 5. Nginx konfiguratsiyani yoqish

Yaratilgan konfiguratsiyani `sites-enabled` papkaga ulaymiz.

```bash
sudo ln -s /etc/nginx/sites-available/flutter_web /etc/nginx/sites-enabled/
```

Standart konfiguratsiyani o‘chirish (ixtiyoriy):

```bash
sudo rm /etc/nginx/sites-enabled/default
```

---

# 6. Nginx konfiguratsiyasini tekshirish

```bash
sudo nginx -t
```

Agar hammasi to‘g‘ri bo‘lsa quyidagiga o‘xshash natija chiqadi:

```
syntax is ok
test is successful
```

---

# 7. Nginx ni qayta ishga tushirish

```bash
sudo systemctl restart nginx
```

---

# 8. Natijani tekshirish

Endi server IP manzilini brauzerda oching:

```
http://SERVER_IP:PORT
```

Agar hammasi to‘g‘ri bajarilgan bo‘lsa, **Flutter Web ilovangiz ochiladi.**

---

