# Group-6-MIST4610-Project-2

# Team Name: 61608 Group 6

**Team Members:**
1. Gio Kim [@gyokode](https://github.com/gyokode)
2. Matheo Brooks [@matheobrooks-cpu](https://github.com/matheobrooks-cpu)
3. Luka Gangemi [@lukagangemi](https://github.com/lukagangemi)
4. Luke Piazza [@lukepiazza479](https://github.com/lukepiazza479)
## Dataset 
We chose the COVID-19 Epidemiological Data set because it included a lot of data we were interested in exploring, specifically how the epidemic responded to changes in geography and demographics, and how the different vaccine roll-outs across the world affected the outbreaks. It also lent itself well to manipulation tools (like timelines) so we could make assess the data and draw conclusions about it. 

## Dataset Description
Dataset: COVID-19 Epidemiological Data

Number of Tables: The dataset contains 43 tables in total. While the core documentation highlights 24 primary sources, the Snowflake instance includes additional data from the CDC, Apple, and the New York Times.

Approximate Row Counts: The dataset is a large-scale time-series collection with several tables exceeding 10 million rows. 

Key table sizes include:
JHU_COVID_19_TIMESERIES: ~12.45 million rows.
GOOG_GLOBAL_MOBILITY_REPORT: ~11.73 million rows.
JHU_COVID_19: ~9.74 million rows.
APPLE_MOBILITY: ~3.85 million rows.


## Questions and Justification (Question 1)
**Which countries had the highest amount of total deaths, and what percentage of cases ended in deaths?**
<br>
This question pulled from the JHU_COVID_19_TIMESERIES table, and used data from COUNTRY_REGION, CASES, and CASE_TYPE within the table to categorize and calculate the totals. It is nontrivial because it looks beyond raw totals and focuses on the relationship between cases and deaths, which helps reveal how different countries were affected by COVID‑19. This data is meaningful because visualizing it can highlight patterns that might connect to larger factors like geography, temperature, healthcare quality, or economic strength. From our point of view, this makes it a strong starting point for deeper analysis because it doesn’t just show what happened, but encourages exploration into why outcomes varied across regions and what underlying conditions may have influenced them.
## Data Manipulations (Question 1)
**Aggregation & Filter**

    MAX(CASE WHEN CASE_TYPE = 'Deaths' THEN CASES ELSE 0 END) AS total_deaths,
    MAX(CASE WHEN CASE_TYPE = 'Confirmed' THEN CASES ELSE 0 END) AS total_cases,

Uses a CASE statement to isolate rows where CASE_TYPE equals 'Deaths' and 'Confirmed'. It then takes the maximum value of CASES for each country, finding the total death count, and filters for 'Confirmed' case type and returns the maximum count.

**Calculation**

    ROUND((total_deaths / NULLIF(total_cases, 0)) * 100, 2) AS cfr_percentage

Calculates the Case Fatality Rate (CFR): the percentage of deaths among confirmed cases. NULLIF(total_cases, 0) prevents division by zero errors, and ROUND(..., 2) formats the result to two decimal places for readability.

**Secondary Filter**

    GROUP BY COUNTRY_REGION
    HAVING total_cases > 1000

The GROUP BY clause organizes all rows by country so that aggregate functions like MAX() and ROUND() apply to each nation’s data rather than the entire dataset. The HAVING total_cases > 1000 filter then removes countries with fewer than 1,000 confirmed cases, keeping the focus on statistically meaningful results for your dashboard visualization.


## Analysis and Results (Question 1)
**Question 1 Chart 1**
<img width="2457" height="757" alt="image" src="https://github.com/user-attachments/assets/f443694e-784d-429b-8a4e-0e655db1f99a" />
<br>
The Total Deaths by Country chart shows how the number of COVID‑19 deaths varied across nations, showing which countries experienced the most deaths. From an analytical perspective, it reflects the pandemic’s impact in those countries and differences in population size, reporting accuracy, and public health response. Seeing Brazil and India at the top suggests regions with large populations were hit harder, while smaller totals in other countries may indicate stronger containment measures or demographic differences. Interpreting this chart helps establish a baseline for comparing how scale and context influence the effect of the pandemic, and can help answer questions about what underlying factors, such as healthcare capacity or socioeconomic conditions, contributed to these disparities.


**Question 1 Chart 2**
<img width="2453" height="749" alt="image" src="https://github.com/user-attachments/assets/455d54fb-d628-458f-8168-f76036302d38" />
<br>
The Percentage of Deaths by Country chart shows deaths by case amount. Analytically, this percentage is important because it normalizes the data. It accounts for differences in population size and testing rates, allowing for a clearer comparison of case fatality rates across regions. Countries like Peru and Egypt, which show higher percentages, may indicate challenges in healthcare capacity, testing accessibility, or reporting accuracy. This measure is meaningful because it highlights efficiency and resilience in health systems, helping identify where outcomes were more or less severe proportional to population and prompting deeper investigation into other factors that may have influenced survival rates.

## Streamlit App (Question 1)
<img width="2392" height="1548" alt="image" src="https://github.com/user-attachments/assets/a3bf2d9a-e2c4-4204-b122-3d6e1691a920" />
<br>
<br>
<img width="2396" height="1547" alt="image" src="https://github.com/user-attachments/assets/b50f864c-e43e-44c2-896c-fbaedb0bed37" />
<br>

Adding the year slider in Streamlit is analytically valuable because it transforms the dashboard from a static snapshot into a dynamic, time‑based analysis tool. The visualization reveals how patterns of total deaths and fatality percentages evolved over time, making it possible to identify trends, turning points, and anomalies that a single‑year view would miss. This ability to change the year  helps supports deeper analysis, as we can compare the progression of the pandemic across regions, evaluate the effectiveness of interventions, and observe how external factors such as vaccine rollout or policy changes influenced outcomes.

Comparing the two screenshots reveals how the year slider changes the analytical perspective by showing shifts in both total deaths and case fatality rates between years. In the earlier year, countries like Brazil and India ranked relatively high on the Total Deaths by Country chart, persumably due to large populations and sustained outbreaks. By contrast, in the later year, the distribution becomes slightly more balanced, with countries such as Germany and Chile appearing more prominently, suggesting either improved reporting or later waves of infection.

The Case Fatality Rate (%) chart also shows meaningful variation: nations like Peru and Bulgaria maintain high fatality percentages, while others such as Indonesia and Greece show moderate rates, indicating possible improvements in healthcare response or testing coverage. Analytically, this comparison highlights how the pandemic’s impact evolved, not only in scale but in severity and management efficiency. Observing these year‑to‑year changes helps identify where interventions may have reduced mortality and where persistent vulnerabilities remained, making the slider a powerful tool for temporal and comparative analysis.

**All data viewable in Streamlit, only some countries listed in screenshots for ease of viewing.

**Use of AI**


I asked Copilot to help me update my Snowflake Streamlit dashboard so that the COVID‑19 graphs could be filtered by year using a slider. I had it look at the auto generated python script Streamlit gave me, and adjust it accordingly. Throughout the process, I requested full script rewrites to avoid unnecessary and confusing complications. The SQL was updated to correctly extract the year from the date field, the code structure was cleaned up to remove indentation errors, and the data‑loading logic was reorganized so both charts update smoothly when the slider changes. The final result was a fully working version of my original dashboard with the required upgrade.

I didn’t use several optional enhancements the AI suggested, such as metric cards, dropdown filters, or additional visualizations, because I did not want to overcomplicate the code or the graphs. I also rejected earlier drafts of the script that included multiple queries or had formatting issues, and kept only the streamlined version that accomplished what I wanted it to.

## Questions and Justification (Question 2)
**Question: How did vaccination rates influence changes in COVID‑19 cases across different countries over time?**

This question is non-trivial because it challenges one of the most widely held assumptions of the pandemic, that being that getting more people vaccinated would directly bring case counts down, when the truth is more complicated than that. It's meaningful because large decisions were made during the pandemic with this assumption in mind, from when governments lifted restrictions and reopened businesses to the billions of dollars spent producing and distributing vaccines worldwide. Whether those rollouts actually did what they were supposed to do in terms of reducing cases has lasting consequences for public trust in health institutions, economic recovery, and how prepared we are to respond to the next crisis.

**Tables/columns used:**

**JHU_COVID_19 (Johns Hopkins table)**

    country_region: identifies the country being analyzed
            
    date: used to aggregate data by month
            
    cases: cumulative confirmed cases
            
    case_type: filtered to include only confirmed cases

**OWID_VACCINATIONS (Our World in Data table)**

    country_region: used to join with case data
      
    date: aligns vaccination data with case data
      
    total_vaccinations: cumulative number of vaccinations administered
      
    people_fully_vaccinated: additional context on vaccination progress

## Data Manipulations (Question 2)
**Filter**

    WHERE j.country_region IN ('Germany')

Limits the data to a single country. The IN operator is used rather than equals to support multiple country selections when the query is called from Streamlit.

**JOIN**

    LEFT JOIN owid_vaccinations v 
        ON j.country_region = v.country_region 
        AND j.date = v.date

This joins the COVID case dataset with the vaccination dataset by matching on country and date. A LEFT JOIN is used to ensure that all case data is preserved even if corresponding vaccination data is missing for certain dates.

**Aggregation**

    MAX(v.total_vaccinations) AS total_vaccinations
    MAX(v.people_fully_vaccinated) AS people_fully_vaccinated

Since the source data contains daily records, these aggregate daily values up to a monthly level by taking the highest value recorded within each month. MAX is used because vaccination counts are cumulative (they only ever increase), so the last day of the month will always hold the highest value.

**Date Truncation**

    DATE_TRUNC('month', j.date) AS month

Rounds each daily date down to the first day of its month, allowing all daily records within the same month to be grouped together.

**LAG Function**

    LAG(total_vaccinations) OVER (PARTITION BY country_region ORDER BY month)

Looks back at the previous month's cumulative vaccination total for the same country, making it available in the current row so it can be subtracted to calculate the monthly increment.

**Calculated Field**

    COALESCE(
        total_vaccinations - LAG(total_vaccinations) OVER (
            PARTITION BY country_region
            ORDER BY month
        ),
        0
    ) AS monthly_vaccination_increment

COALESCE handles the nulls. when LAG tries to subtract the previous month's vaccination total from the current month's, the very first month for each country has no previous row to look back at, so the subtraction returns NULL. COALESCE replaces that NULL with a 0. This is exactly what you want because before vaccinations started there were zero new vaccinations that month, so the chart starts at zero rather than showing a gap or blank space at the beginning of each country's timeline.

The explanations above are for the Monthly New COVID-19 Vaccinations Snowsight visualization. Everything applies to the Monthly New Confirmed COVID-19 Cases Snowsight visualization except for two things — an additional filter for case_type = 'Confirmed' to exclude non-case records such as deaths and recoveries, and the monthly increment calculation does not include a COALESCE wrapper meaning the first month returns NULL rather than zero.

## Analysis and Results (Question 2)
**Question 2 Chart 1**

<img width="756" height="468" alt="Screenshot 2026-04-26 at 8 11 20 PM" src="https://github.com/user-attachments/assets/5d1554b5-fff8-4be8-a8b9-d90b737d077e" />

**Analysis:** This chart shows Germany's monthly COVID vaccinations from early 2020 through early 2023, with two sharp peaks hitting around 25 million and 27 million doses in April and November 2021 before dropping off and staying near zero through 2023. This could be telling us that Germany's vaccination coverage was not all at once, but instead came in two waves, which means any attempt to correlate vaccination rates for the fact that meaningful vaccine coverage only existed during a very specific timeframe. That uneven distribution matters because it limits how you can correlate changes in cases to vaccination alone, and points to the need for additional variables to be factored into any real analysis.


**Question 2 Chart 2**

<img width="757" height="456" alt="Screenshot 2026-04-26 at 8 12 56 PM" src="https://github.com/user-attachments/assets/b7b0f6c8-2c33-42a1-aea5-0c3cb02bba34" />

**Analysis:** This chart shows Germany's monthly new confirmed COVID-19 cases from early 2020 through early 2023, remaining relatively flat and manageable below 200k through all of 2020 and 2021 before increasing to over 1.2 million new cases in early 2022, then staying elevated with several additional waves through 2023. What this tells us analytically is that the largest surge in cases after Germany's vaccination rollout, meaning there is no simple inverse relationship between vaccination rates and case counts in this data and that more variables need to be included in any sort of data analysis regarding this.

For Question 2 charts 1 and 2 above, Snowsight automatically determines x-axis label spacing for readability, which limits the ability to display every time interval even when the underlying data is aggregated monthly. This issue is addressed via Streamlit.

## Streamlit App (Question 2)
<img width="588" height="413" alt="Screenshot 2026-04-27 at 1 32 05 PM" src="https://github.com/user-attachments/assets/9f932259-2c4b-459d-984a-5ec39dfb18a1" />
<img width="587" height="361" alt="Screenshot 2026-04-27 at 1 33 36 PM" src="https://github.com/user-attachments/assets/ef5d3167-bb60-4230-9175-0ec48bb6a3e5" />

**Analysis:** The multiselect dropdown lets users pick up to three countries at once, updating both charts simultaneously so each selected country appears as its own data series. The analytical value comes from being able to put vaccination data and case data side by side across multiple countries on the same timeline. For example, when we load Germany, Brazil, and Japan together, it becomes clear that, while all three countries vaccinated at different times and different volumes between 2021 and 2023, they ended up with similarly unpredictable case outcomes relative to their vaccination efforts. 

This is significant because it suggests that neither vaccination timing or volume could 100% predict case outcomes across these three countries, which directly challenges the assumption that vaccination patterns alone can explain how the pandemic played out differently by country. Other factors like prior infection rates, population behavior, variant timing, and public health policy played a larger role in shaping each country's pandemic trajectory than vaccination patterns did, which is something that can be seen clearly by manipulating the dropdown menu.

**Use of AI**

AI assistance was used during the development of the Snowsight dashboard and Streamlit app to help troubleshoot errors, structure SQL queries, and implement features such as multi-country selection and data transformations. The final implementation reflects manual verification and adjustments to ensure accuracy and functionality.













