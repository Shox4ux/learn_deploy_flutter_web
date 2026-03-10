# learn_deploy_flutter_web

# Yangi Ubuntu Serverni Tayyorlash (Git + Docker + Nginx)

Ushbu qo‘llanma yangi Ubuntu serverni **deployment uchun tayyorlash**ni ko‘rsatadi.  
Natijada serverda quyidagilar o‘rnatiladi:

- Git
- Docker
- Docker Compose
- Nginx

---

# 1. Serverni yangilash

Serverdagi paketlar ro‘yxatini yangilaymiz va barcha paketlarni upgrade qilamiz.

```bash
sudo apt update
sudo apt upgrade -y
```

Keraksiz paketlarni tozalash:

```bash
sudo apt autoremove -y
```

---

# 2. Git o‘rnatish

Git kodlarni repositorydan yuklab olish uchun kerak bo‘ladi.

```bash
sudo apt install git -y
```

Git o‘rnatilganini tekshirish:

```bash
git --version
```

---

# 3. Docker uchun kerakli paketlarni o‘rnatish

```bash
sudo apt install \
ca-certificates \
curl \
gnupg \
lsb-release -y
```

---

# 4. Docker GPG kalitini qo‘shish

```bash
sudo mkdir -p /etc/apt/keyrings
```

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

---

# 5. Docker repository qo‘shish

```bash
echo \
"deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

# 6. Paketlar ro‘yxatini yana yangilash

```bash
sudo apt update
```

---

# 7. Docker o‘rnatish

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

Docker versiyasini tekshirish:

```bash
docker --version
```

---

# 8. Docker ni sudo siz ishlatish

Userni docker guruhiga qo‘shamiz:

```bash
sudo usermod -aG docker $USER
```

O‘zgarishni qo‘llash:

```bash
newgrp docker
```

Docker ishlayotganini tekshirish:

```bash
docker run hello-world
```

---

# 9. Docker Compose tekshirish

Ko‘pchilik yangi Docker versiyalarida Compose ichida bo‘ladi.

```bash
docker compose version
```

---

# 10. Nginx o‘rnatish

Nginx — bu web server bo‘lib, Flutter Web buildni foydalanuvchilarga uzatish uchun ishlatiladi.

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

Server yuklanganda avtomatik ishga tushishi uchun:

```bash
sudo systemctl enable nginx
```

---

# 11. Nginx firewall ruxsatlari (agar UFW ishlatilsa)

```bash
sudo ufw allow 'Nginx Full'
```

Firewall statusini tekshirish:

```bash
sudo ufw status
```

---

# 12. Foydali Docker buyruqlari

Ishlayotgan containerlarni ko‘rish:

```bash
docker ps
```

Barcha containerlarni ko‘rish:

```bash
docker ps -a
```

Containerni to‘xtatish:

```bash
docker stop CONTAINER_ID
```

Containerni o‘chirish:

```bash
docker rm CONTAINER_ID
```

---

# Server tayyor

Endi siz serverda quyidagilarni qila olasiz:

- Git orqali loyihalarni yuklab olish
- Docker orqali backend xizmatlarini ishga tushirish
- Nginx orqali Flutter Web ilovasini deploy qilish
