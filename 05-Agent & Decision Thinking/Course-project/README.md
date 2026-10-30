
<div dir="rtl">

# XYZ Real Estate AI Agent

> AI Agent على Telegram يجمع بيانات عملاء شركة عقارات بالتدريج، ويطبق قواعد العمل، ولا يحفظ البيانات في Google Sheets إلا بعد تأكيد العميل الصريح على الملخص النهائي.

---

## 🎯 Problem

### The Context
تستقبل شركة XYZ Real Estate طلبات من عملاء يرغبون في شراء عقارات أو استئجارها، ويحتاج فريق الشركة إلى معلومات أساسية عن كل عميل لفهم احتياجاته ومتابعته.

### The Problem
جمع هذه المعلومات يدويًا عبر المحادثات يستهلك وقت الفريق. العملاء يقدمون المعلومات بترتيب مختلف، وأحيانًا في رسالة واحدة، وأحيانًا بإجابات غامضة أو ناقصة، فيصعب تنظيمها وضمان صحتها.

### Why It Matters
بيانات العميل المكتملة والصحيحة هي أساس المتابعة. أتمتة جمعها مع ضبط ما يُحفظ ومتى يُحفظ يوفر وقت الفريق ويمنع حفظ معلومات خاطئة أو غير مؤكدة.

---

## 💡 Solution

AI Agent يدير المحادثة مع العميل على Telegram: يفهم ما يقدمه، ويحدد المعلومات الناقصة، ويتحقق من الإجابات، ثم يعرض ملخصًا ويحفظ البيانات بعد تأكيد العميل فقط.

**What does the system do?**

1. يستقبل رسائل العميل عبر Telegram ويرحب به ويبدأ المحادثة.
2. يفهم المعلومات حتى لو وردت بأي ترتيب أو عدة معلومات في رسالة واحدة، ويحتفظ بسياق المحادثة.
3. يسأل عن الحقول الناقصة فقط، ويطلب التوضيح عند الغموض، ويطبق القواعد الشرطية (Rent ← `Not Applicable`).
4. يعرض ملخصًا بالحقول التسعة ويطلب التأكيد، ثم يحفظ البيانات في Google Sheets ويتحقق من نتيجة الحفظ قبل إبلاغ العميل.

---

## 👤 Users

**Primary Users:**
عملاء الشركة الذين يتواصلون عبر Telegram، وفريق المبيعات الذي يستلم البيانات في Google Sheets.

**User Need:**
العميل يريد تقديم طلبه بسهولة وبأسلوب محادثة طبيعي، والفريق يريد بيانات مكتملة وصحيحة ومؤكدة لكل عميل.

---

## 🧠 How I Designed the Solution

صممت الـ Agent وفق طبقات U5 قبل بنائه في n8n:

- **Choose:** اخترت Agent بدل Workflow ثابت، لأن المعلومات تصل بأي ترتيب، وقد يقدم العميل عدة معلومات أو يغيّر إجابته، فيحتاج النظام إلى تحديد الخطوة التالية في كل رسالة.
- **Define:** مسؤوليته جمع بيانات العميل التسع والتحقق منها وحفظها بعد التأكيد. خارج نطاقه: اقتراح عقارات أو أسعار أو تقديم وعود للعميل.
- **Decide:** في كل رسالة يحدد: هل يسأل عن معلومة ناقصة، أم يطلب توضيحًا، أم يعرض الملخص، أم يحفظ.
- **Act:** أداة واحدة فقط هي Google Sheets لإضافة صف، لأنها كل ما تحتاجه المهمة (Least Privilege).
- **Control:** الحفظ مشروط باكتمال البيانات وصحتها وتأكيد العميل الصريح.
- **Evaluate:** راجعت النتيجة والسلوك معًا: هل حفظ البيانات الصحيحة؟ وهل احترم شرط التأكيد؟ عبر سجل تنفيذ n8n ومحتوى الشيت.

**Memory vs. State:**
- **Memory:** Simple Memory بـ Session ID ثابت لكل محادثة، حتى لا تختلط بيانات العملاء.
- **State:** `collecting_information` ← `awaiting_confirmation` ← `saved`

</div>

<div dir="ltr">

```text
Telegram Trigger (customer message)
              ↓
AI Agent + Simple Memory (session per chat)
              ↓
Missing or unclear info? → Ask the customer
              ↓
All 9 fields valid → Show summary → Ask for confirmation
              ↓
Explicit confirmation → Google Sheets Tool (append row)
              ↓
Check the save result
              ↓
Telegram Send Message (success or failure)
```

</div>

<div dir="rtl">

---

## 🤖 Role of AI

**What does AI do in this solution?**

- يفهم رسائل العميل ويستخرج منها قيم الحقول التسعة.
- يحدد المعلومات الناقصة ويختار السؤال التالي.
- يصنّف الميزانية ضمن الفئات المحددة، ويطبق القواعد الشرطية.
- يقرر متى يعرض الملخص ومتى يستخدم أداة الحفظ.

### What AI Should NOT Do

- اختراع معلومات لم يقدمها العميل، أو تخمين إجابة غامضة.
- حفظ البيانات لمجرد اكتمالها دون تأكيد صريح من العميل.
- إخبار العميل بنجاح الحفظ إذا فشلت أداة Google Sheets.

---

## 🔄 Automation

**What parts of the process are automated?**

- استقبال الرسائل والرد عليها عبر Telegram.
- جمع المعلومات وتنظيمها والتحقق منها.
- إضافة صف بيانات العميل إلى Google Sheets بعد التأكيد.

---

## 🗂️ Data

### Input
رسائل العميل النصية عبر Telegram.

### Output
صف جديد في جدول `XYZ Real Estate Leads` (ورقة `Leads`) يحتوي الحقول التسعة بالترتيب: Property type, Buy/Rent, New/Resale, First Ourcase, Timeline, Budget, Name, Email, Phone Number.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| n8n | بناء الـ Workflow وتشغيل الـ Agent |
| Telegram Bot | استقبال رسائل العميل وإرسال الردود |
| AI Agent (n8n) | فهم الرسائل واتخاذ قرار الخطوة التالية |
| OpenRouter Chat Model | نموذج اللغة لمعالجة الرسائل وصياغة الردود |
| Simple Memory | الاحتفاظ بسياق كل محادثة |
| Google Sheets | حفظ بيانات العملاء المؤكدة |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
استخدام AI Agent بدل Workflow ثابت.

**Why:**
ترتيب المعلومات وطريقة تقديمها غير ثابتين، والنظام يحتاج إلى تحديد السؤال أو الإجراء التالي حسب ما قدّمه العميل حتى الآن.

### Decision 2
**Decision:**
الحفظ مشروط بتأكيد صريح من العميل على الملخص، والتحقق من النتيجة في سجل تنفيذ n8n ومحتوى الشيت.

**Why:**
**Decision is not authorization.** أن يقرر الـ Agent أن البيانات مكتملة لا يعني أنه مسموح له بالحفظ؛ التأكيد هو الشرط.

### Decision 3
**Decision:**
Session ID ثابت لكل محادثة في Simple Memory.

**Why:**
يمنع اختلاط بيانات عميلين يتحدثان مع النظام في الوقت نفسه.

### Decision 4
**Decision:**
تطبيق القواعد الشرطية: عند Rent لا يُسأل عن New/Resale وFirst Ourcase وتُحفظ قيمتهما `Not Applicable`.

**Why:**
تقليل الأسئلة غير الضرورية وضمان اتساق البيانات المحفوظة.

---

## 🧪 Testing

### Test 1: Context, missing fields, and unclear answers
**Input:**
محادثة شراء: يذكر العميل نوع العقار ونوع الطلب والميزانية، ثم يرسل إجابة غير دقيقة ("release property" بدل resale).

**Expected Result:**
يحتفظ الـ Agent بالمعلومات السابقة ولا يكرر السؤال عنها، ويسأل عن الحقل الناقص التالي فقط، ويطلب التوضيح عند الإجابة غير الواضحة بدل التخمين.

**Actual Result:**
لخّص الـ Agent ما جمعه (Apartment, Buy, $200,000 to below $400,000) وسأل فقط عن New/Resale، وعند "release property" طلب تأكيد أن المقصود Resale قبل الانتقال إلى السؤال التالي ([Conversation 1](./Screenshots/Telegram-Conversation-1.png) · [Conversation 2](./Screenshots/Telegram-Conversation-2.png)).

**Status:** ✅

---

### Test 2: Summary, confirmation, and saving
**Input:**
اكتمال الحقول التسعة في محادثة الشراء، ثم تأكيد العميل على الملخص.

**Expected Result:**
يعرض الـ Agent ملخصًا بالحقول التسعة ويطلب التأكيد، وبعد التأكيد يُضاف صف مطابق للملخص في الأعمدة المحددة.

**Actual Result:**
عرض الـ Agent الملخص بالحقول التسعة وطلب التأكيد ([Summary](./Screenshots/Summary-Confirmation.png))، وبعد التأكيد أُضيف الصف إلى الشيت ([Sheet Rows](./Screenshots/Sheet-Rows.png)). كشف التشغيل الأول أن قيمة Timeline لم تُحفظ لأن عنوان العمود E كان `First Ourcase` بدل `Timeline`، وأن الصفر حُذف من بداية رقم الهاتف. بعد تصحيح عنوان العمود وتنسيق عمود الهاتف كنص، أصبحت البيانات تُحفظ بشكل صحيح.

**Status:** ✅ (بعد الإصلاح)

---

### Test 3: Rent conditional rule
**Input:**
محادثة استئجار (Rent) حتى التأكيد والحفظ.

**Expected Result:**
لا يسأل الـ Agent عن New/Resale وFirst Ourcase، ويحفظ قيمتهما `Not Applicable`.

**Actual Result:**
حُفظ صف الاستئجار والقيمة `Not Applicable` في New/Resale وFirst Ourcase ([Sheet Rows](./Screenshots/Sheet-Rows.png)).

**Status:** ✅

---

### Test 4: Correcting an answer (Buy → Rent)
**Input:**
بعد اكتمال البيانات، يغيّر العميل طلبه من شراء إلى إيجار ثم يؤكد.

**Expected Result:**
يحدّث الـ Agent البيانات، ويعرض ملخصًا جديدًا فيه `Not Applicable` في New/Resale وFirst Ourcase، ويحفظ البيانات المحدثة بعد التأكيد.

**Actual Result:**
حدّث الـ Agent الطلب إلى Rent وحُفظت القيمة `Not Applicable` في الحقلين بشكل صحيح في الشيت ([Sheet Rows](./Screenshots/Sheet-Rows.png)). لكن الملخص الذي عرضه للعميل بعد التحديث ظل يذكر "Resale" و"نعم" في هذين الحقلين، رغم أن رسالته نفسها تقول إنهما أصبحا غير قابلين للتطبيق ([Correction](./Screenshots/Correction-Rent.png)).

**Status:** ⚠️ Partially Passed

---

## 📸 Evidence

- 🔗 [View n8n Workflow](./Screenshots/Workflow.png)
- 🔗 [View Telegram Conversation (Part 1)](./Screenshots/Telegram-Conversation-1.png)
- 🔗 [View Telegram Conversation (Part 2)](./Screenshots/Telegram-Conversation-2.png)
- 🔗 [View Summary and Confirmation](./Screenshots/Summary-Confirmation.png)
- 🔗 [View Correction from Buy to Rent](./Screenshots/Correction-Rent.png)
- 🔗 [View Saved Rows in Google Sheets](./Screenshots/Sheet-Rows.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- لم تُحفظ قيمة Timeline، لأن عنوان العمود E في الشيت مكتوب `First Ourcase` بدل `Timeline`، فكُتبت قيمة First Ourcase في عمودين.
- يُحذف الصفر من بداية رقم الهاتف لأن Google Sheets يتعامل معه كرقم.
- بعد تغيير الطلب من شراء إلى إيجار، عرض الـ Agent ملخصًا غير متسق: البيانات المحفوظة صحيحة (`Not Applicable`)، لكن الملخص المعروض للعميل ظل يذكر القيم القديمة.
- الاعتماد على الـ System Prompt وحده لا يضمن تمامًا ألا يستدعي الـ Agent أداة الحفظ قبل التأكيد.
- n8n Cloud يعمل بفترة تجريبية، فلا يوجد رابط عام دائم للـ Workflow.

**How did I solve it?**

- **السبب الجذري لمشكلة Timeline** في إعداد الشيت وليس في الـ Agent: الملخص عرض الإطار الزمني بشكل صحيح (1–3 أشهر). صحّحت عنوان العمود E إلى `Timeline` وربطته بالقيمة الصحيحة في أداة Google Sheets.
- **رقم الهاتف:** نسّقت عمود Phone Number كنص (Plain text) فأصبح الرقم يُحفظ كما أدخله العميل.
- **الملخص بعد التصحيح:** تعديل الـ System Prompt بحيث يُعاد بناء الملخص من القيم المحدثة بعد أي تصحيح، وتطبيق قاعدة Rent على الملخص قبل عرضه وليس عند الحفظ فقط.
- كتبت شرط الحفظ بوضوح في الـ System Prompt، ووجّهت الـ Agent إلى طلب التوضيح بدل التخمين.
- وثّقت المشروع بصور الـ Workflow والمحادثة والشيت.

---

## 📚 What I Learned

### Technical Lesson
بناء Agent في n8n بربط Chat Model وMemory وTool بالـ AI Agent، والفرق بين Memory (ما نتذكره) وState (أين وصلت المهمة).

### Problem-Solving Lesson
ليست كل مشكلة تحتاج Agent؛ اخترته هنا لأن المحادثة تحتاج قرارًا في كل خطوة، مع إبقاء الاستقلالية في أضيق حد ممكن.

### AI Lesson
**Prompt guides behavior. System controls execution.** قرار الـ Agent لا يعني الإذن بالتنفيذ، ويجب تقييم سلوكه ومسار قراراته، لا النتيجة النهائية فقط.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إضافة شرط في الـ Workflow نفسه (IF Node) يمنع الحفظ ما لم تُسجّل حالة التأكيد، بدل الاعتماد على الـ Prompt.
- منع إضافة صف مكرر عند إعادة إرسال التأكيد للطلب نفسه.
- إرسال إشعار لفريق المبيعات عند إضافة عميل جديد.

---

## 🔗 Project Links

**Live Demo:** غير متاح (n8n Cloud بفترة تجريبية). راجع قسم Evidence.

**Workflow:** [Workflow Screenshot](./Screenshots/Workflow.png)

**Repository:** [github.com/lilian2005-ui/Lilian_aiAutomation](https://github.com/lilian2005-ui/Lilian_aiAutomation)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)

</div>
