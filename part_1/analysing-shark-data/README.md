# Analysing Shark Attack Data

## Description of the Project

We've been hired as a data professional working for a governmental research organization that studies marine biology. Our team is working on a project to study shark attacks.

The dataset we will be using it available on [Kaggle](https://www.kaggle.com/datasets/mysarahmadbhat/shark-attacks) and available under the [CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/) license.

## Project Goal

Our aim is to analyse the data to answer the following questions:

1. Are there certain locations that see more shark attacks than others?
2. Have shark attacks been icnreasing or decreasing over time?

The other team members will be conducting the analysis. It is our job to prepare the dataset.

## Process

The research team has asked us to prepare the data as follows. These are the fields they are interested in keeping:

- Case Number
- Year
- Type
- Country
- Area
- Location
- Activity
- Sex
- Age
- Injury
- Fatal

### An Overview of the Data

- The dataset has a header row and 6094 rows with data entires. 
- There are a selection of cells beyond the data range that contain characters. E.g. row 25616 contains "xx" in column A; row 6103 contains "N" in column O.
- The dataset has 22 columns.
    - Case Number
    - Date
    - Year
    - Type
    - Country
    - Area
    - Location
    - Activity
    - Name
    - Sex 
    - Age
    - Injury
    - Fatal (Y/N)
    - Time
    - Species
    - Investigator or Source
    - pdf
    - href formula
    - href
    - Case Number
    - Case Number
    - original order
- There is missing data in multiple columns.
- The data within columns is not consistent, for example:
    - Some entires in the ```Date``` column contain "Reported on..." rather than the date in appropriate format.
    - Some entries in the ```Year``` column are blank or contain "0".
    - Some entires in the ```Time``` column contain descriptions of the day (e.g. "morning") rather than a timestamp.

### Cleaning the Data

- Unnecessary columns were kept and will be removed at the last step (may be useful to determine the correct course of action for cleaning other columns).

- The rows below the dataset with miscellaneous characters were removed.

- Duplicate rows were removed (19517 duplicate values; 6097 remain).

- ```X1``` was given the header name ```duplicate_case_number```. ```X2``` was given the formula ```=COUNTIF($A$2:$A$6096,A2)>1``` and filled down. 

- ```Y1``` was given the header name ```duplicate_href```. ```Y2``` was given the formula ```=COUNTIF($S$2:$S$6096,S2)>1``` and filled down.

- ```duplicate_case_number``` was filtered to only show "TRUE" values. ```duplicate_href``` was filtered to only show "TRUE" values.
    - Row 5071 was removed (dates didn't match). Rows 5295 and 5296 report the same incident, but are separate as they each describe part of the crew.
    
- ```duplicate_case_number``` was filtered to only show "TRUE" values.    
    - Duplicate case numbers were appended with ".1", ".2", etc. to individualise case numbers.
    
- ```Year``` was filtered to only show blank values.
    - Updated with years from case numbers using (e.g.) ```=LEFT(A54,4)```
    
- ```Type``` was filtered to only show blank values.
    - Updated with "unknown".
    
- ```Country``` was filtered to only show blank values.
    - Rows without a country were removed.
    
- All blank cells (F5 --> Special --> Blanks) between ```Area``` and ```Injury``` were replaced with "unknown"

- ```Age``` was filtered in ascending order.
    - All cells without a definite age (i.e. those values beyond 87 including ranges, text, or blank) were replaced with "unknown". 
    
- ```Fatal (Y/N)``` was filtered to show values that aren't "Y" or "N".
    - All values were replaced with "unknown".
    
- ```Sex``` was filtered to show values that aren't "M" or "F".
    - All values were replaced with "unknown".
    - All values in the column were then trimmed.
    
- The values in ```Fatal (Y or N)``` were trimmed.

- The columns that the research team are not interested in were deleted (Date, Name, Time, Species, Investigator or Source, pdf, href formula, href, Case Number, Case Number, original order).
    - The remaining dataset (6045 rows including headers) was searched for blanks and none found.