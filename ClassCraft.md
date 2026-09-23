# ClassCraft - Odoo Practice Tasks for Schools & Training Centers

*"Enrollment to graduation, all in one place."*

These are practice tasks for building an education management module in Odoo. I wrote every task the way a real client would ask for it, so don't expect a click-by-click tutorial. Figuring out what the client actually needs is part of the work.

Build it, test it, and if you're making a portfolio video, record it.

## Before you start

- Create a custom module called `classcraft` and put all your work inside it.
- Even when a task is mostly setup (tags, stages, pricelists), try to save that setup in your module as XML or CSV data files. My test is simple: I install your module on a new, empty database and your work should be there. Anything you only clicked in the UI is gone with the database.
- Each task has an **Apps** line. Install those apps before you start the task.
- If you don't see an app called **Accounting**, use **Invoicing**. It covers everything these tasks need.
- Menu names and settings move around a bit between Odoo versions. If a hint points to something you can't find in your version, look for the same feature under a different name.
- Create some test data before testing: a few courses, 2 or 3 teachers (employees), and some students and parents.

## How to read each task

- **Scenario** - the problem, the way the client explains it to you. Read it like the client is sitting in front of you.
- **What to build** - what I expect you to deliver.
- **Done when** - the checklist I'll use to test your work. If every point works, the task is done.
- **Hints** - where to look in Odoo. Only read them if you're stuck.
- **Goal** - what the client gets out of it. If your solution works but doesn't reach the goal, it's not finished.
- **Depends on** - finish that task first, because this one builds on it.

If something is not clear, make a reasonable decision, write it down in a short note, and keep going. That's what you'd do with a real client too.

## Difficulty

- 🟢 **Easy** - one app, mostly configuration. Good for warming up.
- 🟡 **Medium** - one or two apps, with some automation or custom logic. Most real client work looks like this.
- 🔴 **Hard** - three or more apps, real business logic, and reporting across campuses.

## Suggested order

E2 → E1 → E5 → E3 → E4 → E7 → E6 → E8 → E9 → E10 → E11

---

### 🟢 E1. Online Student Registration
**Apps:** Contacts, Website

**Scenario:** Right now parents register their kids by filling in a paper form at the office. The school wants an online form instead.

**What to build:**
1. A registration page on the website with a form for the student's info. At minimum: student name, date of birth, parent name, parent phone, and parent email. Add more fields if you think the school needs them.
2. When the form is submitted, the system creates a **contact** and a **CRM lead** automatically.

**Done when:**
- A visitor who is not logged in can open the page and submit the form.
- After submitting, they see a confirmation (a thank-you page or message).
- A new contact appears in Contacts with the submitted info.
- A new lead appears in CRM, linked to that contact.
- Nobody on the staff has to retype anything.

**Hints:**
- The website form builder can create CRM leads (you'll need the website + CRM integration installed). Creating the contact as well may need some code.

**Goal:** A parent fills in the form from home, and admin staff see the new student show up automatically. No retyping.

---

### 🟢 E2. Course Catalog with Early Bird Pricing
**Apps:** Sales

**Scenario:** The training center sells several courses and wants to reward students who register early with a discount.

**What to build:**
1. Create the courses as products.
2. Group them in categories: **Kids**, **Teens**, and **Adults**.
3. Set up a pricelist that gives a discount when the order is placed before a certain date. Pick a discount (for example 15%) and a cutoff date, and write them down.

**Done when:**
- Every course is in one of the three categories.
- An order placed before the cutoff date gets the discount automatically.
- An order placed after the cutoff date gets the normal price.
- Staff never change a price by hand.

**Hints:**
- Turn on **Pricelists** in Sales settings. Pricelist rules can have start and end dates.
- **New skill:** date-based pricelist rules.

**Goal:** Early registrations get the discount automatically, with no manual price changes by staff.

---

### 🟢 E3. Teacher Attendance
**Apps:** Employees, Attendances

**Scenario:** The school admin wants to know exactly which teachers showed up, and whether they were on time, without walking around checking.

**What to build:**
1. Set up kiosk check-in for teaching staff, so teachers check in and out on a shared screen when they arrive and leave.
2. An absence report grouped by teacher and by month.

**Done when:**
- A teacher can check in and out from the kiosk.
- The admin can open a report and see, for each teacher, how many days they were absent in each month.
- The report only counts days the teacher was supposed to work.

**Hints:**
- Odoo records check-ins, not absences. You need to work out absences by comparing check-ins against the teacher's working schedule.
- If you can also show late arrivals, even better. The client did mention "on time".

**Goal:** The admin gets a monthly report of teacher attendance without tracking it by hand.

---

### 🟡 E4. Teacher Timetable Without Overlaps
**Apps:** Employees, Calendar

**Scenario:** Once, two classes were booked for the same teacher at the same time by mistake. The school wants to make sure this never happens again.

**What to build:**
1. Set working hours for each teacher.
2. A scheduling view (a calendar works well) where staff create classes and assign a teacher.
3. When a new class is created, the system checks the teacher's schedule. If the teacher already has a class at that time, the class is not created and a clear message explains why.

**Done when:**
- Teacher A has a class from 10:00 to 11:00. Trying to add another class for teacher A from 10:30 to 11:30 is blocked with a message.
- Teacher B can have a class at 10:30 with no problem.
- A class from 11:00 to 12:00, right after the 10:00-11:00 one, is allowed.
- Moving or editing an existing class into a busy slot is also blocked.

**Hints:**
- You decide whether a "class" is a calendar event or a new model of your own.
- The check needs Python code. Configuration alone won't do it.

**Goal:** Double-booking a teacher becomes impossible, instead of something staff have to remember to check.

---

### 🟡 E5. Student Enrollment Pipeline
**Apps:** CRM

**Scenario:** The center gets lots of inquiries but loses track of who actually enrolled and who disappeared after the first call.

**What to build:**
1. A CRM pipeline with these stages: **New Inquiry → Trial Class Booked → Enrolled → Lost**.
2. The trial class date and time are stored on the lead.
3. When a lead moves to **Trial Class Booked**, an email is sent automatically to the student/parent confirming the date and time of the trial class.

**Done when:**
- The pipeline shows the 4 stages in the right order.
- Moving a lead to Trial Class Booked sends the email once, with the correct date and time in it.
- The email shows up in the lead's chatter, so staff can see it was sent.
- In the kanban view, staff can see how many leads are in each stage.

**Hints:**
- Look at automated actions (called automation rules in newer versions) and email templates.

**Goal:** Staff can see right away how many leads are stuck at each stage and follow up with the right people.

---

### 🟡 E6. Tuition Fees in Installments
**Apps:** Accounting
**Depends on:** E5

**Scenario:** Many parents can't pay the full year's tuition at once. They need to pay in 3 parts, with a reminder before each due date.

**What to build:**
1. A payment term that splits one invoice into **3 installments** with different due dates.
2. An automatic reminder email sent a few days **before** each installment is due. Pick how many days (for example 3) and write it down.

**Done when:**
- An invoice using this payment term shows 3 amounts with 3 due dates.
- A reminder email goes out automatically before each due date.
- If an installment is already paid, no reminder is sent for it.
- Nobody on the staff sends the reminders by hand.

**Hints:**
- Odoo's standard follow-ups are mostly about invoices that are already late. Here the reminder comes before the due date, so check whether the standard tools cover it or whether you need your own scheduled action.

**Goal:** Parents get reminded automatically, and the school doesn't have to chase late payments by hand.

---

### 🟡 E7. Library and Equipment Tracking
**Apps:** Inventory

**Scenario:** Books and lab equipment go missing because nobody tracks who borrowed what.

**What to build:**
1. Track every book and piece of equipment with its own serial number.
2. A borrow and return flow, so the system always knows who has each item right now.

**Done when:**
- Each copy of a book (or each device) has a unique serial number.
- When someone borrows an item, the system shows who has it and since when.
- When it's returned, it shows as available again.
- The librarian can search by serial number or item name and see straight away whether it's available or who has it.

**Hints:**
- Turn on **Lots & Serial Numbers** in Inventory settings.
- Think about whether borrowing is best as a stock move (for example, a location per borrower) or as a small borrow record of your own.

**Goal:** The librarian can look up any item and see right away whether it's available or who has it.

---

### 🟡 E8. Parent Communication Automation
**Apps:** CRM, Email Marketing

**Scenario:** Parents complain they only hear from the school when something is wrong, and teachers forget to tell them about absences.

**What to build:**
1. An automatic email to the parent when their child is marked **absent**.
2. Another automatic message to the parent when **grades are posted**.

**Done when:**
- Marking a student absent sends an email to that student's parent.
- Marking a student present sends nothing.
- Posting a grade sends the parent a message with the grade.
- Teachers don't send anything by hand.

**Hints:**
- Odoo has no student attendance or grades out of the box. You'll need a simple way to record them first.
- Email Marketing is built for mass mailings. For one email triggered by one event, automated actions with email templates usually fit better. Use whatever does the job.

**Goal:** Parents get notified automatically. No teacher has to remember to send anything.

---

### 🟡 E9. Full Cycle - Enrollment to Certificate
**Apps:** CRM, Sales, Accounting, Project
**Depends on:** E5, E6

**Scenario:** From the moment a lead calls in, to enrolling, to paying, to finishing the course and getting a certificate, none of the steps are connected right now.

**What to build:** Connect these steps so each one comes from the one before it:
1. A lead comes in through CRM.
2. The lead is turned into a sale order for the course.
3. An invoice is created and paid.
4. A project task, linked to that student, tracks this checklist:
   - Attendance completed
   - Final exam passed
   - Certificate printed

**Done when:**
- You can run one student from first call to certificate without typing the same data twice.
- The student's task is created from their enrollment, not made by hand.
- From one student record you can reach their lead, sale order, invoice, and task.
- Staff can see which students still have open checklist items.

**Hints:**
- A service product can create a project task when the sale order is confirmed. Look at the product's settings.
- This is a great one to record. Show one student going through the whole journey.

**Goal:** One student record shows their whole journey, from first call to graduation.

---

### 🔴 E10. Multi-Campus Enrollment Dashboard
**Apps:** CRM, Accounting, Employees

**Scenario:** A school group runs 3 campuses. The owners want one dashboard comparing enrollment numbers, revenue, and teacher workload across all of them.

**What to build:**
1. Set up each campus as a company or an analytic account. Explain which one you picked and why.
2. A report that shows these numbers side by side for each campus:
   - Number of enrollments
   - Revenue
   - Teacher hours

**Done when:**
- The owners open one screen and see all 3 campuses next to each other.
- They can filter by period (this month, this term, this year).
- The numbers match the real enrollments, invoices, and attendance records.

**Hints:**
- Pivot and graph views go a long way. If they're not enough, look at dashboards/spreadsheets or a custom report model.

**Goal:** The owners see all 3 campuses on one screen instead of asking each campus manager.

---
### 🔴 E11. Sibling Discount and One Family Account
**Apps:** Contacts, Sales, Accounting
**Depends on:** E2

**Why this task:** Almost every school gives a discount for the second and third child, and parents want one bill for the whole family. Odoo's pricelists can't tell that two students are brothers, and invoices are per student.

**Scenario:** A family has three kids at the center. The school's policy is 10% off for the second child and 15% off for the third. Right now the accountant works out who is the "second child" by hand and edits the price on every order. Parents also get three separate invoices and three separate reminders, and they keep asking "how much do we owe in total?"

**What to build:**
1. A **family** that groups students together, with one or two parents as the paying contact.
2. A sibling discount policy the school can set up (for example: 1st child full price, 2nd child 10%, 3rd and more 15%).
3. When a course is sold to a student who has siblings already enrolled, the right discount applies automatically.
4. Invoices go to the family's paying parent, with each child's name on their lines.
5. A **family statement**: everything invoiced, paid, and still owed for the whole family, on one page, printable.

**Done when:**
- Enroll the first child, then a second, then a third. The discounts apply in that order with no manual price changes.
- You decide which child counts as "first" (oldest, first enrolled, or most expensive course), write it down, and the system follows that rule every time.
- If a sibling leaves, the next enrollment for the family is priced correctly again.
- The parent receives invoices addressed to them, and each line shows which child it's for.
- The family statement shows the total owed across all kids and matches the invoices.

**Hints:**
- A family can be a company-type contact with the students and parents under it, or a small model of your own. Think about which one makes invoicing and the statement easier.
- Keep the discount percentages in settings, not in code.

**Goal:** Sibling discounts apply on their own, and parents get one clear account for the whole family.

---

## Best task for your portfolio video

Pick **E9 - Full Cycle: Enrollment to Certificate**. It shows CRM, Sales, Accounting, and Project working together as one student journey, which is exactly what clients hire an Odoo developer for.

## What to hand in

- Your `classcraft` module (it should install on a new database without errors).
- A short note with any decisions you made where the task left the choice to you.
- Optional: a short video of the task working.
