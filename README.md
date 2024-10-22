# Project Background
## Project Objective
**Olist, a Brazilian e-commerce marketplace platform,** plays as an intermediary connecting Sellers and Buyers across Brazil. Sellers list their products and services, while Buyers browse the lists and conveniently purchase online via Olist's website and mobile app; and data of these activities are recorded.

This project thoroughly **analyzes these datasets to figure out critical insights** and **propose some recommendations to improve Olist's business operation**, specifically on topic of **Shipment Analysis**, which is analysis on quality of delivery systems.

## Key Metrics 
Focusing on quality of delivery system, I propose some **Key Metrics** acting as a back-bone for my analysis
- **Number of Late Orders**: Number of Orders having the *Actual delivery time* after the *Estimated delivery time*
- **Late Orders Rate**: Number of Late Orders divided by Number of Total Orders
- **Delivery Time**: The whole process starting from Orders purchased by Customers to Orders shipped to Customers
	- **Order Processing Time**: Time starts from Orders purchased by Customer to Orders being approved by Olist’s systemD
	- **Picking Time**: Time starts from Orders being approved to Orders being picked up by Carriers
	- **Shipping Time**: Time starts from Orders being picked up by Carriers to Orders shipped to Customers
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Delivery%20Process" alt="description">
</p>

## Project Tools
With the purpose of **wrangling data and visualizing data** in a dashboard for performance evaluation, **Power BI** is the most suited tool for this whole process. [**Power Query Editor and M language**](https://en.wikipedia.org/wiki/Power_Query), which are languages available in **Power BI**, are used for wrangling and analyzing data, while I can also form data model and utilize Power BI features ([DAX language](https://en.wikipedia.org/wiki/Data_Analysis_Expressions), drag & drop interactions …) for accomplishing overview dashboards

*A Power BI Desktop file is built to monitor Olist's performance. Detailly, I also utilize it for Data Modeling and Data Cleaning (using Data Query Editor).
The file can be downloaded [here](https://drive.google.com/file/d/1u1BTDwYSm05WXSu7CleDgqP8AiVX4PlO/view?usp=share_link)*

# Data Structure & Initial Checks
[Olist's Dataset](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) was published in Kaggle stored in 8 tables. It contains information of 100k orders from 2016 to 2018 made at multiple marketplaces in Brazil and allows viewing orders from multiple dimensions:
- Orders dimension (order status, price, payment, and freight value) 
- Customers/Sellers dimension (location) 
- Product dimension (category, size, weight …), 
- Reviews dimension written by customers (rating, review …)
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Olist%20Dataset%20-%20ERD" alt="description">
</p>

<details>
  <summary>Click to expand -- Details on tables on columns meaning explanation</summary>
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Olist%20Dataset%20-%20Columns%20explanation" alt="description">
</p>
</details>

# Executive Summary
## Overview of Findings --- Shipment Quality
With the exponential growth of business within the period available in the dataset, Total Sales and Total Orders of Olist increased significantly during the 3-year-period from only $41.2 in Sep 2016 to $858.2K in Aug 2018, with its peak was $1,031K in Nov 2017.
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Overview%20(1)" alt="description">
</p>

However, together with Olist’s steep growth was **the emergence of the number of Late Orders**, which were orders shipped to customers later than Expected Delivery Date. This number accounted for **8.2% of Total Orders** and seemed to **reach their spikes during the period of Total Orders reaching its peak, from the end of 2017 to the first 3 months of 2018.**
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Overview%20(2)" alt="description">
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Overview%20(3)" alt="description">
</p>

Consequently, while the average rating of On-time Orders was **4.3**, this number of Late Orders **fell to 2.6** and had **46.9% of Orders getting rating 1.**

<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Overview%20(4)" alt="description">
</p>

## Insight Deep-dive
1. **Key Metric**: Number of Late Orders and Late Orders Rate
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric1%20(1)" alt="description">
</p>

Among **7.8K Late Orders in 3 years**, orders of Sellers from Sao Paulo had the highest number in contribution. This is understandable as Total Orders in Sao Paulo accounted for more than 70% orders in the dataset, so that there was no problem if the Late Order Rate in Sao Paulo is not higher than average. **Hence, it’s much better to look at both 2 metrics: number of Late Orders and Late Orders Rate, instead of just only one of them.**

From now on, I will choose to visualize Late Orders Rate by different dimensions, and simultaneously sort different categorical values of each dimension in descending order.

<p align="center">
<img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric1%20(2)" alt="description">
</p>

Sao Paulo with **its highest contribution of Late Orders**, also had the **Late Orders Rate higher than average** which is a huge problem that Olist should pay attention to *(I will prioritize this state first as the contribution of other states in terms of Late Orders are not high).*

As a Business Data Analyst, I should have some answers for managers about **What were the reasons causing this abnormal pattern in Sao Paulo?**

My whole thinking process to cope with this question is:
- Understand domain knowledge through cross-functional team and online resources
- Propose hypotheses about the root cause the problem using domain knowledge
- Quantify the hypotheses by data
- Accept or reject the hypotheses

Based on some online research about e-commerce delivery process, here are some of my hypotheses for this problem:
-   (1) The shipping distance from Sao Paulo to customer’s location was far
-   (2) The exponential growth of Total Orders in Sao Paulo caused overloaded to Olist’s shipment system

(1) Looking at the Shipping Roads that were **in top contribution of Late Orders** and **had Late Orders Rate higher than average**, the roads were almost from Sao Paulo to nearby states (picture below). So, **hypothesis (1) is rejected.**

<p align="center">
<img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric1%20(3)" alt="description">
</p>

(2) Considering the Growth Rate of Total Orders and Late Orders Rate in Sao Paulo in picture below, **only the significant growth in November 2017** went together with a significant increase in Late Orders Rate; **while the other months highlighted did not show the same trends**. So, **hypothesis (2) is also rejected.**

<p align="center">
<img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric1%20(4)" alt="description">
</p>

With **more dataset relating to Olist’s Delivery process in real life**, I will continue with this thinking process together with domain knowledge to figure out the root cause and end up with a recommendation for my managers.

2. **Key Metric**: Delivery Time
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Delivery%20Process" alt="description">
</p>

From the 2 graphs below which calculate and visualize Delivery Process, I can say that:
- **The Order Processing Time** of Olist’s system was not taken so long, and **it did not show big difference between Late Orders and On-time Orders**
- **Picking Time and Shipping Time** were 2 stages taking much more time and these 2 stages **take two-fold or threefold time longer** comparing Late Orders and On-time Orders

These 2 stages are what I should focus on.

<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric2%20(1)" alt="description">
</p>

Here are some hypotheses relating to time extension of Late Orders, comparing to On-time Orders:
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric2%20(2)" alt="description">
</p>

*( * ) Metric **Pick-up Frequency Rate**, which is calculated by dividing “Number of Days Carriers pick-up orders” by “Number of Days Sellers having Orders”, shows How often Carriers pick-up Orders when Sellers have Orders within a specific period. If the number is low, meaning that Carriers do not usually come over to pick-up orders.*

<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Analysis%20-%20KeyMetric2%20(3)" alt="description">
</p>

However, there is not a big difference between Pick-up Frequency Rate between Late Orders and On-time Orders. **The hypothesis is rejected.**

There are many other hypotheses relating to the Deliver Process that need to be considered, but there is a limit in the dataset to prove them. However, with my real-life experience working in a Business Data Analyst role, I propose some next actions to deep dive into the problems, understand the root cause and give solutions for business improvement.

# Conclusion
With all the problems discovered through the analysis process, here is the table that summary the information and next actions:
<p align="center">
  <img src="https://github.com/phungg164/Olist_Brazilian_Ecommerce_Dataset/blob/main/images/Conclusion" alt="description">
</p>
