# 📦 INSTALLATION GUIDE - دليل التثبيت الشامل

<div align="center">

**Genesis Link - نظام الدفاع الرقمي الجماعي**

[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/genesislink)
[![Python](https://img.shields.io/badge/python-3.8%2B-brightgreen.svg)](https://python.org)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

> 🚀 **دليل تثبيت خطوة بخطوة لجميع أنظمة التشغيل**  
> من الصفر إلى الإطلاق في أقل من 15 دقيقة ⏱️

</div>

---

## 📋 جدول المحتويات

- [✅ المتطلبات الأساسية](#-المتطلبات-الأساسية)
- [🖥️ التثبيت حسب نظام التشغيل](#️-التثبيت-حسب-نظام-التشغيل)
  - [Windows](#-windows)
  - [macOS](#-macos)
  - [Linux (Ubuntu/Debian)](#-linux-ubuntudebian)
  - [Linux (Fedora/RHEL)](#-linux-fedorarhel)
- [🐳 التثبيت عبر Docker](#-التثبيت-عبر-docker)
- [☁️ النشر على السحابة](#️-النشر-على-السحابة)
- [🧪 التحقق من التثبيت](#-التحقق-من-التثبيت)
- [🔧 الإعدادات المتقدمة](#-الإعدادات-المتقدمة)
- [❓ حل المشاكل](#-حل-المشاكل)

---

## ✅ المتطلبات الأساسية

### 📊 جدول المتطلبات

| المكون | الإصدار المطلوب | التحقق | التثبيت |
|--------|-----------------|---------|---------|
| **Python** | 3.8 أو أحدث | `python --version` | [python.org](https://python.org) |
| **pip** | 21.0+ | `pip --version` | يأتي مع Python |
| **Git** | 2.30+ | `git --version` | [git-scm.com](https://git-scm.com) |
| **Node.js** *(اختياري)* | 16.0+ | `node --version` | [nodejs.org](https://nodejs.org) |
| **MongoDB** *(اختياري)* | 5.0+ | `mongod --version` | [mongodb.com](https://mongodb.com) |

### 🔍 فحص سريع للمتطلبات

```bash
# نفذ هذا السكريبت للتحقق من جميع المتطلبات
curl -fsSL https://raw.githubusercontent.com/genesislink/genesis-link/main/scripts/check-requirements.sh | bash
```

**أو يدويًا:**

```bash
echo "🔍 Checking Prerequisites..."
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━"
python --version 2>&1 | grep -q "Python 3.[8-9]\|Python 3.1[0-9]" && echo "✅ Python: OK" || echo "❌ Python: Missing or old version"
pip --version && echo "✅ pip: OK" || echo "❌ pip: Missing"
git --version && echo "✅ Git: OK" || echo "❌ Git: Missing"
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━"
```

---

## 🖥️ التثبيت حسب نظام التشغيل

---

## 🪟 Windows

### الطريقة 1️⃣: التثبيت التفاعلي (مُوصى به للمبتدئين)

#### 1. تثبيت Python

```powershell
# حمّل Python من الموقع الرسمي
# https://www.python.org/downloads/

# أثناء التثبيت، تأكد من تفعيل:
☑️ Add Python to PATH
☑️ Install pip
```

**أو عبر Chocolatey:**
```powershell
# ثبت Chocolatey أولاً (إذا لم يكن مثبتًا)
Set-ExecutionPolicy Bypass -Scope Process -Force
[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072
iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

# ثم ثبت Python
choco install python -y
```

#### 2. تثبيت Git

```powershell
# عبر Chocolatey
choco install git -y

# أو حمّل من:
# https://git-scm.com/download/win
```

#### 3. استنساخ المشروع

```powershell
# افتح PowerShell أو Command Prompt
cd C:\Projects
git clone https://github.com/genesislink/genesis-link.git
cd genesis-link
```

#### 4. إنشاء بيئة افتراضية

```powershell
# إنشاء البيئة
python -m venv venv

# تفعيل البيئة
.\venv\Scripts\activate

# يجب أن ترى (venv) في بداية السطر
```

#### 5. تثبيت المكتبات

```powershell
# تحديث pip أولاً
python -m pip install --upgrade pip

# تثبيت المتطلبات
pip install -r requirements.txt

# تثبيت المتطلبات الإضافية للتطوير (اختياري)
pip install -r requirements-dev.txt
```

#### 6. إعداد ملف البيئة

```powershell
# نسخ ملف القالب
copy .env.example .env

# حرر الملف
notepad .env
```

**محتوى .env:**
```env
# إعدادات التطبيق
APP_ENV=development
DEBUG=True
SECRET_KEY=your-secret-key-here-change-in-production

# قاعدة البيانات (اختياري)
DATABASE_URL=mongodb://localhost:27017/genesis_link

# API Keys (إن وجدت)
API_KEY=your-api-key
GITHUB_TOKEN=your-github-token
```

#### 7. تشغيل المشروع

```powershell
# تشغيل الخادم التطويري
python app.py

# أو عبر Flask
flask run

# يجب أن تشاهد:
# * Running on http://127.0.0.1:5000
```

#### 8. افتح المتصفح

```
http://localhost:5000
```

---

### الطريقة 2️⃣: التثبيت السريع (سكريبت واحد)

```powershell
# حمّل وشغل سكريبت التثبيت التلقائي
irm https://raw.githubusercontent.com/genesislink/genesis-link/main/scripts/install-windows.ps1 | iex
```

---

## 🍎 macOS

### الطريقة 1️⃣: عبر Homebrew (مُوصى به)

#### 1. تثبيت Homebrew (إذا لم يكن مثبتًا)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

#### 2. تثبيت المتطلبات

```bash
# تثبيت Python و Git
brew install python@3.11 git

# تحديث pip
python3 -m pip install --upgrade pip
```

#### 3. استنساخ المشروع

```bash
cd ~/Projects
git clone https://github.com/genesislink/genesis-link.git
cd genesis-link
```

#### 4. إنشاء بيئة افتراضية

```bash
# إنشاء البيئة
python3 -m venv venv

# تفعيل البيئة
source venv/bin/activate

# يجب أن ترى (venv) في بداية السطر
```

#### 5. تثبيت المكتبات

```bash
# تحديث pip
pip install --upgrade pip

# تثبيت المتطلبات
pip install -r requirements.txt

# تثبيت متطلبات التطوير (اختياري)
pip install -r requirements-dev.txt
```

#### 6. إعداد البيئة

```bash
# نسخ ملف القالب
cp .env.example .env

# حرر الملف
nano .env
# أو
vim .env
# أو
open -a TextEdit .env
```

#### 7. تشغيل المشروع

```bash
# تشغيل الخادم
python app.py

# أو
flask run

# افتح المتصفح على:
# http://localhost:5000
```

---

### الطريقة 2️⃣: التثبيت السريع

```bash
# سكريبت تثبيت واحد
curl -fsSL https://raw.githubusercontent.com/genesislink/genesis-link/main/scripts/install-macos.sh | bash
```

---

## 🐧 Linux (Ubuntu/Debian)

### التثبيت الكامل خطوة بخطوة

#### 1. تحديث النظام

```bash
sudo apt update && sudo apt upgrade -y
```

#### 2. تثبيت المتطلبات الأساسية

```bash
# تثبيت Python و pip و Git
sudo apt install -y python3 python3-pip python3-venv git curl wget

# تثبيت أدوات التطوير (اختياري)
sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
```

#### 3. التحقق من الإصدارات

```bash
python3 --version  # يجب أن يكون 3.8+
pip3 --version
git --version
```

#### 4. استنساخ المشروع

```bash
cd ~/projects
git clone https://github.com/genesislink/genesis-link.git
cd genesis-link
```

#### 5. إنشاء بيئة افتراضية

```bash
# إنشاء البيئة
python3 -m venv venv

# تفعيل البيئة
source venv/bin/activate

# تأكد من التفعيل (يجب أن ترى (venv))
```

#### 6. تثبيت المكتبات

```bash
# تحديث pip
pip install --upgrade pip setuptools wheel

# تثبيت المتطلبات الأساسية
pip install -r requirements.txt

# تثبيت متطلبات التطوير (اختياري)
pip install -r requirements-dev.txt
```

#### 7. إعداد قاعدة البيانات (اختياري)

**MongoDB:**
```bash
# تثبيت MongoDB
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
sudo apt update
sudo apt install -y mongodb-org

# تشغيل MongoDB
sudo systemctl start mongod
sudo systemctl enable mongod

# التحقق من التشغيل
sudo systemctl status mongod
```

**PostgreSQL:**
```bash
# تثبيت PostgreSQL
sudo apt install -y postgresql postgresql-contrib

# تشغيل الخدمة
sudo systemctl start postgresql
sudo systemctl enable postgresql

# إنشاء قاعدة بيانات
sudo -u postgres createuser --interactive
sudo -u postgres createdb genesis_link
```

#### 8. إعداد ملف البيئة

```bash
# نسخ القالب
cp .env.example .env

# تحرير الملف
nano .env
```

**مثال على .env:**
```env
APP_ENV=development
DEBUG=True
SECRET_KEY=$(python3 -c 'import secrets; print(secrets.token_hex(32))')

# MongoDB
DATABASE_URL=mongodb://localhost:27017/genesis_link

# PostgreSQL
# DATABASE_URL=postgresql://user:password@localhost/genesis_link

# الإعدادات الأخرى
FLASK_APP=app.py
FLASK_ENV=development
PORT=5000
```

#### 9. تشغيل المشروع

```bash
# الطريقة 1: مباشرة
python app.py

# الطريقة 2: عبر Flask
flask run

# الطريقة 3: مع إعادة التشغيل التلقائي
flask run --reload

# الطريقة 4: على منفذ مخصص
flask run --port=8000

# يجب أن تشاهد:
# * Serving Flask app 'app.py'
# * Running on http://127.0.0.1:5000
```

#### 10. اختبار الاتصال

```bash
# من terminal آخر
curl http://localhost:5000

# أو
wget -qO- http://localhost:5000
```

---

### ⚡ التثبيت السريع (سكريبت واحد)

```bash
curl -fsSL https://raw.githubusercontent.com/genesislink/genesis-link/main/scripts/install-linux.sh | bash
```

---

## 🎩 Linux (Fedora/RHEL)

### التثبيت الكامل

```bash
# 1. تحديث النظام
sudo dnf update -y

# 2. تثبيت المتطلبات
sudo dnf install -y python3 python3-pip python3-virtualenv git

# 3. استنساخ المشروع
cd ~/projects
git clone https://github.com/genesislink/genesis-link.git
cd genesis-link

# 4. إنشاء البيئة الافتراضية
python3 -m venv venv
source venv/bin/activate

# 5. تثبيت المكتبات
pip install --upgrade pip
pip install -r requirements.txt

# 6. إعداد البيئة
cp .env.example .env
nano .env

# 7. تشغيل المشروع
python app.py
```

---

## 🐳 التثبيت عبر Docker

### المتطلبات
- Docker 20.10+
- Docker Compose 2.0+

### الطريقة 1️⃣: Docker Compose (مُوصى به)

#### 1. استنساخ المشروع

```bash
git clone https://github.com/genesislink/genesis-link.git
cd genesis-link
```

#### 2. إنشاء ملف docker-compose.yml

```yaml
version: '3.8'

services:
  app:
    build: .
    container_name: genesis-link-app
    ports:
      - "5000:5000"
    environment:
      - APP_ENV=production
      - DATABASE_URL=mongodb://mongo:27017/genesis_link
    volumes:
      - .:/app
      - /app/venv
    depends_on:
      - mongo
    restart: unless-stopped
    networks:
      - genesis-network

  mongo:
    image: mongo:6.0
    container_name: genesis-link-db
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db
    environment:
      - MONGO_INITDB_DATABASE=genesis_link
    restart: unless-stopped
    networks:
      - genesis-network

  nginx:
    image: nginx:alpine
    container_name: genesis-link-nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./ssl:/etc/nginx/ssl:ro
    depends_on:
      - app
    restart: unless-stopped
    networks:
      - genesis-network

volumes:
  mongo-data:

networks:
  genesis-network:
    driver: bridge
```

#### 3. إنشاء Dockerfile

```dockerfile
FROM python:3.11-slim

# تعيين متغيرات البيئة
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1 \
    PIP_NO_CACHE_DIR=1

# تعيين مجلد العمل
WORKDIR /app

# تثبيت المتطلبات الأساسية
RUN apt-get update && apt-get install -y \
    gcc \
    git \
    && rm -rf /var/lib/apt/lists/*

# نسخ ملفات المتطلبات
COPY requirements.txt .

# تثبيت المكتبات
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# نسخ كود المشروع
COPY . .

# إنشاء مستخدم غير جذري
RUN useradd -m -u 1000 genesis && \
    chown -R genesis:genesis /app

USER genesis

# تعريف المنفذ
EXPOSE 5000

# نقطة الدخول
CMD ["gunicorn", "--bind", "0.0.0.0:5000", "--workers", "4", "app:app"]
```

#### 4. بناء وتشغيل الحاويات

```bash
# بناء الصور
docker-compose build

# تشغيل الخدمات
docker-compose up -d

# مشاهدة السجلات
docker-compose logs -f

# إيقاف الخدمات
docker-compose down

# إيقاف وحذف البيانات
docker-compose down -v
```

#### 5. الوصول للتطبيق

```
http://localhost:5000
```

---

### الطريقة 2️⃣: Docker مباشر

```bash
# بناء الصورة
docker build -t genesis-link:latest .

# تشغيل الحاوية
docker run -d \
  --name genesis-link \
  -p 5000:5000 \
  -e APP_ENV=production \
  -e DATABASE_URL=mongodb://host.docker.internal:27017/genesis_link \
  genesis-link:latest

# مشاهدة السجلات
docker logs -f genesis-link

# إيقاف الحاوية
docker stop genesis-link

# إزالة الحاوية
docker rm genesis-link
```

---

## ☁️ النشر على السحابة

### 🚀 Heroku

```bash
# 1. تسجيل الدخول
heroku login

# 2. إنشاء تطبيق
heroku create genesis-link-app

# 3. إضافة قاعدة بيانات
heroku addons:create mongolab:sandbox

# 4. تعيين متغيرات البيئة
heroku config:set APP_ENV=production
heroku config:set SECRET_KEY=$(openssl rand -hex 32)

# 5. النشر
git push heroku main

# 6. فتح التطبيق
heroku open
```

---

### ☁️ AWS (EC2)

```bash
# 1. الاتصال بالخادم
ssh -i your-key.pem ubuntu@your-ec2-ip

# 2. تحديث النظام
sudo apt update && sudo apt upgrade -y

# 3. تثبيت المتطلبات
sudo apt install -y python3-pip python3-venv git nginx

# 4. استنساخ المشروع
cd /var/www
sudo git clone https://github.com/genesislink/genesis-link.git
cd genesis-link

# 5. إعداد البيئة
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
pip install gunicorn

# 6. إنشاء خدمة systemd
sudo nano /etc/systemd/system/genesis-link.service
```

**محتوى الخدمة:**
```ini
[Unit]
Description=Genesis Link Application
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/var/www/genesis-link
Environment="PATH=/var/www/genesis-link/venv/bin"
ExecStart=/var/www/genesis-link/venv/bin/gunicorn --workers 3 --bind 127.0.0.1:5000 app:app
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
# 7. تفعيل وتشغيل الخدمة
sudo systemctl enable genesis-link
sudo systemctl start genesis-link

# 8. إعداد Nginx
sudo nano /etc/nginx/sites-available/genesis-link
```

**إعداد Nginx:**
```nginx
server {
    listen 80;
    server_name your-domain.com;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}
```

```bash
# 9. تفعيل الإعداد
sudo ln -s /etc/nginx/sites-available/genesis-link /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

---

### 🔷 DigitalOcean

```bash
# استخدم نفس خطوات AWS EC2
# أو استخدم App Platform:

# 1. في لوحة تحكم DigitalOcean
# 2. Apps > Create App
# 3. اختر GitHub repo
# 4. حدد إعدادات البيئة
# 5. Deploy!
```

---

## 🧪 التحقق من التثبيت

### ✅ سكريبت تحقق شامل

```bash
#!/bin/bash
# save as: verify-installation.sh

echo "🔍 Genesis Link - Installation Verification"
echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"

# Check Python
if python --version &> /dev/null; then
    echo "✅ Python installed: $(python --version)"
else
    echo "❌ Python not found"
    exit 1
fi

# Check virtual environment
if [ -d "venv" ]; then
    echo "✅ Virtual environment exists"
    
    # Activate and check packages
    source venv/bin/activate 2>/dev/null || . venv/Scripts/activate 2>/dev/null
    
    if [ $? -eq 0 ]; then
        echo "✅ Virtual environment activated"
        
        # Check installed packages
        required_packages=("flask" "pymongo" "requests")
        for package in "${required_packages[@]}"; do
            if pip show $package &> /dev/null; then
                echo "✅ Package installed: $package"
            else
                echo "⚠️  Package missing: $package"
            fi
        done
    else
        echo "❌ Failed to activate virtual environment"
    fi
else
    echo "❌ Virtual environment not found"
fi

# Check .env file
if [ -f ".env" ]; then
    echo "✅ .env file exists"
else
    echo "⚠️  .env file not found (copy from .env.example)"
fi

# Check if server runs
echo ""
echo "🚀 Testing server startup..."
timeout 5 python app.py &> /dev/null &
sleep 3

if curl -s http://localhost:5000 &> /dev/null; then
    echo "✅ Server is running and accessible"
    pkill -f "python app.py"
else
    echo "⚠️  Server test failed (this might be normal if port is in use)"
fi

echo "━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"
echo "✨ Verification complete!"
```

**تشغيل:**
```bash
chmod +x verify-installation.sh
./verify-installation.sh
```

---

## 🔧 الإعدادات المتقدمة

### 🔐 إعداد SSL/TLS (HTTPS)

#### باستخدام Let's Encrypt (Certbot)

```bash
# تثبيت Certbot
sudo apt install -y certbot python3-certbot-nginx

# الحصول على شهادة
sudo certbot --nginx -d your-domain.com -d www.your-domain.com

# التجديد التلقائي
sudo certbot renew --dry-run
```

---

### ⚡ إعداد Redis للتخزين المؤقت

```bash
# تثبيت Redis
sudo apt install -y redis-server

# تشغيل Redis
sudo systemctl start redis
sudo systemctl enable redis

# التحقق
redis-cli ping  # يجب أن يرد: PONG
```

**إضافة في .env:**
```env
REDIS_URL=redis://localhost:6379/0
CACHE_TYPE=redis
```

---

### 📊 إعداد Monitoring

#### باستخدام Prometheus + Grafana

```yaml
# في docker-compose.yml أضف:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
    networks:
      - genesis-network

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    networks:
      - genesis-network
```

---

## ❓ حل المشاكل

### 🚨 مشاكل شائعة

<details>
<summary><strong>المشكلة: Port 5000 already in use</strong></summary>

**الحل:**
```bash
# ابحث عن العملية المستخدمة للمنفذ
# Linux/Mac:
lsof -i :5000
kill -9 <PID>

# Windows:
netstat -ano | findstr :5000
taskkill /PID <PID> /F

# أو غيّر المنفذ
flask run --port=8000
```
</details>

<details>
<summary><strong>المشكلة: pip install تفشل</strong></summary>

**الحل:**
```bash
# تحديث pip
python -m pip install --upgrade pip

# تثبيت باستخدام --user
pip install --user -r requirements.txt

# تخطي الأخطاء
pip install -r requirements.txt --no-deps
```
</details>

<details>
<summary><strong>المشكلة: Database connection failed</strong></summary>

**الحل:**
```bash
# تأكد من تشغيل قاعدة البيانات
sudo systemctl status mongod

# تحقق من الاتصال
mongo --eval "db.adminCommand('ping')"

# تحقق من .env
cat .env | grep DATABASE_URL
```
</details>

**للمزيد من الحلول:**  
👉 راجع [TROUBLESHOOTING.md](TROUBLESHOOTING.md)

---

## 📚 الخطوات التالية

بعد التثبيت الناجح:

1. ✅ **اقرأ التوثيق:**
   - [README.md](README.md) - نظرة عامة
   - [CONTRIBUTING.md](CONTRIBUTING.md) - دليل المساهمة
   - [API.md](docs/API.md) - توثيق الـ API

2. 🧪 **شغّل الاختبارات:**
   ```bash
   pytest tests/
   ```

3. 🚀 **ابدأ التطوير:**
   ```bash
   # أنشئ فرع جديد
   git checkout -b feature/my-feature
   
   # اعمل على ميزتك
   # ...
   
   # ارفع التغييرات
   git push origin feature/my-feature
   ```

4. 🤝 **انضم للمجتمع:**
   - 💬 [Discord Server](#)
   - 🐦 [Twitter](#)
   - 📧 [Mailing List](#)

---

<div align="center">

**🛡️ Genesis Link - لأن الأمن السيبراني مسؤولية جماعية**

[![GitHub](https://img.shields.io/badge/GitHub-Genesis--Link-black.svg?logo=github)](https://github.com/genesislink)
[![Documentation](https://img.shields.io/badge/Docs-Read%20Now-blue.svg)](README.md)
[![Community](https://img.shields.io/badge/Community-Join%20Us-green.svg)](CONTRIBUTING.md)

**⚔️ نحن لا نثبّت برمجيات فقط، نحن نبني حصون رقمية**

[
