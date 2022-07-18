# MAGIST-DATA-ANALYSIS-PROJECT

## 📕  Table Of Contents

* 0.📋 INTRODUCTION
* 1.📋 PROBLEM STATEMENT 
* 2.🕵 DATA DISCOVERY
* 3.🗄 ANSWERING BUSINESS QUESTIONS
* 4.📊 DATA VISUALIZATIONS
* 5.🕵 CONSCLUSION


## INTRODUCTION

Lets starts with information about company called Eniac. Eniac is an online marketplace specialised in Apple compatible accessories. It was founded 10 years ago in Spain and it has since grown and expanded to other neighbouring countries. Eniac is exploring an expansion to the Brazilian market. Data shows that Brazil has an eCommerce revenue similar to that of Spain and Italy: an already huge market with an even bigger potential for growth.



## PROBLEM STATEMENT
The problem, for Eniac, is the lack of knowledge of such market. The company doesn’t have ties with local providers, package delivery services or customer service agencies. Creating these ties and knowing the market would take a lot of time, while the board of directors has demanded the expansion to happen within the next year.

Here comes Magist. Magist is a Brazilian Software as a Service company that offers a centralised order management system to connect small and medium-sized stores with the biggest Brazilian marketplaces. Magist is already a big player and allows small companies to benefit from its economies of scale: it has signed advantageous contracts with the marketplaces and with the Post Office, thus reducing the cost in fees and, most importantly, the bureaucracy involved to get things started. 
 
## Eniac company had two main concerns


##   --> Is Magist is a good fit for high-end tech products?
##  -->Are orders delivered on time?


## Data discovery/data cleansing


1. Follow step in this video to install mysql on your local computer
https://www.youtube.com/watch?v=WuBcTJnIuzo

2. Download `magist_dump.sql` file to your local computer and import it as per instructions given in the tutorial video

* Import the sql script in MySQL workbench 

<img src="https://github.com/Loveless1234/Magist_Analysis/blob/main/resources/images/import_sql.png" width=75% height=75%>

#### In this same manner We are going to fetch the data from the database and then we are going to transform and load the data in the Tableau to build the dashboard.

<img src="https://github.com/Loveless1234/Magist_Analysis/blob/main/resources/images/img_schema.png" width=75% height=75%>



### Primary analysis of data base by running different SQL statements

1. HOW MANY ORDERS ARE THERE IN THE DATASET?

    `SELECT 
    COUNT(*) AS orders_count
FROM
    orders;`

2.  ARE ORDERS ACTUALLY DELIVERED?

    `SELECT 
    order_status, 
    COUNT(*) AS orders
FROM
    orders
GROUP BY order_status;`

3. IS MAGIST HAVING USER GROWTH?
 
    `SELECT 
    YEAR(order_purchase_timestamp) AS year_,
    MONTH(order_purchase_timestamp) AS month_,
    COUNT(customer_id)
FROM
    orders
GROUP BY year_ , month_
ORDER BY year_ , month_;`

4.  WHICH ARE THE CATEGORIES WITH MOST PRODUCTS?

    `SELECT 
    product_category_name, 
    COUNT(DISTINCT product_id) AS n_products
FROM
    products
GROUP BY product_category_name
ORDER BY COUNT(product_id) DESC;`

5.  HOW MANY OF THOSE PRODUCTS WERE PRESENT IN ACTUAL TRANSACTIONS?

    `SELECT 
	count(DISTINCT product_id) AS n_products
FROM
	order_items;`

6.  WHAT’S THE PRICE FOR THE MOST EXPENSIVE AND CHEAPEST PRODUCTS?

    `SELECT 
    MIN(price) AS cheapest, 
    MAX(price) AS most_expensive
FROM 
	order_items;`

7. WHAT ARE THE HIGHEST AND LOWEST PAYMENT VALUES?

    `SELECT 
	MAX(payment_value) as highest,
    MIN(payment_value) as lowest
FROM
	order_payments;`

## Answering Business Questions



Based on the data from the magist database that we explored we will answer two main questions. Does magist serve as a good marketplace for high-end tech products? and Can eniac rely on a fast delivery of orders through magist.

Two big product categories tech products 20% and products related to house and furniture 26%, two other big categories health_beauty around 8,6% and sports_leisure around 7%

This is total revenue of all sellers on Magist (13 591 643) in 2 years
Compared to toal revenue of Eniac in Spain (12 268 417) in 1 year.


### What’s the average revenue of sellers that sell tech products? 
Average revenue in tech is around 710euros/month which is not much but if we consider only leading sellers (by that, we mean the ones that have more than 20 orders) we can see that average is actually much bigger, it is around 3722euros. If we get more detailed the revenues always grow after summer so if Eniac would want to enter the market September  would be the best month.

When looking into top sellers by revenue we found out that there is one seller that sells computers and telephony that stands out from the rest. It's revenue is 200k+. It is followed by 3 sellers that sell computer accessories that have revenue around 50k. Not much was found out from prices of products from those sellers because the prices vary a lot. For example the top seller sells computers from 700-1700eur and there are simillar quantities sold in each price range.

From the reviews we got some bad informations. From 16350 reviews 59% were rated 5, 20% 4, 8% 3, 3,6% 2 and 13,8% are rated 1. From those 13,8% around 2/3 are about late delivery, wrong products deliverd or damaged packaging.

ok, i also queried the delivery times again and grouped by fast delivery - 3 days, and slow delivery above 7 days, most deliveries are late - maybe we cant compare brazil to our understanding of fast delivery
changing the days to 5 and 14 also shows the majority is delivered slow


    
we are not going to sign the contract with magist due to the average time taken for delivery being too long i.e 13 days,   


 if Eniac is willing enter the brasilian market , they should improve something like   
 
 1. change the carrier by choosing another option like ups, DPD, etc 
 2. opening friendly customer service so that they can ask about the real-time delivery status.
 3. also ccollect the data of last 2-3 years and then analyze it
