# HR Analytics Dashboard — Tableau Calculated Fields

> Note: Tableau does **not** use DAX. DAX is mainly used in Power BI.
> For this Tableau dashboard, use **Calculated Fields**.

## 1. Employee Count

If your dataset has an `Employee Count` field:

```tableau
SUM([Employee Count])
```

If your dataset has one row per employee and an `Employee Number` field:

```tableau
COUNT([Employee Number])
```

Expected dashboard value: **1,470**

---

## 2. Attrition Count

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
```

Expected dashboard value: **237**

---

## 3. Active Employees

```tableau
SUM(
    IF [Attrition] = "No" THEN 1
    ELSE 0
    END
)
```

Expected dashboard value: **1,233**

Alternative:

```tableau
[Employee Count] - [Attrition Count]
```

---

## 4. Attrition Rate

```tableau
[Attrition Count] / [Employee Count]
```

Format this calculated field as **Percentage** with 2 decimal places.

Expected dashboard value: **16.12%**

---

## 5. Average Age

```tableau
AVG([Age])
```

Expected dashboard value: approximately **37**

---

## 6. Department-wise Attrition

Use:

- `Department` → Dimension
- `Attrition Count` → Measure

Calculated field:

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
```

---

## 7. Attrition by Gender

Use:

- `Gender` → Dimension
- `Attrition Count` → Measure

Calculated field:

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
```

Dashboard values shown:

- Male: **150**
- Female: **87**

---

## 8. Education Field-wise Attrition

Use:

- `Education Field` → Dimension
- `Attrition Count` → Measure

Calculated field:

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
```

---

## 9. Age Group

Create a calculated field named `Age Group`:

```tableau
IF [Age] < 25 THEN "Under 25"
ELSEIF [Age] <= 34 THEN "25 - 34"
ELSEIF [Age] <= 44 THEN "35 - 44"
ELSEIF [Age] <= 54 THEN "45 - 54"
ELSE "Over 55"
END
```

Use this field for your age-group attrition analysis.

---

## 10. Attrition by Age Group

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
```

Place:

- `Age Group` → Columns / Detail
- `Gender` → Color
- `Attrition Count` → Angle / Label

---

## 11. Job Satisfaction Rating

No special calculation is required if `Job Satisfaction` already contains ratings 1–4.

Use:

- `Job Role` → Rows
- `Job Satisfaction` → Columns
- Employee Count → Text / Color

For employee count:

```tableau
COUNT([Employee Number])
```

or:

```tableau
SUM([Employee Count])
```

depending on your dataset.

---

## 12. Age Bin

For the histogram, create a bin from the `Age` field in Tableau.

Recommended bin size:

```text
3
```

Then use:

- `Age (bin)` → Columns
- Employee Count → Rows

---

## 13. Attrition Percentage by Department

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
/
TOTAL(
    SUM(
        IF [Attrition] = "Yes" THEN 1
        ELSE 0
        END
    )
)
```

Format as Percentage.

---

## 14. Attrition Percentage by Gender

```tableau
SUM(
    IF [Attrition] = "Yes" THEN 1
    ELSE 0
    END
)
/
TOTAL(
    SUM(
        IF [Attrition] = "Yes" THEN 1
        ELSE 0
        END
    )
)
```

Format as Percentage.

---

## Suggested GitHub File Name

```text
Tableau_HR_Analytics_Calculated_Fields.md
```

Recommended project structure:

```text
HR-Analytics-Dashboard/
│
├── README.md
├── HR_Analytics_Dashboard.twbx
├── Tableau_HR_Analytics_Calculated_Fields.md
│
├── Dashboard/
│   └── hr_dashboard.png
│
└── Report/
    ├── HR_Analytics_Dashboard_Report.pdf
    └── HR_Analytics_Dashboard_Presentation.pptx
```
