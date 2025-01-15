# Azure_E2E_pipeline_project
This project create End to End data pipeline solution in Azure cloud using Azure Data Factory , Azure Databricks , Azure Synapse Anlytics , Azure DL gen2. 
________________________________________________________________________________________________________
## Flow Project Diagram
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/project_strcuture.png)

_________________________________________________________________________________________________________

## Part1: Ingestion Data
Using Azure Data Factory to do data ingestion process from HTTP web to GET csv file and Store file in Azure data lake gen2 (Bronze bucket)
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/e2epipeline%20-%20Azure%20Data%20Factory%20-%20Google%20Chrome%201_15_2025%202_29_18%20AM.PNG)

_________________________________________________________________________________________________________

## Part2: Transform Data
Using Azure Databricks to transform data. In this process we will do 2 step in transformation data
### 1. Transform Bronze to Silver
This step we drop unnecessary columns (Naive_Bayes_Classifier_Attrition_Flag_Card_Category_Contacts_Count_12_mon_Dependent_count_Education_Level_Months_Inactive_12_mon_1', 'Naive_Bayes_Classifier_Attrition_Flag_Card_Category_Contacts_Count_12_mon_Dependent_count_Education_Level_Months_Inactive_12_mon_2) , Rename column CLIENTNUM to Client_Id and Save result to Parquet file in Silver Bucket 
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/Tranform_2_Silver%20-%20Databricks.PNG)

### 2. Transform Silver to Gold
This step we Normalization Data From 1NF to 2 NF. we will break down to 2 table 
- customer_table : contains on customer detail with Client_Id is primary key
- accout_table : contains on account deatail with Client_Id is foreign key
and Save result to Parquet file in Gold Bucket 
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/Transform_2_Gold%20-%20Databricks.PNG)

_________________________________________________________________________________________________________

## Part3: Create Table 
This step we create External Table in Azure Synapse Analytics from result in Part2 
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/e2eproject%20-%20Azure%20Synapse%20Analytics%20-%20Google%20Chrome%201_15_2025%202_22_00%20AM.PNG)

_____________________________________________________________________________________________________________-

## Part4: Reporting 
Create Customer Churn dash board using data from External Table (gold.excustomer , gold.exaccount) 
![alt text](https://github.com/OmegaZeroTribe/Azure_E2E_pipeline_project/blob/main/Untitled.pdf%20-%20Profile%201%20-%20Microsoft%E2%80%8B%20Edge%201_15_2025%202_23_22%20AM.PNG)
