---
title: "Data Commons | Cost of Living and Food Insecurity"
permalink: /dc_cost_of_living/
layout: single
---

## Stakeholder(s)
- MasterCard Center for Inclusive Growth ([MasterCard Center](https://www.mastercardcenter.org/))
- Virginia Department of Health ([VDH](https://www.vdh.virginia.gov/))
- Fairfax County Countywide Data Analytics Unit ([CDA](https://www.fairfaxcounty.gov/data/))

## What is a Data Commons?
Data commons is an open knowledge repository that co-locates data from a variety of sources, builds and curates data insights, and provides tools designed to track issues over time and geography allowing governments and community stakeholders to learn continuously from their own data.

The Social and Decision Analytics Division has already deployed several data commons to empower policymakers with easy access to data analysis and visualizations. One example is the [Virginia Department of Health Data Commons](https://uva-bi-sdad.github.io/vdh_rural_health_site/).

<img src="../assets/img/vdh_data_commons.png" alt="">

Local communities have data on policies, strategies, events, and social behaviors but often lack the analytical tools to use their valuable data. Partnering with the **Mastercard Center for Inclusive Growth**, we hope to equip local communities in the National Capital Region with easy access to analytical tools like this to drive policy and strategy development.

## Cost of Living Calculator

One important section of our data commons is the proportion of households at risk of food insecurity in each region. To make a reliable estimation of households at risk, we need a trustworthy calculator for the cost of living in each corresponding region. A cost-of-living adjustment is important because it allows employees, retirees and people living on fixed incomes to afford housing, goods, services and taxes as prices increase over time.The cost of living is often used to compare how expensive it is to live in one city versus another. To account for sub-county level variations in cost of living, the geographic resolution we target is at census-tract level. According to the [U.S. Census Bureau](https://www.census.gov/programs-surveys/geography/about/glossary.html#par_textimage_13), a census tract is 

### Comparisons of Existing Calculators
We started our process by comparing three cost of living calculators

They are
- Economic Policy institute(EPI)
- MIT living Wage Calculator
- Washington Self Sufficiency (CFWW)

We analyzed data sources in each calculator and found out the best source

We took those different sources, merged them and proposed a new calculator

</center>![Our Process](assets/img/Methods.png){width = 40%}</center>

</center>![](assets/img/COL.png){width =40%}</center></center>

### Our Sources
There are various categories that a calculator have to take into consideration for estimating the Cost of living in a particular area. 

#### Categories
The categories in a calculator can be classified as
- Food
- Housing
- Transportation
- Child care
- Medical
- Miscellaneous
- Tax
- Credit

The following picture shows the **Methodology Summary** of our proposed Cost of Living Calculator

</center>![](assets/img/MethodologySummary.png){width = 40%}</center>

-Our Methodology Summary provides information about various categories present in a cost of living calculator with a description of their **calculation** process

-**Source** section indicates the **data source** 

-**User** section indicates which calculator uses that source

-**Level** of data indicates level of the data like county, tract or zip code level. 

### Examples from Fairfax County, VA

We took three **cesus tracts** from the Fairfax county and tried to calculate the cost of living for a number of hosueholds  and calculated who are food insecure according to our cost of living calculator. We tried it out with various combinations of households ranging from HH1 to HH7.
## Application with Food Insecurity

We use the cost of living calculator to estimate the number of households facing food insecurity or in risk of food insecurity in each census tract. We take the size of household as a independent variable for estimating the cost of living, and compare the cost to their income category to determine the risk.

### Iterative Proportional Fitting (IPF)

For privacy considerations, the Census Bureau only provides the aggregated figures at the census tract level, so from the American Community Survey (ACS), we can only retrieve the total number households in size and the total number of households in each income bracket, not a two-way table of the detailed composition. The following is an example of census tract 51.059.4922.01 in Fairfax County, VA: we can only retrieve the aggregated margins, and what's in the middle cells is missing.

| Household size | HH1  | HH2  | HH3  | HH4  | HH5  | HH6  | HH7  | TOTAL |
| ------------------ | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ----- |
| Less than $10,000    |      |      |      |      |      |      |      | 91    |
| $10,000 to $14,999   |      |      |      |      |      |      |      | 11    |
| $15,000 to $24,999   |      |      |      |      |      |      |      | 13    |
| $25,000 to $34,999   |      |      |      |      |      |      |      | 11    |
| $35,000 to $49,999   |      |      |      |      |      |      |      | 82    |
| $50,000 to $74,999   |      |      |      |      |      |      |      | 23    |
| $75,000 to $99,999   |      |      |      |      |      |      |      | 101   |
| $100,000 to $149,999 |      |      |      |      |      |      |      | 205   |
| $150,000 to $199,999 |      |      |      |      |      |      |      | 326   |
| $200,000 or more     |      |      |      |      |      |      |      | 1043  |
| TOTAL                | 986  | 384  | 309  | 113  | 67   | 20   | 27   | 1906  |

We use iterative proportional fitting (IPF) to estimate each cell and expand the two margins into a two-way table. IPF, a.k.a. RAS Algorithm in econometrics, makes an educated guess on the bivariate joint distribution. It starts with a presumed distribution, known as the seed, and proceeds to fit the aggregated margins. The choice of seed has a significant impact on the accuracy of the guess, so for each census tract, we use the ground-truth distribution of the PUMA they belong to as the seed.

A PUMA, or Public Use Microdata Area, is the aggregation of numerous census tracts that contains a total population of at least 100,000. In this much larger population, it is safer for the Census Bureau to release detailed data on the distribution within. This gives us an approximation of pattern of the two-way table in real life, and becomes our starting seed for IPF algorithm. For example, according to the [relationship file](https://www.census.gov/programs-surveys/geography/guidance/geo-areas/pumas.html), the census tract 51.059.4922.01 is part of PUMA 59304, so we use the two-way table of PUMA 59304 as seed and the margins of 51.059.4922.01 as raw data for IPF, and estimated the detailed distribution.

| 51059492201          | HH1  | HH2  | HH3  | HH4  | HH5  | HH6  | HH7  | TOTAL |
| -------------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ----- |
| Less than $10,000    | 72   | 12   | 7    | 0    | 0    | 0    | 0    | 91    |
| $10,000 to $14,999   | 10   | 0    | 1    | 0    | 0    | 0    | 0    | 11    |
| $15,000 to $24,999   | 10   | 2    | 0    | 0    | 0    | 1    | 0    | 13    |
| $25,000 to $34,999   | 10   | 1    | 0    | 0    | 0    | 0    | 0    | 11    |
| $35,000 to $49,999   | 74   | 2    | 2    | 2    | 2    | 0    | 0    | 82    |
| $50,000 to $74,999   | 18   | 2    | 2    | 0    | 1    | 0    | 0    | 23    |
| $75,000 to $99,999   | 66   | 7    | 13   | 5    | 5    | 5    | 0    | 101   |
| $100,000 to $149,999 | 125  | 38   | 19   | 10   | 3    | 5    | 5    | 205   |
| $150,000 to $199,999 | 186  | 69   | 42   | 12   | 4    | 9    | 4    | 326   |
| $200,000 or more     | 415  | 251  | 223  | 84   | 52   | 0    | 18   | 1043  |
| TOTAL                | 986  | 384  | 309  | 113  | 67   | 20   | 27   | 1906  |

### Real-world Examples

Combining the IPF result and the cost of living calculated in previous section, we can estimate the proportion of households facing or at risk of food insecurity in each census tract. To continue with the example of census tract 51.059.4922.01, in which the cost of living is

| Household size     | HH1    | HH2    | HH3     | HH4     | HH5     | HH6     | HH7     |
| ------------------ | ------ | ------ | ------- | ------- | ------- | ------- | ------- |
| Annual cost in USD | 51,532 | 83,456 | 117,473 | 150,888 | 172,162 | 186,675 | 199,703 |

We consider all households of size 1 making less than \$49,999 a year as food insecure, and in need of government help, and since \$51,532 falls in the category of \$50,000 to \$74,999, we consider households in this category as in risk of food insecurity. In this way, we reach the following table as the conclusion of food insecurity estimations for census tract 51.059.4922.01.
| Status of insecurity | count | percentage |
| ------------------------ | ---- | ---- |
| Food Insecure HH         | 264  | 14%  |
| Food Insecure plus At-Risk HH | 337  | 18%  |
| No Food Insecure HH      | 1569 | 82%  |
| Total                    | 1906 | 100% |
## Evaluation of results

Caveats, implications, etc.

## Team

Some pictures here
