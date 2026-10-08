# MIRZA — میرزا
## دستیار صوتی فارسی آفلاین اندروید

<p align="center">
  <b>یک دستیار صوتی کاملاً آفلاین به زبان فارسی برای اندروید</b>
</p>

---

## ✨ ویژگی‌ها

### 🎤 تشخیص گفتار آفلاین فارسی
- موتور Vosk برای تشخیص گفتار آفلاین
- بدون نیاز به اینترنت
- پشتیبانی از فارسی محاوره‌ای و رسمی

### 🔔 پنج عبارت بیدارباش
1. **میرزا بنویس** — برای ارسال پیامک
2. **میرزا پاشو** — برای تنظیم آلارم
3. **ایرج** — فعال‌سازی عمومی
4. **ایرج پاشو** — فعال‌سازی برای آلارم
5. **ایرج بنویس** — فعال‌سازی برای پیامک

> ⚠️ کلمه «میرزا» به تنهایی دستیار را فعال نمی‌کند.

### 📱 پیامک صوتی
- فرمان صوتی برای ارسال پیامک
- جستجوی مخاطبین اندروید
- پشتیبانی از نام‌های فارسی
- **تأیید اجباری** قبل از ارسال
- پشتیبانی از دو سیم‌کارت

### ⏰ آلارم صوتی
- تنظیم آلارم با فرمان صوتی
- پشتیبانی از عبارت‌های زمانی فارسی
  - «هفت و نیم» → ۷:۳۰
  - «یک ربع به هشت» → ۷:۴۵
  - «فردا صبح ساعت شش» → فردا ۶:۰۰

### 🔵 حباب شناور
- حباب قابل جابجایی روی تمام برنامه‌ها
- نشانگر وضعیت رنگی
- لمس برای فعال‌سازی

### 🔒 حریم خصوصی
- پردازش کاملاً محلی
- بدون ارسال اطلاعات به سرور
- بدون تبلیغات و ردیابی
- بدون نیاز به ثبت‌نام

---

## 📱 نصب

### دستگاه‌های پشتیبانی شده
- Samsung Galaxy Note 9
- هر گوشی اندروید ۱۰ (API 29) یا بالاتر

### روش ۱: ساخت از GitHub Actions
1. این مخزن را fork کنید
2. به تب Actions بروید
3. روی "Build MIRZA APK" کلیک کنید
4. "Run workflow" را بزنید
5. پس از اتمام بیلد، فایل APK را از Artifacts دانلود کنید

### روش ۲: ساخت محلی

```bash
# پیش‌نیازها:
# - Android Studio Hedgehog یا بالاتر
# - JDK 17
# - Android SDK (API 29+)

# ۱. پروژه را کلون کنید
git clone https://github.com/YOUR_USERNAME/mirza-android.git
cd mirza-android

# ۲. مدل Vosk فارسی را دانلود کنید
# از: https://alphacephei.com/vosk/models
# فایل vosk-model-small-fa-0.5 را در:
# app/src/main/assets/vosk-model-small-fa-0.5/
# قرار دهید

# ۳. پروژه را باز کنید
# Android Studio > File > Open > mirza-android

# ۴. بیلد کنید
./gradlew assembleDebug

# ۵. APK در این مسیر قرار دارد:
# app/build/outputs/apk/debug/app-debug.apk
```

### نصب روی گوشی
1. فایل APK را به گوشی منتقل کنید
2. در تنظیمات > امنیت > «نصب از منابع ناشناس» را فعال کنید
3. فایل APK را باز کنید و نصب کنید
4. مجوزهای لازم را بدهید

---

## 📁 ساختار پروژه

```
mirza-android/
├── app/
│   ├── src/main/
│   │   ├── kotlin/com/mirza/assistant/
│   │   │   ├── MirzaApplication.kt     # کلاس اصلی برنامه
│   │   │   ├── MainActivity.kt          # اکتیویتی اصلی
│   │   │   ├── command/                 # مدیریت فرمان‌ها
│   │   │   │   ├── AlarmCommandHandler.kt
│   │   │   │   ├── AlarmReceiver.kt
│   │   │   │   ├── CommandHandler.kt
│   │   │   │   └── SmsCommandHandler.kt
│   │   │   ├── data/                    # مخازن داده
│   │   │   │   ├── SettingsRepository.kt
│   │   │   │   └── VocabularyRepository.kt
│   │   │   ├── nlp/                     # پردازش زبان طبیعی
│   │   │   │   ├── ContactResolver.kt
│   │   │   │   ├── PersianCommandParser.kt
│   │   │   │   └── PersianTextNormalizer.kt
│   │   │   ├── service/                 # سرویس‌های پس‌زمینه
│   │   │   │   ├── BootReceiver.kt
│   │   │   │   ├── FloatingBubbleService.kt
│   │   │   │   └── WakeWordService.kt
│   │   │   ├── speech/                  # موتور گفتار
│   │   │   │   ├── OfflineSpeechEngine.kt
│   │   │   │   ├── PersianTextToSpeech.kt
│   │   │   │   └── WakePhraseDetector.kt
│   │   │   ├── state/                   # مدیریت وضعیت
│   │   │   │   └── AssistantStateManager.kt
│   │   │   ├── ui/                      # رابط کاربری
│   │   │   │   ├── MainViewModel.kt
│   │   │   │   ├── SettingsActivity.kt
│   │   │   │   ├── SetupActivity.kt
│   │   │   │   └── SmsConfirmationActivity.kt
│   │   │   └── util/
│   │   │       └── Constants.kt
│   │   ├── res/                         # منابع
│   │   │   ├── drawable/
│   │   │   ├── layout/
│   │   │   ├── values/
│   │   │   ├── values-fa/
│   │   │   └── values-night/
│   │   └── AndroidManifest.xml
│   └── build.gradle
├── .github/workflows/build.yml          # GitHub Actions
├── build.gradle
├── settings.gradle
└── README.md
```

---

## 🔧 نصب مدل Vosk

برای تشخیص گفتار آفلاین، مدل Vosk فارسی نیاز است:

1. مدل را از [Vosk Models](https://alphacephei.com/vosk/models) دانلود کنید
2. فایل `vosk-model-small-fa-0.5.zip` را استخراج کنید
3. پوشه `vosk-model-small-fa-0.5` را در مسیر `app/src/main/assets/` قرار دهید
4. پروژه را مجدداً بیلد کنید

---

## ⚠️ محدودیت‌ها

### نسخه فعلی (v1.0.0)
- مدل Vosk فارسی باید جداگانه نصب شود
- بازخورد صوتی TTS فارسی بستگی به موتور TTS نصب شده روی گوشی دارد
- آلارم تاریخ‌دار فقط برای امروز/فردا/پس‌فردا پشتیبانی می‌شود
- شنیدن پس‌زمینه ممکن است مصرف باتری را افزایش دهد

### محدودیت‌های اندروید
- شنیدن پس‌زمینه محدودیت‌های اندروید ۱۰+ را رعایت می‌کند
- حباب شناور نیاز به مجوز SYSTEM_ALERT_WINDOW دارد
- ارسال مستقیم SMS نیاز به مجوز SEND_SMS دارد

---

## 🧪 تست‌ها

تست‌های واحد برای بخش‌های زیر موجود است:
- PersianTextNormalizer: تبدیل اعداد، نرمال‌سازی متن
- PersianCommandParser: تشخیص فرمان، عبارت بیدارباش
- AssistantStateManager: انتقال وضعیت، جلوگیری از تکرار

اجرای تست‌ها:
```bash
./gradlew test
```

---

## 📄 مجوز

این پروژه با مجوز Apache 2.0 منتشر شده است.

---

## 🙏 تشکر

- [Vosk](https://alphacephei.com/vosk/) — موتور تشخیص گفتار آفلاین
- [ایرج میرزا](https://fa.wikipedia.org/wiki/ایرج_میرزا) — الهام‌بخش نام برنامه

---

**ساخته شده با ❤️ برای فارسی‌زبانان**
