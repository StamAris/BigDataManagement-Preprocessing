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
## Project Outline

### **Load Dataset from BigQuery**

* **Data Hosting on Google Storage (bdmp_bucket):**

> The project began with hosting the weather anomaly dataset on Google Storage, utilizing the **"bdmp_bucket"** as the storage location. Google Storage provides scalable and secure object storage, making it an ideal choice for managing large datasets.

* **Data Loading into BigQuery:**

> Leveraging Google Cloud's BigQuery, the dataset hosted in the Google Storage bucket was loaded into BigQuery tables, with **project_id = "bamboo-chemist-402814"**. BigQuery is a fully managed, serverless data warehouse that allows for fast SQL queries on large datasets.

* **Loading Data from BigQuery to Colab Notebook:**

> The notebook utilized the google-cloud-sdk and BigQuery's Python client library to run a SQL query against the dataset stored in BigQuery. The query results were fetched into the Colab notebook under the variable name "results".

* **Spark DataFrame Creation:**

> The data fetched into the Colab notebook was transformed into a Spark DataFrame ("weather_df") for scalable and distributed data processing. The Spark DataFrame facilitated efficient exploratory data analysis and machine learning tasks.

---
### **Temperature Anomaly Analysis**
**Identify extreme temperatures with a z-score threshold**

In this phase, we conduct an analysis of temperature anomalies by calculating z-scores based on the mean and standard deviation of the 'degrees_from_mean' attribute. Z-scores help identify data points that deviate significantly from the mean, allowing us to pinpoint extreme temperature events.

**Statistical Summary**
* **Mean and Standard Deviation**: The Spark DataFrame `stats_df` is created to store the mean and standard deviation of 'degrees_from_mean'. These statistical measures serve as a basis for determining the degree of deviation of individual data points.

* **Z-score Calculation**: The 'z_score' column is added to the DataFrame `anomaly_df` using the formula:
   Z =(X - mean)/stddev
   where \(X\) represents the 'degrees_from_mean'. Z-scores quantify how many standard deviations a data point is from the mean.

**Z-score Analysis**
* **Display Z-scores**: The DataFrame `anomaly_df` is displayed, showcasing the calculated z-scores for each data point, providing insights into the relative magnitude of temperature anomalies.

* **Identification of Extreme Temperatures**: Extreme temperatures are identified by applying a threshold to the z-scores. In this case, temperatures with z-scores greater than 4 or less than -4 are considered extreme. The DataFrame `extreme_temps` contains these extreme temperature events.

**Degrees from Mean Analysis**
The DataFrame `degrees_from_mean_analysis` is created to focus on the 'degrees_from_mean' attribute, providing a concise view of the temperature anomalies over time.

By leveraging z-scores, this analysis allows us to categorize and investigate extreme temperature events, providing a statistical perspective on the anomalies present in the dataset. Subsequent sections will explore temporal trends, spatial patterns, and potential correlations to enhance our understanding of the weather dataset.

---
### **Exploratory Data Analysis**

**Code Overview**

We conducted a clustering analysis on geographical data considering three temperature attributes: `degrees_from_mean`, `max_temp`, and `min_temp`. Here's a summary of the key steps:

* **Data Selection**: Relevant columns, including `latitude`, `longitude`, `degrees_from_mean`, `max_temp`, `min_temp`, and `date_str`, were selected for clustering.
* **Vector Assembly**: Features were assembled into a vector using VectorAssembler.
* **KMeans Modeling**: The KMeans model was trained on the assembled features, with the number of clusters set to 15 based on previous analysis.
* **Clustered Data**: The model was applied to the data, and the resulting clusters were assigned to each data point.
* **Average Temperature Calculation**: For each cluster, date_str, and temperature attribute, the average temperature was calculated.

**Visualizations**
We visualized the average temperature for each cluster over time, considering all three temperature attributes. Subplots for each cluster facilitated the observation of temporal trends.

**Trend Analysis**

**Code Overview**

We extended our analysis to explore trends within each cluster over time for all three temperature attributes. Here are the steps:

* **Linear Regression Analysis**: A linear regression model was fitted to the average temperature over time for each cluster and temperature attribute.
* **Trend Line Plotting**: Actual data and the fitted trend line were plotted to visualize trends.
* **Hypothesis Testing**: Hypothesis testing was performed to assess the significance of trends.
* **Thresholds**: Trends were categorized as significant or not based on predetermined thresholds for t-statistic and p-value.

**Visualizations**
Visualizations were created for yearly averages, every 5 years averages, and every decade averages, considering all three temperature attributes. Plots include actual data, trend lines, and information on the significance of trends.


This comprehensive analysis enhances our understanding of spatial-temporal patterns in `degrees_from_mean`, `max_temp`, and `min_temp`. The combination of clustering and trend analysis provides a holistic view of temperature variations and trends across different clusters, aiding in more informed decision-making and insights into the complex dynamics of temperature fluctuations.

---

### **Conclusions - Interpretation of Statistical Analysis Results**

**Overview**
The statistical analysis and hypothesis significance tests were conducted to assess the trends in temperature attributes—`degrees_from_mean`, `max_temp`, and `min_temp`. The results consistently show upward and significant trends across all three attributes. The key findings are as follows:

**1. Degrees from Mean**

- **Upward Trend**: The analysis reveals a consistent upward trend in the `degrees_from_mean` attribute across different clusters.
- **Significance**: The trends are statistically significant, as indicated by t-statistic values consistently greater than 2 and p-values consistently below 0.05.

**2. Maximum Temperature (`max_temp`)**

- **Upward Trend**: Similar to `degrees_from_mean`, the `max_temp` attribute exhibits a significant upward trend across clusters.
- **Statistical Significance**: The t-statistic values, consistently exceeding 2, and the p-values consistently below 0.05 emphasize the statistical significance of these trends.

**3. Minimum Temperature (`min_temp`)**

- **Strong Upward Trend**: The `min_temp` attribute displays a robust and significant upward trend in all clusters.
- **Statistical Significance**: The t-statistic values consistently surpassing 2 and p-values consistently below 0.05 underscore the statistical significance of the observed trends.

**Implications and Considerations**
* **Consistency Across Attributes**: The uniformity of upward trends in all three temperature attributes suggests a broader climatic pattern or environmental influence affecting the study area.
  
* **Climate Change Indicators**: The significant and consistent nature of these trends aligns with expectations in the context of global climate change, indicating a warming trend in the region.

* **Min_temp Sensitivity**: The heightened significance and magnitude of trends in `min_temp` underscore its sensitivity to climate variations. This insight can be crucial for assessing potential impacts on ecosystems and human activities sensitive to minimum temperature fluctuations.

* **Policy and Planning**: These findings have implications for policymakers, urban planners, and environmental scientists, emphasizing the importance of considering temperature trends in long-term planning and decision-making.

In summary, the statistical analysis confirms the presence of significant upward trends in temperature attributes, providing valuable insights into climate dynamics and aiding in the formulation of informed strategies for adaptation and mitigation.
