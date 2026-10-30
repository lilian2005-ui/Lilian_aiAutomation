# TaskBridge

تطبيق ويب متجاوب يحوّل الأهداف وطلبات العمل غير الواضحة إلى خطط منظمة بمهام وأولويات وحالات تنفيذ، مع حفظ دائم للبيانات وعزل لبيانات كل مستخدم عبر Row Level Security.

---

## 🎯 Problem

### The Context
المستقلون والخريجون الجدد والمهنيون في بداية مسيرتهم يتلقون أهدافًا وطلبات عمل بصيغ عامة، ويحتاجون إلى تنظيمها ومتابعتها.

### The Problem
قد يعرف الشخص ما يريد تحقيقه، لكنه لا يعرف كيف يحوّله إلى خطوات عملية: ما النتيجة المطلوبة؟ ما المهام اللازمة؟ بماذا يبدأ؟ ما الذي أُنجز وما الذي لا يزال قيد التنفيذ؟ وما الخطوة التالية؟

### Why It Matters
غياب خطة واضحة يصعّب تنظيم العمل وتحديد الأولويات ومتابعة الإنجاز. وجود مساحة واحدة تربط الهدف بالمهام وحالاتها ونسبة الإنجاز يجعل التقدم مرئيًا وقابلًا للمتابعة.

---

## 💡 Solution

مساحة منظمة لإدارة الخطط والمهام، تعتمد التسلسل: **Goal → Plan → Tasks → Priorities → Status → Progress**.

**What does the system do?**

1. ينشئ حسابًا ويسجّل الدخول عبر Supabase Auth.
2. ينشئ المستخدم خططه ويعدّلها ويحذفها (title, description, goal, deadline).
3. يضيف المهام داخل كل خطة ويحدد Priority (High / Medium / Low) وStatus (To Do / In Progress / Done).
4. يحسب نسبة الإنجاز: `Completed Tasks ÷ Total Tasks × 100`، وتكون 0% إذا لم تحتوِ الخطة على مهام.
5. يحفظ البيانات في PostgreSQL فتبقى بعد تحديث الصفحة أو إعادة تسجيل الدخول.
6. يعزل البيانات بحيث يرى كل مستخدم سجلاته فقط.

---

## 👤 Users

**Primary Users:**
Freelancers وRecent Graduates وEarly-Career Professionals والأفراد الذين يحتاجون إلى تنظيم أهدافهم. النسخة الأولى للاستخدام الفردي دون تعاون بين عدة مستخدمين.

**User Need:**
تحويل هدف غير واضح إلى مهام مرتبة بأولويات وحالات، ومعرفة مقدار ما أُنجز في أي لحظة.

---

## 🧠 How I Designed the Solution

اعتمدت مبدأ **Build the System, Not the Screen**: بدأت بتصميم البيانات والعلاقات وسياسات الأمان قبل الواجهة، ثم بنيت التطبيق على مراحل: إعداد Supabase، ثم ربط Lovable به، ثم بناء الواجهة، ثم تنفيذ الوظائف، ثم الاختبار والتحسين.

العلاقة الأساسية في النظام: **User → Plans → Tasks**

- يمتلك المستخدم عدة خطط، وتحتوي الخطة على عدة مهام، وتنتمي كل مهمة إلى خطة واحدة.
- يجب أن يكون مالك المهمة هو نفسه مالك الخطة.
- يؤدي حذف الخطة إلى حذف مهامها.
- تُفرض قيم Priority وStatus المسموح بها في قاعدة البيانات، وليس في الواجهة فقط.

---

## ⚙️ How It Works

```text
User signs up / logs in (Supabase Auth)
              ↓
My Plans: only the user's own plans (RLS)
              ↓
Create / Edit Plan: title, description, goal, deadline
              ↓
Plan Details: add and update tasks (priority, status)
              ↓
Progress = Completed Tasks ÷ Total Tasks × 100
              ↓
Saved in PostgreSQL: persists after refresh and re-login
```

---

## 🤖 Role of AI

**What does AI do in this solution?**

- دور الذكاء الاصطناعي في بناء التطبيق وليس داخله: استخدمت Lovable (AI App Builder) لتنفيذ التطبيق وفق مواصفات وملف تصميم قاعدة البيانات.
- راجعت ما بُني بدل افتراض أنه صحيح، وتحققت من الوظائف والبيانات والصلاحيات فعليًا.

### What AI Should NOT Do

- لا يوجد توليد خطط بالذكاء الاصطناعي داخل التطبيق في النسخة الأولى؛ هذا خارج النطاق.
- لا يُعتبر اقتراح AI للإصلاح دليلًا على نجاحه؛ يجب إعادة الاختبار.
- لا تُشارك معه مفاتيح أو بيانات مستخدمين حساسة.

---

## 🔄 Automation

**What parts of the process are automated?**

- إعادة حساب نسبة الإنجاز عند تغيير حالة أي مهمة.
- ربط كل خطة ومهمة بالمستخدم المصادق عليه.
- حذف المهام تلقائيًا عند حذف الخطة.
- تطبيق القيم الافتراضية وتحديث تواريخ الإنشاء والتعديل.

---

## 🗂️ Data

### Input
بيانات الحساب، ومعلومات الخطة (title, description, goal, deadline)، والمهام (title, description, priority, status).

### Output
قائمة خطط المستخدم، وتفاصيل كل خطة بمهامها، ونسبة الإنجاز.

| Table | Purpose |
|---|---|
| `plans` | بيانات الخطط: id, user_id, title, description, goal, deadline, deliverables, next_step, created_at, updated_at |
| `plan_tasks` | المهام التابعة للخطط: id, plan_id, user_id, title, description, priority, status, sort_order, created_at |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Lovable | بناء التطبيق باستخدام AI App Builder |
| Supabase Auth | المصادقة وإدارة حسابات المستخدمين |
| Supabase PostgreSQL | تخزين الخطط والمهام |
| Supabase RLS | التحكم في الوصول إلى البيانات |
| GitHub | توثيق المشروع وإدارة ملفاته |
| Recus | اختبار آلي للتطبيق عبر المتصفح (AI-Assisted Browser Testing) |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
فرض الصلاحيات على مستوى قاعدة البيانات باستخدام RLS على جدولي `plans` و`plan_tasks`.

**Why:**
إخفاء البيانات أو الأزرار من الواجهة لا يحمي البيانات. يجب أن تمنع قاعدة البيانات نفسها وصول مستخدم إلى سجلات غيره.

### Decision 2
**Decision:**
اشتراط تطابق مالك المهمة مع مالك الخطة، وحذف المهام عند حذف الخطة.

**Why:**
يحافظ على Data Integrity ويمنع إنشاء مهمة مرتبطة بخطة يملكها مستخدم آخر.

### Decision 3
**Decision:**
عدم استخدام مفتاح `service_role` في الواجهة الأمامية أو رفعه إلى GitHub.

**Why:**
هذا المفتاح يتجاوز سياسات RLS، وكشفه يلغي الحماية.

### Decision 4
**Decision:**
نطاق أولي محدد: بدون توليد خطط بالـ AI أو تعاون أو مدفوعات.

**Why:**
التركيز على جودة الوظائف الأساسية والتحقق منها قبل إضافة قدرات جديدة.

---

## 🧪 Testing

اختبرت التطبيق الفعلي وليس الواجهة فقط، بحالات صحيحة (Positive) وغير صحيحة (Negative)، واستخدمت حسابين مختلفين للتحقق من عزل البيانات.

### Test Coverage

| Area | What is verified | Status | Evidence |
|---|---|---|---|
| Authentication | إنشاء حساب، تسجيل الدخول والخروج، حماية الصفحات الخاصة | ✅ | [Sign-in Page](./Screenshots/Auth.png) |
| Plan Management | إنشاء الخطة واستعراضها وتعديلها وحذفها | ✅ | [My Plans](./Screenshots/Progress-40.png) |
| Task Management | إضافة المهمة وتعديلها وحذفها وتغيير الأولوية والحالة | ✅ | [Plan Tasks](./Screenshots/Plan-Details.png) |
| Progress & Persistence | نسبة الإنجاز، وبقاء البيانات بعد التحديث وإعادة الدخول | ✅ | [Progress 40%](./Screenshots/Progress-40.png) · [Progress 0%](./Screenshots/Progress-0.png) |
| Security & Isolation | منع الوصول إلى بيانات مستخدم آخر | ✅ | [B's Plan URL](./Screenshots/Isolation-B-Plan-URL.png) · [RLS Policies](./Screenshots/RLS-Policies.png) |
| Automated QA (Recus) | فحص آلي للصفحات والتفاعلات والمسارات | ⚠️ 71 / 82 | [Recus Summary](./Screenshots/Recus-Summary.png) · [Recus Issues](./Screenshots/Recus-Issues.png) |

**ما لم يُختبر:** محاولة تعديل أو حذف بيانات مستخدم آخر، أو إضافة مهمة داخل خطته، عبر طلبات مباشرة إلى قاعدة البيانات. اختبرت القراءة من الواجهة، وتغطي سياسات RLS الظاهرة في الصورة باقي العمليات.

### Test 1: Progress calculation
**Input:**
خطة تحتوي خمس مهام، ثم تغيير حالة مهمتين إلى Done، ثم إعادة إحداهما إلى In Progress، وكذلك فحص خطة بلا مهام.

**Expected Result:**
تظهر النسبة 40% عند اكتمال مهمتين من خمس، وتنخفض إلى 20% عند إعادة إحداهما، وتظهر 0% للخطة التي لا تحتوي مهام.

**Actual Result:**
ظهرت النسبة 40% (2 of 5 tasks done) عند اكتمال مهمتين من خمس ([Progress 40%](./Screenshots/Progress-40.png))، وانخفضت إلى 20% بعد إعادة إحداهما إلى In Progress، وظهرت 0% (0 of 0 tasks done) في الخطة قبل إضافة أي مهمة ([Progress 0%](./Screenshots/Progress-0.png)).

**Status:** ✅

### Test 2: Data isolation between two users
**Input:**
تسجيل الدخول بالمستخدم A ومراجعة قائمة خططه، ثم محاولة فتح رابط خطة يملكها المستخدم B مباشرة، ومراجعة سياسات RLS على جدولي `plans` و`plan_tasks` في Supabase.

**Expected Result:**
لا تعرض قائمة A أي خطة تخص B، ولا يعرض رابط خطة B أي بيانات، وتكون RLS مفعّلة على الجدولين مع سياسات تحصر الوصول بصاحب السجل.

**Actual Result:**
لم تظهر خطط B في قائمة A، ولم يعرض رابط خطة B أي بيانات عند فتحه بحساب A ([B's Plan URL](./Screenshots/Isolation-B-Plan-URL.png))، وظهرت RLS مفعّلة على الجدولين مع سياسات تقيّد الوصول بمالك السجل ([RLS Policies](./Screenshots/RLS-Policies.png)).

**Status:** ✅

### Test 3: Automated QA with Recus
**Input:**
جلسة اختبار آلية باستخدام Recus على `taskbridge-ai.lovable.app` تفحص الصفحات والتفاعلات والمسارات الأساسية.

**Expected Result:**
نجاح المسارات الأساسية، وكشف أي مشكلات ظاهرة في الواجهة أو في التحقق من المدخلات.

**Actual Result:**
نفّذ Recus 82 فحصًا: نجح 71 وظهرت 11 مشكلة، منها التعامل غير المتسق مع المسافات قبل الإيميل وبعده (Validation, Medium priority) ([Recus Summary](./Screenshots/Recus-Summary.png) · [Recus Issues](./Screenshots/Recus-Issues.png)).

**Status:** ⚠️ 71 / 82 Passed

---

## 📸 Evidence

**Application & Test Results**

- 🔗 [View Sign-in Page](./Screenshots/Auth.png)
- 🔗 [View Plan Tasks (priority and status)](./Screenshots/Plan-Details.png)
- 🔗 [View My Plans at 40% Progress](./Screenshots/Progress-40.png)
- 🔗 [View Plan with No Tasks (0%)](./Screenshots/Progress-0.png)
- 🔗 [View Database Tables and RLS Policies](./Screenshots/RLS-Policies.png)
- 🔗 [View User B Plan URL Opened by User A](./Screenshots/Isolation-B-Plan-URL.png)

**Automated QA (Recus)**

- 🔗 [View Recus Session Summary](./Screenshots/Recus-Summary.png)
- 🔗 [View Recus Issues](./Screenshots/Recus-Issues.png)

**Issues**

- 🔗 [View Signup Error (Email Rate Limit)](./Screenshots/Signup-Rate-Limit.png)
- 🔗 [View Confirmation Email After the Limit Reset](./Screenshots/Signup-Confirmation-Email.png)
- 🔗 [View Expired Confirmation Link](./Screenshots/Email-Link-Expired.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- فشل إنشاء حساب جديد برسالة `email rate limit exceeded` رغم أنني أنشأت حسابًا واحدًا فقط في ذلك اليوم، وتظهر الرسالة التقنية الخام للمستخدم كما هي.
- عند فتح رابط تأكيد البريد بعد انتهاء صلاحيته، يعود التطبيق إلى الصفحة الرئيسية دون أي رسالة، ويظهر الخطأ (`otp_expired`) في عنوان الصفحة فقط.
- كشف فحص Recus الآلي 11 مشكلة من أصل 82 فحصًا، منها عدم التعامل بشكل متسق مع المسافات قبل الإيميل وبعده.

**How did I solve it?**

- **Email rate limit:** السبب الجذري أن خدمة البريد الافتراضية في Supabase لها حد منخفض جدًا لعدد رسائل التأكيد في الساعة، ويُحسب على المشروع كله (تأكيد التسجيل وإعادة الإرسال واسترجاع كلمة المرور والمحاولات السابقة) وليس على حساب واحد. انتظرت انتهاء فترة الحد، ثم نجح إرسال إيميل التأكيد من Supabase Auth. وللاستخدام الفعلي يُربط مزود بريد خاص (Custom SMTP).
- **الرسائل غير الواضحة ورابط التأكيد المنتهي:** المشكلة في Error Handling داخل الواجهة؛ والإصلاح عرض رسالة مفهومة وإتاحة إعادة إرسال رابط التأكيد، وهو مؤجل للإصدار القادم.
- **مشكلات Recus:** سجّلها Recus مع أولوية كل مشكلة، وتبقى مفتوحة إلى أن تُصلح ويُعاد تشغيل الفحص (Re-testing).

| Issue | Severity | Root Cause | Fix | Re-test |
|---|---|---|---|---|
| إنشاء الحساب يفشل بـ `email rate limit exceeded` | High | حد إرسال الإيميلات في خدمة البريد الافتراضية بـ Supabase | انتظار انتهاء الحد، وربط Custom SMTP للاستخدام الفعلي | ✅ وصل إيميل التأكيد |
| عرض رسالة الخطأ التقنية الخام للمستخدم | Medium | لا توجد معالجة واضحة لأخطاء المصادقة (Error Handling) | عرض رسالة مفهومة (مؤجل) | ⬜ Not Tested |
| رابط تأكيد منتهي يعيد إلى الصفحة الرئيسية دون رسالة | Medium | الواجهة لا تقرأ الخطأ من الرابط ولا تعرضه | عرض رسالة وإتاحة إعادة إرسال الرابط (مؤجل) | ⬜ Not Tested |
| 11 مشكلة من فحص Recus، مثل المسافات حول الإيميل | Medium | قواعد تحقق ناقصة في بعض المدخلات (Validation) | معالجتها حسب الأولوية (مؤجل) | ⬜ Not Tested |

---

## 📚 What I Learned

### Technical Lesson
نجاح الحفظ وظهور البيانات لا يثبتان صحتها: يجب التحقق من Persistence وIntegrity، ومن أن RLS تعمل ضمن سياق المستخدم العادي وليس من حساب إداري.

### Problem-Solving Lesson
عند فشل الاختبار لا أعدّل عشوائيًا: أجمع الأدلة، وأبحث عن السبب الجذري، وأطبق الإصلاح، ثم أعيد الاختبار وأتحقق من عدم ظهور مشكلات جديدة.

### AI Lesson
**AI can suggest. Evidence must verify.** يبني الذكاء الاصطناعي بسرعة، لكن الجودة تثبتها الاختبارات والأدلة.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إضافة توليد خطة أولية بالذكاء الاصطناعي من وصف الهدف بلغة طبيعية، مع تقييم مخرجاتها من حيث الوضوح والاكتمال والواقعية.
- ربط التطبيق بمنصات أتمتة لنقل البيانات أو تنفيذ إجراءات تلقائيًا.
- دراسة تحويله إلى Progressive Web App لتجربة أقرب إلى التطبيقات المثبتة.
- ربط Custom SMTP وعرض رسائل خطأ مفهومة للمستخدم عند فشل المصادقة أو انتهاء رابط التأكيد.
- إصلاح المشكلات التي كشفها Recus ثم إعادة تشغيل الفحص للتحقق من الإصلاح وعدم ظهور مشكلات جديدة.
- إضافة اختبارات Negative مباشرة على قاعدة البيانات (تعديل وحذف وإنشاء مهمة داخل خطة مستخدم آخر).

---

## 🔗 Project Links

**Live Demo:** [taskbridge-ai.lovable.app](https://taskbridge-ai.lovable.app)

**Repository:** [github.com/lilian2005-ui/Lilian_aiAutomation](https://github.com/lilian2005-ui/Lilian_aiAutomation)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
