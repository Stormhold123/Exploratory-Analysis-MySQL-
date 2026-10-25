# World Layoffs: Exploratory Data Analysis (MySQL)

Which companies, industries and countries were hit hardest by tech layoffs between 2020 and 2023, and how did the layoffs change over time?

This project explores the cleaned layoffs dataset using SQL. The cleaning process is documented in [World Layoffs: Data Cleaning](https://github.com/Stormhold123/Data-Cleaning-Project-MySQL-).

## Questions Explored
- How large were the biggest layoffs, and which companies shut down completely?
- Which companies, industries, countries and funding stages saw the most layoffs?
- How did layoffs change year by year and month by month?
- Who were the top 5 companies for layoffs in each year?

## Data
Cleaned layoffs table (`layoffs_working2`) covering **March 2020 to March 2023**. Raw data and cleaning steps are in the cleaning project.



![Date range of the data](images/E2.png)



## Analysis

1. **Extremes**: `MAX()` for the largest layoff and the highest percentage laid off. The largest single event was 12,000 employees, and some companies laid off 100% of staff
   

![Max layoffs](images/E1.png)


2. **Grouped totals** with `GROUP BY` and `SUM()` by company, industry, country, stage, date and year
3. **Rolling total**: a CTE with `SUBSTRING` to group layoffs by month, then `SUM() OVER (ORDER BY ...)` to track cumulative layoffs
   

![Monthly rolling total](images/E3.png)


4. **Top 5 companies per year**: two chained CTEs with `DENSE_RANK() OVER (PARTITION BY years ...)`
   

![Top companies per year](images/E4.png)



## Key Findings

- **About 384,000 layoffs** were recorded across the period
- **2022 was the peak year** with roughly 161,000 layoffs, and 2023 already had about 126,000 by early March, on pace to exceed 2022
- **Big Tech dominated**: Amazon (~18,150), Google (12,000), Meta (11,000), Salesforce (~10,090) and Microsoft (10,000) lead all companies
- **The United States accounted for about two thirds of layoffs** (~255K), followed by India (~36K) and the Netherlands (~17K)
- **Consumer and Retail were the hardest-hit industries**, followed by Other, Transportation and Finance
- **Post-IPO companies made up over half of layoffs** (~204K), so mature, publicly traded companies drove the totals
- **2020 looked different**: the top layoffs came from travel and gig companies such as Uber (7,525), Booking.com (4,375) and Groupon (2,800)
- Over 100 companies laid off **100% of their workforce**

## Files
- [`Exploratory_Analysis.sql`](Exploratory_Analysis.sql): full analysis script

## Skills Demonstrated
Aggregations · `GROUP BY` · CTEs · Window functions (`SUM() OVER`, `DENSE_RANK`) · Date functions · Rolling totals · Ranking within groups

## Tools
MySQL · MySQL Workbench
