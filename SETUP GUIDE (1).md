# راهنمای کامل راه‌اندازی تست Medizoom AI Bot

-----

## بخش ۱ — اینستاگرام Business + Facebook App

### مرحله ۱: ساخت اکانت اینستاگرام جدید

1. اپ اینستاگرام → **Sign Up**
1. یه ایمیل جدید استفاده کن (مثلاً [medizoom.test@gmail.com](mailto:medizoom.test@gmail.com))
1. نام: `medizoom_test` یا هر چیزی
1. بعد از ساخت → **Settings → Account → Switch to Professional Account**
1. نوع: **Business** → دسته‌بندی: Health/Medical
1. ✅ اکانت Business آماده‌ست

-----

### مرحله ۲: ساخت Facebook Page و اتصال

1. برو به **facebook.com/pages/create**
1. نام Page: `Medizoom Test`
1. دسته: Health/Medical
1. بعد از ساخت Page، برو به اینستاگرام:
- Settings → **Linked Accounts → Facebook**
- همین Facebook Page رو انتخاب کن
1. ✅ اینستاگرام به Facebook وصل شد

-----

### مرحله ۳: ساخت Facebook Developer App

1. برو به: **developers.facebook.com**
1. **My Apps → Create App**
1. نوع: **Business**
1. نام App: `medizoom-bot-test`
1. بعد از ساخت:
- **Add Product → Instagram Graph API → Set Up**
1. ✅ App ساخته شد

-----

### مرحله ۴: گرفتن Access Token

1. در Developer App برو به:
   **Tools → Graph API Explorer**
1. از منوی بالا App خودت رو انتخاب کن
1. کلیک کن **Generate Access Token**
1. پرمیشن‌های زیر رو tick کن:
- `instagram_basic`
- `instagram_content_publish`
- `pages_read_engagement`
1. کلیک **Generate Token** و کپی کن
1. برای Long-lived token (60 روزه) این URL رو باز کن:

```
https://graph.facebook.com/v19.0/oauth/access_token
  ?grant_type=fb_exchange_token
  &client_id=YOUR_APP_ID
  &client_secret=YOUR_APP_SECRET
  &fb_exchange_token=YOUR_SHORT_TOKEN
```

1. ✅ Access Token آماده

-----

### مرحله ۵: گرفتن Instagram Account ID

این رو در مرورگر باز کن (با توکنت جایگزین کن):

```
https://graph.facebook.com/v19.0/me/accounts?access_token=YOUR_TOKEN
```

از نتیجه `id` صفحه Facebook رو کپی کن، بعد:

```
https://graph.facebook.com/v19.0/YOUR_PAGE_ID?fields=instagram_business_account&access_token=YOUR_TOKEN
```

عدد داخل `instagram_business_account.id` = همون **INSTAGRAM_ACCOUNT_ID** توی config.py

-----

## بخش ۲ — سایت تست یک صفحه‌ای (GitHub Pages)

### مرحله ۱: ساخت repo در GitHub

1. برو به **github.com → New Repository**
1. نام: `medizoom-test-site`
1. Public ✅
1. Add README ✅
1. Create Repository

-----

### مرحله ۲: فعال کردن GitHub Pages

1. در repo → **Settings → Pages**
1. Source: **Deploy from a branch**
1. Branch: **main** → folder: **/ (root)**
1. Save
1. آدرس سایتت میشه:
   `https://USERNAME.github.io/medizoom-test-site`

-----

### مرحله ۳: آپلود فایل index.html

فایل `index.html` که کنارشه رو در repo آپلود کن.
(Add file → Upload files → index.html رو بکش بنداز)

-----

### مرحله ۴: فعال کردن GitHub Actions

1. در repo → **Settings → Secrets and variables → Actions**
1. کلیک **New repository secret**
1. این secretها رو یکی یکی اضافه کن:

|Name                    |Value                        |
|------------------------|-----------------------------|
|`ANTHROPIC_API_KEY`     |کلید از console.anthropic.com|
|`OPENAI_API_KEY`        |کلید از platform.openai.com  |
|`INSTAGRAM_ACCESS_TOKEN`|توکن از مرحله ۴ بالا         |
|`INSTAGRAM_ACCOUNT_ID`  |ID از مرحله ۵ بالا           |

1. فایل‌های پایتون رو هم آپلود کن (همه فایل‌های قبلی)
1. ✅ سیستم آماده‌ست!

-----

## تست نهایی

بعد از همه مراحل، برو به **Actions → Daily Post → Run workflow**
اگه سبز شد = همه چیز کار می‌کنه! 🎉

-----

## هزینه‌ها

|سرویس                 |هزینه                  |
|----------------------|-----------------------|
|Instagram + Facebook  |رایگان                 |
|GitHub Pages + Actions|رایگان                 |
|Claude API (Anthropic)|~$0.01 per post        |
|DALL-E 3 (OpenAI)     |~$0.04 per image       |
|**جمع روزانه**        |**~$0.05 = ۲۵۰۰ تومان**|