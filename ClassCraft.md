# ClassCraft — Odoo Practice Tasks for Schools & Training Centers

*"Enrollment to graduation, all in one place."*

A set of practice tasks for building an education management module in Odoo. Each task is written like a real client request, not a coding exercise. Build it, then record it if you're making a portfolio video.

## How to use this file

1. Start from Easy, move to Medium, then try Hard once you're comfortable.
2. Read the "Scenario" like it's an actual client sitting in front of you. That's the real skill — turning a vague request into a working system.
3. Some tasks say **Depends on** — do that task first, since the next one builds on it.
4. Tasks marked **Full Cycle** need 3-4 modules working together. These are the best ones to show in a video because they prove you understand how Odoo modules connect, not just isolated fixes.

## Difficulty guide

- 🟢 **Easy** — one module, basic configuration, good for warming up
- 🟡 **Medium** — one or two modules, some automation or logic, this is where most real work lives
- 🔴 **Hard** — three or more modules, real business logic, reporting across campuses

---

### 🟢 E1. Online Student Registration
**Modules:** Contacts, Website

**Scenario:** Parents currently register their kids by filling a paper form at the office. The school wants an online form instead.

**What to build:** Build a website form that captures student info and automatically creates a contact record and a CRM lead when submitted.

**Goal:** A parent fills the form from home, and admin staff see the new student appear automatically — no retyping.

---

### 🟢 E2. Course Catalog with Early Bird Pricing
**Modules:** Sales

**Scenario:** The training center sells multiple courses and wants to reward students who register early with a discount.

**What to build:** Create courses as products with categories (Kids, Teens, Adults). Set up a pricelist that gives a discount if the order is placed before a certain date.

**Goal:** Early registrations get the discount automatically, no manual price changes by staff.

**New skill:** Date-based pricelist rules.

---

### 🟢 E3. Teacher Attendance
**Modules:** Employees, Attendances

**Scenario:** School admin wants to know exactly which teachers showed up and on time, without walking around checking.

**What to build:** Set up attendance kiosk check-in for teaching staff. Build an absence report grouped by teacher and month.

**Goal:** Admin gets a monthly report of teacher attendance without manual tracking.

---

### 🟡 E4. Teacher Timetable Without Overlaps
**Modules:** Employees, Calendar

**Scenario:** Two teachers were once booked for the same classroom at the same time by mistake. The school wants this to never happen again.

**What to build:** Set working hours per teacher. Build a scheduling view that blocks a new class from being created if the teacher already has a class at that time.

**Goal:** Double-booking a teacher becomes impossible instead of something staff has to remember to check.

---

### 🟡 E5. Student Enrollment Pipeline
**Modules:** CRM

**Scenario:** The center gets a lot of inquiries but loses track of who actually enrolled and who ghosted after the first call.

**What to build:** Build a pipeline: New Inquiry → Trial Class Booked → Enrolled → Lost. Add an automatic email at "Trial Class Booked" confirming the date and time.

**Goal:** Staff can instantly see how many leads are stuck at each stage and follow up on the right ones.

---

### 🟡 E6. Tuition Fees in Installments
**Modules:** Accounting

**Scenario:** Many parents can't pay the full year's tuition at once and need to pay in 3 parts, with reminders before each due date.

**What to build:** Split one invoice into 3 payment terms with different due dates. Set up automatic payment reminder emails a few days before each due date.

**Goal:** Parents get reminded automatically and the school doesn't have to chase late payments manually.

**Depends on:** E5

---

### 🟡 E7. Library and Equipment Tracking
**Modules:** Inventory

**Scenario:** Books and lab equipment go missing because nobody tracks who borrowed what.

**What to build:** Track books/equipment using serial numbers. Set up a borrow and return flow so the system always knows who currently has an item.

**Goal:** Librarian can look up any item and instantly see if it's available or who is holding it.

---

### 🟡 E8. Parent Communication Automation
**Modules:** CRM, Email Marketing

**Scenario:** Parents complain they only hear from the school when there's a problem, and teachers forget to notify them about absences.

**What to build:** Set up an automated email triggered when a student is marked absent, and another automated message when grades are posted.

**Goal:** Parents get notified automatically, no teacher has to remember to send anything.

---

### 🟡 E9. Full Cycle — Enrollment to Certificate
**Modules:** CRM, Sales, Accounting, Project

**Scenario:** From the moment a lead calls in, to being enrolled, to paying, to finishing the course and getting a certificate — right now none of these steps are connected.

**What to build:** Lead comes in through CRM → converted to a sale order for the course → invoice created and paid → a task checklist (attendance completed, final exam passed, certificate printed) tracked as a project task tied to that student.

**Goal:** One student record shows their entire journey from first call to graduation.

**Depends on:** E5, E6

---

### 🔴 E10. Multi-Campus Enrollment Dashboard
**Modules:** CRM, Accounting, Employees

**Scenario:** A school group runs 3 campuses. Owners want one dashboard comparing enrollment numbers, revenue, and teacher workload across all of them.

**What to build:** Set up each campus as a company or analytic account. Build a report comparing enrollment count, revenue, and teacher hours per campus, side by side.

**Goal:** Owners see all 3 campuses on one screen instead of asking each campus manager separately.

---

## Best task for your portfolio video

**E9 — Full Cycle: Enrollment to Certificate** is the strongest pick for ClassCraft. It proves you can connect CRM, Sales, Accounting, and Project into one working student journey — not just fix one isolated bug.
