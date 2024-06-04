# Chicago Data Analysis Project

This project involves exploring various datasets related to Chicago, including census data, public school data, and crime data. The analysis is performed using SQLite and includes several SQL queries to extract valuable insights from the data.

## Dataset Information

1. **Socioeconomic Indicators in Chicago**
   
This dataset contains a selection of six socioeconomic indicators of public health significance and a “hardship index,” for each Chicago community area, for the years 2008 – 2012.

Source: [Chicago Data Portal](https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2)

Description: This dataset includes information on various socioeconomic factors like per capita income, percent of households below the poverty line, and more.

2. **Chicago Public Schools**

This dataset shows all school-level performance data used to create CPS School Report Cards for the 2011-2012 school year. This dataset is provided by the city of Chicago's Data Portal.

Source: [Chicago Data Portal](https://data.cityofchicago.org/Education/Chicago-Public-Schools-Progress-Report-Cards-2011-/9xs2-f89t)

Description: This dataset includes details about public schools in Chicago, including safety scores and types of schools.

3. **Chicago Crime Data**

This dataset reflects reported incidents of crime (with the exception of murders where data exists for each victim) that occurred in the City of Chicago from 2001 to present, minus the most recent seven days.

Source: [Chicago Data Portal](https://data.cityofchicago.org/Public-Safety/Crimes-2001-to-present/ijzp-q8t2)

Description: This dataset includes records of crimes reported in Chicago, including details like case numbers, crime descriptions, and locations.

## Installation Instructions

1. **Clone the Repository**

`git clone https://github.com/your-username/Chicago-Data-Analysis.git`

`cd Chicago-Data-Analysis`

2. **Set Up the Environment**

Ensure you have Python and the necessary libraries installed. You can use the following commands to set up the environment:

`pip install pandas sqlite3 ipython-sql`

3. **Download the Datasets**

The datasets are automatically downloaded and imported into an SQLite database when you run the provided script.

## Usage Instructions

1. Load the Jupyter Notebook
Open the Jupyter notebook in your environment:

`jupyter notebook chicago_crime_analysis.ipynb`

2. Run the Analysis
Execute the cells in the notebook to run the SQL queries and analyze the data.

## SQL Queries Included

The following SQL queries are included in the analysis:

1. Total number of crimes recorded
   
`SELECT COUNT(*) FROM CRIME_DATA;`

3. Community areas with per capita income less than 11,000
   
`SELECT COMMUNITY_AREA_NUMBER, COMMUNITY_AREA_NAME, PER_CAPITA_INCOME FROM CENSUS_DATA WHERE PER_CAPITA_INCOME < 11000;`

5. Case numbers for crimes involving minors
   
`SELECT * FROM CRIME_DATA WHERE DESCRIPTION LIKE "%MINOR%";`

7. Kidnapping crimes involving a child
   
`SELECT * FROM CRIME_DATA WHERE IUCR BETWEEN 1790 AND 1792;`

9. Crimes recorded at schools
    
`SELECT * FROM CRIME_DATA WHERE LOCATION_DESCRIPTION LIKE "%SCHOOL%" GROUP BY IUCR;`

11. Average safety score for each type of school
    
`SELECT "Elementary, Middle, or High School", AVG(SAFETY_SCORE) AS Avg_Safety_Score FROM PUBLIC_SCHOOLS GROUP BY "Elementary, Middle, or High School";`

13. Community areas with highest % of households below poverty line
    
`SELECT COMMUNITY_AREA_NAME, PERCENT_HOUSEHOLDS_BELOW_POVERTY FROM CENSUS_DATA GROUP BY COMMUNITY_AREA_NAME ORDER BY PERCENT_HOUSEHOLDS_BELOW_POVERTY DESC LIMIT 5;`

15. Most crime-prone community area
    
`SELECT COMMUNITY_AREA_NUMBER, COUNT(CASE_NUMBER) AS NUMBER_OF_CASES FROM CRIME_DATA WHERE COMMUNITY_AREA_NUMBER IS NOT NULL GROUP BY COMMUNITY_AREA_NUMBER ORDER BY NUMBER_OF_CASES DESC LIMIT 10;`

17. Community area with highest hardship index
    
`SELECT COMMUNITY_AREA_NAME, HARDSHIP_INDEX FROM CENSUS_DATA WHERE HARDSHIP_INDEX = (SELECT MAX(HARDSHIP_INDEX) FROM CENSUS_DATA);`

19. Community Area Name with most number of crimes
    
`SELECT COMMUNITY_AREA_NAME, COUNT(CASE_NUMBER) AS NUMBER_OF_CASES FROM CENSUS_DATA CD, CRIME_DATA CCD WHERE CD.COMMUNITY_AREA_NUMBER = CCD.COMMUNITY_AREA_NUMBER GROUP BY COMMUNITY_AREA_NAME ORDER BY NUMBER_OF_CASES DESC LIMIT 1;`
