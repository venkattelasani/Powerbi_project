#  Telangana Weather Data Analysis (2021–2024) — Power BI Project

##  Overview
This project analyzes and visualizes Telangana’s weather patterns between **2021 and 2024** using **Power BI**.  
The goal is to transform raw weather data into meaningful insights about **temperature, rainfall, humidity, and wind speed** across different districts, seasons, and years.

---

##  Objective
To build a Power BI dashboard that provides:
- Yearly and seasonal weather trends  
- Regional comparisons (District & Mandal)  
- Insights on temperature, humidity, wind speed, and rainfall variations  

---

##  Key Business Problem
Telangana has diverse climate conditions across its districts. Understanding weather behavior helps in:
- **Agricultural planning and crop management**  
- **Urban development and disaster preparedness**  
- **Identifying extreme conditions and climate change patterns**

**Challenge:** Combine multiple years of weather data, clean it, and visualize it in an interactive dashboard for insights.

---

## ⚙️ Project Workflow

### 1️ Data Collection
- Collected yearly weather data for **2021–2024** (District and Mandal level).  
- Each file contained **daily readings** such as temperature, humidity, rainfall, and wind speed.

---

### 2️ Data Integration (Power Query)
- Imported all four yearly files into Power BI.  
- Used **Power Query → Append Queries** to combine them into a single dataset named `FactWeather`.

---

### 3️ Data Cleaning and Validation
Ensured the dataset was consistent and reliable by handling missing or invalid values.

| Parameter | Issue Found | Cleaning Applied |
|------------|-------------|------------------|
| Rain (mm) | Null values | Replaced with 0 |
| Temperature (°C) | 0 or negative values (impossible for Telangana) | Replaced with null |
| Humidity (%) | 0 or negative values | Replaced with null |
| Wind Speed (Kmph) | Negative values | Replaced with null |

 **Result:** Clean and trustworthy dataset ready for transformation.

---

### 4️ Feature Engineering (DAX Calculations)

#### **A. Measures**
```DAX
Avg_Temp =
AVERAGEX(
    FactWeather,
    (FactWeather[Max Temp (°C)] + FactWeather[Min Temp (°C)]) / 2
)

Avg_Humidity =
AVERAGEX(
    FactWeather,
    (FactWeather[Max Humidity (%)] + FactWeather[Min Humidity (%)]) / 2
)

Avg_Windspeed =
AVERAGEX(
    FactWeather,
    (FactWeather[Max Wind Speed (Kmph)] + FactWeather[Min Wind Speed (Kmph)]) / 2
)
```

#### **B. Calculated Columns**
```DAX
diff_Humidity =
FactWeather[Max Humidity (%)] - FactWeather[Min Humidity (%)]

Mandal_Name =
IF(NOT ISERROR(VALUE([Mandal])), [District] & "_" & [Mandal], [Mandal])

Month_Name = FORMAT(FactWeather[Date], "mmmm")

Season =
IF(FactWeather[Month_Name] IN {"December", "January", "February"}, "Winter",
IF(FactWeather[Month_Name] IN {"March", "April", "May"}, "Spring",
IF(FactWeather[Month_Name] IN {"June", "July", "August"}, "Summer", "Autumn")))

Year = YEAR(FactWeather[Date])
```

---

### 5️ Data Modeling
Created a single **Fact Table (`FactWeather`)** with all necessary fields for analysis:

| Column Name | Description |
|--------------|--------------|
| Date, Year, Month_Name, Season | Time dimensions |
| District, Mandal, Mandal_Name | Location dimensions |
| Avg_Temp, Avg_Humidity, Avg_Windspeed | Calculated measures |
| Rain (mm) | Daily rainfall |
| diff_Humidity, Max Temp, Min Temp | Derived insights |

 Optimized model for performance and easy filtering.

---

### 6️ Visualization (Power BI Dashboard Design)

| Section | Description | Visualization Type |
|----------|--------------|--------------------|
| KPI Summary | Displays overall metrics | Cards (Avg Temp, Avg Humidity, Avg Wind Speed, Total Rainfall) |
| District Analysis | Compare metrics across districts | Bar / Column Chart |
| Seasonal Trend | Weather variation across seasons | Line / Area Chart |
| Yearly Comparison | Weather changes over years | Line Chart |
| Humidity & Temperature Relation | Relation between humidity and temperature | Scatter / Combo Chart |

**Filters (Slicers):**
- Year (2021–2024)  
- District  
- Season  

---

### 7️ Insights Derived
-  **Rainfall** peaks during **June–September (Monsoon Season)**.  
-  **Highest temperatures** in **May**, especially in *Nalgonda* and *Mahabubnagar*.  
-  **Wind speed** increases during summer months due to convection currents.  
-  **Humidity** lowest in winter, highest in monsoon months.

---

##  Project Outcome
 Combined 4 years of Telangana weather data into one clean dataset  
 Removed anomalies and improved data quality  
 Created custom DAX measures and calculated columns  
 Designed an interactive Power BI dashboard  
 Derived actionable insights on seasonal and district-level climate patterns  

---

##  Key Learnings
- Practical understanding of **Power Query (ETL)**  
- Experience with **DAX measures and calculated columns**  
- Designed an **optimized data model**  
- Built clear and **interactive visual storytelling** in Power BI  

---

##  Tools & Technologies

| Tool | Purpose |
|------|----------|
| Power BI Desktop | Data modeling, DAX, visualization |
| Power Query | Data extraction and transformation |
| Excel / CSV Files | Source data |
| DAX | Custom measures and logic creation |

---

##  Project Structure
```
Telangana_Weather_Analysis/
│
├── Data/
│   ├── Weather_2021.csv
│   ├── Weather_2022.csv
│   ├── Weather_2023.csv
│   └── Weather_2024.csv
│
├── PowerBI_Files/
│   └── Telangana_Weather.pbix
│
├── Reports/
│   └── Dashboard_Screenshots/
│
└── README.md
```

---

##  Future Enhancements
- Add **forecasting visuals** using time-series prediction.  
- Build a **Date Dimension Table** for deeper analysis.  
- Automate **data refresh** with Power BI Service and APIs.

---


