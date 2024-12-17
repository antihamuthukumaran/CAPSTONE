# Mortality Trends in Mental Health Disorders - Microsoft Fabric

![image](https://github.com/user-attachments/assets/46cd0898-61e8-41b5-a0c7-c383c50e7592)

## 🌟 Project Overview
This project aims to design and develop a semantic model to analyze trends in mortality rates, causes of death, and population statistics related to mental health disorders. The goal is to provide clear insights for data-driven decisions to support healthcare and public health initiatives.

## 🎯 Objective
The project focuses on:
- Analyzing mortality rates and identifying trends.
- Exploring causes of death and their impact.
- Visualizing population data across multiple dimensions to gain a better understanding of mental health-related mortality.

**Data Sources**:  
- MySQL  
- Excel  
- JSON  
- CSV

## 🗂 Data Tables
The project uses the following tables to structure the data:

### 🔹 Fact Tables:
- **FactZone**: Captures the relationship between mortality data and geographical zones.
- **FactAge**: Focuses on mortality trends by age groups.

### 🔹 Dimension Tables:
- **DimYear**: Provides a year-wise breakdown of mortality data.
- **DimDate**: Allows the breakdown of data by days or months.
- **DimCauses**: Categorizes various causes of death.
- **DimGender**: Contains mortality data segmented by gender.
- **DimZonePopulation**: Stores population data segmented by geographical zones.
- **DimAgePopulation**: Stores population data segmented by age groups.

## 🔧 Tools & Technologies Used
- **Microsoft Fabric**: Used for data ingestion, transformation, and modeling.
- **SQL Server**: Employed to write complex queries for analyzing the data.
- **Power BI**: Used for data visualization, creating interactive dashboards.

## 📊 Insights Derived
Key insights include:
- **Deaths Across All Ages**: Mortality trends across different age groups.
- **Mortality Rates by Gender and Age**: Breakdown of mortality rates segmented by gender and age.
- **Top Causes of Death Across Zones**: Identifying the leading causes of death in various geographical zones.
- **Year-over-Year Population Trends**: Analyzing population changes over time and their impact on mortality rates.

## 📈 Visualizations
The following visualizations were created using Power BI:
- **Bar Charts**: Visualized mortality rates segmented by gender, age, and cause of death.
- **Line Charts**: Displayed trends in mortality rates over the years.
- **Column Charts**: Showed the top causes of death across different geographical zones.
- **Tables**: Displayed detailed breakdowns of data, offering more in-depth analysis.
- **Map Visualizations**: Geographic visualizations to show mortality trends in different zones.

![image](https://github.com/user-attachments/assets/2e0b418a-7af3-4892-b23b-6c263a8981ca)

## 🔍 Project Execution – Step-by-Step

### 1. **Project Initiation and Objective Definition**
   - **Objective**: Defined the scope and the need for the analysis, focusing on trends in mortality rates, causes of death, and population statistics across age, gender, and geographical zones.

### 2. **Data Collection and Integration**
   - **Data Sources**: Data was collected from MySQL databases, Excel spreadsheets, and files in JSON and CSV formats.
   - **Data Cleaning**: Data was cleaned and prepared for analysis by handling missing values, ensuring consistency in formats, and joining datasets from different sources.
   
### 3. **Designing the Semantic Model**
   - **Modeling**: A semantic model was built using a **star schema**, where fact tables contained numerical data (mortality rates and population) and dimension tables contained descriptive data (age, gender, causes of death).
   - **Fact Tables**:
     - `FactZone`: Represents geographical areas and mortality rates across them.
     - `FactAge`: Represents mortality data by age groups.
   - **Dimension Tables**:
     - `DimYear`, `DimDate`: Represent temporal dimensions (year, month, date).
     - `DimCauses`: Categorizes the causes of death.
     - `DimGender`, `DimZonePopulation`, `DimAgePopulation`: Provides demographic breakdowns.

### 4. **Data Ingestion and Transformation in Microsoft Fabric**
   - **Ingestion**: Data was ingested into **Microsoft Fabric**, enabling seamless integration from different sources.
   - **Transformation**: The data was transformed into the required structure, cleaning any inconsistencies and joining multiple data sources into a unified format.

### 5. **SQL Server for Data Querying**
   - **SQL Queries**: Written in SQL Server to extract relevant metrics and trends, such as:
     - Mortality rates for different age groups and genders.
     - Year-over-year comparisons of population and mortality trends.
     - Identifying the leading causes of death in various geographical zones.

### 6. **Data Visualization Using Power BI**
   - **Power BI Dashboards**: Interactive dashboards were created to visualize key insights. These visualizations helped in understanding the trends and patterns in the mortality data:
     - **Bar Charts**: Represented mortality rates across different gender and age groups.
     - **Line and Column Charts**: Showed temporal trends and top causes of death.
     - **Map Visualizations**: Displayed geographical trends, providing a deeper insight into how mortality rates vary across regions.

![image](https://github.com/user-attachments/assets/05c86551-8308-4c8d-a3e1-01407b9ac094)

### 7. **DAX Formulas Used**

#### Mortality Rate Calculation
A DAX formula was used to calculate the **Mortality Rate** per 100,000 population:

    MortalityRate = 
      DIVIDE(SUM(FactAge[Deaths]), SUM(DimAgePopulation[Population])) * 100000
  This formula divides the total number of deaths (FactAge[Deaths]) by the total population (DimAgePopulation[Population]) and then multiplies the result by 100,000 to express the rate per 100,000 people.

#### Year-over-Year Mortality Comparison
A DAX formula was used to calculate the Year-over-Year Mortality Comparison:
 
    YoY_Mortality_Comparison = 
      CALCULATE(SUM(FactAge[Deaths]), SAMEPERIODLASTYEAR(DimDate[Date]))
   This formula calculates the total number of deaths for the same period in the previous year, allowing for year-over-year comparisons.

#### Gender-based Mortality Calculation
To calculate mortality rates based on Gender:

    MortalityByGender = 
      CALCULATE(SUM(FactAge[Deaths]), DimGender[Gender] = "Male")
  This formula calculates mortality for males by filtering the dataset where the gender is male.

#### Leading Causes of Death by Zone
To find the leading causes of death by geographical zone, the following DAX formula was used:

    TopCausesByZone = 
     TOPN(5, SUMMARIZE(FactZone, DimCauses[Cause], "TotalDeaths", SUM(FactZone[Deaths])), [TotalDeaths], DESC)
  This formula retrieves the top 5 causes of death based on the highest death counts in each geographical zone.
![image](https://github.com/user-attachments/assets/2857dc3e-f9e3-4f1d-a68c-bac0fb2f2c72)
## 📊 8. Insights and Analysis
Key Findings:
Trends in mortality rates were clearly visible across age groups, with some regions and genders showing higher mortality rates.
Year-over-year analysis provided insights into the overall changes in mortality trends.
Geographical insights helped pinpoint areas with high mortality rates and potential factors contributing to these rates.

## 9. Key Learnings
Microsoft Fabric: Greatly facilitated the data ingestion, transformation, and analysis process, enhancing the data lifecycle management.
Medallion Architecture: The architecture used in Microsoft Fabric improved data management by ensuring traceability and scalability.
Power BI Integration: Enabled real-time, interactive visualizations that were crucial for gaining actionable insights.

## 10. Acknowledgements
A special thank you to Instructor Frank Bergdoll and Instructor Steven Nich for their continuous guidance and mentorship throughout the project. Their expertise in Business Intelligence and data modeling has been instrumental in the successful completion of this project.

## 11. Future Improvements
Future enhancements could involve adding more detailed data (e.g., data on specific mental health disorders) and incorporating real-time data feeds for up-to-date insights.
Expansion to include additional dimensions such as socioeconomic factors and healthcare access could provide more comprehensive insights.

### DAX Formula Details:
 1. **Mortality Rate Calculation**: This formula calculates the mortality rate per 100,000 people by dividing the total number of deaths by the population size for each age group.
 2. **Year-over-Year Comparison**: The `SAMEPERIODLASTYEAR` function compares the current year's mortality to that of the previous year.
 3. **Gender-based Mortality**: This formula calculates mortality for a specific gender (in this case, males).
 4. **Top Causes of Death by Zone**: This formula ranks the causes of death by their total number of deaths in each zone.

These DAX formulas provide the essential calculations for analyzing the data in Power BI. You can integrate these formulas in your Power BI reports to derive actionable insights.






