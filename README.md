# Airline_Database

## 1. Introduction
It is undeniable that COVID-19 has bring a sufficient impact on the commercial aviation industry. According to Mckinsey&Co, the aviation industry has dropped 44% on global revenues for airlines in 2020 compared to pre-COVID-19 period. However, most of the countries have decided to reopening their boarders for travelling, businesses and other purposes. Therefore, it is important to regain the customer’s trust and main a good reputation for the airlines. Therefore, the idea of creating a commercial aviation database has created so that we can discover all type of useful information on the selected airlines. (Bouwer and Tufft, 2022)
Objective:
- Collect the relevant datasets of selected airlines to understand the customer satisfaction of the airlines.
- Create data pipelines to maintain and extract the relevant dataset, such as airline reviews and airline information.
- Using ML pipeline to create an auto process to analyse the reviews of the airlines in depth.
- Create API for the ML model

## 2. Overview of Data Architecture workflow
This research is an extension of the Airwatch groupwork, which the total process will be set into 4 main steps.
1. Different type of data sources will be explored during this process, such as airline review website and airline information sharing platforms. The data sources will be reviewed to see whether it is suitable for the airline research.
2. Then data extraction will be conducted to create an automated pipeline on the AWS S3 bucket. So that the experience of data extraction will be more sustainable and effective.
3. Data transformation is considered in this research to create an effective data format into the PostgreSQL database so that the user can analyse the data in a more effective and automated format.
4. Creating a ML pipeline can be considered as the most important step in this research. Amazon SageMaker Pipeline is adopted as the ML pipeline so that the process can be built and automated on the machine learning workflows for customer satisfaction each airline.

## 3. Data Exploration and Extraction
These steps will be conducted a similar process based on the Airwatch groupwork since most of the datasets will be used in the later stage for this research. However, there are some changes will be made.

## 3.1 Data Exploration
Since the research is mainly focusing on the customer satisfaction on the selected airlines, the Twitter Tweet data and Yahoo Finance dataset will be removed from the original Airwatch database. And all the selected airlines will be the same from the Airwatch database, but additional airlines will be added into this new research, which are Tap-Portugal, Emirates, JetBlue-Airways, United-Airlines, Air-Canada, Singapore-Airlines.

The relevant data source:
Route, Airline and Airport data:
These datasets are mainly collected from different Github resources that contain multiple information about the airlines, such as country of the airport and airline names etc.

Skytrax Airline Review data
The review dataset is the main dataset in this research, which will explore further in later stage. It contains 700+ reviews from customers on the selected airlines, from airline rating to comment of the flight experience. Therefore, it allows us to explore the reputation of the airline in a qualitative and quantitative way.

## 3.2 Data Extraction method

Route, Airline and Airport data:
The dataset of these airline information is collected on GitHub by using web-scraping technique.

Skytrax Airline Review data:
The dataset of airline review is collected on the official Skytrax website by using Beautiful Soup web-scraping package.

## 3.3 Data Extraction pipeline
![image](https://user-images.githubusercontent.com/100432868/172072465-fb293dc4-9a7b-4999-b25a-847ea1ce5cbf.png)

From the web scraping pipeline, the dataset is collected through the selected Github and scraped the available dataset on the selected Github. Then the dataset will be stored into the personal faculty.ai. platform.
For the airline review data, the dataset is collected through the Skytrax API on the selected airlines. The dataset is set to automated to scrape monthly so that more reviews can be generated into the faculty.ai. platform. The data is set to scrape 50 reviews for each airline each time since the website has limits on the data collection for users.
Both datasets will be stored into a csv and parquet file storage, which allows us to run the ML pipeline process in an efficient way.

## 3.4 Data Storage
![image](https://user-images.githubusercontent.com/100432868/172072474-f25680ce-2813-4bf9-8a84-b7eeb52c2045.png)

After the data collection, all the available datasets are stored into the AWS S3 buckets with 5 buckets in total for data storage. Firstly, S3 bucket is chosen due its highly secured cloud system that is offering to the users. Most importantly, S3 bucket will be useful on the ML pipeline process, which is on the later stage. The whole process will be more efficient since most of the steps will be conducted on the AWS, which it can created a more auto-process.

## 4. Data Transformation

## 4.1 Database design
![image](https://user-images.githubusercontent.com/100432868/172072506-81f8d5cf-fe5e-4114-8db8-dc3d47be8a16.png)

Since there are only two data sources for the database, I have split the data categories into 5 data table in total. The purpose of creating a data schema for the database is it allows different raw dataset to create relationship between the entities. Therefore, the process of data queries will become efficient for the users.
In this database schema, I have managed to divide into 2 categories within 5 tables, which are routes, country, airline and airport from airline information categories and reviews from customer satisfaction information.

## 4.2 Database connection

![image](https://user-images.githubusercontent.com/100432868/172072556-dd42debb-fd8e-478d-bf34-4c29dba93f49.png)

Firstly, a database is needed to be created to store the PostgreSQL database storage. Therefore, I managed to set up a RDS database to store all the selected dataset into this database. The rationale of creating RDS database is it allows users want to access the raw dataset in anytime without any restriction.

## 4.2.2 Connecting AWS RDS

![image](https://user-images.githubusercontent.com/100432868/172072592-d7d5ffd2-6fe4-4ad1-9852-1c43f581d626.png)
![image](https://user-images.githubusercontent.com/100432868/172072602-5695e451-e189-4987-904f-7fef4e7e5dc5.png)

## 4.2.2 Creating tables
To create a database schema, we need to create the tables for the database diagram, which this is the example of creating one of the tables.
![image](https://user-images.githubusercontent.com/100432868/172072624-caf96191-b309-4c7c-86bb-0938c6f8c530.png)

## 4.2.3 Implementing database schema
Now we need create the schema into the Postgres sql database, and the schema will be stored into a sql file which will contain all the data type and information from the table.

## 4.3 Database linkage
![image](https://user-images.githubusercontent.com/100432868/172072844-03bc0dd4-9b67-413d-8e57-5fbe8b7aa9d8.png)

After the postgres sql database has been created, we need to use PySpark as a data pipeline to push it into the AWS RDS database on faculty.ai. Since we are pushing a large amount of data, PySpark creates a stable and fast data transformation for the data processing to Postgres.

## 5. ML pipeline with AWS SageMaker

The ML pipeline is used because it allows us to see the end-to-end construct on the ML workflow of the whole ML process with other team members. This is to avoid any larger bugs that has been appeared on the process so that other team members can spot them earlier to do the debugging process. Therefore, it allows the team to work on other important tasks and make the code consistent.
In this case, AWS SageMaker Pipeline is adopted because it not only allows users to build and sacle the ML workflows easier, but it allows us to experiment with different algorithms, training, turning, and deploying models in an automotive process. When users want to develop and manage the ML workflow manually can take a long period of time in the coding process, which AWS SageMaker can shorten this process. Most importantly, AWS SageMaker allows us to create an API Gateway in a later stage, which can create a more interactive process for all users in anytime and any location.
In this research, I will be using the AWS SageMaker Pipeline to train and deploy a text binary classification model to predict airline ratings based on the customers’ comments. Therefore, we can conduct a sentiment analysis on the airline ratings based on the comments to see whether it is negative or positive. BlazingText will be used, which is one of the SageMaker built-in algorithms, it allows us to minimise the workflow to train and deploy the model manually. BlazingText is mainly run through the implementations of Word2vec and text classification algorithms, which is suitable for this sentiment analysis task.

## 5.1 AWS SageMaker set up
![image](https://user-images.githubusercontent.com/100432868/172072942-5591da5c-4fca-4752-8d82-4bbb709530a0.png)

To set up the AWS SageMaker, I have created a Notebook instance on the AWS SageMaker so that we can use the Blazing Text build-in algorithms on a Jupyter Notebook environment. Moreover, I managed to pull request to my personal Github by getting the personally token on Github. Therefore, it can show changes and create version control automatically.

## 5.2 Data cleaning and data selection
From this stage, we are only focusing on the airline reviews
![image](https://user-images.githubusercontent.com/100432868/172072975-67e82e10-2d58-4944-98ed-04d12d10af74.png)

Columns:
Comments – reviews on the experience for each airline.
Ratings – From scale 1 to 10 with 1 is most negative experience and 10 is the best experience.

From this stage, we are only focusing on the airline reviews for the research. The data cleanse process is needed to conduct due to the csv file is still in a raw format. Since we are only focusing on the “comment” and “rating” columns to conduct the sentiment analysis, the figure shows the dataset is imbalanced; it shows the observations with lowest rating outstands the rest of the rating index. This suggests that many customers are not happy with most of the airline experience. The imbalance data can lead to over-biased result to the negative reviews with poor model accuracy on the training data. Therefore, we might need to consider conducting these following steps:

Data cleaning on “rating” attribute:
1. Grouping the 1&2 ratings as the negative review category and 9&10 ratings as the positive review category and create a new column as “Label”.
2. Oversampling the positive reviews category to increase the sample size
3. Remove the ratings from 3-8, which is the natural reviews since it is difficult to distinguish the neutral reviews from positive and negative reviews for the sentiment analysis.

Data cleaning on “comment” attribute:
1. Remove the rows if there is missing comment text on the rows
2. Remove all the “Verified” and “Not Verified” with emoji on the comment text since it will reduce the model accuracy on the training model in later stage.

![image](https://user-images.githubusercontent.com/100432868/172072996-8d612b06-d04c-4515-be3f-5094d7f834d4.png)

This figure shows the new data frame with the cleaned attributes “comment” and “Label” and 588 rows of data size. To save the new dataset, I have managed to save as csv and parquet format for later stage on the training model.

![image](https://user-images.githubusercontent.com/100432868/172073004-c43b0061-d1c3-4abe-98e1-73e5aad78cc7.png)

Moreover, I have also considered to store all the new dataset into the new S3 bucket so that I can direct pull my dataset from the S3 bucket on the same environment to train the built-in SageMaker model.

## 5.3 Manual testing on Training and Deploying a Text Classification model
## 5.3.1 BlazingText Algorithm
![image](https://user-images.githubusercontent.com/100432868/172073031-b03f3406-045c-4793-94bf-3cc0d0492a7a.png)

The BlazingText algorithm is used because it provides an implementation of the Word2Vec and text classification algorithms. Since this research is a sentiment analysis on airline reviews, both implementations will be useful for this NLP tasks, such as sentiment analysis in this case. As we can see, this research task is a supervised learning type. This suggests that the modes of BlazingText algorithm will be conducted on text classification.

## 5.3.2 Error
Errors are shown on the very late stage on the pipeline creation for this SageMaker pipeline task. The error shows when I am examining the JSON pipeline definition, it does not allow me to submit the pipeline definition to the SageMaker Pipeline service, which means it did not connect properly to the AWS service. Therefore, the manual attempt of building a SageMaker pipeline did not work in this case.

## 5.4 Automatic testing on Autopilot
![image](https://user-images.githubusercontent.com/100432868/172073059-e5336064-b093-4f18-8446-14fe730d9738.png)

Since the manual ML pipeline did not work in this case, Amazon Sagemaker Autopilot is considered in this stage. The AutoML service will create less human error on the manual preparation on features, which will reduce the chance of creating errors in the model training. The AWS SageMaker Autopilot allows the system to conduct the ML process automatically
while the users can have full control on the model training. Moreover, all the information will be saved into the S3 bucket as a backup.

![image](https://user-images.githubusercontent.com/100432868/172073067-5a73f97d-035a-4fc1-bdef-f24053c09772.png)

To set up the AutoML process, I managed to create an Autopilot experiment on the Amazon SageMaker Studio. The figure shows the settings that I have done for this experiment with “Labal” column as the target in this case. Also, I selected the airline review with cleaned parquet format in this experiment.




The BlazingText algorithm is used because it provides an implementation of the Word2Vec and text classification algorithms. Since this research is a sentiment analysis on airline reviews, both implementations will be useful for this NLP tasks, such as sentiment analysis in this case. As we can see, this research task is a supervised learning type. This suggests that the modes of BlazingText algorithm will be conducted on text classification.

## 5.4.1 Model performance
![image](https://user-images.githubusercontent.com/100432868/172073092-a5e7ad1e-9064-437c-b461-a425c73845cc.png)

The figure shows the experiment has produced a promising result with 0.944 accuracy on XGBoost algorithm. The experiment is completed with 250 different model training on a binary classification problem type.

![image](https://user-images.githubusercontent.com/100432868/172073103-17e0a541-969b-4ab3-88fb-071af955f83d.png)

Both figures show most of the reviews that are commented by the customers are mostly negative and it fits to the prediction on the confusion matrix. Therefore, the selected airlines should consider how they can improve the customer experience on the flights and their services to regain the trust from the existing customers. This can increase the reputation of airline industry.

## 5.5 Deploy model
![image](https://user-images.githubusercontent.com/100432868/172073122-96855f69-32b3-41f1-b1ff-31fbf7e61fa1.png)

After the AutoML expertiment, the deployment for model can be proceed. The figure shows the deployment of this model should be working in the service. From this process, it creates a SageMaker model, endpoint, and endpoint configuration, which will be useful in API creation stage.

## 5.6 IAM role for S3, SageMaker, API Gateway and RDS
![image](https://user-images.githubusercontent.com/100432868/172073141-d9ba7258-1569-423f-b259-d7735052bd9d.png)

Processing every stage on cloud service can be dangerous due to a possibility of third-party access to the files. However, AWS IAM resource can limit such consideration. IAM roles provides temporary security credentials to access certain files. Each role can be set on different level of permissions. In this case, IAM role can create short-term credential for this research so that I would not public my files or models on public without my full knowledge.

## 5.7 Create API for the model deployment
![image](https://user-images.githubusercontent.com/100432868/172073146-ffdd2b8c-b95b-4c04-90b2-9fbf6a954bd3.png)

The Amazon API Gateway has been used, as shown on this figure. This service is used in this research because the deployment of the model is only running on the user platform, but other users cannot access and test the model. Creating a API Gateway allows other users to test the SageMaker model with a web-friendly approach REST API as an example. In this case, the end-users can interact with the sentiment analysis on airline reviews that has been produced by SageMaker on either a web browsers or mobile device.

## 6.Limitation
Due to the practicality of the research, there are only a very limited data can be collected due to its availability. Most of the API and website requires a certain amount of expenses to scrape the data. Therefore, the available of dataset may not provide the most robust accuracy on the training data process, which could lead to the accuracy of the result.
Moreover, the available of resources are limited in this research. This is because the available budget of this research is limited due to the high cost of AWS service. Some of the AWS services provide free access to students. However, AWS SageMaker Autopilot does not provide free access to students. Therefore, I can only train the dataset in a set number of times due to available budget restraint.
Lastly, the manual ML pipeline process did not work as it planned in this research. This is because there are many unforeseen errors that I have ever occurred in my knowledge. Since this is my first-time using AWS service to conduct research, my knowledge of using AWS service is limited. For example, certain pathway of the file has occurred multiple times in the system. Therefore, it is difficult proceed the process given the available time frame.

## 7. Conclusion
In conclusion, I have managed to use AWS services to conduct the sentiment analysis on the airline reviews to produce an autoML process and create an API for the deployment of the model for other users to test. For further improvement, other methods to attempt the auto-process can be considered, such as using Lambda function to create the auto-process for this research. Also, we can explore other available AWS services to create a more efficient ML process with higher budget control.



