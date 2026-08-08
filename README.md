# مكة كول — مشروع أندرويد جاهز

هذا مشروع **Capacitor** كامل يحوّل تطبيق الويب إلى تطبيق أندرويد حقيقي.
تم بالفعل: تثبيت الحزم، إنشاء مشروع Android Studio، ربط ملف `www/index.html`،
وتصميم أيقونة التطبيق بكل الأحجام المطلوبة.

## ⭐ الطريقة الأسرع: بناء تلقائي عبر GitHub Actions (بدون تثبيت أي برنامج)

هذا المشروع يحتوي على خط بناء جاهز (`.github/workflows/build-apk.yml`) يبني
APK تلقائياً في السحابة عند رفع المشروع على GitHub — لا تحتاج تثبيت Android
Studio ولا Android SDK على جهازك إطلاقاً.

### الخطوات:

1. أنشئ حساباً مجانياً على [github.com](https://github.com) إن لم يكن لديك واحد.
2. أنشئ مستودعاً (Repository) جديداً فارغاً (خاص أو عام، لا فرق).
3. ارفع محتويات هذا المشروع إليه. من داخل مجلد `makkah-call-app`:
   ```
   git init
   git add .
   git commit -m "أول رفع لمشروع مكة كول"
   git branch -M main
   git remote add origin https://github.com/USERNAME/REPO-NAME.git
   git push -u origin main
   ```
4. افتح صفحة المستودع على GitHub، ثم تبويب **Actions** — ستجد بناءً يعمل تلقائياً
   (يأخذ من 3 إلى 6 دقائق تقريباً).
5. بعد اكتمال البناء (علامة ✓ خضراء)، افتح البناء واضغط على قسم **Artifacts**
   بالأسفل، وحمّل `makkah-call-debug-apk`.
6. فك ضغط الملف الذي حمّلته، ستجد `app-debug.apk` — انقله لجوالك (عبر رابط
   تحميل مباشر أو USB) وثبّته مباشرة (فعّل "السماح بالتثبيت من مصادر غير معروفة"
   في إعدادات أندرويد إن طُلب منك ذلك).

> **ملاحظة:** APK هذا موقّع بمفتاح تجريبي (debug) — يعمل ويُثبَّت بشكل طبيعي
> على أي جهاز أندرويد، لكنه غير صالح للرفع على Google Play. لذلك يبني ملف
> `app-release-unsigned.apk` أيضاً كخطوة تالية عندما تكون جاهزاً للنشر الرسمي
> (يحتاج توقيعاً بمفتاح Keystore خاص بك قبل الرفع للمتجر).

## البديل: البناء يدوياً عبر Android Studio

1. **ثبّت [Android Studio](https://developer.android.com/studio)**.
2. **فك ضغط هذا المشروع** في أي مجلد على جهازك.
3. من داخل المجلد، شغّل:
   ```
   npm install
   npx cap sync android
   ```
4. افتح مجلد `android` من داخل Android Studio مباشرة (File > Open).
5. انتظر مزامنة Gradle (أول مرة تحمّل SDK تلقائياً).
6. للتجربة: اضغط ▶ Run على محاكي أو جهاز حقيقي.
7. للبناء النهائي: `Build > Generate Signed Bundle / APK`
   - **APK** للتثبيت المباشر السريع.
   - **AAB** للرفع على Google Play (يحتاج Keystore موقّع، احفظه بأمان).

## قبل التشغيل: فعّل Firebase

التطبيق يستخدم Firebase لتفعيل الدردشة الفورية. افتح `www/index.html`
وابحث عن `firebaseConfig` قرب نهاية الملف، واستبدل القيم بمفاتيح مشروعك
من [console.firebase.google.com](https://console.firebase.google.com):
- فعّل **Firestore Database**
- فعّل **Authentication > Anonymous**

بعد أي تعديل على `www/index.html`، نفّذ `npx cap sync android` لنقل
التحديث إلى مشروع أندرويد قبل إعادة البناء.

## هيكل المشروع

```
makkah-call-app/
├── www/index.html          ← كود التطبيق (HTML/CSS/JS + Firebase)
├── android/                 ← مشروع أندرويد الكامل (Android Studio)
├── capacitor.config.ts      ← إعدادات اسم التطبيق ومعرّف الحزمة
├── playstore-icon-512.png   ← أيقونة جاهزة لرفعها على Google Play
└── package.json
```

**معرّف الحزمة (Package ID):** `com.makkahcall.app`
**اسم التطبيق:** مكة كول
