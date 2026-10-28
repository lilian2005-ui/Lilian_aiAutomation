# SkillBridge Lite

تطبيق ويب يحوّل الملف المهني وفرصة مهنية محددة إلى تحليل مدعوم بالذكاء الاصطناعي (AI Fit Analysis) يوضح التوافق والفجوات والخطوات المقترحة.

---

## 🎯 Problem

### The Context
طلاب وخريجون جدد ومهنيون في بداية مسيرتهم يملكون مهارات ومشاريع وخبرات، ويبحثون عن فرص مهنية مناسبة.

### The Problem
يجد الشخص صعوبة في الإجابة عن أسئلة مثل: ما المهارات في ملفي المرتبطة بهذه الفرصة؟ ما الأدلة في مشاريعي التي تدعم ملاءمتي؟ ما المتطلبات التي لم أقدم معلومات كافية عنها؟ وما الخطوات التي تحسّن استعدادي؟ المشكلة هي تحويل المعلومات المهنية المتفرقة إلى فهم واضح للعلاقة بين الملف المهني ومتطلبات فرصة محددة.

### Why It Matters
فهم الفجوات والمهارات المرتبطة بفرصة معينة يساعد المستخدم على تحسين ملفه واستعداده بخطوات عملية بدل التخمين.

---

## 💡 Solution

تجربة بسيطة تقود المستخدم من ملفه المهني إلى تحليل واضح لمدى توافقه مع فرصة يختارها. المشروع ليس منصة توظيف متكاملة، بل حل صغير يعالج مشكلة محددة بتجربة استخدام واضحة ووظيفة AI ذات غرض محدد.

**What does the system do?**

- يعرض الملف المهني ويتيح تعديله (Name, Headline, About Me, Skills, Projects, Experience).
- يعرض ثلاث فرص مهنية تجريبية جاهزة.
- يعرض تفاصيل الفرصة المختارة: الوصف والمتطلبات والمسؤوليات.
- يطلب AI Fit Analysis يقارن الملف بالفرصة.
- يعرض النتيجة في ثلاثة أقسام: Relevant Skills وPotential Gaps وRecommended Next Steps.

---

## 👤 Users

**Primary Users:**
Student / Recent Graduate / Early-Career Professional. صُممت التجربة لمستخدم واحد فقط، دون أدوار متعددة أو لوحات تحكم.

**User Need:**
فهم مدى ارتباط ملفه المهني بفرصة محددة، ومعرفة ما يمكنه فعله لتحسين استعداده.

---

## 🧠 How I Designed the Solution

مشيت على طبقات U2 الخمس قبل أي بناء: فهمت المستخدم وهدفه، ثم عرّفت الحل وحدود الـ MVP، ثم صممت User Flow والشاشات، ثم صممت البيانات ومهمة الـ AI وقواعدها، وبعدها كتبت Specification ووجّهت Lovable تدريجيًا بدل Prompt ضخم واحد.

| U2 Layer | Applied in the Project |
|---|---|
| 01 — Understand the User | تحديد المستخدم وهدفه واحتياجه |
| 02 — Define the Solution | صياغة المشكلة وتحديد الحل وحدود الـ MVP |
| 03 — Design the Experience | الشاشات والتنقل والتفاعلات (User Flow) |
| 04 — Design the System | البيانات والمدخلات والمخرجات ومنطق النظام |
| 05 — Specify & Build with AI | كتابة Specification وتوجيه Lovable للبناء |

---

## ⚙️ How It Works

```text
HOME
  ↓
MY PROFILE (view / edit)
  ↓
EXPLORE OPPORTUNITIES
  ↓
OPPORTUNITY DETAILS
  ↓
ANALYZE MY FIT   ← Profile + Selected Opportunity → AI Analysis
  ↓
AI FIT ANALYSIS (Relevant Skills · Potential Gaps)
  ↓
RECOMMENDED NEXT STEPS
```

---

## 🤖 Role of AI

**What does AI do in this solution?**

- يستقبل الملف المهني والفرصة المختارة ويقارن بينهما.
- يحدد المهارات والخبرات في الملف المرتبطة بمتطلبات الفرصة.
- يحدد المتطلبات التي لا تكفي معلومات الملف لإثباتها.
- يقترح خطوات عملية لتحسين الملف أو الاستعداد.

**What AI Should NOT Do**

- اختراع مهارات أو خبرات غير موجودة في الملف.
- اعتبار غياب المعلومات دليلًا مؤكدًا على غياب المهارة.
- ضمان القبول في وظيفة أو التنبؤ بنتيجة التوظيف.
- تقديم النتيجة كحكم نهائي على قدرات المستخدم؛ هي تقدير مساعد فقط.

---

## 🔄 Automation

**What parts of the process are automated?**

- تحليل الملف المهني مقابل الفرصة المختارة عند طلب المستخدم.
- عرض النتيجة في الأقسام الثلاثة المحددة.

---

## 🗂️ Data

**Input**
بيانات الملف المهني (`name`, `headline`, `about`, `skills`, `projects`, `experience`) وبيانات الفرصة (`title`, `company`, `description`, `requiredSkills`, `responsibilities`).

**Output**
AI Fit Analysis يتضمن Relevant Skills وPotential Gaps وRecommended Next Steps.

يعتمد المشروع على بيانات بسيطة داخل التطبيق بدلًا من قاعدة بيانات أو Backend، لأنها خارج نطاق الـ MVP.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Lovable | بناء التطبيق بمساعدة الذكاء الاصطناعي |
| AI Analysis | توليد تحليل التوافق بين الملف والفرصة |
| GitHub | استضافة المشروع وتوثيقه |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
تحديد MVP صغير بخمس وظائف، واستبعاد Authentication وDatabase وAdmin Dashboard والتكاملات الخارجية.

**Why:**
يحافظ على وضوح النطاق ويجعل المشروع قابلًا للتنفيذ ضمن الوقت والـ Credits المتاحة، ويركز على الـ Core User Flow.

### Decision 2
**Decision:**
جعل الـ AI وظيفة داخل الحل (AI Fit Analysis) وليس المنتج بأكمله، مع قواعد صريحة تمنع اختراع المهارات أو ضمان التوظيف.

**Why:**
مخرجات الـ AI يجب أن تكون موثوقة ومحدودة بالمعلومات المقدمة، وأن يُفهم أنها تقدير مساعد.

### Decision 3
**Decision:**
بناء التطبيق تدريجيًا عبر مراحل (Foundation ← Core Experience ← Opportunity Flow ← AI Analysis ← Review & Refine).

**Why:**
يقلل استهلاك الـ Credits ويتيح مراجعة النتيجة بعد كل مرحلة بدل إعادة بناء كل شيء.

---

## 🧪 Testing

### Test 1: Core User Flow
**Input:**
فتح التطبيق، ثم عرض الملف المهني وتعديل بعض بياناته، ثم استعراض الفرص الثلاث وفتح تفاصيل إحداها.

**Expected Result:**
ينتقل المستخدم بين الصفحات دون أخطاء، وتظهر التعديلات في الملف، وتُعرض تفاصيل الفرصة المختارة كاملة.

**Actual Result:**
اكتمل التنقل بين الصفحات وعملت التعديلات وعُرضت التفاصيل كما هو متوقع.

**Status:** ✅

### Test 2: AI Fit Analysis
**Input:**
اختيار فرصة والضغط على Analyze My Fit بملف مهني يحتوي مهارات ومشاريع.

**Expected Result:**
تظهر النتيجة في ثلاثة أقسام: Relevant Skills وPotential Gaps وRecommended Next Steps، دون مهارات مخترعة غير موجودة في الملف.

**Actual Result:**
ظهرت النتيجة بالأقسام الثلاثة. لكل مهارة ذُكر الدليل من الملف (Evidence) وسبب ارتباطها بالفرصة (Relevance)، وعُرضت الفجوات بسبب غياب معلومات عنها في الملف، ونبّه التحليل إلى أن الملف التجريبي (Alex Sample) يحتاج إلى تأكيد بياناته قبل استخدامه.

**Status:** ✅

---

## 📸 Evidence

🔗 [View Home Page](./Screenshots/Home.png)

🔗 [View My Profile Page](./Screenshots/Profile.png)

🔗 [View Opportunities Page](./Screenshots/Opportunities.png)

🔗 [View Opportunity Details Page](./Screenshots/Opportunity-Details.png)

🔗 [View Analyze My Fit Page](./Screenshots/Analyze-My-Fit.png)

🔗 [View AI Fit Analysis Result](./Screenshots/AI-Analysis.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- الواجهة قد تعرض نتيجة AI تبدو حقيقية بينما تكون بيانات تجريبية ثابتة، والتمييز بين الاثنين يحتاج تحققًا.
- تعديلات الملف المهني دون قاعدة بيانات تحتاج قرارًا واضحًا حول مكان الحفظ.
- التعديلات الصغيرة قد تستهلك Credits إذا لم تكن التعليمات محددة.

**How did I solve it?**

- راجعت ما بناه Lovable ولم أفترض أن كل ما طلبته نُفّذ، وتحققت من الوظيفة الفعلية وليس المظهر فقط.
- حددت أسلوب حفظ التعديلات ضمن نطاق الـ MVP دون إضافة Backend.
- كتبت تعليمات محددة لكل مرحلة وتجنبت إعادة بناء التطبيق كاملًا.

---

## 📚 What I Learned

### Technical Lesson
كيف أحوّل Specification إلى تعليمات تدريجية لـ Lovable، وأفرّق بين البيانات المعروضة والبيانات المحفوظة فعلًا.

### Problem-Solving Lesson
تحديد ما لن أبنيه لا يقل أهمية عن تحديد ما سأبنيه؛ فالنطاق الصغير الواضح يجعل الحل قابلًا للإنجاز والمراجعة.

### AI Lesson
الذكاء الاصطناعي ينفّذ ما أحدده له، لكن مسؤولية التصميم والمراجعة والتحقق تبقى عليّ. نجاح البناء لا يعني أن التطبيق صحيح.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إضافة تسجيل الدخول وحفظ الملف المهني في قاعدة بيانات ليتاح من أي جهاز.
- السماح للمستخدم بإضافة فرصة مهنية بنفسه (لصق وصف وظيفة) بدل الفرص الجاهزة.
- حفظ التحليلات السابقة للمقارنة بين الفرص ومتابعة تحسّن الملف.

---

## 🔗 Project Links

**Live Demo:** [pixel-perfect-playbook-530.lovable.app](https://pixel-perfect-playbook-530.lovable.app/)

**Repository:** [github.com/lilian2005-ui/SkillBridge-Lite](https://github.com/lilian2005-ui/SkillBridge-Lite)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
