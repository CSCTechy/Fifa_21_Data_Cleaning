# Fifa_21_Data_Cleaning
Data cleaning ensures integrity and obtaining accurate results


## INTRODUCTION

Data cleaning is very important for effective analysis. It is one thing every data analyst should do and do properly before carrying out analysis otherwise it can cause serious problems. Before cleaning data, it is important to look out for some of the following that wo uld like make a data dirty, these includes spelling and other texts errors, inconsistent labels, formats and field lane, missing data and duplicates.

Here a documentation of the cleaning process for FIFA '21 dataset is being presented. This dataset was provided as part of a challenge #Datacleaningchallenge launched on twitter by data ethusiasts to test the abilities of newbies, intermediate and advanced Data analyst for a large messy dataset.

The fifa '21 dataset contains 18,980 rows and 77 columns of football players statistics and demography in 2021. The dataset is publicly available on kaggle which contains data scrapped from sofifa. The datafile also includes a Data dictionary. a column named player url which contains a link to the player profile on sofifa to give the analyst furher insight and full details of players just in case of missing information. Here's a link to the dataset source  https://www.kaggle.com/datasets/yagunnersya/fifa-21-messy-raw-dataset-for-cleaning-exploring

In carrying out the data cleaning process, the tool I used was the Power Query Editor in Microsoft Excel.

### GOAL OF THE PROJECT

The goal of the data cleaning project on the fifa '21 dataset is to ensure the data is clean from dirt so as to allow for effective analysis.


### DATA CLEANING PROCESS

Before I began the cleaning process after loading the dataset, the following columns were marked for cleaning; Longname ,Nationality , OVA , POT , Club , Contract , Height , Weight , BOV , Loan End date , Value, wage , release clause , W/F , SM , IR , and Hits.

| Before | After |
| --- | --- |
| ![Identified dirtydata](https://user-images.githubusercontent.com/63916057/225563068-c0f84644-07e9-45d3-97bc-812b476e62bd.JPG) | yes |
| Identified dirty data | Cleaned Data  |

> Note: Some columns were hidden for screenshot purpose so as to capture those worked on for display in this documentation.
                                                   
### LongName
Cleaning this, I used the filter to look through the names and having identified some names were abbreviated here, I filtered those names and ensured they were fully spelt. Then I inserted an column to the right and applied the TRIM() function to remove any leading whitepace available in the name column that might cause issues later on and then copied and paste as values to get rid of the function.


### Nationality
Here there wasn’t much to clean but all I did was to apply the TRIM() function so as to get rid of any whitespace that might possibly exist in any of the rows.

### OVA
From the provided data dictionary for the challenge, we were required to format the data type of this column as percentage. In achieving this, I inserted a new column to the right and typed 100 into the first cell and copied it, after which I moved to the original column, highlighted all the rows using Ctrl + Shift + Down-arrow, the right clicked to paste special and clicked divide. After doing so I finally changed the datatype to percentage and got my result.

| Before | After |
| --- | --- |
| ![OVA](https://user-images.githubusercontent.com/63916057/225574375-11dfc2ef-26b1-4ab2-b887-c2b598269368.JPG) | ![OVA cleaned](https://user-images.githubusercontent.com/63916057/225575478-9d455284-f52c-4c3c-bf40-00c92668c00b.JPG) |


### POT
Same requirement as the OVA and I also applied the same process to achieve my results too.

### Club
I noticed some data in this column contained nonprintable characters and also using the filter I also noticed some blank spaces. Firstly, I sorted out all blanks and filled them up with “no club”. Then in solving the rows with nonprintable characters I used the CLEAN() function.

| Before | After |
| --- | --- |
| ![club](https://user-images.githubusercontent.com/63916057/225576710-29bb7317-40aa-468e-8769-14bece2b4d3e.JPG) | ![club cleaned](https://user-images.githubusercontent.com/63916057/225576870-fdd90299-ed90-4346-a239-a66e8ec3082e.JPG) |


### Contract
Here, I simply used the text to columns command on the data tab to split this column into “contract_start” and “contract_end” using  “-” as the delimiter.

| Before | After |
| --- | --- |
| ![contract](https://user-images.githubusercontent.com/63916057/225590476-0c6deb03-d913-478f-98d1-35a5ce68ab03.JPG) | ![contract cleaned](https://user-images.githubusercontent.com/63916057/225590539-185c1695-ec07-446e-bab5-d591e53f1d6e.JPG) |

### Height
From the provided data dictionary for the challenge, we were required to present the unit of this column as feet and inches. In achieving this, the first thing I did was to use the filter feature of excel to filter this column and got to see mixed units of cm and feet-inches. Solving this and unifying the unit to that needed, I first inserted another column to the right to convert all unit in cm to feet using the formula =IFERROR(CONVERT(LEFT(N2,LEN(N2)-2),"cm","ft"),N2). Then created another column to convert the resulting feet into ft’inches by using the formula =IFERROR(INT(P3)+(12*MOD(P3,1)>=11.5)&"'"&IF(12*MOD(P3,1)>=11.5,0,ROUND(12*MOD(P3,1),0))&"""",N3)

| Before | After |
| --- | --- |
| ![Height](https://user-images.githubusercontent.com/63916057/225580314-3bb24ccd-52a0-4795-8e81-c75e2b0baa8f.JPG) | ![height cleaned](https://user-images.githubusercontent.com/63916057/225578318-9c52aec3-bf8e-4d62-809a-6b086ac198a6.JPG) |

### BOV
Same requirement as the OVA and POT. I also applied the same process as shown for OVA above to achieve my results for it.

| Before | After |
| --- | --- |
| ![BOV](https://user-images.githubusercontent.com/63916057/225582739-cf315210-d2e7-4325-b158-3d620076f800.JPG) | !![BOV cleaned](https://user-images.githubusercontent.com/63916057/225582782-396f85c6-2a80-4272-aad1-3bf92c0bffa7.JPG) |

### Loan Date End
Here I filtered all blanks and replaced them with “not specified” values since none were specified for such players.

### Value, Wage and Release Clause
The provided data dictionary for the challenge required us to present each of these column in dollars which was originally valued in euros and also to convert values having “K”and “M” representing thousand and million to their respective digits. Firstly, I used the find and replace feature to get rid of all the Euros symbol. Thereafter, I  applied the formula  =IF(RIGHT(W2)="M",LEFT(W2,LEN(W2)-1)*10^6, IF(RIGHT(W2)="K",LEFT(W2,LEN(W2)-1)*10^3,W2))*1.183  to convert the K’s and M’s into their respective digits. My final conversion for each of the three columns used the average Euro to dollar exchange rates as at 2021 because our dataset was on 2021 data.

| Before | After |
| --- | --- |
| ![value, wage, release clause](https://user-images.githubusercontent.com/63916057/225583004-90f33282-c25b-48aa-9445-ed2f1835bace.JPG) | ![Value cleaned](https://user-images.githubusercontent.com/63916057/225583074-b0513ac9-51e4-4360-85b0-c1d0a31d5b4d.JPG) |

### W/F, SM rating and IR
Similar approach was adopted for all three columns. I used the formular  =VALUE(TRIM(REPLACE(LEFT(BO3),1,0," ")))   to get rid of the star symbols in each of these column,renamed the column attribute to something readable and then formatted to the appropriate data type.

| Before | After |
| --- | --- |
| ![ir](https://user-images.githubusercontent.com/63916057/225587850-aaa8b995-c4fd-43d7-8432-764bc2fc9966.JPG) | ![cleaned WF SM IR](https://user-images.githubusercontent.com/63916057/225587704-f4b018d3-0b1d-434e-a764-bc49b08f155d.JPG) |

### Hits
Here I filtered all blanks and replaced them with zeros. And then applied the =TRIM(IF(RIGHT(CB2)="k",LEFT(CB2,LEN(CB2)-1)*10^3,CB2)) formula. Also the number data type didn’t had any effect when I tried changing it until I applied the value function which converts a text string that represents a number into a number.

| Before | After |
| --- | --- |
| ![Hits](https://user-images.githubusercontent.com/63916057/225588026-58d3bb1d-6718-4e5c-a862-c0b0a68d7a87.JPG) | ![Hits cleaned](https://user-images.githubusercontent.com/63916057/225588227-6b9d95d0-262f-4b20-9aa1-956d1a299bbc.JPG) |



