# AI Client Intake & Request Routing System

نظام أتمتة يحوّل طلبات العملاء غير المنظمة إلى سجلات منظمة وموجّهة، ويحيل أي طلب ناقص أو غير واضح إلى المراجعة البشرية (Human Review).

---

## 🎯 Problem

### The Context
شركة خدمات تقدم حلولًا مثل تصميم المواقع والتسويق الرقمي وتطوير التطبيقات، وتستقبل طلبات من عملاء محتملين عبر نماذج إلكترونية. كل عميل يكتب طلبه بطريقته؛ بعضهم يشرح احتياجه بالتفصيل، وبعضهم يرسل رسالة قصيرة، وبعضهم ينسى معلومات مهمة.

### The Problem
كل طلب يحتاج إلى موظف يقرأه ويفهم الاحتياج وينظّم التفاصيل ويتحقق من وضوح المعلومات واكتمالها، ثم يحدد الخطوة التالية. ومع زيادة عدد الطلبات يتأخر التواصل مع العملاء وتضيع بعض التفاصيل.

### Why It Matters
المشكلة ليست في استقبال الرسائل فقط، بل في طريقة معالجة الطلبات وتنظيمها وتوجيهها. تقليل هذا العمل المتكرر يوفّر وقت الفريق، ويضمن ألا يُنسى أي طلب أو يُعالج بشكل خاطئ.

---

## 💡 Solution

سير عمل آلي (Automation Workflow) يستقبل كل طلب، ويستخدم الذكاء الاصطناعي لاستخراج التفاصيل المهمة، ويتحقق من كفاية المعلومات، ثم يوجّه الطلب وفق قواعد واضحة، ويسجل النتيجة ويُشعر الفريق. أما الطلبات الناقصة أو غير الواضحة فتبقى للمراجعة البشرية بدل معالجتها بشكل أعمى.

**What does the system do?**

- يستقبل طلبات العملاء عبر Google Form.
- يستخرج المعلومات المهمة وينظّمها.
- يحدد إن كانت المعلومات كافية لمتابعة الطلب.
- يوجّه الطلب إلى Valid Path أو Fallback Path.
- يسجل النتيجة في Google Sheets.
- يرسل الإشعار المناسب عبر Gmail.

---

## 👤 Users

**Primary Users:**
أعضاء فريق الشركة الذين يتعاملون مع طلبات العملاء الواردة.

**User Need:**
الحصول على طلبات منظمة ومصنّفة مسبقًا، ومعرفة فورًا أيها يمكن متابعته وأيها يحتاج إلى قرار بشري.

---

## 🧠 How I Designed the Solution

لم أبدأ بالأداة، بل بفهم العمل أولًا: كيف يُعالج الطلب اليوم، ثم تفكيكه إلى خطوات، وتحديد البيانات المطلوبة لكل خطوة، وتصميم القرارات التي يجب على النظام اتخاذها، بما فيها حالة نقص المعلومات. وبعد ذلك فقط صممت تدفق الأتمتة ونفذته في Zapier.

| File | Purpose |
|---|---|
| `01-business-analysis.md` | فهم العمل والمشكلة الحالية والنتيجة المطلوبة |
| `02-workflow-decomposition.md` | تقسيم العمل إلى خطوات ومهام مترابطة |
| `03-data-design.md` | تحديد البيانات المطلوبة وكيفية تنظيمها |
| `04-decision-and-exception-design.md` | قواعد القرار والتعامل مع الحالات التي تحتاج إلى مراجعة |
| `05-automation-design.md` | تصميم تدفق الأتمتة بناءً على التحليل السابق |

---

## ⚙️ How It Works

```text
Client submits a request (Google Form)
              ↓
AI extracts the client request details
              ↓
Paths: split by validity of the request
        ↙                      ↘
   Valid path              Fallback path
        ↓                          ↓
 Log result in Sheets      Log result in Sheets
        ↓                          ↓
 Send email notification   Send email notification
```

---

## 🤖 Role of AI

**What does AI do in this solution?**

- يقرأ الطلب النصي الحر ويستخرج التفاصيل المهمة.
- ينظّم المعلومات المستخرجة في حقول منظمة (Structured Fields).
- يدعم التحقق من وضوح الطلب واكتماله.

**What AI Should NOT Do**

- اتخاذ القرار النهائي في الطلبات غير الواضحة أو الناقصة؛ هذه تذهب إلى Human Review.
- استبدال قواعد التوجيه المحددة؛ التوجيه يعتمد على شروط صريحة.

---

## 🔄 Automation

**What parts of the process are automated?**

- استقبال الطلب عند إرسال النموذج.
- استخراج التفاصيل وتنظيمها.
- توجيه الطلب إلى المسار الصحيح.
- تسجيل النتيجة في Google Sheets.
- إرسال بريد الإشعار.

---

## 🗂️ Data

**Input**
طلب العميل من Google Form بنص حر وبمستويات تفصيل متفاوتة.

**Output**
سجل منظم في Google Sheets يحتوي على التفاصيل المستخرجة ونتيجة المعالجة، مع بريد إشعار عبر Gmail.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | استقبال طلبات العملاء |
| AI by Zapier | استخراج تفاصيل الطلب وتنظيمها |
| Zapier (Paths) | بناء الأتمتة والتوجيه حسب الشروط |
| Google Sheets | تسجيل الطلبات ونتائج معالجتها |
| Gmail | إرسال الإشعارات |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
تصميم العملية (التحليل، Workflow، البيانات، القرارات) قبل بناء أي أتمتة.

**Why:**
الأتمتة المبنية على عملية غير مفهومة تؤتمت الفوضى فقط.

### Decision 2
**Decision:**
توجيه الطلبات إلى Valid Path وFallback Path، وإبقاء الطلبات غير الواضحة أو الناقصة تحت Human Review.

**Why:**
طلبات العملاء غير متسقة، فيفصل النظام ما يمكنه معالجته عمّا يحتاج إلى شخص بدل التصرف بناءً على مدخلات غير موثوقة.

### Decision 3
**Decision:**
تسجيل كل طلب ونتيجته في Google Sheets في كلا المسارين.

**Why:**
سجل واحد لكل ما عولج يضمن عدم ضياع أي طلب، ويتيح للفريق معرفة ما حدث لكل طلب.

---

## 🧪 Testing

### Test 1: Clear and complete request
**Input:**
طلب يحتوي على اسم العميل وبريده والخدمة المطلوبة (مثل موقع لمشروع صغير) ووصف واضح وموعد مطلوب.

**Expected Result:**
يستخرج AI by Zapier جميع الحقول، ويمر الطلب بالـ Valid Path، ويُضاف صف في Google Sheets، ويُرسل بريد الإشعار.

**Actual Result:**
مرّ الطلب بالـ Valid Path وسُجّل الصف وأُرسل البريد كما هو متوقع.

**Status:** ✅

### Test 2: Incomplete or unclear request
**Input:**
طلب قصير مثل "أحتاج مساعدة في التسويق" دون ميزانية أو موعد أو تفاصيل الخدمة.

**Expected Result:**
يمر الطلب بالـ Fallback Path، ويُسجل في Google Sheets على أنه يحتاج مراجعة، ويُرسل البريد المناسب ليتابعه أحد أعضاء الفريق.

**Actual Result:**
مرّ الطلب بالـ Fallback Path وسُجّل للمراجعة وأُرسل البريد المناسب.

**Status:** ✅

---

## 📸 Evidence

### Workflow
🔗 [View Workflow Screenshot](./Screenshots/Workflow.png)

### Final Result
🔗 [View Final Result Screenshot](./Screenshots/Final%20Result.jpg)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- يستخدم الـ Zap ميزات مدفوعة (مثل Paths)، وبعد انتهاء فترة التجربة تعطّل ولم يعد يعمل مباشرة.
- طلبات النص الحر متباينة جدًا، فقد يفوّت الاستخراج بعض الحقول أو يسيء فهمها عندما تكون الرسالة قصيرة أو غامضة.
- تحديد ما يُعد "Valid" وما يُعد "Fallback" تطلّب تعريف شروط واضحة أولًا.

**How did I solve it?**

- وثّقت الـ Workflow بصور وملفات التصميم ليمكن مراجعة العمل بدون رابط مباشر.
- أبقيت الطلبات غير الواضحة على Fallback Path مع Human Review بدل ترك القرار للذكاء الاصطناعي.
- عرّفت شروط التوجيه في ملف تصميم القرارات قبل بناء الـ Paths.

---

## 📚 What I Learned

### Technical Lesson
كيفية بناء Workflow متعدد الخطوات في Zapier: Trigger من Google Forms، واستخراج منظم بـ AI by Zapier، وتفرّع بـ Paths، وكتابة النتائج في Google Sheets وGmail.

### Problem-Solving Lesson
الأتمتة الجيدة تبدأ بعملية مفهومة جيدًا وليس بأداة. تحليل العمل أولًا جعل كل قرار لاحق أوضح.

### AI Lesson
الذكاء الاصطناعي قوي في تحويل النص غير المنظم إلى بيانات منظمة، لكن القرارات في الحالات غير الواضحة أكثر أمانًا مع قواعد صريحة ومراجعة بشرية.

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- إضافة بريد متابعة تلقائي يطلب من العميل المعلومات الناقصة في الـ Fallback Path.
- إضافة حقل Priority ليرى الفريق الطلبات الأكثر إلحاحًا أولًا.
- إعادة بناء التدفق على أداة مجانية أو مستضافة ذاتيًا مثل n8n ليبقى يعمل دون ميزات مدفوعة.

---

## 🔗 Project Links

**Live Demo:** غير متاح (الـ Zap يعتمد على ميزات مدفوعة وتعطل بعد التجربة). راجع قسم Evidence.

**Workflow:** `./Screenshots`

**Repository:** [github.com/lilian2005-ui/Lilian_aiAutomation](https://github.com/lilian2005-ui/Lilian_aiAutomation)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
