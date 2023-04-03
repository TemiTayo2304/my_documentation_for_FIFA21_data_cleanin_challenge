# my_documentation_for_FIFA21_data_cleanin_challenge
FIFA 21 DATA CLEANING CHALLENGE - TEMITAYO ANIFOWOSE
THE CHALLENGE
The FIFA 21 data cleaning challenge was organized for the purpose of challenging aspiring data analyst to implement what they have leant so far in data cleaning. It was an eye opening task that pushed me out of my comfort zone, beyond my limit and I must say that I found it fascinating and at the same time challenging. It has helped me broaden my knowledge in data cleaning, network with other like-minded data analyst, as well as facilitate my creative thinking ability, developing  new ways to approach a problem.
I participated in this challenge so I could experience working with real life project using the knowledge of cleaning data Excel that I have gathered in the past weeks, which was why Microsoft Excel was my go-to tool for this challenge. The thought of cleaning such huge data was at first terrifying at a glance, but with an enthusiastic approach, and result driven mindset, I was able pull through.
About the Data
The dirty FIFA 21 raw data consisting of 77 Rows and 18980 columns was originally from Kaggle.com, and it contained information about the players. Here are the things I watched out for during the data cleaning process;
•	Duplicate data
•	Null entries/Blank cells
•	Inconsistent Data
•	Missing Values
•	Unusual Characters
•	Incorrect Format
•	Spelling Errors
THE CLEANING PROCESS
After careful observation of each column, the columns with Names, Height & Weight, OVA, POT, BOV, Positions, Club, Contract, Values, Wages and Release clause, and Hits, were found to have dirty data. First, I created a separate worksheet for the cleaned data before beginning the cleaning process for each column was cleaned is explained below.
NAME
The column with the name contained loads of unusual characters with need proper attention to be cleaned as I found out that some of the players name originally has special characters in them. I went ahead to extract the names of the players from their profile URL using the “split text to column”, using “/” as the delimiter. Then I used “Find and replace (CLT+H) to replace the hyphens in between them with a space. In a separate column, I went ahead to use the proper function =PROPER (B2) to Capitalize the first letter of the names. 
AGE
A separate column was created for their current age using the sum function =SUM (A1+2) upon realizing that that the age in the data is that of 2021. However the column with their ages as of 2021 was not discarded.
HEIGHT
The height column was the most challenging for me because 18939 of its cells were in “cm” and 41 others in feet and inches such as 5’7”. However from the data dictionary, they were required to be in feet (ft). After copying the pasting the column into a separate worksheet, I used the “find and replace” to highlight cells like 5’7” with a color, then sorted out the column with the colored cells on the top. To convert values in colored cells to “ft”, (“) was first eradicated using “find and replace”, then the values were grouped into separate columns separating the feet from the inches. 
1ft = 12inches, so to convert the convert the values to feet, I used the formula;
=CONCATENATE (ROUND (A1+ (B1/12), 1),"ft"). The round function was to round up the result of the expression to 1 decimal place while the concatenate function merged the result with the unit “ft”.
For the rest of the cells with unit “cm”, their conversion was made using the convert function =CONCACENATE (CONVERT (A1,”cm”,”ft”)”ft”), with the concatenate function used to apply the unit to the values. This step was however done after discarding the “cm” with the use of “find and replace”.
WEIGHT
This column had 18939 of its cells in “kg” and 41 in “lbs”, and from the data dictionary; the unit has to be “lbs”. 
1kg = 2.20462, and to make sure all the cells have uniform units, this formula was applied; =IF(RIGHT(A1,2)="kg",CONCATENATE(ROUND(LEFT(A1,LEN(A1)-2)*2.20462,0),"lbs"),A1), "). The round function was to round up the result of the expression to 0 decimal place and concatenate function was to merge the result with the unit “lbs”.
CONTRACT
Using the “text to column” tool, and the “ ~ “ including the space as the delimiter, I divided the contract into two separate columns, to separate the beginning the end of the contract. However, some players were on loan having only the full date of the contract start with no end date. From my research, I found out that a loan contract for any player usually last for a year, and so, I took the following steps;
The On Loan attached to the cells was removed using find and replace, leaving only the date. The day and month was also discarded, leaving the year only. Afterwards, I applied the formula;
 IF (B2=” ”, A2+1, B2). This formula added a year to the cells with empty contract end cells, and returned results which tallied with the values in a Loan end date column which was eventually discarded.
OVA, POT & BOV
These abbreviated headers were written in full as Overall Rating, Potential, & Best Overall with the help of the data dictionary and were also written as percentage using the concatenate formula. I achieved this by creating a separate column and used =CONCATENATE (A1,” %”), which I copy and pasted afterwards as values.
VALUES, WAGES AND RELEASE CLAUSE
In a separate worksheet, the formula; =IF(RIGHT(A1)=”M”,LEFT(A1,LEN(A1)-1)*1000000, LEFT(A1,LEN(A1)-1)*1000) which returned values written as 5M to 5,000,000 and 6.7K written as 6,700 was applied Values column which had 20 cells with “M”  and 30 with “K”, and Release Clause column which had 20 cells with “M” and 30 with “K”. 
As for the Wages, the formula; =IF (RIGHT (A1) =”K”, LEFT (A1, LEN (A1)-1)*1000, A1) was applied, returning values with K as thousand and values without K as hundreds.
 These columns were then copied and pasted as values (without the underlying formula) into their original column and were formatted as currency in $, as instructed in the data dictionary. 
HITS
This column had a number of28 cells written with their unit in thousand such as 1.5K and to resolve this, I implored the IF formula written as = IF (RIGHT (A1) =”K”, LEFT (A1, LEN (A1)-1)*1000, A1). This resulted in the value written as”0000” such as 1500.
#Note: The number of cells containing certain values with unit were counted using the “countif formula” such as =COUNTIF (O: O,”*cm”) except for values written as 5’4” which was counted by subtracting the total number of cells of the other values in other unit in the same column from the total number of cells in the column(COUNTA(O:O)).
At the end of the data cleaning process, I sorted the data set in alphabetical order with respect to the names because I like to see it in order.
