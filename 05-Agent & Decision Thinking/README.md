<div dir="rtl">

# U5 — CONTROL ITS AGENCY

## Agent & Decision Thinking

> The goal is not maximum autonomy. The goal is controlled, purposeful, and verifiable autonomy.

في هذه الوحدة، أنتقل إلى سؤال جديد: متى نسمح للذكاء الاصطناعي أن يقرر بنفسه؟

أتعلم كيف أصمم AI Agent يمتلك القدر المناسب من الاستقلالية لتحقيق هدف محدد، ويتخذ قرارات مفيدة، وينفذ إجراءات مسموح بها، ويتوقف عندما ينبغي له التوقف، مع إمكانية تقييم سلوكه وتحسينه.

---

## 🎯 Capability

**Agent & Decision Thinking**

القدرة على تحديد متى نحتاج إلى Agent، وتصميم مسؤوليته وحدوده وطريقة اتخاذه للقرار، والتحكم في صلاحياته، وتقييم نتائجه وسلوكه.

---

## 🧠 What I Learned

- **Choose:** التمييز بين Workflow وAI-Powered Workflow وAI Agent، واختيار أبسط بنية تحقق الهدف (Minimum Necessary Agency).
- **Define:** كتابة Agent Contract يحدد المسؤولية ومعايير النجاح والنطاق وحدود القرار، وما يفعله الـ Agent عند نقص المعلومات.
- **Decide:** تصميم Decision Loop (Observe → Interpret → Decide → Validate → Act)، وفهم أن القرار ليس إذنًا بالتنفيذ (Decision Is Not Authorization).
- **Act:** إعطاء الـ Agent الأدوات التي يحتاجها فقط، وتحديد الـ Context، والتمييز بين Memory (ما نحتفظ به) وState (أين وصلت المهمة).
- **Control:** تطبيق Least Privilege وGuardrails، وتحديد متى يحتاج الـ Agent إلى Human Approval أو Escalation، وتصميم Stop Conditions واضحة.
- **Evaluate:** تقييم النتيجة والسلوك ومسار القرارات (Trajectory)، واستخدام التقييم لتحسين التصميم بدل افتراض أن المشكلة في النموذج وحده.

---

## 🛠️ Projects

### 01 — Guided Project

**Project:** XYZ Real Estate AI Agent

أصمم Agent يجمع بيانات العملاء ويتخذ قرار الخطوة التالية ضمن حدود واضحة.

- **Agent Responsibility:** جمع بيانات عملاء شركة عقارات عبر Telegram بأي ترتيب، وتطبيق قواعد العمل، وحفظها في Google Sheets.
- **Control:** لا يُحفظ أي شيء إلا بعد تأكيد صريح من العميل على الملخص، مع التحقق من نتيجة الحفظ قبل إبلاغه.
- **Tools:** n8n · Telegram · OpenRouter · Simple Memory · Google Sheets
- **Result:** نجحت 3 اختبارات من 4 (أحدها بعد إصلاح إعداد الشيت)، وكشف اختبار التصحيح أن الملخص المعروض بعد تغيير الطلب لم يتحدث رغم حفظ البيانات الصحيحة.

[Explore the Project](./Course-project/)

### 02 — Independent Project

**Project:** Recruiter Matching Agent

أطبق تصميم الـ Agent على فكرتي الخاصة لمساعدة مسؤولي التوظيف.

- **Agent Responsibility:** جلب أحدث الوظائف عن بُعد، وتقييم المرشحين من 100 وفق Rubric ثابت، واقتراح الخطوة التالية.
- **Control:** الحالات الحدية (60 إلى 74) تُحوّل لإنسان، والملفات الناقصة تُعلَّم `Needs Review`، ولا يتواصل مع المرشحين ولا يتخذ قرار التوظيف، ويتجاهل العمر والجنس.
- **Tools:** n8n · Telegram · OpenRouter · Simple Memory · HTTP Request (Himalayas Jobs API)
- **Result:** المشروع في مرحلة البناء؛ عمل الرد على Telegram بعد إصلاح ربط Chat ID، وجلب الوظائف والتقييم لم يُختبرا بعد.

[Explore the Project](./Independent-Project/)

---

## 🔍 Engineering Focus

1. هل نحتاج إلى Agent أصلًا، أم يكفي Workflow؟
2. ما مسؤولية الـ Agent، وما الذي يقع خارج نطاقه؟
3. كيف يختار الخطوة التالية، وماذا يفعل عند نقص المعلومات؟
4. ما الأدوات والصلاحيات التي يحتاجها فعلًا؟
5. متى يحتاج إلى موافقة بشرية، ومتى يجب أن يتوقف؟
6. هل حقق الهدف وتصرف ضمن الحدود المحددة؟

---

## 📌 Key Takeaway

**Engineer the autonomy — don't just enable it.**

الـ Agent الجيد ليس الأكثر استقلالية، بل الذي يعرف ما يُسمح له به ومتى يتوقف. **Prompt guides behavior. System controls execution.**

---

## 📈 Capability Progress

- [x] اختيار البنية المناسبة (Workflow / AI-Powered Workflow / Agent).
- [x] تحديد مسؤولية الـ Agent ونطاقه وحدود قراراته.
- [x] تصميم آلية اتخاذ القرار والتعامل مع نقص المعلومات.
- [x] تحديد الأدوات والـ Memory والـ State.
- [x] تصميم الضوابط وشروط الموافقة والتوقف.
- [x] تقييم النتيجة والسلوك ومسار القرارات.
- [ ] تحسين التصميم وإعادة التقييم.

---

## 🔗 Related Projects

- [Guided Project](./Course-project/)
- [Independent Project](./Independent-Project/)

---

**Previous:** U4 — GROUND ITS KNOWLEDGE
**Next:** U6 — CONNECT IT TO THE WORLD

</div>
