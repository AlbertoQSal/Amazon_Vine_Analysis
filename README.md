# Amazon_Vine_Analysis Module 17
## Overview
Allong this module I analized information from different sources using Big data tools like Spark, Postgresql, and Amazon Web Services (AWS). The main objective of the Challenge 17 was to analize Amazon reviews written by members of the paid Amazon Vine program.

This analysis was performed using Google Colaboratory with PySpark to perform ETL to the Amazon Product Reviews, Postgresql to create the Relational Databases allong with Google Colaboratory, and Jupyter Notebook with python pandas to determine if there was any bias towards reviews that were written as part of the Vine program.

## Results
### ETL on Amazon Product Reviews
The first part of the challenge consisted in the use of Google Colaboratory, Spark, and Postgres for the performing of the ETL process. 

#### Extract
Connecting the Google Colaboratory notebook with AWS the data was Extracted from an AWS Bucket, where the database used was the "amazon_reviews_us_Video_Games_v1_00". The data was imported in a csv format, and assigned to a variable as a spark DataFrame.

#### Transform 
Using the spark DataFrame properties, four DataFrames were created from the original Dataframe. 

The first one was the "customers_df", this DataFrame grouped the amount of customer reviews performed by each customer. The Figure 1 shows the final DataFrame.

<img width="255" alt="Captura de pantalla 2023-02-06 a la(s) 9 43 26" src="https://user-images.githubusercontent.com/93279134/217016834-631a12bd-aa0a-4c21-9879-ea088c534295.png"> 

Figure 1. "customers_df" DataFrame.

The second one was the "products_df", this DataFrame only selected two specific columns from the original DataFrame, the "product_id" column and the "product_title" column. The resulting DataFrame is shown in Figure 2.

<img width="289" alt="Captura de pantalla 2023-02-06 a la(s) 9 48 05" src="https://user-images.githubusercontent.com/93279134/217018052-95250034-d53d-4f19-94d8-15cccc0e9f6f.png">

Figure 2. "products_df" DataFrame.

The third one was the "review_id_df", this DataFrame selected the 'review_id', 'customer_id', 'product_id', 'product_parent, and 'review_date' columns. The resulting DataFrame is shown in Figure 3.

<img width="569" alt="Captura de pantalla 2023-02-06 a la(s) 9 55 58" src="https://user-images.githubusercontent.com/93279134/217019989-cbe1adb5-ddad-4b69-b9d9-fb5efa7a0b93.png">

Figure 3. "review_id_df" DataFrame.

The fourth and last Dataframe was the "vine_df" DataFrame, this DataFrame selected the 'review_id', 'star_rating', 'helpful_votes', 'total_votes', 'vine',  and 'verified_purchase' columns. The resulting DataFrame is shown in Figure 4.

<img width="659" alt="Captura de pantalla 2023-02-06 a la(s) 9 58 30" src="https://user-images.githubusercontent.com/93279134/217020647-b2cebd32-ea02-4d88-9ce4-e82b4fdbb3cd.png">

Figure 4. "vine_df" DataFrame.

#### Load 
Using spark and postgres, the DataFrames created above were loaded into a database created in AWS and postgres. Each DataFrame was assigned to an specific table in postgres.

### Determine Bias of Vine Reviews
The second part of the challenge consisted in the use of Jupyter Notebook and Pandas to analize the "vine_df" DataFrame.  This DataFrame was imported as a table named "vine_table.csv". The objective of this part was to determine if there is any bias towards reviews that were written as part of the Vine program. The analysis helped us to determine if having a paid Vine review makes a difference in the percentage of 5-star reviews.

Allong the development of this part, 4 DataFrames and a results dictionary were created, so the bias or not could be shown.

The first DataFrame consisted in filtering the 'total_votes' column so that the new DataFrame only contained those rows with a total of votes greater than 20 votes. The Figure 5 shows the resulting DataFrame.

![Captura de pantalla 2023-02-06 a la(s) 10 15 30](https://user-images.githubusercontent.com/93279134/217025086-c72060f2-7943-4ab9-9c44-3e2681079751.png)

Figure 5. "totalVotes_df" DataFrame.

The second DataFrame consisted in filtering the 'total_votes' column so that the new DataFrame only contained those rows where the percentage of helpful_votes divided by total_votes is equal to or greater than 50%. The Figure 6 shows the resulting DataFrame.

![Captura de pantalla 2023-02-06 a la(s) 10 18 29](https://user-images.githubusercontent.com/93279134/217025743-3d2e6852-9b48-42eb-bc50-94e560246dee.png)

Figure 6. "votesPercentage_df" DataFrame.

The third DataFrame consisted in filtering the 'vine' column so that the new DataFrame only contained those rows where the reviews were paid. The Figure 7 shows the resulting DataFrame.

![Captura de pantalla 2023-02-06 a la(s) 10 22 55](https://user-images.githubusercontent.com/93279134/217026790-1836b86e-ebbe-4a23-aada-097ddc187d81.png)

Figure 7. "reviewY_df" DataFrame.

The fourth DataFrame consisted in filtering the 'vine' column so that the new DataFrame only contained those rows where the reviews were unpaid. The Figure 8 shows the resulting DataFrame.

![Captura de pantalla 2023-02-06 a la(s) 10 25 05](https://user-images.githubusercontent.com/93279134/217027334-f3b25c57-39de-424b-9f27-f323ae798602.png)

Figure 8. "reviewN_df" DataFrame.

The last part consisted in the creation of the results dictionary. This dictionary contained the total number of reviews, the number of 5-star reviews, and the percentage of 5-star reviews for the two types of review (paid vs unpaid). The Figure 9 shows the results dictionary.

![Captura de pantalla 2023-02-06 a la(s) 10 29 02](https://user-images.githubusercontent.com/93279134/217028316-8506973f-7e28-4d68-97b5-f6293d8e91e7.png)

Figure 9. "results" Dictionary.

## Summary 
Based on the Figure 9, we can see that ther is no bias towards the paid reviews because they only represent the 0.13% of the 5 Stars reviews. The 99.87% of the 5 Stars reviews were unpaidm this means that the quality of the product is inherent itself and it doesn't need a paid review.

An additional analysis could be performed on the 1 Stars reviews, this could show us which products should be eliminated or should be stop being selled. This with the objective of reducing the amount of these reviws.
