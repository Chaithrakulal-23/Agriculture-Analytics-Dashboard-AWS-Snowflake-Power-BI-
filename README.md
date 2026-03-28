# Agriculture-Dashboard

### Dashboard Link :[ https://app.powerbi.com/groups/me/reports/your-report-id/ReportSection](https://app.powerbi.com/links/zWrSjzH8Qm?ctid=51697115-1ecd-42b5-b509-2d62c3919f76&pbi_source=linkShare)

## Problem Statement

This dashboard helps agricultural analysts and stakeholders understand crop yield patterns and climate conditions across seasons and regions. It enables data-driven decisions by analyzing the impact of rainfall, temperature, and humidity on agricultural output. Through various visual breakdowns by crop type, location, year, and season, it identifies trends and anomalies that can guide farming strategies and policy decisions.

Since climate factors like rainfall and temperature vary significantly across years and regions, this dashboard helps pinpoint underperforming areas and seasons, allowing authorities to focus efforts on improving agricultural yield through better resource planning.

Also, since rainfall and yield patterns differ across crop types and locations, stakeholders can use this dashboard to prioritize irrigation, crop selection, and climate-adaptive strategies.

---

### Steps Followed

- **Step 1 :** Loaded the data_season dataset (Excel file) into AWS S3 by creating a dedicated S3 bucket via the AWS Management Console and uploading the seasonal dataset.

  ![S3 Bucket with Dataset](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/6fb9d3c9f1311644f789fc330786bdb452e70a74/s3bucket.png)

- **Step 2 :** Established a secure connection between AWS S3 and Snowflake by creating an IAM Role in AWS:
  - Navigated to IAM → Create Role → Selected AWS Account type.
  - Provided a placeholder External ID and attached the **AmazonS3FullAccess** permission policy.
  - Named the role and noted the generated **ARN** and **Trust Policy**.
 ![Role](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/9402765349ba026cb3d7b4795b0fa09351006cd3/role.png)

- **Step 3 :** In Snowflake, created a **Storage Integration Object** using the IAM Role ARN to authorize Snowflake to read from the S3 bucket.

  ![Snowflake Storage Integration Code](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/67c0062ec089869e7d36b8d9f82e275cda202fee/integrations3%26snowflake.png)

- **Step 4 :** Retrieved the Snowflake-generated **ARN** and **External ID** using:
  ```sql
  DESC INTEGRATION Tableau_IntegrationC;
  ```
  Pasted these values into the IAM Role's Trust Policy in AWS and updated it to complete the secure handshake.

  ![DESC Integration Output + Updated Trust Policy](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/7c8a5d406e2ff90e541326e2fbd3df52af551f2a/editarn%26extid.png)

- **Step 5 :** In Snowflake, set up the data pipeline:
  - Created a **Database**, **Schema**, and **Table** to store the agriculture data.
  - Created a **Stage** pointing to the S3 bucket location.
  - Loaded data from the Stage into the Snowflake table.

  ![Table](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/634b6b9ae06d87b1508d0ef55fdc4ee14db4af7f/createtable.png)

    ![Snowflake Database Schema Stage Table](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/e9c4c238105a39ce0f2cc4d91a7d21cc3b65652c/stage.png)

- **Step 6 :** Performed **Data Profiling** to understand the dataset structure, column types, and value distributions.

- **Step 7 :** Copied data from the original table into a working table to perform transformations without affecting raw data. Transformations applied:

  - Updated **Rainfall** column by multiplying values by `1.1` (10% adjustment).
  - Updated **Area** column by multiplying values by `0.9` (10% reduction).
  - Added a new **Year Group** column using conditional logic:
    - `2004–2009` → `Y1`
    - `2010–2015` → `Y2`
    - `2016–2019` → `Y3`

   ![Year Group Columns](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/a465317db660328c5fbdb8646d446385533b1a64/YRGRPCLM.png)

  - Added a new **Rainfall Group** column:
    - `255–1000` → `Low`
    - `1200–2800` → `Medium`
    - `2800–4103` → `High`

  ![Transformed Table Rainfall Group Columns](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/98eb4b5f2e0bbcd288f766f98228c2079060ae2e/raifallgrpresult.png)

- **Step 8 :** Connected **Power BI Desktop** to Snowflake:
  - Used **Get Data → Snowflake** in Power BI.
  - Pasted the Snowflake account URL and authenticated.
  - Selected the transformed database and loaded it into Power BI Desktop.

  ![Power BI Get Data Snowflake Connection](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/68141e4f540679b686bd67c70d3ff3c51574af88/connectsnwpwb.png)

- **Step 9 :** Built the following analysis pages using **Bar Charts** for all visuals:

  **Rainfall Analysis**
  - Average Rainfall by Year
  - Average Rainfall by Season
  - Average Rainfall by Crop
  - Average Rainfall by Location

 

  **Temperature Analysis**
  - Average Temperature by Year
  - Average Temperature by Season
  - Average Temperature by Crop
  - Average Temperature by Location



  **Humidity Analysis**
  - Average Humidity by Year
  - Average Humidity by Season
  - Average Humidity by Crop
  - Average Humidity by Location


  **Yield Analysis**
  - Average Yield by Year
  - Average Yield by Season
  - Average Yield by Crop
  - Average Yield by Location

 
- **Step 10 :** Published the completed report to **Power BI Cloud Service** for stakeholder access.

  ![Power BI Publish Success Message](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/b0f367b66fdbe028d02ed014907a4c3dc85df556/publipower.png)

---

# Snapshot of Dashboard (Power BI Service)

![Dashboard Snapshot Power BI Service](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/db8075a436d1384d7650b6117d3a21f53f99ccce/rainpowerapp.png)

![Dashboard Snapshot Power BI Service](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/870dd55591775d6186b2a8eec691ac0644b217d9/temperaturepowerapp.png)

![Dashboard Snapshot Power BI Service](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/abe421d0c760056a4beb9045e4e37f7fa67e0404/humiditypowerapp.png)

![Dashboard Snapshot Power BI Service](https://github.com/Chaithrakulal-23/Agriculture-Analytics-Dashboard-AWS-Snowflake-Power-BI-/blob/f6dced48d03aabbc7b7e023c504da696fc3e8e95/yieldpowewrapp.png)

# Report Snapshot (Power BI Desktop)

![Report Snapshot Power BI Desktop](https://user-images.githubusercontent.com/your-id/dashboard-powerbi-desktop.jpg)

![Rainfall Analysis Dashboard](https://user-images.githubusercontent.com/your-id/rainfall-analysis.jpg)

![Temperature Analysis Dashboard](https://user-images.githubusercontent.com/your-id/temperature-analysis.jpg)

![Humidity Analysis Dashboard](https://user-images.githubusercontent.com/your-id/humidity-analysis.jpg)

![Yield Analysis Dashboard](https://user-images.githubusercontent.com/your-id/yield-analysis.jpg)

---

# Insights

A multi-page report was created on Power BI Desktop & published to Power BI Service.

The following inferences can be drawn from the dashboard:

### [1] Rainfall Analysis

- Rainfall levels vary considerably across years, with certain years showing significantly higher averages — categorized as **High (2800–4103 mm)**.
- Seasonal patterns show that specific seasons consistently receive more rainfall, directly influencing crop selection strategies.
- Certain crops require and receive higher average rainfall, making them viable only in high-rainfall zones.
- Location-wise rainfall distribution reveals regional disparities that can inform irrigation investment priorities.

### [2] Temperature Analysis

- Average temperatures fluctuate across years, with the **Y2 (2010–2015)** period showing notable variation.
- Seasonal temperature analysis helps identify optimal planting and harvesting windows for different crops.
- Crop-specific temperature averages highlight which crops thrive under warmer or cooler conditions.
- Location-based temperature data assists in regional crop suitability planning.

### [3] Humidity Analysis

- Humidity levels are closely tied to seasonal and geographic factors.
- High-humidity regions correlate with specific crop types that perform better under moist conditions.
- Year-over-year humidity trends indicate possible shifts in microclimates across the agricultural zones.

### [4] Yield Analysis

- Yield trends over years reflect the impact of climate variability, with **Y2 (2010–2015)** showing a distinct yield pattern compared to other groups.
- Seasonal yield analysis confirms that certain seasons consistently produce higher agricultural output.
- Crop-wise yield comparison reveals the most and least productive crops in the dataset.
- Location-based yield analysis identifies high-performing agricultural zones and areas needing intervention.

---

### [5] Data Transformations Applied

- **Rainfall** values were scaled up by **10%** to account for measurement calibration.
- **Area** values were reduced by **10%** to reflect net cultivable land after exclusions.
- Customers (records) grouped into **Year Groups**: Y1 (2004–2009), Y2 (2010–2015), Y3 (2016–2019).
- Rainfall grouped into **Low, Medium, and High** categories for comparative analysis.

---

### Tech Stack

| Layer | Tool |
|---|---|
| Cloud Storage | AWS S3 |
| Data Warehouse | Snowflake |
| Visualization | Microsoft Power BI |
| Dataset Format | Excel (.xlsx) |
| Integration | AWS IAM Role + Snowflake Storage Integration |
