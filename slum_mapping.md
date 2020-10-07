# Slum mapping

## Sources
| Dataset name | Source | URL | 
| ------- | ----- | ---- |
| Ward and prabhag shape file | Datameet Pune | https://github.com/datameet/Municipal_Spatial_Data/tree/master/Pune |
| ward population | PMC | https://www.pmc.gov.in/sites/default/files/miscellaneous/WARD-OFFICE-POPULATION-DATA.pdf |
| Pune slum shapefile | Mundhe (2019) | https://www.int-arch-photogramm-remote-sens-spatial-inf-sci.net/XLII-5-W3/57/2019/isprs-archives-XLII-5-W3-57-2019.pdf |
| Pune slum census | DCHB Part A 2011 (Pg 1282-1306) | https://censusindia.gov.in/2011census/dchb/DCHB_A/27/2725_PART_A_DCHB_PUNE.pdf |

## Objective of exercise
To understand the ward wise distribution of Water, Sanitation and Hygine (WASH) infrastructure
* The census DCHB has data about infrastructure in slums, however, this slum data is not mapped to any ward boundary or location
* Mundhe (2019) mapped slums in Pune as shapefiles to wards, however the wards are not as per the revised wards used by PMC in COVID reporting
* The revised wards used by PMC for COVID reporting can be formed by combining prabhags- eg- https://twitter.com/mohol_murlidhar/status/1305109505328312320
* This exercise tried to match the slum names in the census to the slum names in Dr.Mundhes mapping to get ward wise data

## Data
Refer excel workbook MAPPED_Pune_slums_df.xlsx

## Method (refer to excel sheet)
1. In sheet 1, using datameets prabhag shapefile and Mundhe (2019) slum shapefile, the prabhag that the centre of each slum settlement lies in was found, and the area of the prabhag has been found (using R)
* In Mundhe (2019), there are 458 slum settlements that are marked
* There were minor differences in the area of the slum identified (Shape_Area) and the area calculateed using R (slum_area_calc)

2. sheet 2.1 and 2.2 were created simultaneously and manually by referring to each other
* 2.1 shows the slum wise infrastrastructure taken from the census- there are 358 slums as per census 2011
* This is 100 settlements less than Dr.Mundhes mapping, hence, several of his settlements are not mapped on to the census data
* Slums with a unique and same name in both the lists were first matched with each other- 246/358 settlements were matched this way
* A pattern was observed while doing this, by matching with Dr.Mundhes data it was observed that all the slums in the census were arranged by ward even though the ward was not mentioned
* Using this slums with similar names and google map checks were matched with 'Reasonable confidence'. This included 16/358 settlemets
* 25/358 settlements in the census were matched to just 8 shapefiles. This is because the census showed multiple slums in the same locaton, but Dr.Mundhes shapefiles identified just a few in the same location. This could be possible if there were multiple settlements earlier which were later merged into one
* 2/358 slums in the census had multiple matches, and an aproximate location close to the original in the same ward was selected
* 70/358 settlements were matched by considering a huge approximation. This was still done by following the reasonable assumption that sequential slums in the censes fall in the same ward, however since there is no way to check it, it was marked as a 'huge aroximation'
* Based on this, the shapefiles were matched on to the census slum data (sheet 2.1)

3. After this matching process was done, sheet 3.prabhag was created by summing the values in sheet 2.1 over each prabhag
* ward population, SC/ST population was added to the prabhag data
* For each prabhag the total area of slums, total population and HH in the slums was calculated
* For each prabhag, the number of toilets and public taps and the per capita values were calculated

## Error calculation
* For each prabhag, the population of slums that were matched with a "huge aproximation" in step 2 was found
* This population found by a huge aproximation was divided by the total population of the ward to find the possible percentage of error
* Maximum possible error was in prabhag Vadgaon Dhayari - Vadgaon Budruk followed by (Kahdakmal Aali - Mahatma Phule Peth) and (Pune University - Wakadewadi)
* The error for the whole city is estimated to be at the most **14.2%**
