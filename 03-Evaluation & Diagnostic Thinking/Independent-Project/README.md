# ContentFlow AI

> منصة تولّد محتوى جاهزًا للنشر على Instagram وFacebook وLinkedIn وX بالعربية أو الإنجليزية، مبنيًا على هوية العلامة التجارية.

---

## 🎯 Problem

### The Context
العلامات التجارية الصغيرة والمستقلون يحتاجون إلى حضور مستمر على أكثر من منصة تواصل اجتماعي، وكل منصة لها أسلوبها وطول منشوراتها.

### The Problem
لا يملك أغلبهم الوقت ولا الموارد التصميمية لإنتاج محتوى منتظم يشبه علامتهم في الشكل والأسلوب، فتبقى القنوات غير نشطة أو يظهر المحتوى بشكل غير متسق.

### Why It Matters
المحتوى المتسق مع هوية العلامة يبني الثقة ويحافظ على حضورها. توفير منشورات جاهزة لكل منصة من ملف علامة واحد يختصر وقتًا وجهدًا كبيرين.

---

## 💡 Solution

ملف علامة تجارية واحد ينتج أربعة منشورات مخصصة لكل منصة في تشغيل واحد، لكل منشور Caption وHashtags وصورة، مع إمكانية التعديل وإعادة التوليد والتصدير.

**What does the system do?**

1. يرفع المستخدم شعار العلامة ويصفها، فيستخرج النظام ألوان العلامة من الشعار تلقائيًا.
2. يولّد أربعة منشورات (Instagram, Facebook, LinkedIn, X) بأسلوب وطول مناسبين لكل منصة، بالعربية أو الإنجليزية.
3. يتيح تعديل الـ Caption يدويًا أو إعادة توليد منشور واحد دون إعادة الدفعة كاملة.
4. يصدّر المنشورات بصيغ PDF وCSV وJSON.

**Current Status:** MVP قيد التطوير. يعمل إنشاء الحساب وتأكيد البريد وإنشاء العلامة واستخراج الألوان، أما توليد المنشورات فما زال قيد الإصلاح.

---

## 👤 Users

**Primary Users:**
أصحاب العلامات التجارية الصغيرة والمستقلون الذين يديرون حساباتهم على وسائل التواصل بأنفسهم.

**User Need:**
الحصول على منشورات جاهزة ومتسقة مع هوية علامتهم لعدة منصات، دون خبرة في التصميم أو كتابة المحتوى.

---

## 🧠 How I Designed the Solution

جعلت **هوية العلامة** محور النظام: كل ما يُولّد يعتمد على ملف العلامة (الشعار والوصف والألوان المستخرجة). عمل المشروع فريق من شخصين: أنا مسؤولة عن جزء الذكاء الاصطناعي، وزميل مسؤول عن الـ Backend.

بدأنا بنموذج UI/UX تفاعلي بالعربية والإنجليزية، وبنينا التطبيق باستخدام v0 بوصفه AI App Builder، ثم اتفقنا على شكل البيانات المتبادل بين الـ AI والـ Backend (Data Contract) قبل البناء، ثم نفذنا على مراحل: تسجيل الدخول وإدارة العلامة، ثم توليد النص، ثم توليد الصور، ثم إعادة التوليد والتعديل، ثم التصدير.

**My role:** استخراج ألوان الشعار، وهندسة الـ Prompts، وخط توليد النص والصور، ومنطق إعادة التوليد، وعقد البيانات بين الـ AI والـ Backend.

---

## ⚙️ How It Works

```text
Brand profile: logo + description
              ↓
Color extraction from the logo (image processing)
              ↓
AI generation per platform: caption + hashtags + image
              ↓
Schema validation of the AI output
              ↓
Review: edit caption / regenerate a single post
              ↓
Export: PDF · CSV · JSON
```

---

## 🤖 Role of AI

**What does AI do in this solution?**

- يكتب Google Gemini الـ Caption والـ Hashtags لكل منصة بالأسلوب والطول المناسبين لها، وفق نبرة العلامة ولغتها.
- يولّد صورة لكل منشور متسقة مع ألوان العلامة.
- في البناء: استخدمنا v0 لبناء التطبيق بمساعدة الذكاء الاصطناعي، مع مراجعة ما يبنيه وتعديله بدل قبوله كما هو.

### What AI Should NOT Do

- إنتاج مخرجات غير منظمة؛ كل استجابة تُتحقق من مطابقتها لـ Schema قبل حفظها.
- عرض محتوى وهمي عند الفشل؛ يظهر للمستخدم حالة خطأ واضحة بدلًا من ذلك.
- النشر مباشرة على حسابات المستخدم؛ المستخدم يراجع ويقرر.

---

## 🔄 Automation

**What parts of the process are automated?**

- استخراج ألوان العلامة من الشعار دون اختيار يدوي.
- توليد المنشورات الأربعة في تشغيل واحد.
- التحقق من صحة مخرجات الـ AI قبل حفظها.
- إنشاء ملفات التصدير.

---

## 🗂️ Data

### Input
اسم العلامة، والمجال (Industry)، ووصف العلامة، ولغة المحتوى، ونبرة العلامة (Brand Tone)، والشعار (مطلوب)، وحتى صورتين مرجعيتين اختياريتين.

### Output
أربعة منشورات (Caption وHashtags وصورة لكل منصة)، ولوحة ألوان العلامة، وملفات تصدير PDF وCSV وJSON.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| v0 | AI App Builder: بناء التطبيق (الواجهة والمنطق) بمساعدة الذكاء الاصطناعي |
| Google Gemini | توليد محتوى المنشورات (Caption وHashtags) |
| AI SDK | ربط التطبيق بنموذج Gemini من جهة الـ Server |
| Next.js | إطار التطبيق (الواجهة والـ Server) |
| Supabase | Auth وقاعدة بيانات PostgreSQL وStorage مع RLS |
| Tailwind CSS | تنسيق الواجهة ودعم RTL |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
استخراج ألوان العلامة تلقائيًا من الشعار بدل أن يختارها المستخدم.

**Why:**
يقلل الجهد على المستخدم ويضمن أن المحتوى المولّد متسق مع هويته الفعلية.

### Decision 2
**Decision:**
تشغيل كل استدعاءات الـ AI على الـ Server، والتحقق من مخرجاتها بـ Schema قبل الحفظ.

**Why:**
لا تُكشف مفاتيح الـ API في الواجهة، ولا تُحفظ مخرجات ناقصة أو بصيغة خاطئة.

### Decision 3
**Decision:**
تفعيل RLS على كل الجداول مع Composite Foreign Keys، وتخزين خاص للملفات عبر Signed URLs.

**Why:**
يضمن أن مالك أي سجل هو نفسه مالك السجل الأب، وأن ملفات كل مستخدم لا يصل إليها غيره.

---

## 🧪 Testing

### Test 1: Sign up and access the workspace
**Input:**
إنشاء حساب جديد بالاسم والإيميل وكلمة المرور، ثم تأكيد البريد وتسجيل الدخول.

**Expected Result:**
تظهر رسالة تطلب تأكيد البريد، ويصل إيميل التأكيد من Supabase Auth، ثم يفتح Workspace المستخدم.

**Actual Result:**
ظهرت رسالة "Check your email to confirm your account" ([Register](./Screenshots/Register.png))، ووصل إيميل التأكيد ([Confirmation Email](./Screenshots/Confirmation-Email.png))، وفُتح الـ Workspace بعد الدخول ([Dashboard](./Screenshots/Dashboard%20%281%29.png)).

**Status:** ✅

---

### Test 2: Brand creation and color extraction
**Input:**
إنشاء علامة Amira Coffee (المجال والوصف واللغة العربية والنبرة Friendly) ورفع شعار بثلاثة ألوان رئيسية: بني غامق وذهبي وكريمي.

**Expected Result:**
يستخرج النظام لوحة ألوان تمثل ألوان الشعار الرئيسية دون تكرار.

**Actual Result:**
استُخرجت خمسة ألوان: `#866138` و`#E0D1BE` و`#F5EBDD` مكرر ثلاث مرات ([Brand Profile](./Screenshots/Brand-Profile.png)). ظهر لون الخلفية الكريمي ولون بني متوسط، لكن الألوان تكررت ولم يُفصل البني الغامق عن الذهبي.

**Status:** ⚠️ Partially Passed

---

### Test 3: Content generation
**Input:**
حفظ العلامة وطلب توليد المنشورات الأربعة.

**Expected Result:**
تظهر أربعة منشورات (Instagram, Facebook, LinkedIn, X) لكل منها Caption وHashtags وصورة.

**Actual Result:**
انتقل التطبيق إلى شاشة "Creating your content" وظهرت خطوة "Generating captions and prompts" ([Generating](./Screenshots/Generating.png))، لكن التوليد لم يكتمل إلى المنشورات النهائية في النسخة الحالية.

**Status:** ❌

---

## 📸 Evidence

- 🔗 [View Register Page](./Screenshots/Register.png)
- 🔗 [View Confirmation Email](./Screenshots/Confirmation-Email.png)
- 🔗 [View Workspace Dashboard](./Screenshots/Dashboard%20%281%29.png)
- 🔗 [View Brand Profile and Extracted Colors](./Screenshots/Brand-Profile.png)
- 🔗 [View Content Generation Screen](./Screenshots/Generating.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- يتوقف توليد المحتوى عند خطوة "Generating captions and prompts" ولا تظهر المنشورات النهائية.
- استخراج الألوان يكرر اللون نفسه (`#F5EBDD` ثلاث مرات) ولا يفصل ألوان الشعار المتقاربة (البني والذهبي).
- تعرض القائمة الجانبية مستخدمًا تجريبيًا (Jordan Davis) بدل بيانات المستخدم الذي سجّل الدخول.
- تنسيق العمل بين الـ AI والـ Backend كان صعبًا في البداية لأن كل طرف يتوقع شكلًا مختلفًا للبيانات.

**How did I solve it?**

- اتفقنا على Data Contract واضح بين الـ AI والـ Backend قبل البناء، وأضفنا التحقق بـ Schema لرفض أي مخرجات لا تطابقه.
- **قيد الإصلاح:** تتبّع استدعاء Gemini من جهة الـ Server لمعرفة سبب توقف التوليد، وإزالة الألوان المكررة واختيار ألوان متباعدة من الشعار، وربط القائمة الجانبية ببيانات جلسة المستخدم الفعلية.
- نبني على مراحل ونختبر كل مرحلة قبل الانتقال للتالية.

---

## 📚 What I Learned

### Technical Lesson
مخرجات الـ AI يجب أن تكون منظمة ومتحقق منها قبل أن يعتمد عليها النظام، وتشغيل الاستدعاءات على الـ Server ضروري لحماية المفاتيح.

### Problem-Solving Lesson
في مشروع فريق، الاتفاق المبكر على شكل البيانات بين الأجزاء يوفر وقتًا كبيرًا ويقلل الأخطاء عند الربط.

### AI Lesson
جودة المحتوى المولّد تعتمد على وضوح السياق المعطى للنموذج: هوية العلامة والمنصة واللغة والنبرة.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إكمال مسار التوليد والتصدير، ثم تشغيل فحص شامل للتطبيق قبل الإطلاق.
- إضافة جدولة النشر مباشرة على حسابات التواصل الاجتماعي.
- دعم منصات إضافية مثل TikTok وPinterest، وحسابات فرق متعددة المستخدمين.

---

## 🔗 Project Links

**Live Demo:** [contentflow-ai-lac.vercel.app](https://contentflow-ai-lac.vercel.app)

**Repository:** [github.com/lilian2005-ui/Lilian_aiAutomation](https://github.com/lilian2005-ui/Lilian_aiAutomation)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
