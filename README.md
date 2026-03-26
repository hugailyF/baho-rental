# دليل نشر نظام إدارة العقارات — بهو المدينة العقارية
## الإصدار 5.0 السحابي

---

## ملخص المشروع

هذا النظام السحابي يتيح:
- ✅ تسجيل دخول بالبريد الإلكتروني وكلمة المرور
- ✅ تخزين سحابي مشترك بين المستخدمين (Firebase Firestore)
- ✅ يعمل كتطبيق PWA (أيقونة على الجوال وسطح المكتب)
- ✅ يعمل بدون إنترنت (Offline Mode)
- ✅ جميع المراحل الأربع

---

## الخطوة 1: إنشاء مشروع Firebase (مجاني)

1. افتح https://console.firebase.google.com
2. سجّل دخول بحساب Google
3. اضغط "إنشاء مشروع" (Create project)
4. سمّه مثلاً: `baho-rental`
5. أوقف Google Analytics (غير ضروري) → اضغط "إنشاء المشروع"

### تفعيل Authentication:
1. من القائمة اليسرى اختر "Authentication"
2. اضغط "البدء" (Get started)
3. فعّل "البريد الإلكتروني/كلمة المرور" (Email/Password)

### تفعيل Firestore:
1. من القائمة اليسرى اختر "Firestore Database"
2. اضغط "إنشاء قاعدة بيانات" (Create database)
3. اختر الموقع: `europe-west1` (الأقرب للسعودية)
4. اختر "وضع الاختبار" (Start in test mode)

### الحصول على بيانات الإعداد:
1. اضغط ⚙️ إعدادات المشروع (Project settings)
2. انزل لقسم "تطبيقاتك" → اضغط أيقونة الويب `</>`
3. سمّه: `baho-web`
4. انسخ البيانات التالية:
```
apiKey: "xxxxxxxxxxxxxxxxxxxxxxxx"
authDomain: "baho-rental.firebaseapp.com"
projectId: "baho-rental"
storageBucket: "baho-rental.appspot.com"
messagingSenderId: "xxxxxxxxxxxx"
appId: "x:xxxxxxxxxxxx:web:xxxxxxxxxxxx"
```

### إدخال البيانات في النظام:
1. افتح ملف `index.html` بأي محرر نصوص
2. ابحث عن `FIREBASE_CONFIG`
3. استبدل `YOUR_API_KEY` و `YOUR_PROJECT_ID` إلخ بالبيانات الحقيقية

---

## الخطوة 2: نشر على GitHub Pages (مجاني)

### إنشاء حساب GitHub:
1. افتح https://github.com وسجّل حساب جديد (مجاني)

### إنشاء مستودع:
1. اضغط "New repository"
2. سمّه: `baho-rental`
3. اجعله Public
4. اضغط "Create repository"

### رفع الملفات:
1. اضغط "uploading an existing file"
2. ارفع الملفات الثلاثة:
   - `index.html`
   - `manifest.json`
   - `sw.js`
3. اضغط "Commit changes"

### تفعيل GitHub Pages:
1. اذهب لـ Settings → Pages
2. في Source اختر "main" branch
3. اضغط "Save"
4. بعد دقيقة يظهر الرابط: `https://اسمك.github.io/baho-rental/`

---

## الخطوة 3: تثبيت كتطبيق PWA

### على الجوال (Android):
1. افتح الرابط في Chrome
2. اضغط ⋮ → "إضافة إلى الشاشة الرئيسية"

### على الجوال (iPhone):
1. افتح الرابط في Safari
2. اضغط زر المشاركة ⬆️ → "إضافة إلى الشاشة الرئيسية"

### على الكمبيوتر:
1. افتح الرابط في Chrome
2. اضغط أيقونة التثبيت في شريط العنوان
3. أو: ⋮ → "تثبيت التطبيق"

---

## ملاحظات مهمة

- **Firebase مجاني** للاستخدام الشخصي والمشاريع الصغيرة (حتى 50,000 قراءة/يوم)
- **النظام يعمل بدون Firebase** في الوضع المحلي (localStorage)
- **النسخ الاحتياطي**: استخدم زر "تصدير JSON" بانتظام
- **الأمان**: بعد الانتهاء من الاختبار، عدّل قواعد Firestore:
  ```
  rules_version = '2';
  service cloud.firestore {
    match /databases/{database}/documents {
      match /tenants_data/{userId} {
        allow read, write: if request.auth != null && request.auth.uid == userId;
      }
    }
  }
  ```
  هذا يضمن أن كل مستخدم يرى بياناته فقط.

---

## المراحل المتوفرة في النظام

| المرحلة | المحتوى |
|---------|---------|
| 1 | ملاك ← عقارات ← وحدات ← عقود ← دفعات جزئية ← مصاريف |
| 2 | صيانة ← تنبيهات ← سجل عمليات |
| 3 | تحليلات ← KPIs ← مقارنة عقارات ← مركز تكلفة |
| 4 | وسطاء وعمولات ← مشاريع تحت التطوير |

---

تم الإعداد بواسطة بهو المدينة العقارية © 2026
