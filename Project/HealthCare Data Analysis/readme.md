# Patient Wait List Dashboard

An interactive Power BI dashboard that analyzes patient wait lists over time, across case types, specialties, age groups, and waiting-time bands.

---

## 🧭 Project Overview

This dashboard visualizes and analyzes patient waiting lists spanning **2018 to 2021**. It helps hospital administrators, analysts, and decision-makers:

- Monitor the **current size** of the wait list and compare with historical values  
- Understand **monthly trends** and fluctuations  
- Dive into **specialty-level** performance  
- Analyze how **waiting times** vary by **age group** and **time bands**  
- Enable interactive filtering, drill-through, and detailed analysis  

The goal is to support data-driven decisions to optimize patient flow, resource allocation, and reduce wait times.

---

### Key Objectives

1. Display the **total wait list** with comparisons (e.g. latest vs previous year)  
2. Analyze historical trends by case type (Outpatient, Inpatient, Day Case)  
3. Drill into specialties, age groups, and time bands  
4. Offer both a **Summary page** and a **Detailed view** for granular analysis  
5. Make the dashboard **interactive**, usable, and maintainable  

### Metrics & KPIs

- Latest total wait list  
- Previous year’s same-month wait list  
- Median / average wait time  
- Patient counts by specialty, age, and time band  
- Growth / decline trends over time  

### Data Scope

- Time period: 2018 – 2021 :contentReference[oaicite:1]{index=1}  
- Data includes outpatient and inpatient records  
- Specialty, age profile, time bands, and case type as key dimensions  

---

## 🗂️ Data & Dataset Description

**Source(s):**  
Data is loaded from a folder-based data repository (CSV / Excel files). :contentReference[oaicite:2]{index=2}

**Key Columns / Attributes:**

| Column / Field        | Description |
|------------------------|-------------|
| `Archive_Date`         | Date / month of record |
| `Case_Type`             | Outpatient, Inpatient, Day Case |
| `Specialty_Name`        | Name of medical specialty |
| `Age_Profile`           | Age bracket (0–15, 16–64, 65+) |
| `Time_Bands`             | Waiting-time ranges (e.g. 0–3 months, 3–6 months, etc.) |
| `Total`                 | Count of patients in that category / cell |
| (Plus any calculated fields) | — |

**Data Cleaning / Transformation:**

- Renamed and standardized column names across outpatient/inpatient data :contentReference[oaicite:3]{index=3}  
- Appended tables into a unified `All_Data` table :contentReference[oaicite:4]{index=4}  
- Trimmed whitespace, replaced inconsistent labels (e.g. “18+ months” vs “18 month +”) :contentReference[oaicite:5]{index=5}  
- Imported a **specialty mapping** file to group or categorize specialty names :contentReference[oaicite:6]{index=6}  
- Established relationships (e.g. between mapping table and master data) :contentReference[oaicite:7]{index=7}  

**Data Model & Relationships:**

- The main table `All_Data` is the core fact table  
- Specialty mapping table linked via `Specialty_Name`  
- Hidden original inpatient/outpatient tables (for intermediary use) :contentReference[oaicite:8]{index=8}  

---

## 📊 Dashboard Structure & Features

### Pages / Views

1. **Summary Page**  
   - Cards showing latest vs previous year totals  
   - Toggle switch for median vs average metrics  
   - Line charts trends (separate for Outpatient and Inpatient/Day Case)  
   - Top-5 specialties display  
   - Slicers / filters: date, specialty, case type  

2. **Detailed View**  
   - Matrix / tabular view: Archive_Date × Specialty × Age Profile × Time Bands × Case_Type × Total  
   - Enables drill-down and slicing for granular insight  

3. **Tooltip Page**  
   - Custom tooltip with charts & metrics  
   - Configured to show specialty-level wait list when hovering over visuals :contentReference[oaicite:9]{index=9}  

### Interactivity & Navigation

- **Toggle slicer** (Average / Median) to switch metric context dynamically  
- **Drill-through** via specialty or level filters  
- **Tooltips** with extra detail  
- **Navigation buttons**, conditional formatting, and alt text  
- Dynamic titles and responsive visuals using DAX SWITCH logic :contentReference[oaicite:10]{index=10}  

### DAX Measures & Logic

- `Latest Month Wait List = CALCULATE(SUM(All_Data[Total]), All_Data[Archive_Date] = MAX(All_Data[Archive_Date]))` :contentReference[oaicite:11]{index=11}  
- `PY Latest Month Wait List = … EDATE(MAX(...), -12)` :contentReference[oaicite:12]{index=12}  
- `Median Wait List`, `Average Wait List`, and a SWITCH measure to choose between them :contentReference[oaicite:13]{index=13}  
- Dynamic title measure to reflect “Average” vs “Median” context :contentReference[oaicite:14]{index=14}  
- Logic to handle “no data” scenarios when selection yields no records :contentReference[oaicite:15]{index=15}  

### Design & Layout

- Use of **gridlines** and **snap-to-grid** in layout for alignment :contentReference[oaicite:16]{index=16}  
- Background image design (created in external tools like PowerPoint / Canva) used as report canvas background :contentReference[oaicite:17]{index=17}  
- Color palette selection using tools like Adobe Color, inspired by external dashboard samples :contentReference[oaicite:18]{index=18}  

---

## ⚙️ Tools & Technologies Used

- **Power BI Desktop** (latest)  
- **Power Query / M** for data import & transformation  
- **DAX** for measure creation and logic  
- **Custom visuals** and built-in visuals (cards, line, bar, matrix)  
- **Folder connector** as data source  
- Published to **Power BI Service** for sharing / refreshing  

---

## 👤 Author & Credits

- **Author:** Chirag Mittal 
- **Credits / Inspiration:** PivotalStats’ end-to-end Power BI dashboard methodology

---
