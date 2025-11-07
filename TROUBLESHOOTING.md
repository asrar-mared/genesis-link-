# 🧯 TROUBLESHOOTING - دليل حل المشاكل

<div align="center">

**Genesis Link - نظام الدفاع الرقمي الجماعي**

[![Project Status](https://img.shields.io/badge/status-active-success.svg)](https://github.com/genesislink)
[![Support](https://img.shields.io/badge/support-community-blue.svg)](mailto:help@genesislink.io)

> 📘 **دليلك الأول لحل المشاكل قبل التواصل مع الفريق**  
> إذا واجهتك مشكلة، ابدأ من هنا - معظم الحلول جاهزة ومجربة ✅

</div>

---

## 📋 جدول المحتويات

- [🎯 من يستخدم هذا الملف؟](#-من-يستخدم-هذا-الملف)
- [⚡ المشاكل الشائعة والحلول السريعة](#-المشاكل-الشائعة-والحلول-السريعة)
  - [مشاكل التثبيت](#1️⃣-مشاكل-التثبيت)
  - [مشاكل Git و GitHub](#2️⃣-مشاكل-git-و-github)
  - [مشاكل GitHub Actions](#3️⃣-مشاكل-github-actions)
  - [مشاكل قواعد البيانات](#4️⃣-مشاكل-قواعد-البيانات)
  - [مشاكل الشبكة والاتصال](#5️⃣-مشاكل-الشبكة-والاتصال)
  - [مشاكل التوثيق والروابط](#6️⃣-مشاكل-التوثيق-والروابط)
- [🧪 أدوات التشخيص](#-أدوات-التشخيص)
- [🆘 متى تتواصل معنا؟](#-متى-تتواصل-معنا)
- [📚 موارد إضافية](#-موارد-إضافية)

---

## 🎯 من يستخدم هذا الملف؟

| الفئة | الاستخدام |
|-------|-----------|
| 🆕 **مستخدم جديد** | حل مشاكل التثبيت والإعداد الأولي |
| 💻 **مطور** | حل مشاكل البيئة التطويرية والـ Dependencies |
| 🤝 **مساهم** | حل مشاكل Git، Pull Requests، وسير العمل |
| 🔧 **مدير نظام** | حل مشاكل النشر والبنية التحتية |

---

## ⚡ المشاكل الشائعة والحلول السريعة

### 1️⃣ مشاكل التثبيت

<details>
<summary><strong>❌ المشكلة: ModuleNotFoundError أو ImportError</strong></summary>

**الرسالة:**
```
ModuleNotFoundError: No module named 'flask'
ImportError: cannot import name 'xyz'
```

**الأسباب المحتملة:**
- المكتبات غير مثبتة
- إصدار Python غير متوافق
- بيئة افتراضية غير مفعلة

**الحل:**

```bash
# 1. تأكد من إصدار Python (يجب أن يكون 3.8+)
python --version

# 2. فعّل البيئة الافتراضية
# على Windows:
venv\Scripts\activate
# على Linux/Mac:
source venv/bin/activate

# 3. ثبت جميع المتطلبات
pip install -r requirements.txt

# 4. تحقق من التثبيت
pip list
```

**إذا استمرت المشكلة:**
```bash
# احذف البيئة القديمة وأعد إنشاءها
rm -rf venv
python -m venv venv
source venv/bin/activate  # أو venv\Scripts\activate على Windows
pip install --upgrade pip
pip install -r requirements.txt
```

</details>

<details>
<summary><strong>❌ المشكلة: pip install تفشل مع خطأ Permission Denied</strong></summary>

**الرسالة:**
```
ERROR: Could not install packages due to an EnvironmentError: [Errno 13] Permission denied
```

**الحل:**

```bash
# استخدم --user لتثبيت في مجلد المستخدم
pip install --user -r requirements.txt

# أو استخدم sudo (Linux/Mac فقط - غير مفضل)
sudo pip install -r requirements.txt

# الحل الأفضل: استخدم بيئة افتراضية
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

</details>

<details>
<summary><strong>❌ المشكلة: command not found عند تشغيل python أو pip</strong></summary>

**الأسباب:**
- Python غير مثبت
- Python غير مضاف لـ PATH

**الحل:**

**على Windows:**
```powershell
# تحقق من التثبيت
where python
where pip

# إذا لم يكن مثبتًا، حمّله من:
# https://www.python.org/downloads/

# أضفه للـ PATH يدويًا من System Properties > Environment Variables
```

**على Linux:**
```bash
# ثبت Python
sudo apt update
sudo apt install python3 python3-pip python3-venv

# تأكد من الإصدار
python3 --version
```

**على Mac:**
```bash
# ثبت عبر Homebrew
brew install python3
```

</details>

---

### 2️⃣ مشاكل Git و GitHub

<details>
<summary><strong>❌ المشكلة: Permission denied (publickey)</strong></summary>

**الرسالة:**
```
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
```

**الحل:**

```bash
# 1. تحقق من وجود مفتاح SSH
ls -al ~/.ssh

# 2. أنشئ مفتاح SSH جديد إذا لزم الأمر
ssh-keygen -t ed25519 -C "your_email@example.com"

# 3. أضف المفتاح لـ ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 4. انسخ المفتاح العام
cat ~/.ssh/id_ed25519.pub

# 5. أضفه في GitHub:
# Settings > SSH and GPG keys > New SSH key
```

**البديل: استخدم HTTPS بدلًا من SSH**
```bash
git remote set-url origin https://github.com/username/genesis-link.git
```

</details>

<details>
<summary><strong>❌ المشكلة: fatal: refusing to merge unrelated histories</strong></summary>

**الحل:**
```bash
# السماح بدمج التواريخ غير المرتبطة
git pull origin main --allow-unrelated-histories

# ثم حل أي تعارضات يدويًا
git add .
git commit -m "Merge unrelated histories"
git push origin main
```

</details>

<details>
<summary><strong>❌ المشكلة: Your branch is behind 'origin/main'</strong></summary>

**الحل:**
```bash
# اسحب آخر التحديثات
git pull origin main

# أو إذا كنت تريد إعادة كتابة التاريخ (احذر!)
git pull --rebase origin main
```

</details>

<details>
<summary><strong>❌ المشكلة: Git conflict أثناء الـ merge</strong></summary>

**الحل:**
```bash
# 1. افتح الملفات المتعارضة وابحث عن:
# <<<<<<< HEAD
# your changes
# =======
# their changes
# >>>>>>> branch-name

# 2. حرر الملف يدويًا واحذف العلامات

# 3. أضف الملفات المعدلة
git add .

# 4. أكمل الـ merge
git commit -m "Resolve merge conflicts"
```

</details>

---

### 3️⃣ مشاكل GitHub Actions

<details>
<summary><strong>❌ المشكلة: Workflow تفشل عند Push</strong></summary>

**الرسالة:**
```
Error: Process completed with exit code 1
```

**الحل:**

```bash
# 1. افحص سجلات الـ Actions في GitHub
# Actions tab > اختر الـ workflow الفاشل > انقر على الوظيفة الحمراء

# 2. المشاكل الشائعة:

# أ. ملف YAML به أخطاء صياغة
# تحقق من المسافات والبنية في .github/workflows/

# ب. متغيرات البيئة مفقودة
# أضفها في: Settings > Secrets and variables > Actions

# ج. الصلاحيات غير كافية
# Settings > Actions > General > Workflow permissions
# اختر "Read and write permissions"
```

**مثال على إصلاح ملف workflow:**
```yaml
name: CI Pipeline
on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
      
      - name: Run tests
        run: |
          pytest tests/
```

</details>

<details>
<summary><strong>❌ المشكلة: Secret غير متاح في Workflow</strong></summary>

**الحل:**
```yaml
# تأكد من إضافة السر في Settings > Secrets
# ثم استخدمه هكذا:

env:
  API_KEY: ${{ secrets.API_KEY }}
  
# وليس:
env:
  API_KEY: $API_KEY  # ❌ خطأ
```

</details>

---

### 4️⃣ مشاكل قواعد البيانات

<details>
<summary><strong>❌ المشكلة: ECONNREFUSED أو Connection refused</strong></summary>

**الرسالة:**
```
Error: connect ECONNREFUSED 127.0.0.1:27017
MongoNetworkError: failed to connect to server
```

**الأسباب:**
- قاعدة البيانات غير شغالة
- عنوان الاتصال خاطئ
- Firewall يحجب الاتصال

**الحل:**

**MongoDB:**
```bash
# تحقق من تشغيل MongoDB
# على Linux:
sudo systemctl status mongod
sudo systemctl start mongod

# على Mac:
brew services start mongodb-community

# على Windows:
net start MongoDB
```

**PostgreSQL:**
```bash
# على Linux:
sudo systemctl status postgresql
sudo systemctl start postgresql

# على Mac:
brew services start postgresql
```

**تحقق من المتغيرات البيئية:**
```bash
# أنشئ ملف .env
echo "DATABASE_URL=mongodb://localhost:27017/genesis_link" > .env
```

</details>

<details>
<summary><strong>❌ المشكلة: Authentication failed</strong></summary>

**الحل:**
```bash
# تأكد من بيانات الاعتماد في .env
DATABASE_URL=mongodb://username:password@localhost:27017/dbname

# أو إذا كنت تستخدم قاعدة بيانات محلية بدون مصادقة:
DATABASE_URL=mongodb://localhost:27017/genesis_link
```

</details>

---

### 5️⃣ مشاكل الشبكة والاتصال

<details>
<summary><strong>❌ المشكلة: Timeout أو Network error</strong></summary>

**الحل:**
```bash
# 1. تحقق من الاتصال بالإنترنت
ping google.com

# 2. تحقق من DNS
nslookup github.com

# 3. تحقق من Proxy/VPN
# عطّل الـ VPN مؤقتًا أو أضف إعدادات Proxy:

git config --global http.proxy http://proxy.example.com:8080
git config --global https.proxy https://proxy.example.com:8080

# لإلغاء الـ proxy:
git config --global --unset http.proxy
git config --global --unset https.proxy
```

</details>

<details>
<summary><strong>❌ المشكلة: SSL Certificate problem</strong></summary>

**الرسالة:**
```
SSL certificate problem: unable to get local issuer certificate
```

**الحل المؤقت (غير آمن للإنتاج!):**
```bash
git config --global http.sslVerify false
```

**الحل الصحيح:**
```bash
# حدّث الشهادات
# على Ubuntu/Debian:
sudo apt update
sudo apt install ca-certificates

# على Mac:
brew install curl-ca-bundle
```

</details>

---

### 6️⃣ مشاكل التوثيق والروابط

<details>
<summary><strong>❌ المشكلة: روابط لا تعمل في README</strong></summary>

**الأسباب:**
- مسارات نسبية خاطئة
- ملفات محذوفة أو منقولة

**الحل:**
```markdown
<!-- استخدم مسارات نسبية صحيحة -->

<!-- ✅ صحيح -->
[Contributing Guide](CONTRIBUTING.md)
[API Docs](docs/API.md)

<!-- ❌ خطأ -->
[Contributing Guide](/CONTRIBUTING.md)
[API Docs](docs/api.md)  # حساس لحالة الأحرف!
```

</details>

---

## 🧪 أدوات التشخيص

### فحص البيئة

```bash
# فحص شامل للنظام
echo "=== System Info ==="
uname -a
python --version
pip --version
git --version

echo "=== Installed Packages ==="
pip list

echo "=== Git Configuration ==="
git config --list

echo "=== Environment Variables ==="
printenv | grep -i genesis

echo "=== Network Test ==="
ping -c 4 github.com
```

### سكريبت تشخيص تلقائي

```bash
#!/bin/bash
# save as: diagnose.sh

echo "🔍 Genesis Link - Diagnostic Tool"
echo "=================================="

# Check Python
if command -v python3 &> /dev/null; then
    echo "✅ Python: $(python3 --version)"
else
    echo "❌ Python: Not found"
fi

# Check pip
if command -v pip3 &> /dev/null; then
    echo "✅ pip: $(pip3 --version)"
else
    echo "❌ pip: Not found"
fi

# Check Git
if command -v git &> /dev/null; then
    echo "✅ Git: $(git --version)"
else
    echo "❌ Git: Not found"
fi

# Check virtual environment
if [ -d "venv" ]; then
    echo "✅ Virtual environment: Found"
else
    echo "⚠️  Virtual environment: Not found"
fi

# Check requirements
if [ -f "requirements.txt" ]; then
    echo "✅ requirements.txt: Found"
else
    echo "❌ requirements.txt: Not found"
fi

echo "=================================="
echo "📊 Diagnostic complete!"
```

**استخدام:**
```bash
chmod +x diagnose.sh
./diagnose.sh
```

---

## 🆘 متى تتواصل معنا؟

جرّب الحلول أعلاه أولًا. إذا استمرت المشكلة:

### 📝 افتح Issue جديد

<div align="center">

[![Open Issue](https://img.shields.io/badge/Open-Issue-red.svg?style=for-the-badge)](https://github.com/genesislink/genesis-link/issues/new)

</div>

**يُرجى تضمين:**
- ✅ وصف واضح للمشكلة
- ✅ خطوات إعادة إنتاج المشكلة
- ✅ رسائل الخطأ كاملة
- ✅ نظام التشغيل وإصدار Python
- ✅ ما جربته من حلول

**قالب Issue مقترح:**
```markdown
## 🐛 وصف المشكلة
[وصف واضح]

## 📋 خطوات إعادة الإنتاج
1. افتح...
2. اضغط على...
3. لاحظ الخطأ...

## 💻 البيئة
- OS: [e.g. Ubuntu 22.04]
- Python: [e.g. 3.10.5]
- Commit: [e.g. abc123]

## 📸 لقطات الشاشة
[إن وجدت]

## ✅ ما جربته
- [ ] حل 1
- [ ] حل 2
```

### 📧 تواصل مباشر

| القناة | الاستخدام | الرد |
|--------|-----------|------|
| 📧 **Email** | help@genesislink.io | 24-48 ساعة |
| 💬 **Discord** | [انضم للمجتمع](#) | فوري |
| 🐦 **Twitter** | [@GenesisLinkDev](#) | يوم واحد |

---

## 📚 موارد إضافية

### وثائق المشروع
- 📖 [README الرئيسي](README.md)
- 🤝 [دليل المساهمة](CONTRIBUTING.md)
- 🗺️ [خارطة الطريق](ROADMAP.md)
- 🔒 [سياسة الأمان](SECURITY.md)
- 📋 [سجل التغييرات](CHANGELOG.md)

### موارد خارجية
- 🐍 [Python Docs](https://docs.python.org/)
- 🐙 [GitHub Docs](https://docs.github.com/)
- 📦 [pip Docs](https://pip.pypa.io/)
- 🔐 [Git SSH Setup](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)

---

<div align="center">

**🛡️ Genesis Link - لأن الأمن السيبراني مسؤولية جماعية**

[![Made with ❤️](https://img.shields.io/badge/Made%20with-❤️-red.svg)](https://github.com/genesislink)
[![Community Driven](https://img.shields.io/badge/Community-Driven-blue.svg)](CONTRIBUTING.md)

**⚔️ نحن لا نحمي الكود فقط، نحن نحمي الحلم الرقمي بأكمله**

[🏠 العودة للرئيسية](README.md) • [🤝 ساهم معنا](CONTRIBUTING.md) • [📬 تواصل معنا](mailto:help@genesislink.io)

</div>
