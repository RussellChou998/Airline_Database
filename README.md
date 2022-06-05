# Airline_Database

## 1. Introduction
It is undeniable that COVID-19 has bring a sufficient impact on the commercial aviation industry. According to Mckinsey&Co, the aviation industry has dropped 44% on global revenues for airlines in 2020 compared to pre-COVID-19 period. However, most of the countries have decided to reopening their boarders for travelling, businesses and other purposes. Therefore, it is important to regain the customer’s trust and main a good reputation for the airlines. Therefore, the idea of creating a commercial aviation database has created so that we can discover all type of useful information on the selected airlines. (Bouwer and Tufft, 2022)
Objective:
- Collect the relevant datasets of selected airlines to understand the customer satisfaction of the airlines.
- Create data pipelines to maintain and extract the relevant dataset, such as airline reviews and airline information.
- Using ML pipeline to create an auto process to analyse the reviews of the airlines in depth.
- Create API for the ML model

## 2. Overview of Data Architecture workflow
This research is an extension of the Airwatch groupwork, which the total process will be set into 5 main steps.
1. Different type of data sources will be explored during this process, such as airline review website and airline information sharing platforms. The data sources will be reviewed to see whether it is suitable for the airline research.
2. Then data extraction will be conducted to create an automated pipeline on the AWS S3 bucket. So that the experience of data extraction will be more sustainable and effective.
3. Data transformation is considered in this research to create an effective data format into the PostgreSQL database so that the user can analyse the data in a more effective and automated format.
4. Creating a ML pipeline can be considered as the most important step in this research. Amazon SageMaker Pipeline is adopted as the ML pipeline so that the process can be built and automated on the machine learning workflows for customer satisfaction each airline.

