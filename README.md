# Hospital Emergency Room (ER) Dashboard — README

**File:** `ER_Dashboard.pbix`
**Tool:** Power BI Desktop
**Core data table:** `Hospital ER_Data` (fact table) + `Date Table` (date dimension)
**Pages:** 4 — Monthly View, Consolidated View, Patient Details, Key Takeaways

---

## 1. What this dashboard does

It's an Emergency Room operations dashboard — tracks patient volume, wait times, satisfaction, referrals, admission outcomes, and demographic mix, sliced by date/month. It's built as a portfolio-style analytics report but the pattern is a good starting template for any healthcare ops / patient-flow product.

---

## 2. Pages & layout

| Page | Purpose |
|---|---|
| **Monthly View** | Day-level trend view of KPIs for a selected month (area charts by day) |
| **Consolidated View** | Month-over-month trend view of the same KPIs (column charts by month) |
| **Patient Details** | Row-level patient record table, filterable by date |
| **Key Takeaways** | Summary/insights landing page (title + narrative placeholders) |

Monthly View and Consolidated View are mirror pages — same KPIs and charts, just one sliced by **day** and the other by **month**.

---

## 3. Filters / Slicers used

Power BI has three filter layers — this report only uses **visual-level slicers** (no report-level or page-level filters were configured):

| Page | Slicer field | What it filters |
|---|---|---|
| Monthly View | `Date Table` → relative/column date filter | Restricts the whole page to a specific date range |
| Monthly View | `Date Table.Month Name` | Lets the user pick which month to drill into |
| Consolidated View | `Date Table.Date` | Date-range slicer for the trend page |
| Patient Details | `Date Table.Date` | Filters the patient record table by admission date |
| Key Takeaways | `Date Table.Date` | Filters the summary page |

Because there's a dedicated `Date Table` (a standard Power BI date dimension marked as a date table), all slicers filter through relationships rather than filtering the fact table's raw date column directly — this is best practice and keeps time-intelligence measures accurate.

**No other filter types are used** — there are no top-N filters, no advanced/relative-date filters visible at page/report level, and no bookmarks (so there's no "filter reset" or guided-navigation button setup).

---

## 4. Charts & visuals used

| Visual type | Count | Used for |
|---|---|---|
| **Card** (KPI number) | 8 | Headline metrics: No. of Patients, Avg Wait Time, Satisfaction Score, No. of Patients Referred, Month & Year label |
| **Area chart** | 4 | Daily trend of Patients / Wait Time / Satisfaction / Referrals (Monthly View) |
| **Column chart** | 4 | Monthly trend of the same 4 KPIs (Consolidated View) |
| **Clustered column chart** | 1 | Patients by **Age Group** |
| **Clustered bar chart** | 2 | Patients by **Department Referral**; Patients by **Patient Race** |
| **Bar chart** | 1 | Patients by **Admission Status** |
| **Donut chart** | 2 | % Patients seen within 30 min (wait-time SLA); Patients by **Gender** |
| **Column chart (categorical)** | 1 | Patients by **Day of Week / Hour** |
| **Pivot table (matrix)** | 2 | Patient Admission Status breakdown; Waittime Interval × Day Name breakdown |
| **Table (tableEx)** | 1 | Full patient-level detail grid (Patient Details page) |
| **Slicer** | 5 | Date/Month filtering (see section 3) |
| **Shapes / textboxes** | many | Page titles, section dividers, background panels — cosmetic, not data-bound |

**Chart-to-KPI mapping (what each visual measures):**
- No. of Patients (volume)
- Avg Wait Time
- Satisfaction Score
- No. of Patients Referred
- % seen within 30 minutes (SLA compliance)
- Breakdown dimensions: Age Group, Gender, Race, Admission Status, Department Referral, Waittime Interval, Day of Week/Hour

---

## 5. Underlying data fields (from `Hospital ER_Data`)

Patient Id, Patient Full Name, Patient Gender, Patient Age, Patient Race, Patient Admission Date, Patient Waittime, Department Referral, Admission Status, Waittime Interval, plus derived measures: `No of Patients`, `Avg Wait Time`, `Satisfaction Score`, `No of Patient Referred`.

Date intelligence runs off a separate `Date Table` (Day, Day Name, Month Name, Month & Year, Date Hierarchy) — the standard star-schema pattern.


*

