# 🚦 Road Accident Analysis Dashboard
### SQL + Power BI Data Analytics Project

## 📌 Project Overview
Road accidents are a major global public safety issue. Analyzing accident data helps identify patterns that can improve traffic safety policies, infrastructure planning, and emergency response strategies.

This project analyzes **road accident data using SQL and Power BI** to extract meaningful insights about accident severity, vehicle types involved, environmental conditions, and accident locations.

The analysis transforms raw accident data into **interactive visual insights** that help stakeholders understand accident patterns and identify risk factors.

---

## 🎯 Project Objectives

The main objectives of this project are:

- Analyze **total accidents and casualties**
- Calculate **fatal accident percentage**
- Identify **vehicles responsible for the most casualties**
- Discover **monthly accident trends**
- Compare **urban vs rural accident patterns**
- Study the effect of **light vs darkness conditions**
- Identify **road types with the highest casualties**
- Determine **top cities with the highest accident rates**

---

## 🛠 Tools & Technologies

| Tool | Purpose |
|-----|------|
| SQL | Data querying and analysis |
| Power BI | Data visualization and dashboard creation |
| Excel | Data storage and preprocessing |

---

## 📂 Dataset Description

The dataset includes detailed information about road accidents such as:

- Accident Date
- Accident Severity
- Number of Casualties
- Vehicle Type
- Road Type
- Urban or Rural Area
- Light Conditions
- Local Authority (City)

These attributes help analyze accident patterns across different dimensions.

---

## 📊 Key Performance Indicators (KPIs)

### 1️⃣ Total Casualties
Total number of casualties recorded in the dataset.

```sql
SELECT SUM(number_of_casualties) AS CY_Casualties
FROM road_accident
WHERE YEAR(accident_date) = '2022';
```

---

### 2️⃣ Total Accidents

```sql
SELECT COUNT(accident_index) AS CY_Accidents
FROM road_accident
WHERE YEAR(accident_date) = '2022';
```

---

### 3️⃣ Fatal Casualties

```sql
SELECT SUM(number_of_casualties) AS Fatal_Casualties
FROM road_accident
WHERE YEAR(accident_date) = '2022'
AND accident_severity = 'Fatal';
```

---

### 4️⃣ Fatal Accident Percentage

```sql
SELECT 
CAST(SUM(number_of_casualties) AS DECIMAL(10,2))*100 /
(SELECT CAST(SUM(number_of_casualties) AS DECIMAL(10,2)) 
FROM road_accident) AS Fatal_Percentage
FROM road_accident
WHERE accident_severity = 'Fatal'
AND YEAR(accident_date) = '2022';
```

---

## 🚗 Accident Analysis Performed

### Vehicle Type Analysis

```sql
SELECT Type, SUM(number_of_casualties) AS Casualties
FROM (
SELECT *,
CASE 
WHEN vehicle_type IN ('Agricultural vehicle') THEN 'Agricultural'
WHEN vehicle_type IN ('Car','Taxi/Private hire car') THEN 'Car'
WHEN vehicle_type IN (
'Motorcycle 50cc and under',
'Motorcycle over 500cc',
'Motorcycle 125cc and under',
'Motorcycle over 125cc and up to 500cc',
'Pedal cycle') THEN 'Bike'
WHEN vehicle_type IN (
'Minibus (8 - 16 passenger seats)',
'Bus or coach (17 or more pass seats)') THEN 'Bus'
WHEN vehicle_type IN (
'Van / Goods 3.5 tonnes mgw or under',
'Goods over 3.5t. and under 7.5t',
'Goods 7.5 tonnes mgw and over') THEN 'Van'
ELSE 'Other'
END AS Type
FROM road_accident
) TEMP
WHERE YEAR(accident_date) = '2022'
GROUP BY Type
ORDER BY Casualties DESC;
```

---

### Monthly Accident Trends

```sql
SELECT DATENAME(MONTH, accident_date) AS Month,
SUM(number_of_casualties) AS Casualties
FROM road_accident
WHERE YEAR(accident_date) = '2022'
GROUP BY DATENAME(MONTH, accident_date);
```

---

### Accidents by Road Type

```sql
SELECT road_type,
SUM(number_of_casualties) AS Casualties
FROM road_accident
WHERE YEAR(accident_date) = '2022'
GROUP BY road_type
ORDER BY Casualties DESC;
```

---

### Urban vs Rural Accident Distribution

```sql
SELECT urban_or_rural_area,
CAST(SUM(number_of_casualties) AS DECIMAL(10,2))*100 /
(SELECT CAST(SUM(number_of_casualties) AS DECIMAL(10,2))
FROM road_accident
WHERE YEAR(accident_date)='2022') AS Percentage
FROM road_accident
WHERE YEAR(accident_date)='2022'
GROUP BY urban_or_rural_area;
```

---

### Light vs Darkness Conditions

```sql
SELECT 
CASE 
WHEN light_conditions IN (
'Darkness - no lighting',
'Darkness - lights lit',
'Darkness - lighting unknown',
'Darkness - lights unlit') 
THEN 'Darkness'
ELSE 'Light'
END AS Light_Condition,

CAST(SUM(number_of_casualties) AS DECIMAL(10,2))*100 /
(SELECT CAST(SUM(number_of_casualties) AS DECIMAL(10,2))
FROM road_accident
WHERE YEAR(accident_date)='2022') AS Percentage

FROM road_accident
WHERE YEAR(accident_date)='2022'

GROUP BY CASE 
WHEN light_conditions IN (
'Darkness - no lighting',
'Darkness - lights lit',
'Darkness - lighting unknown',
'Darkness - lights unlit') 
THEN 'Darkness'
ELSE 'Light'
END;
```

---

### Top 10 Cities with Highest Casualties

```sql
SELECT TOP(10)
local_authority,
SUM(number_of_casualties) AS Total_Casualties
FROM road_accident
GROUP BY local_authority
ORDER BY Total_Casualties DESC;
```

---

## 📊 Power BI Dashboard Features

The Power BI dashboard provides interactive visualizations including:

- Total casualties KPI
- Total accidents KPI
- Fatal accident percentage
- Monthly accident trends
- Vehicle type distribution
- Road type analysis
- Urban vs rural comparison
- Light vs darkness accident comparison
- Top cities with highest casualties

These visual insights help identify **patterns and risk factors in road accidents**.

---

## 📁 Project Structure

```
Road-Accident-Analysis
│
├── Road Accident Data.xlsx
├── Road Accident Analysis.pbix
├── Road Accident SQL Queries.sql
└── README.md
```

---

## 📈 Key Insights

Some insights discovered during the analysis include:

- Certain **vehicle categories contribute more to accident casualties**
- **Urban areas report a higher number of accidents**
- **Low-light conditions increase accident risks**
- Certain **road types show higher accident frequency**
- Some **cities consistently report higher casualty numbers**

---

## 🚀 Future Improvements

Possible improvements for this project:

- Add **geospatial accident analysis**
- Build a **Python-based accident prediction model**
- Deploy dashboard on **Power BI Service**
- Integrate **real-time traffic datasets**

---

## 👨‍💻 Author

Data Analytics Project demonstrating:

- SQL Data Analysis  
- Data Aggregation  
- Data Cleaning  
- Power BI Dashboard Development  
- Data Visualization  
- Analytical Thinking

---

### 📬 Connect
If you found this analysis interesting or have feedback, feel free to connect!
[**My LinkedIn Profile**](https://www.linkedin.com/in/yashmahadik-d77/)