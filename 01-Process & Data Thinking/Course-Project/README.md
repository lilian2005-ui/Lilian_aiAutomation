# AI Client Intake & Request Routing System

An automation that turns unstructured client requests into organized, routed records, and sends anything incomplete or unclear to human review.

---

## 🎯 Problem

### The Context
A services company (web design, digital marketing, app development) receives requests from potential clients through online forms. Every client writes differently: some explain their needs in detail, some send a one-line message, and some forget to include important information.

### The Problem
Each incoming request has to be read by an employee, who then has to understand the need, organize the details, check whether the information is clear and complete, and decide on the next step. As volume grows, this manual handling slows follow-up and details get lost.

### Why It Matters
This is not only a message-receiving problem. It is a problem of how requests are processed, organized, and routed. Reducing the repetitive work frees the team's time and makes sure no request is forgotten or mishandled.

---

## 💡 Solution

An automation workflow that receives each request, uses AI to extract the key details, checks whether the information is sufficient, routes the request by clear rules, logs the result, and notifies the team. Incomplete or unclear requests are kept under human review instead of being processed blindly.

### What does the system do?

- Receives client requests through a Google Form.
- Extracts and organizes the important information from each request.
- Decides whether the information is sufficient to follow up.
- Routes the request through a valid path or a fallback path based on defined rules.
- Records the processing result in Google Sheets.
- Sends the appropriate email notification.

---

## 👤 Users

**Primary Users:**
The company's team members who handle incoming client requests.

**User Need:**
Get requests that are already organized and classified, and know immediately which ones can be followed up and which need a human decision.

---

## 🧠 How I Designed the Solution

I did not start with the tool. I started by understanding the work: how a request is handled today, then breaking it into steps, defining the data each step needs, and designing the decisions the system must make, including what happens when information is missing. Only after that did I design the automation flow and implement it in Zapier.

The analysis is documented step by step in the project files:

| File | Purpose |
|---|---|
| `01-business-analysis.md` | Understanding the business, the current problem, and the desired outcome |
| `02-workflow-decomposition.md` | Breaking the work into connected steps and tasks |
| `03-data-design.md` | Defining the required data and how it is organized |
| `04-decision-and-exception-design.md` | Decision rules and handling of cases that need review |
| `05-automation-design.md` | Designing the automation flow from the analysis |

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

- Reads the free-text request and extracts the important details.
- Organizes the extracted information into structured fields.
- Supports the check of whether the request is clear and complete.

**What AI Should NOT Do**

- Make the final decision on unclear or incomplete requests; those are held for human review.
- Replace the defined routing rules; the routing follows explicit conditions.

---

## 🔄 Automation

**What parts of the process are automated?**

- Receiving the request when the form is submitted.
- Extracting and structuring the request details.
- Routing the request to the correct path.
- Logging the outcome in Google Sheets.
- Sending the notification email.

---

## 🗂️ Data

**Input**
The client's request as submitted through the Google Form, in free text and with varying levels of detail.

**Output**
A structured record in Google Sheets with the extracted request details and the processing result, plus a notification email.

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| Google Forms | Receive client requests |
| AI by Zapier | Extract and organize the request details |
| Zapier (Paths) | Build the automation and route requests by conditions |
| Google Sheets | Record requests and processing results |
| Gmail | Send notifications |

---

## 🔑 Key Design Decisions

### Decision 1
**Decision:**
Design the process (analysis, workflow, data, decisions) before building any automation.

**Why:**
Automation built on a poorly understood process only automates confusion. Understanding the work first makes the tool choices and the rules clear.

### Decision 2
**Decision:**
Route requests into a valid path and a fallback path, and keep unclear or incomplete requests under human review.

**Why:**
Client requests are inconsistent. Instead of letting AI act on unreliable input, the system separates cases it can handle from cases that need a person.

### Decision 3
**Decision:**
Log every request and its outcome in Google Sheets, on both paths.

**Why:**
A single record of everything that was processed means no request is lost and the team can see what happened to each one.

---

## 🧪 Testing

### Test 1: Clear and complete request
**Input:**
[Describe the test request you submitted]

**Expected Result:**
The request goes through the valid path, a row is recorded in Google Sheets, and the notification email is sent.

**Actual Result:**
[What actually happened]

**Status:** ✅ / ❌

### Test 2: Incomplete or unclear request
**Input:**
[Describe the test request you submitted]

**Expected Result:**
The request goes through the fallback path, is recorded for review, and the matching email is sent.

**Actual Result:**
[What actually happened]

**Status:** ✅ / ❌

---

## 📸 Evidence

### Workflow
![Workflow](./Screenshots/workflow.png)

### Final Result
![Final Result](./Screenshots/final-result.png)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- The Zap uses paid features (Paths and others). After the Zapier trial ended, the Zap was disabled, so the workflow can no longer run live.
- [Add any other issue you ran into while building or testing]

**How did I solve it?**

- I documented the workflow with screenshots and the design files so the work can still be reviewed without a live link.
- [Add how you solved the other issues]

---

## 📚 What I Learned

### Technical Lesson
[What you learned about building the workflow in Zapier, for example Paths and AI extraction]

### Problem-Solving Lesson
A good automation starts with a well-understood process, not with a tool. Analyzing the work first made the design much clearer.

### AI Lesson
[What you learned about where AI helps and where explicit rules or human review are the better choice]

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- [Improvement 1]
- [Improvement 2]
- [Improvement 3]

---

## 🔗 Project Links

**Live Demo:** Not available (the Zap relies on paid features and is disabled after the trial). See the screenshots in the Evidence section.

**Workflow:** See `./Screenshots`

**Repository:** [github.com/lilian2005-ui/Lilian_aiAutomation](https://github.com/lilian2005-ui/Lilian_aiAutomation)

---

## 👩‍💻 Author

**Lilian Abu Ramadan**

[LinkedIn](https://linkedin.com/in/lilian-abu-ramadan) · [GitHub](https://github.com/lilian2005-ui)
