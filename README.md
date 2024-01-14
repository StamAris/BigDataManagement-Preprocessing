# Exploring Climate Change through Historical Weather Data

#### **Basic Information:**

*	**Project Title:** Exploring Climate Change through Historical Weather Data
*	**Name:** Aristeidis Stamou
*	**Email Address:** astamou92@gmail.com

**Background and Motivation:** Climate change is a critical global issue with far-reaching consequences. Motivated by a keen interest in environmental science and the urgency of understanding climate patterns, this project aims to analyze historical weather data to explore trends and anomalies that may indicate the presence of climate change. The project's significance lies in contributing insights that can inform discussions and actions related to environmental sustainability.

**Project Objectives (Hypothesis):** The primary questions to be addressed in this project include:
1.	Are there observable trends in average temperatures over the years?
2.	Can we identify seasonal patterns and shifts in temperature extremes?
3.	Do certain regions show more pronounced changes in temperature?

**Data Sources:** The project will utilize a historical weather dataset obtained from DataWorld, spanning from 1964 to 2013 in the USA. Each entry represents a report from a weather station, detailing high and low temperatures that were historical outliers within each month. The dataset is expected to provide insights into long-term temperature trends.
*	Link to dataset: https://data.world/carlvlewis/u-s-weather-outliers-1964

**Big Data Dimensions:** This project qualifies as a Big Data problem due to:
*	**Volume:** The dataset spans several decades, accumulating a significant volume of historical weather records (approximately 3 million rows).
*	**Variety:** The dataset exhibits variety with diverse types of information, including temporal data (date_str), geospatial data (longitude, latitude, location), and various meteorological measurements (max_temp, min_temp, type). The presence of different data types contributes to the variety dimension.
*	**Velocity:** While the data is not real-time, the temporal aspect introduces velocity. The changes in temperature over the years represent a dynamic process that can be analyzed with respect to time.

**Solution Overview:** The project will leverage Big Data processing frameworks, particularly Apache Spark, for efficient analysis of the extensive weather dataset. Exploratory data analysis, statistical methods, and machine learning concepts will be employed to uncover patterns and trends. The project will focus on visualizations to effectively communicate findings.

**Tools/Libraries:**
* Google Cloud Platform (BigQuery, Dataproc)
*	Programming Language: Python
*	Big Data Framework: Apache Spark (PySpark)
*	Data Analysis Libraries: Pandas, Matplotlib, Seaborn
*	Statistical Analysis: SciPy, Statsmodels

---
### **Load Dataset from BigQuery**

* **Data Hosting on Google Storage (bdmp_bucket):**

> The project began with hosting the weather anomaly dataset on Google Storage, utilizing the **"bdmp_bucket"** as the storage location. Google Storage provides scalable and secure object storage, making it an ideal choice for managing large datasets.

* **Data Loading into BigQuery:**

> Leveraging Google Cloud's BigQuery, the dataset hosted in the Google Storage bucket was loaded into BigQuery tables, with **project_id = "bamboo-chemist-402814"**. BigQuery is a fully managed, serverless data warehouse that allows for fast SQL queries on large datasets.

* **Loading Data from BigQuery to Colab Notebook:**

> The notebook utilized the google-cloud-sdk and BigQuery's Python client library to run a SQL query against the dataset stored in BigQuery. The query results were fetched into the Colab notebook under the variable name "results".

* **Spark DataFrame Creation:**

> The data fetched into the Colab notebook was transformed into a Spark DataFrame ("weather_df") for scalable and distributed data processing. The Spark DataFrame facilitated efficient exploratory data analysis and machine learning tasks.
