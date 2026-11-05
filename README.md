# Companies in India – Data Analysis Using Python

## 📌 Project Overview

Choosing a company to work for is an important decision, especially for job seekers who want to understand the working environment, employee feedback, and career opportunities available in different organizations.

This project explores a dataset containing information about companies in India. Using Python, I aim to understand the available company information, explore employee ratings, and identify patterns in company reviews, salaries, job listings, and other workplace-related details.

The goal is to turn raw company data into meaningful insights that can help job seekers and other interested users better understand the companies represented in the dataset.

## 🎯 Project Objectives

The main objectives of this project are:

* Explore company ratings and understand how they vary across organizations.
* Identify companies with higher numbers of employee reviews.
* Examine the distribution of companies across different industries.
* Explore salary-related information available in the dataset.
* Analyze job listings, interview information, and employee benefits.
* Compare companies based on their available information.
* Identify data quality issues and prepare the dataset for analysis.
* Present findings through clear visualizations and summaries.

## 📂 Dataset Information

**Dataset Name:** Companies in India

**Source:** [Kaggle – Companies in India](https://www.kaggle.com/datasets/dhruvnegi2006/companies-in-india)

**File Format:** CSV

**Number of Records:** 10,000

**Number of Columns:** 11

### Dataset Columns

| Column              | Description                              |
| ------------------- | ---------------------------------------- |
| `name`              | Name of the company                      |
| `rating`            | Overall company rating                   |
| `company_type`      | Type or industry of the company          |
| `hq`                | Company headquarters and other locations |
| `number_of_reviews` | Number of reviews available              |
| `salaries`          | Number of salary-related entries         |
| `interviews`        | Number of interview-related entries      |
| `jobs`              | Number of job listings                   |
| `benefits`          | Number of benefits-related entries       |
| `photos`            | Number of company photos                 |
| `Unnamed: 0`        | Index column included in the dataset     |

*Note: The columns such as `salaries`, `interviews`, `jobs`, and `benefits` represent counts of available entries, not necessarily salary amounts or direct measurements of employee benefits.*

## 🛠️ Tools and Technologies

This project is being developed using Python and its data analysis libraries.

* **Python** – Main programming language
* **Pandas** – Data loading, cleaning, and manipulation
* **NumPy** – Numerical operations
* **Matplotlib** – Data visualization
* **Seaborn** – Statistical visualizations
* **Jupyter Notebook** – Analysis and documentation

## 🔍 Project Workflow

I will follow a structured data analysis process to understand the dataset and extract useful information.

### 1. Data Understanding

* Load the dataset into Python.
* Understand the number of rows and columns.
* Examine column names and data types.
* Explore sample records.
* Understand what each column represents.

### 2. Data Quality Assessment

* Check for missing values.
* Identify duplicate records.
* Examine inconsistent text values.
* Identify incorrect or unusual ratings.
* Check whether numerical information is stored in the correct format.

---
### Key Attributes

| Column                     | Description                              |
|----------------------------|------------------------------------------|
| name                       | Official company name                    |
| rating                     | Average employee satisfaction rating     |
| company_type               | Industry or company classification       |
| hq                         | Company headquarters and other locations |
| number_of_reviews          | Total employee reviews                   |
| salaries                   | Total salary reports                     |
| interviews                 | Total interview experiences              |
| jobs                       | Total active job postings                |
| benefits                   | Total employee benefit mentions          |
| photos                     | Number of uploaded workplace photos      |

---

## 3. Data Cleaning and Preprocessing Steps

### 3.1 Importing Libraries and Loading Dataset

Imported the required Python libraries and loaded the CSV file using Pandas.

**Libraries used:**
- Pandas – Data manipulation and preprocessing.
- NumPy – Numerical operations.
- Matplotlib – Data visualization.
- Seaborn – Statistical visualization.

### 3.2 Initial Data Inspection

Performed an initial examination of the dataset to understand its structure and identify data quality issues.

The following functions were used:

- `df.head()` – Displayed the first five records.
- `df.info()` – Examined column names, data types, and non-null values.
- `df.shape` – Identified the number of rows and columns.
- `df.dtypes` – Checked individual column data types.
- `df.size` – Calculated the total number of elements.
- `df.nunique()` – Identified unique values in each column.
- `df.isnull().sum()` – Identified missing values.

**Initial observations:**
- 10,000 records and 11 columns.
- 598 duplicate company profile records.
- Numerical attributes contained abbreviated values such as K and L.
- The headquarters column contained combined location information.
- Significant missing values were present in the jobs and photos columns.

### 3.3 Removing Unnecessary Columns

Removed the following columns:

- `Unnamed: 0` – An unnecessary index column generated during CSV storage.
- `photos` – Removed due to a high number of missing values (5,596 records).

Used `drop()` with `errors='ignore'` to avoid errors if the specified columns were unavailable.

### 3.4 Removing Duplicate Records

Identified and removed duplicate company profiles using:

- `duplicated()` – Identified duplicate records.
- `drop_duplicates()` – Removed duplicate rows.
- `reset_index()` – Reset the DataFrame index after removing duplicates.

**Result:** Removed 598 duplicate records from the initial dataset.

### 3.5 Converting Abbreviated Values into Numeric Format

The columns `number_of_reviews`, `salaries`, `interviews`, `jobs`, and `benefits` contained abbreviated numerical values.

Examples:
- `54k` = 54,000
- `1.2L` = 120,000
- `5K` = 5,000

**Preprocessing performed:**
- Removed leading and trailing spaces.
- Replaced K/k with the numerical multiplier for thousands.
- Replaced L with the numerical multiplier for lakhs.
- Converted the values into numeric format using `pd.to_numeric()`.
- Used `errors='coerce'` to convert invalid values into NaN.

### 3.6 Extracting Headquarters Information

The original `hq` column contained headquarters city names along with information about additional company locations.

Created two new columns:

**1. hq_city**
- Extracted the primary headquarters city.
- Removed unnecessary spaces.
- Replaced missing city values with `Unknown`.

**2. other_locations**
- Extracted the number of additional company locations.
- Replaced missing values with 0.
- Converted the column into integer format.

The original `hq` column was subsequently removed because the extracted columns contained the required information.

### 3.7 Cleaning Text Columns

Standardized the following text columns:

- `name`
- `company_type`

Used the Pandas `str.strip()` method to remove unnecessary leading and trailing whitespace.

This helps maintain consistency when grouping and analyzing company names and classifications.

### 3.8 Handling Missing Values

Applied different missing-value treatment methods depending on the columns.

| Column     | Missing Value Treatment                       | Method              |
|------------|-----------------------------------------------|---------------------|
| rating     | Removed records                               | dropna()            |
| salaries   | Removed records                               | dropna()            |
| interviews | Replaced with 0                               | fillna(0)           |
| benefits   | Replaced with 0                               | fillna(0)           |
| jobs       | Group-wise median, followed by overall median | transform('median') |

**Explanation:**

- **Rating and Salaries:** Removed records where these values were missing because they are important attributes for the planned analysis.
- **Interviews and Benefits:** Replaced missing values with 0, assuming missing records indicate no reported activity.
- **Jobs:** Applied median imputation based on company type. Any remaining missing values were replaced using the overall median.

### 3.9 Renaming Columns

Renamed selected columns to make their meanings clearer and improve readability.

| Original Column | Updated Column   |
|-----------------|------------------|
| salaries        | salary_records   |
| interviews      | total_interviews |
| jobs            | job_postings     |
| benefits        | benefits_count   |

### 3.10 Standardizing Data Types

Performed final data type standardization.

- Converted `job_postings` into integer format.
- Converted `salary_records` into integer format.
- Converted `number_of_reviews` into integer format.
- Converted `hq_city` into string format.

Finally, used `df.info()` and `df.isnull().sum()` to inspect the processed dataset and verify its structure and remaining missing values.

---

## 4. Final Dataset Structure

After preprocessing, the dataset contains the following analytical attributes:

| Column                  | Description                        |
|-------------------------|------------------------------------|
| name                    | Company name                       |
| rating                  | Employee satisfaction rating       |
| company_type            | Company or industry classification |
| number_of_reviews       | Total employee reviews             |
| salary_records          | Total salary submissions           |
| total_interviews        | Total interview experiences        |
| job_postings            | Total job postings                 |
| benefits_count          | Total employee benefit mentions    |
| hq_city                 | Primary headquarters city          |
| other_locations         | Number of additional locations     |

**Note:** The final row count and remaining missing-value count should be obtained from the final notebook output rather than assumed.

---

### 4. Exploratory Data Analysis (EDA)

Explore the dataset to answer questions such as:

* Which companies have the highest ratings?
* Which companies have the most employee reviews?
* Which company types are most common?
* How are company ratings distributed?
* Which companies have more job listings?
* How do reviews, salary entries, and interview entries vary across companies?
* Are there any noticeable patterns between company ratings and the number of reviews?

### 5. Data Visualization

Create visualizations to communicate the analysis clearly.

Planned visualizations include:

* Top-rated companies.
* Company distribution by type.
* Rating distribution.
* Companies with the highest number of reviews.
* Job listings across companies.
* Comparison of reviews, salaries, and interview entries.
* Relationship between company ratings and review counts.

### 6. Insights and Recommendations

* Summarize the important patterns identified during analysis.
* Highlight interesting observations about the companies.
* Explain what the findings may mean for job seekers.
* Mention data limitations that could affect interpretation.

## 📊 Expected Outcome

By the end of this project, I aim to develop a better understanding of the company information available in the dataset.

The analysis will help explore company ratings, industry distribution, review activity, job listings, and other available indicators. Visualizations and findings will be documented to make the information easier to understand.

## ⚠️ Dataset Limitations

A few limitations should be considered while interpreting the data:

* The dataset contains company-level information and may not represent every company in India.
* Ratings and review counts do not necessarily represent the experience of every employee.
* Salary-related values appear to represent the number of salary entries rather than actual salary amounts.
* Job listings and other counts may change over time.
* The dataset may contain missing, inconsistent, or outdated information.
* Relationships identified during analysis should not automatically be interpreted as cause-and-effect relationships.

## 📁 Project Structure

```text
Companies-in-India-Analysis/
│
├── Dataset/
│   └── companies_in_india.csv
│
├── Notebooks/
│   ├── 01_Data_Understanding.ipynb
│   ├── 02_Data_Quality_Assessment.ipynb
│   ├── 03_Data_Cleaning.ipynb
│   ├── 04_Exploratory_Data_Analysis.ipynb
│   ├── 05_Data_Visualization.ipynb
│   └── 06_Insights_and_Recommendations.ipynb
│
├── Visualizations/
│
├── README.md
└── requirements.txt
```

## 🚀 Project Status

**Status:** In Progress

This project is being developed step by step, starting with understanding the dataset and assessing its quality, followed by data cleaning, exploratory analysis, visualization, and insight generation.

---

*This project is part of my continuous learning journey in Python and Data Analytics. My focus is on developing practical analytical skills and learning how to turn raw data into meaningful business insights.*

