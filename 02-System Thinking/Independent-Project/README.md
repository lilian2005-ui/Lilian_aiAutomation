# DataSense Lite

تطبيق ويب (MVP تجريبي) لأصحاب المشاريع: يرفعون ملف بياناتهم (CSV أو Excel) فيحصلون على لوحة واضحة بأهم الأرقام والرسوم، مع Insights وRecommendations مبنية على بياناتهم.

---

## 🎯 Problem

### The Context
أصحاب المشاريع الصغيرة والمتوسطة يملكون بيانات (مبيعات، عملاء، مخزون...) في ملفات CSV أو Excel، لكن معظمهم ليسوا محللي بيانات، ولا يملكون الوقت أو الأدوات لتحويل هذه الملفات إلى فهم واضح.

### The Problem
الملف وحده لا يجيب عن سؤال "ماذا أفعل الآن؟". يحتاج صاحب المشروع إلى رؤية الأرقام المهمة والاتجاهات بوضوح، ثم إلى توصيات عملية مبنية على بياناته، وغالبًا لا يعرف من أين يبدأ.

### Why It Matters
تحويل البيانات إلى قرارات يساعد صاحب المشروع على اكتشاف ما يحتاج إلى انتباه واتخاذ خطوات عملية، بدل ترك البيانات في ملفات لا يستفيد منها.

---

## 💡 Solution

تطبيق يقرأ ملف البيانات، ويعرض لوحة (Dashboard) بمؤشرات ورسوم مناسبة لهذه البيانات، ثم يولّد Insights وRecommendations مكتوبة بلغة بسيطة.

**What does the system do?**

1. يستقبل ملف CSV أو Excel (حتى 5 MB و50,000 صف و50 عمودًا).
2. يقرأ الملف داخل المتصفح (Browser) ويعرض صفحة Data Check: ملخص الملف، وجودة البيانات (القيم المفقودة والصفوف المكررة)، ونوع كل عمود، ومعاينة للصفوف، مع اختيار المقياس الرئيسي (Main Measure) وعمود التاريخ.
3. يعرض لوحة Dashboard بمؤشرات (KPIs) ورسوم: اتجاه عبر الزمن، وأعلى الفئات، وتوزيع القيم.
4. يولّد AI Insights تتضمن Summary وKey Findings (مع الأهمية والدليل) وRisks & Anomalies وRecommendations (مع الأولوية) وData Limitations.
5. يدعم العربية والإنجليزية.

---

## 👤 Users

**Primary Users:**
أصحاب المشاريع (Business Owners)، وهم الفئة الأكثر حاجة لهذا النوع من التحليل.

**User Need:**
فهم بياناتهم بسرعة ومعرفة الخطوة التالية، دون الحاجة إلى مهارات تحليل أو أدوات معقدة.

---

## 🧠 How I Designed the Solution

طبّقت نفس تسلسل U2 الذي تعلمته في المشروع الموجّه: بدأت بتحديد المستخدم الأول (أصحاب المشاريع)، ثم عرّفت المشكلة والحل وحدود الـ MVP، وصممت الشاشات ومنطق البيانات ومهمة الـ AI، وكتبت ملفات المواصفات (من 01 إلى 05) قبل أن أوجّه Lovable للبناء عبر Prompts متتابعة.

أهم قراراتي في التصميم:

- قبول أي نوع من البيانات بدل تقييد التطبيق بمجال واحد.
- الاكتفاء برفع CSV/Excel في الـ MVP.
- دعم العربية والإنجليزية من البداية.
- طلب تحليل حقيقي ورسوم واضحة وليس بيانات شكلية.

---

## ⚙️ How It Works

```text
User uploads a CSV / Excel file
              ↓
File is read inside the browser
              ↓
Data Check: column types, data quality, Main Measure, Date Column
              ↓
Dashboard: KPIs + Charts
              ↓
Statistical summary only (never raw rows) is sent to the AI
              ↓
AI Insights: Summary · Key Findings · Risks · Recommendations · Limitations
```

---

## 🤖 Role of AI

**What does AI do in this solution?**

- يقرأ الملخص الإحصائي للبيانات ويستخرج منه Key Findings مع الدليل (Evidence) لكل نتيجة.
- يحدد المخاطر والشذوذات (Risks & Anomalies) مثل الصفوف المكررة والقيم المفقودة.
- يولّد Recommendations عملية مرتبة حسب الأولوية ومربوطة بالبيانات التي بُنيت عليها.
- يذكر حدود التحليل (Data Limitations).

### What AI Should NOT Do

- اختراع أرقام أو استنتاجات غير مدعومة بالبيانات المرفوعة؛ كل نتيجة تُعرض مع الدليل الذي بُنيت عليه.
- الوصول إلى الصفوف الأصلية؛ يستلم ملخصًا إحصائيًا فقط.
- تقديم التوصيات كقرارات نهائية؛ هي اقتراحات يراجعها صاحب المشروع.

---

## 🔄 Automation

**What parts of the process are automated?**

- قراءة الملف وتحليل أعمدته.
- حساب المؤشرات وبناء الرسوم البيانية.
- توليد الـ Insights والـ Recommendations بعد الرفع.

---

## 🗂️ Data

### Input
ملف CSV أو Excel يرفعه المستخدم (حتى 5 MB و50,000 صف و50 عمودًا)، ويمكن أن يحتوي أي نوع من البيانات.

### Output
صفحة Data Check، ولوحة بمؤشرات ورسوم بيانية، وAI Insights تتضمن Summary وKey Findings وRisks وRecommendations وLimitations، بالعربية أو الإنجليزية.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Lovable | بناء التطبيق بمساعدة الذكاء الاصطناعي |
| Google Gemini API | توليد الـ Insights والـ Recommendations |
| GitHub | استضافة المشروع وتوثيقه |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
قراءة الملف داخل المتصفح بدل رفعه إلى خادم.

**Why:**
بيانات الأعمال حساسة، وبقاؤها في المتصفح يحافظ على خصوصية المستخدم.

### Decision 2
**Decision:**
استهداف أصحاب المشاريع كأول مستخدم، وقبول أي نوع من البيانات.

**Why:**
حاجتهم هي الأكبر، وقبول أي بيانات يجعل التطبيق مفيدًا لأكثر من نشاط دون مجال ثابت.

### Decision 3
**Decision:**
دعم العربية والإنجليزية في الواجهة والنتائج.

**Why:**
المستخدم المستهدف قد يعمل بأي من اللغتين، ولا يجب أن تكون اللغة عائقًا أمام فهم بياناته.

### Decision 4
**Decision:**
إضافة خطوة Data Check قبل الـ Dashboard، وإرسال ملخص إحصائي فقط إلى الـ AI، مع استبعاد الأعمدة النصية والمعرّفات.

**Why:**
يتأكد المستخدم من فهم التطبيق لبياناته (أنواع الأعمدة والجودة) قبل التحليل، وتبقى بياناته الأصلية في متصفحه.

---

## 🧪 Testing

### Test 1: CSV upload
**Input:**
رفع ملف `udemy.csv` (3,682 صفًا و11 عمودًا) من صفحة Upload.

**Expected Result:**
يُقرأ الملف، وتظهر صفحة Data Check بأنواع الأعمدة وجودة البيانات، ثم Dashboard بمؤشرات ورسوم، ثم AI Insights.

**Actual Result:**
قُرئ الملف وعرضت Data Check ملخص الملف (3,682 صفًا و11 عمودًا) وجودة البيانات (6 صفوف مكررة) وأنواع الأعمدة ومعاينة الصفوف. بعد اختيار المقياس الرئيسي (`price`) وعمود التاريخ بُنيت اللوحة بمؤشرات واتجاه عبر الزمن وأعلى الفئات وتوزيع القيم، ثم ظهرت AI Insights بالأقسام المتوقعة مع الدليل والأولوية.

**Status:** ✅

---

### Test 2: Language switching
**Input:**
تبديل لغة الواجهة بين العربية والإنجليزية بعد تحليل البيانات.

**Expected Result:**
تتغير الواجهة واتجاه الصفحة (RTL / LTR) بشكل صحيح، وتظهر النتائج باللغة المختارة.

**Actual Result:**
تبدّلت الواجهة بين العربية والإنجليزية بشكل صحيح، وتغيّر اتجاه الصفحة (RTL / LTR) وظهرت النتائج باللغة المختارة.

**Status:** ✅

---

## 📸 Evidence

### Demo Video

🎥 [Watch the Demo Video](https://drive.google.com/file/d/1bmqYGAZIpLortw2klJba2RoqJrzYLx7z/view?usp=sharing)

يعرض الفيديو التطبيق وهو يعمل: رفع الملف، ثم اللوحة، ثم الـ Insights والـ Recommendations، مع تبديل اللغة.

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- بعد أول Prompts كانت لوحة المؤشرات عامة وغير واضحة: مثلًا مجموع ومتوسط لكل سجل على عمود سعر دون معنى، ورسم Scatter غير مفيد.

**How did I solve it?**

- راجعت المخرجات بدل قبول أول نتيجة، وأعدت صياغة مواصفات لوحة المؤشرات لتكون المؤشرات والرسوم أكثر معنى ووضوحًا، ثم وجّهت Lovable للتحسين (Iteration).

---

## 📚 What I Learned

### Technical Lesson
كيف أبني تطبيقًا يقرأ ملفات CSV/Excel داخل المتصفح ويحوّلها إلى مؤشرات ورسوم، وكيف أدعم اللغتين مع RTL.

### Problem-Solving Lesson
أول نتيجة من أداة البناء نادرًا ما تكون النهائية. المراجعة وتحديد الفجوة بين المطلوب والمنفّذ ثم التحسين هي ما رفع جودة اللوحة.

### AI Lesson
الذكاء الاصطناعي يحتاج إلى مواصفات واضحة ليعطي نتائج ذات معنى. مؤشرات "عامة" تنتج عندما تكون التعليمات عامة.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إضافة قوالب جاهزة لقطاعات محددة (مثل التعليم أو الصحة أو الزراعة) فوق محرك التحليل العام.
- إضافة تسجيل دخول وحفظ التحليلات السابقة للمقارنة عبر الزمن.
- إتاحة تصدير التقرير (PDF) للمشاركة مع الفريق.

---

## 🔗 Project Links

**Live Demo:** [datasense-lite.lovable.app](https://datasense-lite.lovable.app/)

**Demo Video:** [Watch on Google Drive](https://drive.google.com/file/d/1bmqYGAZIpLortw2klJba2RoqJrzYLx7z/view?usp=sharing)

**Repository:** [github.com/lilian2005-ui/datasense-lite](https://github.com/lilian2005-ui/datasense-lite)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
