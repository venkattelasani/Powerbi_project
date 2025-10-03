# Powerbi_project
Weather analysis based on rain,Temparature,Humidity and wind speed 
# Telangana Weather Data Analysis – Power BI Project

## 1. Data Loading
- Load all monthly tables from yearly folders (2021–2024).  
- Ensure **column names are consistent** across all tables.  
- Append all tables into a single dataset named **`FactWeather`**.  
- **Note:**  
  - Each district contains multiple mandals.  
  - Mandal names repeat daily for multiple records.  

## 2. Data Validation Rules

| Column               | Valid Values     | Invalid Values     | Action                        |
|---------------------|----------------|------------------|-------------------------------|
| Rainfall (mm)        | ≥ 0             | null              | Replace null with 0           |
| Min Temperature (°C) | > 0             | 0, -1, -15        | Replace with null             |
| Max Temperature (°C) | > 0             | -1                | Replace with null             |
| Min Humidity (%)     | > 0             | 0, -1             | Replace with null             |
| Max Humidity (%)     | > 0             | 0, -1             | Replace with null             |
| Wind Speed (kmph)    | ≥ 0             | Negative values   | Remove negative values        |

**Key Notes:**  
- Temperature values ≤ 0°C are invalid for Telangana.  
- Wind speed = 0 is valid (calm conditions).  

## 3. Data Integrity Rules
- **Uniqueness Constraint:** Only one record per mandal per date is allowed.  
- **Handling Duplicates:**  
  - If multiple records exist for the same mandal and date, retain the most valid record (least invalid/missing values).  
  - Remove all other duplicates.  

## 4. Missing Data Handling
- After validation, fill remaining null values using:  
  - **Forward fill (ffill)**  
  - **Backward fill (bfill)**  
- **Do not use averaging**, to preserve realistic weather patterns.  

## 5. Additional Notes
- Districts and mandals are the primary geographic units for analysis.  
- Data spans **January 2021 – April 2024**.  
- Dashboard allows filtering by **Year, Month, District, and Mandal**.  
- All transformations are performed in **Power Query** before visualization.  
