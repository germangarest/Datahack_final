Index

    1. Problem Description
    2. Dataset
        2.1 Data Acquisition
        2.2 Fields and Records
    3. ETL
        3.1 Extraction (source connection)
        3.2 Transformation (PowerQuery)
        3.3 Loading (PowerBI)
    4. Data Model (Star Schema)
    5. Ratios and Metrics of Interest
    6. Final Result
    7. References
    8. Appendix
        8.1 DAX Formulas Used
        8.2 PowerQuery

1. Problem Description

DH Marketing Consultants has hired you as a data analyst to investigate and analyze a dataset from the marketing department. The marketing director requires generating value from these data and asks you to perform an analysis. This analysis must be based on the various factors that we can measure in the dataset. At minimum, the following tasks are expected:

    Data Cleaning
    Data Transformation
    Visualization

2. Dataset

The data provided comes from a publicly accessible data source that contains information related to five marketing campaigns conducted by a company. These data include details on the platforms used and the number of sales generated through these platforms, along with other highly relevant data that offer significant potential for extracting a large amount of valuable information.
2.1 Data Acquisition

The data has been obtained publicly and free of charge through the following link. The context is based on the need to create a response model that significantly enhances the efficiency of a marketing campaign by increasing responses or reducing expenses. The goal lies in foreseeing who will respond to an offer for a product or service, which can optimize the marketing strategy and maximize the resources invested in the campaign.
2.2 Fields and Records

The fields that make up the dataset could be classified into 4 main groups, totaling 29:

    Demographic and Personal Data:
    <br></br>

    ID: Unique customer identification. (Data type: Integer)

    Year_Birth: Customer's year of birth. (Data type: Integer)

    Education: Customer's educational level. (Data type: Text)

    Marital_Status: Customer's marital status. (Data type: Text)

    Income: Annual household income of the customer. (Data type: Numeric - decimal)

    Kidhome: Number of young children in the customer's home. (Data type: Integer)

    Teenhome: Number of teenagers in the customer's home. (Data type: Integer)

    Dt_Customer: Customer's registration date with the company. (Data type: Date)
    <br></br>

    Purchasing Behavior:
    <br></br>

    Recency: Number of days since the customer's last purchase. (Data type: Integer)

    NumDealsPurchases: Number of purchases made with a discount. (Data type: Integer)

    NumWebPurchases: Number of purchases made through the company's website. (Data type: Integer)

    NumCatalogPurchases: Number of purchases made using a catalog. (Data type: Integer)

    NumStorePurchases: Number of purchases made directly in stores. (Data type: Integer)

    NumWebVisitsMonth: Number of visits to the company's website in the last month. (Data type: Integer)
    <br></br>

    Spending on Products:
    <br></br>

    MntWines: Amount spent on wine products in the last 2 years. (Data type: Numeric - decimal)

    MntFruits: Amount spent on fruit products in the last 2 years. (Data type: Numeric - decimal)

    MntMeatProducts: Amount spent on meat products in the last 2 years. (Data type: Numeric - decimal)

    MntFishProducts: Amount spent on fish products in the last 2 years. (Data type: Numeric - decimal)

    MntSweetProducts: Amount spent on sweet products in the last 2 years. (Data type: Numeric - decimal)

    MntGoldProds: Amount spent on gold products in the last 2 years. (Data type: Numeric - decimal)
    <br></br>

    Responses to Marketing Campaigns:
    <br></br>

    AcceptedCmp3: 1 if the customer accepted the offer in the third campaign, 0 otherwise. (Data type: Integer - binary)

    AcceptedCmp4: 1 if the customer accepted the offer in the fourth campaign, 0 otherwise. (Data type: Integer - binary)

    AcceptedCmp5: 1 if the customer accepted the offer in the fifth campaign, 0 otherwise. (Data type: Integer - binary)

    AcceptedCmp1: 1 if the customer accepted the offer in the first campaign, 0 otherwise. (Data type: Integer - binary)

    AcceptedCmp2: 1 if the customer accepted the offer in the second campaign, 0 otherwise. (Data type: Integer - binary)

    Complain: 1 if the customer filed a complaint in the last 2 years. (Data type: Integer - binary)

    Z_CostContact: Fixed cost associated with contacting the customer. (Data type: Integer)

    Z_Revenue: Revenue generated from customer contact. (Data type: Integer)

    Response: 1 if the customer accepted the offer in the last campaign, 0 otherwise. (Data type: Integer - binary)

3. ETL
3.1 Extraction (source connection)

For data extraction, a source data connection has been made from PowerBI to the file named marketing_campaign.xlsx from Menu Data > Excel Workbook obtaining the following visualization:

<br></br>

E1

<br></br>
The data were then displayed in the PowerQuery Editor for subsequent processing and transformation (see next figure)
<br></br>

E2
<br></br>

The M Language code implemented for data extraction is found in section 8.2 of this document
3.2 Transformation (PowerQuery)
3.3 Loading (PowerBI)
4. Data Model (Star Schema)
<br>

    Fact Table:

The fact table contains the quantitative metrics we will analyze. In this case, the most relevant metrics for the marketing campaign dataset are:
<br>

    CustomerID: foreign key linked to the Customer dimension

    CampaignID: foreign key linked to the Campaign dimension

    AcceptedCmp1, AcceptedCmp2, AcceptedCmp3, AcceptedCmp4, AcceptedCmp5, Response: 1 for accepted, 0 for not accepted

    Complain: 1 for complaint, 0 for no complaint

    NumDealsPurchases, NumWebPurchases, NumCatalogPurchases, NumStorePurchases, NumWebVisitsMonth: quantitative metrics.
    <br>
    Customer Dimension:

<br>

    CustomerID: primary key

    Year_Birth, Education, Marital_Status, Income, Kidhome, Teenhome: descriptive attributes
    Campaign Dimension:

<br>

    CampaignID: primary key
    CampaignName: "Campaign 1", "Campaign 2", etc.
    PlatformUsed: Descriptive attributes about the campaign

5. Ratios and Metrics of Interest

There are several key metrics that we could extract from this Dataset.
<br>

    Conversion Rate for Each Campaign:
    <br>

Metric: Calculates the conversion rate for each campaign (AcceptedCmp1 to AcceptedCmp5) by dividing the number of customers who accepted the offer in a campaign by the total number of customers in that campaign.
This evaluates the effectiveness of each campaign. A very high conversion rate will indicate a more successful campaign.
<br>

2.Overall Response Rate:
<br></br>

Metric: Calculates the overall response rate by dividing the total number of customers who responded positively in the last campaign (Response=1) by the total number of customers.
This metric provides a general view of the overall effectiveness of the campaign and customer engagement.
<br></br>

    Customer Complaint Rate:
    <br></br>

Metric: Calculates the percentage of customers who filed complaints (Complain=1) in the last 2 years.
This indicates the degree of customer dissatisfaction, which could affect future marketing strategies and customer retention efforts.
<br></br>

    Demographic Analysis of Customers:
    <br></br>

Metrics: Explores the distribution of customers based on Education, Marital Status, and Income.
Understanding the demographic profile of customers can help tailor marketing campaigns to specific customer segments.
<br></br>

    Purchase Patterns:
    <br></br>

Metrics: Analyzes the average amount spent on different product categories (MntWines, MntFruits, MntMeatProducts, etc.).
We calculate the spending ratios on different product categories to understand customer preferences.
In this way, we identify popular product categories and customer preferences, facilitating targeted marketing efforts.
<br></br>

    Household Composition of Customers:
    <br></br>

Metrics: Explores the average number of children (Kidhome) and teenagers (Teenhome) in customers' households.
We calculate the ratios of children and teenagers relative to adults in households.
It seeks to provide insight into the family structure of customers, which can influence marketing strategies, especially for family-oriented products.
<br></br>

    Customer Purchase Channels:
    <br></br>

Metrics: Analyzes the number of purchases made through different channels (NumWebPurchases, NumCatalogPurchases, NumStorePurchases, etc.).
We calculate the proportion of online purchases relative to total purchases, catalog purchases relative to total purchases, etc.
We thus identify the most popular purchase channels, guiding marketing efforts and resource allocation.
<br></br>

    Purchase Frequency:
    <br></br>

Metric: Analyzes the average number of days since the last purchase (Recency).
It indicates customer participation and loyalty. A lower recency value suggests active customer engagement.
<br></br>

    Customer Response Analysis Based on Purchase Frequency:
    <br></br>

Metric: Calculates response rates based on different periods of recency (e.g., response rates for customers who made a purchase in the last 30 days, 60 days, etc.).
We identify if recent customer activity correlates with responses to campaigns, allowing targeted campaigns toward active customers.
<br></br>

    Customer Loyalty Metrics:
    <br></br>

Metrics: Explores the number of offers and discounts customers have used (NumDealsPurchases) and analyze the response rates for these customers.
We identify the impact of loyalty programs and discounts on customer responses, helping to optimize future campaigns.
<br></br>

    Customer Engagement on the Company Website:
    <br></br>

Metric: Analyzes the average number of website visits per month (NumWebVisitsMonth) and the response rates for customers based on their participation on the website.
It helps us understand the correlation between online engagement and responses to campaigns, guiding digital marketing strategies.
<br></br>

    Cohort Analysis:
    <br></br>

Metric: Groups customers by their registration date (DtCustomer) and analyze their responses over time.
We provide insights into the evolution of customer behavior, helping to understand long-term participation trends.
<br></br>

    Analysis of Revenue and Costs:
    <br></br>

Metrics: Calculates the revenue generated per customer (Income) and analyze the marketing costs for each campaign.
We calculate the ROI (Return on Investment) for each campaign by comparing the revenue generated with the marketing costs.
It helps to evaluate the profitability of marketing campaigns and optimize budget allocation.
