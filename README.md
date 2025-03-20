# 🚆 Train Ticket Data Analysis

## 📌 Project Overview
This project analyzes train ticket sales and journey performance using **Python (Pandas, Matplotlib) & SQL**. The goal is to identify popular routes, delays, cancellations, and revenue trends to improve railway efficiency.

## 📂 Dataset Description
- **File Name:** `railway.csv`
- **Total Records:** 31,653
- **Columns:** 18 (Transaction ID, Purchase Details, Journey Details, Status, etc.)

## 🔧 Data Cleaning & Preprocessing
### **1️⃣ Convert CSV to Excel**
- Converted CSV to Excel for easier analysis in Excel.

### **2️⃣ Change Data Types**
- `Transaction_ID` → **Text**
- `Date_of_Purchase`, `Date_of_Journey` → **Date**
- `Time Columns (Departure, Arrival, Actual_Arrival)` → **Custom Time Format**
- Other categorical fields → **Text**

### **3️⃣ Rename Columns (Remove Spaces & Standardize)**
- Example: `Date of Purchase` → `date_of_purchase`
- All columns formatted to lowercase with underscores.

### **4️⃣ Standardizing Data & Removing Duplicates**
- Standardized **text format (lowercase, trimmed spaces)**.
- Merged duplicate categories (`staff shortage` → `staffing`, `weather condition` → `weather`).
- Removed **duplicate rows**.

### **5️⃣ Remove Unnecessary Columns**
- **Deleted:** `Time_of_Purchase` (not used in analysis).
- **Kept:** `Transaction_ID` (important for linking in SQL & Tableau).

### **6️⃣ Handling Missing Values**
- `Actual_Arrival_Time` blanks kept (indicates canceled trips).
- `Reason_for_Delay` blanks filled as **"No Delay"**.

## 🔍 Analysis Questions & SQL Queries
### **Main Questions:**
- **Top 5 most popular routes?**
- **Bottom 5 least popular routes?**
- **Top 5 canceled trips?**
- **Top 5 delayed trips?**
- **Which months have the highest on-time consistency?**
- **Most & least popular destinations?**
- **Percentage of canceled & delayed trips?**
- **Leading causes of cancellation & delays?**

### **SQL Queries Used**
#### **1️⃣ Top 5 Most Popular Routes**
```sql
SELECT departure_station, arrival_destination, COUNT(*) AS trip_count
FROM train_tickets
GROUP BY departure_station, arrival_destination
ORDER BY trip_count DESC
LIMIT 5;
```
#### **2️⃣ Most Canceled & Delayed Trips**
```sql
SELECT journey_status, COUNT(*) AS count
FROM train_tickets
WHERE journey_status IN ('canceled', 'delayed')
GROUP BY journey_status;
```

## 📊 Data Visualizations & Insights
### **1️⃣ Overview Analysis**
- **Purchase type distribution**
- **Ticket class & type breakdown**
- **Railcards usage & payment methods**
- **Journey status summary**
- **Total refund requests & revenue impact**

### **2️⃣ Route Analysis**
- **Top 5 most & least popular routes**
- **Most canceled & delayed routes**

### **3️⃣ Railway Performance**
- **Planned vs On-Time vs Delayed vs Canceled trips**
- **Trend line for canceled & delayed trips**
- **Monthly performance trends**
- **Leading causes of delays & cancellations**

## 🚀 How to Run This Project
### **1️⃣ Install Required Libraries**
```bash
pip install pandas numpy matplotlib seaborn sqlite3
```
### **2️⃣ Run Data Cleaning Script**
```bash
python scripts/data_cleaning.py
```
### **3️⃣ Execute SQL Queries**
```bash
sqlite3 data/railway_analysis.db < sql_queries/analysis.sql
```
### **4️⃣ Run Jupyter Notebook for Analysis & Visualization**
```bash
jupyter notebook notebooks/temp.ipynb
```

## 📌 Conclusion
- The dataset provides insights into **route popularity, delays, and cancellations**.
- Identifying **leading causes of delays** helps improve railway services.
- SQL & Python-based analysis allows **efficient reporting & visualization**.




