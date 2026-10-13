# HR Data Analytics Project

## Overview
This project cleans, explores and analyses HRDataset_v14, a 311-employee HR dataset from Kaggle, using Python in Google Colab. It was completed as my AltSchool Africa third semester data analytics project. The notebook walks through the full process: loading, cleaning, exploratory analysis, transformation, visualisation and interpretation, with markdown notes explaining the reasoning at each step.

## Dataset
HRDataset_v14 was created by Dr. Rich Huebner and Carla Patalano. It covers employee salary, department, performance, engagement, recruitment source and employment status. The copy I used had real data quality problems, which made it a good dataset for practising cleaning.

## Data cleaning
- Dropped 10 columns that were completely empty in all 311 rows. The file header had more fields than the data filled.
- Found that "DateofHire" appeared twice in the header. Pandas had renamed the second one "DateofHire.1". Every Active employee had a value in it, so it could not be a termination date, and I dropped it instead of guessing what it meant.
- Stripped hidden trailing spaces from text columns (for example "M " vs "F", and padded values in Department).
- Converted the date columns to datetime and ManagerID to a nullable integer type.
- Left 8 missing ManagerID values as missing. All 8 belong to employees managed by the same person, so the gap looks structural, and inventing IDs would misrepresent the data.
- Checked the $250,000 salary outlier against job titles. It belongs to the President & CEO, so I kept it.

Final cleaned shape: 311 rows, 23 columns, no duplicate rows.

## Transformation
- YearsSinceHire: tenure measured from each hire date to the latest performance review date in the data (28 Feb 2019), because the dataset has no "today" field.
- SalaryBand: salary grouped into four ranges with pd.cut().
- HireYear: extracted from DateofHire.
- A pivot table of average engagement by department and performance score, plus a crosstab of headcounts.

## Key findings
- Overall attrition is 33.4%.
- Production has both the lowest average salary ($59,954) and the highest attrition (39.7%). Software Engineering is second on both measures (36.4%).
- Hires from the company website (7.7%) and employee referrals (16.1%) left less often than hires from Indeed (24.1%) or LinkedIn (23.7%). Sources with only 1-2 hires, such as "On-line Web application" (1 person, 100% attrition), are too small to draw conclusions from.
- Engagement correlates with lateness (-0.585) but not with absences (-0.008). Lateness may be a better early warning sign of disengagement.
- Employees rated "Exceeds" or "Fully Meets" had higher engagement scores than those rated "Needs Improvement" or "PIP".
- Hiring peaked sharply in 2011 (83 hires) and declined steadily afterwards.

## Visualisations
- Bar chart: average salary by department
- Line chart: hires per year
- Scatter plot: engagement score vs days late

## Recommendation
Start a retention and pay review in Production, which combines the lowest pay with the highest attrition. Track lateness as well as absences when watching for disengagement.

## Tools
Python, pandas, NumPy, Matplotlib, Google Colab

## Files
- HR_Data_Analytics_Project.ipynb: the full notebook
- HR_Data_Analytics_Project.pdf: PDF export of the notebook
- HRDataset_v14.csv: the dataset
