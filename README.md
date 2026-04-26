# Group-6-MIST4610-Project-2

# Team Name
61608 Group 6

**Team Members:**
1. Gio Kim [@gyokode](https://github.com/gyokode)
2. Matheo Brooks [@matheobrooks-cpu](https://github.com/matheobrooks-cpu)
3. Luka Gangemi [@lukagangemi](https://github.com/lukagangemi)
4. Luke Piazza [@lukepiazza479](https://github.com/lukepiazza479)

**Dataset Description**
Dataset: Covid-19
Number of Tables: The dataset contains 43 tables in total. While the core documentation highlights 24 primary sources, the Snowflake instance includes additional data from the CDC, Apple, and the New York Times.
Approximate Row Counts: The dataset is a large-scale time-series collection with several tables exceeding 10 million rows. Key table sizes include:
JHU_COVID_19_TIMESERIES: ~12.45 million rows.
GOOG_GLOBAL_MOBILITY_REPORT: ~11.73 million rows.
JHU_COVID_19: ~9.74 million rows.
APPLE_MOBILITY: ~3.85 million rows.


## Question 1
**Which countries had the highest amount of total deaths, and what percentage of cases ended in deaths?**

This question pulled from the JHU_COVID_19_TIMESERIES table, and used data from COUNTRY_REGION, CASES, and CASE_TYPE within the table to categorize and calculate the totals. It is nontrivial because it looks beyond raw totals and focuses on the relationship between cases and deaths, which helps reveal how different countries were affected by COVID‑19. It’s interesting and meaningful because visualizing this data can highlight patterns that might connect to larger factors like geography, temperature, healthcare quality, or economic strength. From our point of view, this makes it a strong starting point for deeper analysis because it doesn’t just show what happened, but encourages exploration into why outcomes varied across regions and what underlying conditions may have influenced them.

## Question1 Chart 1
<img width="2457" height="757" alt="image" src="https://github.com/user-attachments/assets/f443694e-784d-429b-8a4e-0e655db1f99a" />
The Total Deaths by Country chart shows how the absolute number of COVID‑19 deaths varied across nations, highlighting which countries experienced the most severe outcomes in raw terms. From an analytical perspective, it reflects both the scale of the pandemic’s impact and potential differences in population size, reporting accuracy, and public health response. Seeing Brazil and India at the top suggests regions with large populations and prolonged waves of infection, while smaller totals in other countries may indicate stronger containment measures or demographic differences. Interpreting this chart helps establish a baseline for comparing how scale and context influence mortality, setting up deeper questions about what underlying factors, such as healthcare capacity or socioeconomic conditions, contributed to these disparities.
