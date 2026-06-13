## اطلاعات جمع‌آوری‌شده
- فایل workflow: `.github/workflows/universal-apk.yml`
- خطای GitHub Actions: `Invalid workflow file` با پیام `You have an error in your yaml syntax on line 12`
- بررسی محتوای فایل نشان می‌دهد دو مرحله‌ی زیر به درستی هم‌تراز (indent) نشده‌اند:
  - `- name: Set up JDK 17 ...`
  - `- name: Build universal APK`
  - و در ادامه همین موضوع برای `- name: Upload universal outputs` هم تأثیر می‌گذارد.
- در فایل فعلی، پس از step اول `actions/checkout@v4` یک خط خالی هست و سپس `- name: Set up JDK 17 ...` بدون فاصله‌ی درست نسبت به `steps:` آمده است.

## برنامه اصلاح
1. اصلاح YAML indentation:
   - تمام `- name: ...` ها باید در یک سطح هم‌سطح با `- name: Checkout` باشند (یعنی دقیقاً زیر `steps:` با همان indent).
2. بررسی اینکه بخش `with:` و `run:` درست و تحت همان step قرار بگیرند.
3. ذخیره فایل و اطمینان از اینکه workflow پس از push معتبر (valid) می‌شود.
4. (اختیاری) اگر خواستی، یک اقدام کمکی برای تست/اعتبارسنجی YAML انجام می‌دهیم.

## فایل‌های وابسته برای ویرایش
- `.github/workflows/universal-apk.yml`
- (فقط برای مدیریت کار) `TODO.md` / `blackboxai_plan_universal_apk.md`

## مراحل بعدی
- بعد از اصلاح فایل: دوباره workflow را با commit/push یا با rerun workflow اجرا کن تا مطمئن شو خطای YAML رفع شده است.

<ask_followup_question>
آیا اجازه می‌دهی فایل `.github/workflows/universal-apk.yml` را فقط با اصلاح indent (هم‌تراز کردن stepهای JDK/Build/Upload) بازنویسی کنم؟
</ask_followup_question>

