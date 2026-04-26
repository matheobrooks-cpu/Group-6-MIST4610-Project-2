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
<br>
This question pulled from the JHU_COVID_19_TIMESERIES table, and used data from COUNTRY_REGION, CASES, and CASE_TYPE within the table to categorize and calculate the totals. It is nontrivial because it looks beyond raw totals and focuses on the relationship between cases and deaths, which helps reveal how different countries were affected by COVID‑19. It’s interesting and meaningful because visualizing this data can highlight patterns that might connect to larger factors like geography, temperature, healthcare quality, or economic strength. From our point of view, this makes it a strong starting point for deeper analysis because it doesn’t just show what happened, but encourages exploration into why outcomes varied across regions and what underlying conditions may have influenced them.

## Question 1 Chart 1
<img width="2457" height="757" alt="image" src="https://github.com/user-attachments/assets/f443694e-784d-429b-8a4e-0e655db1f99a" />
<br>
The Total Deaths by Country chart shows how the absolute number of COVID‑19 deaths varied across nations, highlighting which countries experienced the most severe outcomes in raw terms. From an analytical perspective, it reflects both the scale of the pandemic’s impact and potential differences in population size, reporting accuracy, and public health response. Seeing Brazil and India at the top suggests regions with large populations and prolonged waves of infection, while smaller totals in other countries may indicate stronger containment measures or demographic differences. Interpreting this chart helps establish a baseline for comparing how scale and context influence mortality, setting up deeper questions about what underlying factors, such as healthcare capacity or socioeconomic conditions, contributed to these disparities.


## Question 1 Chart 2
<img width="2453" height="749" alt="image" src="https://github.com/user-attachments/assets/455d54fb-d628-458f-8168-f76036302d38" />
<br>
The Percentage of Deaths by Country chart shows how deadly COVID‑19 was relative to the number of confirmed cases in each country. Analytically, this percentage is important because it normalizes the data. It accounts for differences in population size and testing rates, allowing for a clearer comparison of case fatality rates across regions. Countries like Peru and Egypt, which show higher percentages, may indicate challenges in healthcare capacity, testing accessibility, or reporting accuracy. This measure is meaningful because it highlights efficiency and resilience in health systems, helping identify where outcomes were disproportionately severe and prompting deeper investigation into social, environmental, or policy factors that influenced survival rates.

## Question 1 Streamlit Analysis
<img width="2392" height="1548" alt="image" src="https://github.com/user-attachments/assets/a3bf2d9a-e2c4-4204-b122-3d6e1691a920" />
<br>
<br>
<img width="2396" height="1547" alt="image" src="https://github.com/user-attachments/assets/b50f864c-e43e-44c2-896c-fbaedb0bed37" />
<br>
Adding the year slider in Streamlit is analytically valuable because it transforms the dashboard from a static snapshot into a dynamic, time‑based analysis tool. By allowing users to adjust the year, the visualization reveals how patterns of total deaths and fatality percentages evolved over time, making it possible to identify trends, turning points, and anomalies that a single‑year view would miss. This temporal flexibility supports deeper analytical reasoning, as users can compare the progression of the pandemic across regions, evaluate the effectiveness of interventions, and observe how external factors such as vaccine rollout or policy changes influenced outcomes. In essence, the year slider enhances the dashboard’s explanatory power, enabling a more nuanced understanding of how the pandemic’s impact shifted across different periods and helping connect data patterns to broader social, economic, and environmental contexts.
<br>
Comparing the two screenshots reveals how the year slider changes the analytical perspective by showing shifts in both total deaths and case fatality rates between years. In the earlier year, countries like Brazil and India dominate the Total Deaths by Country chart, reflecting large populations and sustained outbreaks. By contrast, in the later year, the distribution becomes more balanced, with countries such as Germany and Spain appearing more prominently, suggesting either improved reporting or later waves of infection.
<br>
The Case Fatality Rate (%) chart also shows meaningful variation: nations like Peru and Bulgaria maintain high fatality percentages, while others such as Indonesia and Greece show moderate rates, indicating possible improvements in healthcare response or testing coverage. Analytically, this comparison highlights how the pandemic’s impact evolved — not only in scale but in severity and management efficiency. Observing these year‑to‑year changes helps identify where interventions may have reduced mortality and where persistent vulnerabilities remained, making the slider a powerful tool for temporal and comparative analysis.
