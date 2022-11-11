# EDA-Airbnb
This is a real time capstone project based on Airbnb.
Exploratory Data Analysis (EDA) on NYC
Airbnb is an online marketplace that connects people who want to rent out their homes with people looking for accommodations in that locale. NYC is the most populous city in the United States, and one of the most popular tourism and business places globally.
Since 2008, guests and hosts have used Airbnb to expand on traveling possibilities and present a more unique, personalized way of experiencing the world. Nowadays, Airbnb became one of a kind service that is used by the whole world. Data analysts become a crucial factor for the company that provided millions of listings through Airbnb. These listings generate a lot of data that can be analyzed and used for security, business decisions, understanding of customers’ and providers’ behaviour on the platform, implementing innovative additional services, guiding marketing initiatives, and much more.

Import Libraries 

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
%matplotlib inline
import seaborn as sns
sns.set() 


   
Import the data

The dataset we use are “New York Airbnb Open data”.  This
data is in my Google drive & this is a CSV file. I importing this 
data by using Panda library as follows –

from google.colab import drive
drive.mount('/content/drive')                                                                                                                                            


Read the data   
 
Now after importing the data we have to read it & we read it via panda library as follows –

df = pd.read_csv('/content/drive/MyDrive/project/Copy of Airbnb NYC 2019.csv')
                                                                                                                                                                         
here df = “ Data Frame”


After reading the data we have to cleaning & manuplating the data which are done by further steps. In , further steps we keep only useful data which are really helpful in data analyzing.
Problem Statement

For this project we are analyzing Airbnb’s New York City(NYC) data of 2019. NYC  is not only the most famous city in the world but also top global destination for  visitors drawn to its museums, entertainment, restaurants and commerce.

Our main objective is to ﬁnd out the key metrics that inﬂuence the listing of  properties on the platform. For this, we will explore and visualize the dataset  from Airbnb in NYC using basic exploratory data analysis (EDA) techniques.

Data analysis on thousands of listings provided through Airbnb is a crucial  factor for the company.

We will be ﬁnding out the distribution of every Airbnb listing based on their  location, including their price range, room type, listing name, and other related  factors.

Understanding the Data

There are 49,000 observations with various types of field in our dataset.
List of field:
■	Id
■	Name
■	Host  id
■	Host name
■	Neighbourhood group
■	Neighbourhood
■	Latitude
■	Longitude
■	Room type
■	Price
■	Minimum nights
■	Number of reviews
■	Last review
■	Reviews per month
■	Calculated host listing  count
■	Availability  365

Analyzing the data
Now we have to analyzing the data according the given condition in starting.
There are four given parameters:-

What can we learn about different hosts and areas?

What can we learn from predictions? (ex: locations, prices, reviews, etc)

Which hosts are the busiest and why?

Is there any noticeable difference of traffic among different areas and what could be the reason for it?
By using df.info() in coding shell we get every column & its value count & data type 


Data columns (total 16 columns):
 #   Column                          Non-Null Count  Dtype  
---  ------                          --------------  -----  
 0   id                              48895 non-null  int64  
 1   name                            48879 non-null  object 
 2   host_id                         48895 non-null  int64  
 3   host_name                       48874 non-null  object 
 4   neighbourhood_group             48895 non-null  object 
 5   neighbourhood                   48895 non-null  object 
 6   latitude                        48895 non-null  float64
 7   longitude                       48895 non-null  float64
 8   room_type                       48895 non-null  object 
 9   price                           48895 non-null  int64  
 10  minimum_nights                  48895 non-null  int64  
 11  number_of_reviews               48895 non-null  int64  
 12  last_review                     38843 non-null  object 
 13  reviews_per_month               38843 non-null  float64
 14  calculated_host_listings_count  48895 non-null  int64  
 15  availability_365                48895 non-null  int64  
dtypes: float64(3), int64(7), object(6)

Now we use only particular or selected columns for our data analyzing & we drop unwanted columns as follows:



new_df = df[['id','name','host_id','host_name','neighbourhood_group','neighbourhood','room_type','price','minimum_nights','number_of_reviews','calculated_host_listings_count','availability_365']]

Now condition first,
What can we learn about different hosts and areas?

We get this by using following method
hosts_areas = new_df.groupby(['host_name','neighbourhood_group'])['calculated_host_listings_count'].max().reset_index()
hosts_areas.sort_values(by='calculated_host_listings_count', ascending=False).head(10)
From the above method we get that  Airbnb listing in New York are near Manhattan & brooklyn has the highest share of hotels.
We shows it via pie chart

 


Now condition second,
What can we learn from predictions? (ex: locations, prices, reviews, etc)

We get this by using following method

Area_reviews = new_df.groupby(['neighbourhood_group'])['number_of_reviews'].max().reset_index()
Area_reviews

Area Vs review

 


price_area = new_df.groupby(['price'])['number_of_reviews'].max().reset_index()
price_area.head(5)

Price Vs Review

 
From the above graph it is concluded people wants leave where price is low.

Now condition third,
Which hosts are the busiest and why?

We get this by using following method
busiest_hosts = new_df.groupby(['host_name','host_id','room_type'])['number_of_reviews'].max().reset_index()
busiest_hosts = busiest_hosts.sort_values(by='number_of_reviews', ascending=False).head(10)
busiest_hosts


after that we get the list of 10 busiest hosts.The 5 busiest hosts are as below
Busiest hosts are:
1.	Dona
2.	Ji
3.	Maya
4.	Carol
5.	Danielle
They are busiest because these hosts listed room type as Entire home and Private room which is preferred by most number of people.

Now condition fourth,
Is there any noticeable difference of traffic among different areas and what could be the reason for it?
We get this by using following method
traffic_areas = new_df.groupby(['neighbourhood_group','room_type'])['minimum_nights'].count().reset_index()
traffic_areas = traffic_areas.sort_values(by='minimum_nights', ascending=False)
traffic_areas
 
Conclusion:
1. The people who prefer to stay in Entire home or Apartment they      are going to stay bit longer in that particular Neighbourhood only.
2. The people who prefer to stay in Private room they won't stay   longer as compared to Home or Apartment.
3. Most people prefer to pay less price.
4. If there are more number of Reviews for particular Neighbourhood group that means that place is a tourist place.
5. If people are not staying more then one night means they are travellers.

Reference:
Analytics Vidhya, Alma better live classes &
You tube
