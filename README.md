# MGH Project
# TABLE OF CONTENTS
 Project Overview
 Detailed Description of the Data Analysis Process
 Findings
 Recommendations
 Conclusion

# PROJECT OVERVIEW
# Project Overview 
This project involves an in-depth analysis of six datasets provided by Massachusetts General Hospital (MGH), a leading healthcare institution in the U.S. Our goal is to extract meaningful insights regarding healthcare trends, patient outcomes, and organizational efficiency. The analysis is structured around five key hypotheses focused on provider utilization, mortality rates across age groups, racial health disparities, revenue generation by encounter type, and payer coverage effectiveness.

# Detailed Description of the Data Analysis Process
Data Preparation
The analysis began with the extraction of six tables from an initial dataset, focusing on the encounter table. This step ensured a robust foundation for our analysis. We conducted a thorough review of data types and addressed discrepancies to maintain data integrity. Using Power Query, we optimized resource usage by employing the "close and load" option with "connection only" settings, preserving efficient access to the dataset.

Data Processing Tools
Power Query: Initial data extraction and quality checks were performed here. Discrepancies were rectified to establish a solid data foundation.
Alteryx: We imported the dataset, utilized various tools for data cleansing (removing null values, duplicates), and transformed the dataset by calculating patient ages and standardizing gender entries. The cleaned data was saved in CSV and YXMD formats for future use.
SQL: The refined datasets were imported into SQL for further analysis. We executed complex queries and joined tables to integrate datasets, which facilitated a deeper understanding of patient and provider interactions.
Methodologies
Each hypothesis was tested using statistical analysis and data visualization techniques:

General Practitioners Dominance: Analyzed provider demographics and utilization patterns to assess the proportion of general practitioners.
Age and Mortality: Examined mortality rates across age cohorts, utilizing descriptive statistics to uncover correlations.
Race and Disease Prevalence: Analyzed the frequency of hospital encounters and diagnoses across racial demographics to identify disparities.
Revenue Generation by Encounter Type: Compared revenue data from various encounter types to identify the most lucrative services.
Payer Coverage Analysis: Assessed coverage provided by major insurance companies to evaluate their effectiveness across healthcare categories.
Findings
General Practitioners were confirmed to be the largest segment of providers, highlighting their crucial role in healthcare delivery.
Older Age Groups exhibited significantly higher mortality rates, confirming the association between age and health risks.
White Individuals showed higher prevalence rates for various illnesses, indicating potential health disparities.
Ambulatory Encounters generated more revenue compared to inpatient and emergency services, emphasizing the financial viability of outpatient care.
Medicaid, BlueCross BlueShield, and Medicare demonstrated comprehensive coverage, reflecting their importance in patient healthcare access.

# Recommendations
Based on our findings, we recommend:
Resource Allocation:
Focus on enhancing support for general practitioners and expanding outpatient services to optimize revenue generation.
Geriatric Care Strategies: Implement targeted interventions for older patients to improve outcomes and resource management.
Addressing Health Disparities: Develop programs to reduce the prevalence of illness in underrepresented racial groups, promoting equitable healthcare access.
Insurance Provider Collaboration: Engage with major payers to ensure that coverage gaps are addressed, particularly in high-need areas.
