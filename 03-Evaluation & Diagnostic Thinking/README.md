# U3 — PROVE IT WORKS

## Quality Thinking

> Building a solution is not the same as proving it works.

في هذه الوحدة، أنتقل من بناء الحل إلى التحقق من جودته.

أتعلم كيف أصمم اختبارات مناسبة، وأتحقق من النتائج المتوقعة والفعلية، وأكشف الأخطاء والحالات التي قد لا يتعامل معها النظام بالشكل الصحيح.

الهدف هو الانتقال من الانطباع بأن الحل يعمل إلى امتلاك أدلة تدعم هذا الاستنتاج.

---

## 🎯 Capability

**Quality Thinking**

القدرة على التحقق من سلوك النظام وجودة مخرجاته باستخدام الاختبارات والأدلة والتحليل المنهجي للأخطاء.

---

## 🧠 What I Learned

- **Testing Strategy:** تحديد ما الذي يجب اختباره: البيانات، والصلاحيات، والوظائف الأساسية، ومخرجات الذكاء الاصطناعي.
- **Test Cases:** تصميم حالات اختبار تمثل استخدامات مختلفة، صحيحة (Positive) وغير صحيحة (Negative).
- **Expected vs. Actual Results:** مقارنة النتائج المتوقعة بالنتائج الفعلية، وتسجيل الاختلاف بدل افتراض أن الوظيفة تعمل.
- **Edge Cases:** اختبار الحالات غير المعتادة أو التي تقع عند حدود السلوك المتوقع، مثل خطة بلا مهام أو رابط تأكيد منتهي الصلاحية.
- **Failure Analysis:** تحليل أسباب الإخفاق والوصول إلى السبب الجذري (Root Cause).
- **Iteration:** تحسين الحل بناءً على نتائج الاختبارات ثم إعادة الاختبار.
- **Evidence-Based Evaluation:** توثيق الأدلة (Screenshots وتقارير أدوات الفحص وسياسات قاعدة البيانات) التي تدعم تقييم النظام.

---

## 🛠️ Projects

### 01 — Guided Project

**Project:** TaskBridge — Work Planning Web Application

أختبر حلًا عمليًا باستخدام حالات اختبار محددة، وأوثق النتائج وأحدد جوانب التحسين.

- **System Under Test:** تطبيق ويب لتحويل طلبات العمل غير الواضحة إلى خطط ومهام، مبني بـ Lovable وSupabase.
- **Testing Focus:** إدارة الخطط والمهام (CRUD)، وحساب نسبة الإنجاز، وحفظ البيانات، وعزل بيانات المستخدمين عبر RLS، والمصادقة.
- **Tools:** Recus · Supabase Dashboard · Manual Testing
- **Result:** نجحت الاختبارات الأساسية، ونجح 71 من 82 فحصًا آليًا في Recus، ووُثّقت 4 مشكلات مع أسبابها وخطورتها.

[Explore the Project](./Course-Project/)

### 02 — Independent Project

**Project:** ContentFlow AI — AI-Powered Social Content Generation

أطبق منهجية الاختبار على حل مستقل، وأوثق حالات النجاح والفشل والتحسينات التي أجريتها.

- **System Under Test:** منصة لتوليد محتوى التواصل الاجتماعي من هوية العلامة، مبنية بـ v0 وNext.js وSupabase وGoogle Gemini.
- **Testing Focus:** إنشاء الحساب وتأكيد البريد، وإنشاء العلامة واستخراج ألوانها من الشعار، وتوليد المحتوى.
- **Tools:** Manual Testing · Supabase Auth
- **Result:** نجح التسجيل والدخول، ونجح استخراج الألوان جزئيًا، ولم يكتمل توليد المحتوى في النسخة الحالية؛ والمشكلات موثقة وقيد الإصلاح.

[Explore the Project](./Independent-Project/)

---

## 🔍 Engineering Focus

1. ما السلوك الذي يجب أن يحققه النظام؟
2. كيف يمكنني التحقق من هذا السلوك؟
3. ما الحالات التي قد يفشل فيها الحل؟
4. هل النتيجة الفعلية مطابقة للنتيجة المتوقعة؟
5. ما سبب الفشل الذي اكتشفته؟
6. هل أدى التعديل إلى تحسين يمكن إثباته؟

---

## 📌 Key Takeaway

**A working demonstration is useful. Repeatable tests and documented evidence provide stronger confidence.**

عرض ناجح واحد لا يكفي دائمًا؛ الاختبارات الموثقة والأدلة تساعد على تقييم النظام بصورة أفضل.

---

## 📈 Capability Progress

- [x] تحديد نطاق الاختبار.
- [x] إعداد Test Cases.
- [x] تحديد Expected Results.
- [x] توثيق Actual Results.
- [x] اختبار الحالات غير المعتادة.
- [x] تحليل الأخطاء.
- [ ] توثيق التحسينات ونتائج إعادة الاختبار.

---

## 🔗 Related Projects

- [Guided Project](./Course-Project/)
- [Independent Project](./Independent-Project/)

---

**Next:** U4 — GROUND ITS KNOWLEDGE
