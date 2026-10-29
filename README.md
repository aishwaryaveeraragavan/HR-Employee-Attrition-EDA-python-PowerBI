# HR Employee Attrition Analysis

Exploratory Data Analysis (EDA) in Python and an interactive Power BI dashboard to find out **who is leaving a company, where, and why**.

<img width="645" height="377" alt="image" src="https://github.com/user-attachments/assets/6e4f67fb-8178-4c1f-8c0d-c8b10d75ec9c" />

---

## Project Overview

Employee attrition (employees leaving the company) is costly: it brings recruitment expense, training effort and loss of experience. This project analyses an IBM HR dataset to understand the factors linked to attrition and to recommend practical retention actions.

The analysis moves from simple to complex:

| Level | Variables | Question answered |
|---|---|---|
| Univariate | 1 | What does each column look like? |
| Bivariate | 2 | Which factors are related to attrition? |
| Multivariate | 3+ | Who exactly is at risk? |

Every chart is followed by a written interpretation, with the focus on the business story rather than just the plots.

---

## Dataset

| Item | Detail |
|---|---|
| File | `IBM_HR_Attrition_Enhanced.csv` |
| Rows | 1,470 employees |
| Columns | 39 (demographics, job, pay, satisfaction, tenure) |
| Missing values | None |
| Target | `Attrition` (Yes / No) |

**Data preparation**
- Dropped columns with no information: `EmployeeCount`, `StandardHours`, `Over18` (same value for every row) and `EmployeeNumber` (only an ID).
- Created a 0/1 attrition flag so that the average equals the attrition rate for any group.
- The data is imbalanced (1,233 stayed vs 237 left), so groups are compared using **percentage rates**, not raw counts.

---

## Tools and Technologies

- **Python:** Pandas, NumPy, Matplotlib, Seaborn
- **Google Colab:** notebook environment
- **Power BI Desktop:** interactive dashboard and DAX measures

---

## Key Findings

| Metric | Value |
|---|---|
| Total employees | 1,470 |
| Employees who left | 237 |
| Attrition rate | **16.12%** |
| Average monthly income | 6,503 |

1. **Overtime is the biggest driver.** 30.5% of overtime workers left versus 10.4% without overtime, about 3 times higher.
2. **Sales Representatives leave the most** (about 40%), followed by Laboratory Technicians (about 24%) and HR (about 23%). Managers (about 5%) and Research Directors (about 2.5%) are very stable.
3. **Sales with overtime is the highest-risk group** at 37.5% attrition. R&D rises from 8.6% to 27.3% with overtime, showing overtime is the real cause, not the department.
4. **Leavers are young and low-paid.** Median income of leavers is about 3,200 versus about 5,200 for stayers, and they cluster in the 18 to 35 age range.
5. **Lowest satisfaction and work-life balance together** show the highest attrition (47.1%).
6. **Performance rating does not explain attrition.** Ratings 3 and 4 both show about 16%, so high performers leave as often as others.

---

## Recommendations

| Problem found | Recommended action |
|---|---|
| High overtime attrition | Set overtime limits, hire extra staff in Sales, monitor overtime monthly |
| Young and low-paid staff leaving | Review entry-level pay, introduce career growth plans and mentoring |
| Sales Representatives (about 40%) | Improve incentives, workload and early-career support |
| Low satisfaction and work-life balance | Run satisfaction surveys, offer flexible working and wellbeing programs |
| Talent lost regardless of performance | Add recognition and promotion paths for high performers |

---

## Analysis Performed

### Univariate Analysis
- Attrition distribution (countplot)
- Age distribution (histogram)
- Monthly income distribution (histogram, right-skewed)

### Bivariate Analysis
- Attrition percentage by overtime
- Attrition rate by job role
- Monthly income by attrition (boxplot)

### Multivariate Analysis
- Attrition by department and overtime (heatmap)
- Age vs monthly income by attrition (scatterplot)
- Attrition by job satisfaction and work-life balance (heatmap)
- Attrition rate by performance rating

---

## Power BI Dashboard

The dashboard contains:
- **4 KPI cards:** Total Employees, Employees Left, Attrition Rate, Average Monthly Income
- **Charts:** attrition by overtime, job role and age group
- **Heatmaps (matrix):** department by overtime, satisfaction by work-life balance
- **Scatter chart:** age vs monthly income
- **Slicers:** Department, Job Role, Overtime, Age Group

**DAX measures used**

```DAX
Total Employees = COUNTROWS(df)

Employees Left = CALCULATE(COUNTROWS(df), df[Attrition] = "Yes")

Attrition Rate = DIVIDE([Employees Left], [Total Employees])

Avg Monthly Income = AVERAGE(df[MonthlyIncome])
```

> Add your dashboard screenshot here:
> `![Dashboard](images/dashboard.png)`

---

## Repository Structure

```
HR-Attrition-Analysis/
│
├── data/
│   └── IBM_HR_Attrition_Enhanced.csv
├── notebook/
│   └── HR_Attrition_EDA.ipynb
├── powerbi/
│   └── HR_Attrition_Dashboard.pbix
├── images/
│   └── dashboard.png
├── docs/
│   └── HR_Attrition_Project_Documentation.pdf
└── README.md
```

---

## How to Run

**Python notebook**
1. Open `notebook/HR_Attrition_EDA.ipynb` in Google Colab or Jupyter.
2. Upload `IBM_HR_Attrition_Enhanced.csv` (or update the file path in the first cell).
3. Click **Runtime > Run all**.

**Power BI dashboard**
1. Open `powerbi/HR_Attrition_Dashboard.pbix` in Power BI Desktop.
2. If prompted, update the data source path to the CSV file in the `data` folder.

---

## Limitations

- The analysis shows association, not proof of cause.
- The data is a single snapshot with no time dimension.
- Differences between groups are not tested statistically.

---


---

## Acknowledgement

Dataset: IBM HR Analytics Employee Attrition dataset (enhanced version).
