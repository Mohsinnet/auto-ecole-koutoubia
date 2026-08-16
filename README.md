# Auto-Ecole KOUTOUBIA MARRAKECH

واجهة HTML لإدارة بطاقات المرشحين في مدرسة تعليم السياقة، مع حفظ محلي ومزامنة اختيارية عبر Firebase Realtime Database.

## التشغيل

افتح `index.html` عبر GitHub Pages أو خادم HTTPS. سجّل الدخول بالبريد الإلكتروني وكلمة المرور عبر Firebase Authentication، ثم استخدم «تحميل» أو «رفع» للمزامنة.

## Firebase Storage

تقوم الصفحة برفع صورة المرشح وصور الوثائق إلى Firebase Storage عند الضغط على «رفع للسحابة»، ثم تحفظ روابط الصور داخل بطاقة المرشح في Realtime Database. يجب تفعيل Storage من Firebase Console قبل أول رفع.

قواعد مبدئية مناسبة للمستخدمين المصادق عليهم:

```text
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /candidates/{candidateId}/{allPaths=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

للحماية الأقوى، استبدل شرط `request.auth != null` بشرط يطابق UID حساب المدير أو قائمة المستخدمين المصرح لهم. لا تخزن كلمات المرور داخل الموقع.

## آخر التعديلات

- وضع رقم الهاتف ضمن قسم «معلومات شخصية».
- تغيير تسمية تاريخ السيزي إلى `Date de Saisie`.
- تغيير تسمية رقم السيارة إلى «رقم العربة».
- تغيير تسمية تاريخ التسجيل إلى «إضافية».
- إصلاح أخطاء JavaScript في أزرار العرض والتعديل والحذف.
- إضافة فحص اتصال Firebase تلقائي عند تشغيل الصفحة.
