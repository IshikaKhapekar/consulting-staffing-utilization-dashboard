# 👥 Consulting Staffing & Utilization Dashboard
### Staffing Reporting Project | IBM HR Data + Excel + Power BI
---

## 📖 The Business Problem

In a global consulting firm, staffing is everything. Every consultant needs to be deployed 
on a case, tracked for billable hours, and measured for utilization. 
When timesheets go missing, billing becomes inaccurate. When employees 
sit on bench too long, revenue is lost. When utilization drops below 
target, managers need to act fast.

This project simulates exactly that — a staffing reporting system for 
a 1,470-employee consulting firm. The system tracks who is on case, 
who is on bench, whether timesheets are submitted, whether billing 
matches logged hours, and which employees need immediate manager attention.

This is not just a data project. It is a business operations tool 
that directly impacts revenue accuracy and workforce efficiency.

---

## 📌 Project Overview

| Detail | Info |
|---|---|
| Project Type | Staffing Reporting & Utilization Analytics |
| Tools Used | Microsoft Excel, Power BI Desktop, GitHub |
| Base Dataset | IBM HR Analytics — Kaggle |
| Total Employees | 1,470 |
| Departments | 6 (Consulting, Finance, Technology, Operations, HR, Business Development) |
| Job Roles | 9 |
| Regions | 5 (North India, South India, West India, East India, International) |
| Utilization Target | 75% |

---

---

## 📊 Dataset Deep Dive

### Source
**IBM HR Analytics Employee Attrition Dataset** — Kaggle
Link: [kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset)


### 15 New Columns Added — The Staffing Layer

These 15 columns transform the IBM HR dataset into a 
consulting staffing operations system. Each column was 
designed to simulate data that a BCN staffing team would 
actually maintain.

<img width="1687" height="636" alt="Screenshot 2026-03-29 005609" src="https://github.com/user-attachments/assets/154cc53b-d11b-466a-8cc2-49abfc62c741" />


| Column | Formula Logic | Business Purpose |
|---|---|---|
| EmployeeName | Random Indian names generated | Readable employee identification on dashboard |
| CaseName | Random project names (Alpha/Beta/Gamma etc) | Case assignment tracking |
| StaffingStatus | Weighted random: 49% On Case, 20% Bench, 19% Training, 11% Leave | Core staffing classification — most important column |
| BillableHours | Based on StaffingStatus: On Case=25-40hrs, Training=5-15hrs, Leave=0 | Revenue generating hours tracking |
| NonBillableHours | Inverse of BillableHours by status | Internal time tracking |
| TargetHours | Fixed at 40 hours | Weekly utilization benchmark |
| TotalHours | BillableHours + NonBillableHours | Total logged hours |
| UtilizationRate | BillableHours / TargetHours | Core KPI — % of time spent on billable work |
| UtilizationFlag | ≥75% = On Target, ≥50% = At Risk, <50% = Critical | Traffic light system for manager alerts |
| TimesheetStatus | On Case random 10% = Missing, Bench/Training = Incomplete, Leave = N/A | Timesheet compliance tracking |
| BillingDiscrepancy | Random 0-15% of BillableHours for On Case employees | Hours billed vs hours logged gap |
| ReconciliationStatus | Based on discrepancy size: 0 = Reconciled, ≤1 = Reconciled, ≤3 = Minor Variance, >3 = Review Required | Billing accuracy classification |
| Region | Random 5 Indian + International regions | Geographic staffing distribution |
| ClientFeedbackScore | Random 3.0-5.0 for On Case employees | Client satisfaction tracking |
| WeekNumber | Random 1-52 | Weekly reporting period |
| DataQuality | Master flag: CLEAN if all key columns populated | Data quality control |

---

## 🧹 Data Cleaning Process

### Philosophy
With 1,470 employee records, data quality directly impacts staffing 
decisions. A single missing timesheet record means a billing gap. 
A wrong utilization flag means a manager misses an at-risk employee. 
Every column was validated systematically before Power BI import.

### Cleaning Summary

| Check | Total | Issues | Fixed | Impact% | Status |
|---|---|---|---|---|---|
| Duplicates | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Missing EmployeeID | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Missing Department | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Missing StaffingStatus | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Missing BillableHours | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Negative BillableHours | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Utilization Over 100% | 1,470 | 0 | 0 | 0.00% | ✅ Clean |
| Missing Timesheets | 1,470 | 79 | 0 | 5.37% | ⚠ Flagged |
| Incomplete Timesheets | 1,470 | 577 | 0 | 39.25% | ⚠ Flagged |
| Review Required | 1,470 | 391 | 0 | 26.60% | ⚠ Flagged |
| Critical Utilization | 1,470 | 295 | 0 | 20.07% | ⚠ Flagged |
| CLEAN Rows | 1,470 | 1,470 | — | 100% | ✅ Clean |


<img width="711" height="368" alt="Screenshot 2026-03-29 005715" src="https://github.com/user-attachments/assets/bb1655df-a42d-4c23-9dcd-2c6d32748699" />

### Key Cleaning Decisions

**Decision 1 — Deleted 11 Irrelevant Columns**
The dataset contains many columns designed for attrition 
prediction that have no relevance in staffing operations reporting. 
Removing them reduced noise and made the dataset cleaner for 
Power BI import.

**Decision 2 — Replaced Department Column**
Original departments (HR/Sales/R&D) don't reflect consulting firm 
structure. Replaced with 6 consulting-relevant departments: 
Consulting, Finance, Technology, Operations, HR, Business Development.

**Decision 3 — Flagged Not Deleted**
Missing timesheets (79) and Review Required reconciliations (391) 
were flagged rather than deleted. In real FP&A operations, these 
records need manager review — deleting them would hide the problem.

**Decision 4 — Excluded Leave and Training from Utilization**
Employees on leave or in training cannot be expected to log 
billable hours. Including them in utilization calculations would 
unfairly drag down the firm's overall utilization rate. They are 
marked N/A in UtilizationFlag.

**Decision 5 — Weighted StaffingStatus Distribution**
Used a 10-value CHOOSE formula to create realistic distribution: 
40% On Case, 20% Bench, 10% Leave, 20% Training — reflecting 
typical consulting firm headcount allocation patterns.

---

## 📈 Power BI Dashboard

### Page 1 — Staffing Overview

<img width="1253" height="702" alt="Screenshot 2026-03-29 005936" src="https://github.com/user-attachments/assets/c3d040c3-c768-460b-840d-cf8b62a1b5b3" />


**Purpose:** Executive level snapshot of entire workforce 
staffing position — who is deployed, who is available, 
and how efficiently the firm is utilizing its talent.

**Visual 1 — KPI Cards (5 across top)**

| KPI | Value | Business Meaning |
|---|---|---|
| Total Headcount | 1,470 | Total workforce size |
| On Case | 720 | Revenue generating employees |
| On Bench | 295 | Available but undeployed — cost without revenue |
| Avg Utilization | 81.4% | Above 75% target — healthy |
| Bench Rate | 20.1% | 1 in 5 employees not generating revenue |

**Visual 2 — Staffing Status Donut Chart**

Shows the complete breakdown of workforce deployment at a glance. 
The donut immediately tells a manager what proportion of their 
team is generating revenue vs sitting idle. A healthy consulting 
firm should have minimum 50% On Case at any time.

**Result:** 49% On Case, 20% Bench, 19% Training, 11% Leave — 
healthy distribution with training investment visible.

**Visual 3 — Utilization Gauge**

The gauge is the single most important visual on this dashboard. 
It shows average utilization rate of 81.4% against the 75% target 
line. Green fill crossing the red target line immediately 
communicates: we are above target.

**Business Significance:** Every 1% drop in utilization across 
1,470 employees represents significant revenue loss. Maintaining 
above 75% is critical for firm profitability.

**Visual 4 — Staffing Status by Department Stacked Bar**

Shows which departments are most deployed vs most benched. 
A department with high bench percentage signals either project 
completion without new case pipeline, or poor staffing planning.

**Result:** Technology and Consulting departments show highest 
On Case ratios — aligned with firm's core revenue drivers.

**Visual 5 — Utilization by Job Role Bar Chart**

Shows which roles are most efficiently utilized. Senior roles 
typically show higher utilization as they are harder to replace 
on cases. Junior roles may show lower utilization as they are 
still in training pipeline.

**Result:** Manager and Senior Consultant roles show highest 
utilization — expected as they are most client-facing.

**Visual 6 — Headcount by Region Column Chart**

Shows geographic distribution of workforce deployment. 
Regions with high bench count signal need for business 
development activity to generate new cases in that geography.

---

### Page 2 — Timesheet & Reconciliation Report


<img width="1250" height="702" alt="Screenshot 2026-03-29 005959" src="https://github.com/user-attachments/assets/02086c57-8114-4183-ab5a-114b0816a8ab" />

**Purpose:** Operational deep-dive into timesheet compliance 
and billing accuracy — the two metrics that directly impact 
revenue reporting accuracy.

**Visual 1 — KPI Cards (Top 4)**

| KPI | Value | Business Meaning |
|---|---|---|
| Missing Timesheets | 79 | Employees with no hours logged — billing gap risk |
| Compliance Rate | 89% | % of On Case employees with submitted timesheets |
| Billing Reviews Required | 391 | Discrepancies between billed and logged hours |
| Total Discrepancy | 1,753.5 hrs | Total hours gap across all billing discrepancies |

**Visual 2 — Timesheet Status Donut**

Breaks down timesheet submission status across all 1,470 employees. 
The most critical segment is Missing — these are On Case employees 
who have logged no hours, creating a direct billing gap.

**Result:** 43.6% Submitted, 39.3% Incomplete (Bench/Training — 
expected), 5.4% Missing (critical), 11.8% N/A (Leave).

**Business Discussion:** The 5.4% missing rate (79 employees) 
represents a significant revenue risk. If each missing employee 
averages 30 billable hours per week at consulting rates, the 
firm is potentially unable to bill for thousands of hours of 
actual work done.

**Visual 3 — Reconciliation Status by Department**

Shows which departments have highest billing discrepancies. 
This is the most actionable visual for a finance manager — 
it tells them exactly where to focus reconciliation efforts.

**Result:** Review Required cases distributed across all 
departments — no single department is significantly worse, 
suggesting a systemic process issue rather than a 
department-specific problem.

**Visual 4 — Missing Timesheets by Department Bar Chart**

Ranks departments by missing timesheet count. The department 
at the top of this chart needs immediate manager intervention. 
Missing timesheets are not just a compliance issue — they are 
a revenue recognition issue.

**Visual 5 — Utilization vs Client Feedback Scatter Plot**

This is the most analytically sophisticated visual in the 
dashboard. It plots each employee's utilization rate against 
their client feedback score, colored by utilization flag.

**Four Quadrants:**

| Quadrant | Utilization | Feedback | Label | Action |
|---|---|---|---|---|
| Top Right | High | High | Star Performers | Retain and reward |
| Top Left | Low | High | Underutilized Talent | Deploy on more cases |
| Bottom Right | High | Low | Overworked | Check workload balance |
| Bottom Left | Low | Low | At Risk | Urgent manager review |

**Result:** Majority of On Case employees (green dots) cluster 
in top right quadrant — high utilization, high feedback. 
This validates that deployment strategy is working for 
most employees.

**Visual 6 — At Risk Employee Detail Table**

The most actionable output of the entire dashboard. Shows 
every employee with either missing timesheet or review required 
reconciliation status — sorted by billing discrepancy hours.

Finance managers use this table to:
- Call specific employees about missing timesheets
- Initiate billing review conversations with case managers
- Escalate high discrepancy cases to finance leadership

---

## 💡 Key Business Findings & Discussion

### Finding 1 — Utilization is Healthy but Bench is Expensive
Average utilization of 81.4% is above the 75% target — positive 
signal. However 295 employees (20%) on bench represent significant 
cost without corresponding revenue. At average MonthlyCTC of 
the dataset, bench employees cost the firm money every day 
they remain undeployed.

**Recommendation:** Introduce a maximum bench duration policy 
of 3 weeks. After 3 weeks on bench, employees should be 
auto-enrolled in billable training programs or assigned to 
internal projects that can be partially billed.

### Finding 2 — Timesheet Compliance is a Revenue Risk
79 employees with missing timesheets is not just a compliance 
issue — it is a billing accuracy issue. Consulting firms bill 
clients based on hours logged. Missing timesheets = unbilled 
hours = lost revenue.

**Recommendation:** Implement automated weekly reminder system 
for all On Case employees. Any employee with no timesheet 
submission by Wednesday should trigger a manager alert. 
Timesheet compliance should be a KPI in performance reviews.

### Finding 3 — 391 Billing Discrepancies Need Investigation
26.6% of On Case employees show billing discrepancies between 
hours logged and hours billed. Total gap of 1,753.5 hours 
across the firm represents material revenue risk.

**Recommendation:** Launch a billing reconciliation sprint 
targeting the top 50 Review Required cases first — these 
have the largest discrepancies and highest financial impact. 
Assign each case to a finance analyst with a 2-week resolution 
deadline.

### Finding 4 — Scatter Analysis Reveals Talent Insights
The utilization vs client feedback scatter shows that high 
utilization generally correlates with high client feedback 
— employees who are busy tend to perform better. However 
the bottom right quadrant (high util, low feedback) signals 
potential burnout cases that need immediate attention.

**Recommendation:** Any employee showing utilization above 
90% for more than 4 consecutive weeks with below average 
client feedback should be flagged for a manager 1:1 and 
potential workload redistribution.

---

## 📋 CFO Recommendations Summary

1. Set maximum bench duration of 3 weeks with auto-escalation
2. Implement automated timesheet reminder — Wednesday deadline
3. Launch billing reconciliation sprint for top 50 discrepancy cases
4. Add utilization floor of 60% as manager alert trigger
5. Flag employees with utilization above 90% + low feedback for burnout review
6. Make timesheet compliance a formal KPI in quarterly performance reviews

---

## 🛠️ Tools & Skills Used

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data transformation, formula engineering, cleaning |
| Power BI Desktop | Dashboard design, DAX measures, interactive visuals |
| DAX | CALCULATE, AVERAGE, DIVIDE, COUNTROWS, FILTER, SUM |
| GitHub | Version control and project documentation |
| Kaggle | Base dataset source |

**Key Excel Functions Used:**
CHOOSE, RANDBETWEEN, IF, OR, AND, COUNTIF, COUNTBLANK, 
SUMPRODUCT, AVERAGEIF, UNIQUE, COUNTA, IFERROR, ROUND

**Power BI Visuals Used:**
Card, Gauge, Donut Chart, Stacked Bar Chart, Clustered Bar Chart, 
Column Chart, Scatter Chart, Table, Slicer

---

## 👤 Author

**Ishika Khapekar**
Aspiring Data Analyst  
https://www.linkedin.com/in/ishika-khapekar-a068182ab


---

*This project was built as part of my data analytics portfolio 
targeting FP&A and Staffing Reporting roles in consulting 
and professional services firms .*
```
