# 📊 Power BI Role-Playing Dimension – Sales Analysis

## 📌 Overview

This project demonstrates how to implement a **role-playing dimension** in Power BI to analyze sales data using multiple date perspectives.

The objective is to analyze **sales based on Shipping Date**, even though the default relationship uses **Order Date**.

---

## 🧠 Business Scenario

Adventure Works needs to analyze **sales for a specific month (August)** based on **Shipping Date**.

However:

* There is only one **Date table**
* The **Sales table contains two date columns**:

  * Order Date (default)
  * Shipping Date

This creates a challenge because one Date table must serve **multiple roles**.

👉 Solution: **Role-Playing Dimension**

---

## 🏗️ Data Model

### Tables:

* **Sales**
* **Date**

---

## 🔗 Relationships

### 1️⃣ Active Relationship (Default)

* `Sales[OrderDate] → Date[Date]`
* Cardinality: Many-to-One (*:1)
* Cross filter: Single
* Status: ✅ Active

👉 Used for default filtering

---

### 2️⃣ Inactive Relationship (Role-Playing)

* `Sales[ShippingDate] → Date[Date]`
* Cardinality: Many-to-One (*:1)
* Cross filter: Single
* Status: ❌ Inactive

👉 Used only when explicitly activated in DAX

---

## 🧠 Relationship Summary

| Relationship        | Status     | Purpose          |
| ------------------- | ---------- | ---------------- |
| OrderDate → Date    | ✅ Active   | Default analysis |
| ShippingDate → Date | ❌ Inactive | Used via DAX     |

---

## 🧮 DAX Measure (Using FILTER)

```DAX
August Sales by Shipping Date =
CALCULATE(
    SUM(Sales[SalesAmount]),
    USERELATIONSHIP(Sales[ShippingDate], Date[Date]),
    FILTER(
        Date,
        MONTH(Date[Date]) = 8
    )
)
```

---

## 🔍 Explanation

* **SUM(Sales[SalesAmount])**
  → Calculates total sales

* **CALCULATE(...)**
  → Modifies filter context

* **USERELATIONSHIP(...)**
  → Activates the Shipping Date relationship

* **FILTER(...)**
  → Restricts calculation to August records

---

## 📊 Visualization

A **Table visual** is created with:

* `Date[Month]`
* `August Sales by Shipping Date`

### Expected Output:

* August → Shows value
* Other months → May still display values due to FILTER overriding context

---

## 🎨 Formatting

* Measure formatted as **Currency (£)**
* Decimal places set to **2**
* Clean and user-friendly layout

---

## ✅ Validation Steps

1. Verify that the measure returns correct **August sales total**
2. Cross-check totals with dataset
3. Confirm Shipping Date relationship is being used
4. Compare with Order Date results to validate difference

---

## 💡 Real-Life Analogy

Think of a **calendar 📅**:

* Used for **Order Date 📦**
* Used for **Shipping Date 🚚**

👉 Same table, multiple roles
👉 This is a **Role-Playing Dimension**

---

## 🚀 Key Learnings

* Role-playing dimensions in Power BI
* Active vs inactive relationships
* Using `USERELATIONSHIP` in DAX
* Applying filters using `FILTER`
* Understanding filter context behavior

---
```

---

## 🎯 Conclusion

This project demonstrates how to:

* Reuse a single dimension table for multiple roles
* Handle business requirements using DAX
* Build flexible Power BI reports

---

## 🙌 Author

**Vidya Vishnuvihar Geetha**

---

