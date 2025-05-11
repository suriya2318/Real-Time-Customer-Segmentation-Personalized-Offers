![image](https://github.com/user-attachments/assets/6afa3d57-49e7-41e4-87ed-2780b0cb2e09)# Real-Time Customer Segmentation & Personalized Offers Using KNIME
## Project Objective
The goal of this project is to develop a real-time customer segmentation system that helps retail businesses deliver personalized discount offers based on customer purchasing behavior, demographics, and engagement. This enables better marketing targeting, increased customer retention, and improved revenue generation.
## Problem Statement 
The retail industry is increasingly competitive, with e-commerce platforms setting high 
standards for personalized customer experiences. Traditional customer segmentation 
methods are often static and fail to capture real-time customer behavior, leading to missed 
opportunities for targeted marketing and customer engagement. 

Retailers need a solution that can: 

  • Analyze customer behavior in real-time. 
  
   • Segment customers dynamically based on their purchasing patterns and preferences. 
  
   • Deliver personalized discounts and offers to improve customer retention, conversion rates, and revenue. 

Key Challenges: 
    
  • Lack of real-time insights into customer behavior. 
  
  • Inability to deliver hyper-personalized offers. • Difficulty in competing with e-commerce giants.

## Solution 
To address these challenges, we propose a Real-Time Customer Segmentation & 
Personalized Offers solution using KNIME. This solution leverages: 
  
  • Real-Time Data Integration: Streaming POS transaction data, CRM data, and IoT data (e.g., in-store foot traffic sensors). 
  
  • Advanced Analytics: Clustering algorithms (k-means, DBSCAN) for customer segmentation. 
  
  • Machine Learning: Predictive modeling to forecast discount usage. 
  
  • Automation: Dynamic discount triggering via email or APIs. 
  
  • Real-Time Dashboards: KNIME WebPortal for monitoring customer segments and campaign performance. 

Key Benefits: 
  
  • Real-time customer insights. 
  
  • Hyper-personalized offers. 
  
  • Improved customer retention and revenue.
  
## Dataset Used

- <a href="https://github.com/suriya2318/Real-Time-Customer-Segmentation-Personalized-Offers/blob/main/Customer_segments.csv">Customer Segmendation Dataset </a>

- <a href="https://github.com/suriya2318/Real-Time-Customer-Segmentation-Personalized-Offers/blob/main/customer_transactions.csv">Customer Transactions Dataset</a>

## Working Process of Real-Time Customer Segmentation & Personalized Offers Using KNIME

The workflow is divided into the following steps: 
1. Data Ingestion 
2. Data Preprocessing 
3. Feature Engineering 
4. Customer Segmentation (Clustering) 
5. Predictive Modeling (Discount Usage Prediction) 
6. Personalized Discount Assignment 
7. Data Visualization 
8. Email Automation for Personalized Offers

### Step 1: Data Ingestion
   
  • Node Used: CSV Reader

   • Input File: customer_transactions.csv

   • Configuration:
   
   o Detect delimiter (comma ,)
   
  o Ensure correct data types (e.g., PurchaseAmount as Double, TransactionDate as Date/Time)

   • Output: A structured dataset containing customer transactions ready for 
      preprocessing.

   ![Screenshot 2025-02-17 123657](https://github.com/user-attachments/assets/6a76a8c4-bec3-4b03-a60d-6a0f303c2a36)

### Step 2: Data Preprocessing

  • Nodes Used:
   
  o Missing Value Node: Handles missing data.

   ▪ Numeric values replaced with median/mean.

   ▪ Categorical values replaced with the most frequent entry.

  o Normalizer Node: Scales numerical features (PurchaseAmount, StoreVisits) to ensure uniformity.

   • Output: A cleaned and normalized dataset ready for feature engineering. 

   ![Screenshot 2025-05-11 163519](https://github.com/user-attachments/assets/86409e5f-e600-4de7-b0a9-663075c45b3d)

### Step 3: Feature Engineering 

  • Nodes Used:  
  
  o Math Formula Node: Computes AvgSpendPerVisit = PurchaseAmount / StoreVisits.
  
  o Date&Time Difference Node: Computes Recency (days since the last purchase). 
  
  • Output: An enriched dataset with newly derived features (AvgSpendPerVisit,Recency). 
  
  ![image](https://github.com/user-attachments/assets/8e1dbd58-fc0d-473c-9494-4f10b2e66c10)


  ### Step 4: Customer Segmentation (Clustering) 

  • Nodes Used:  
  
  o k-Means Clustering: Identifies distinct customer groups by analyzing behavioral features.
  
  o DBSCAN: Used for density-based clustering to detect noise and anomalies. 
  
  • Features Used:
  
  o PurchaseAmount 
  
  o StoreVisits 
  
  o AvgSpendPerVisit 
  
  o Recency 
  
  • Configuration:  
  
  o k-Means: Optimal k determined using the Elbow Method. 
  
  o DBSCAN: Defined epsilon and min points for density estimation. 
  
  • Output: Segmented customer groups such as High-Value Customers, Frequent Buyers, At-Risk Customers, and One-Time Buyers.
  
  ![image](https://github.com/user-attachments/assets/0a01beb5-3bc0-4c93-8b7f-daa494edc742)


  ### Step 5: Predictive Modeling (Discount Usage Prediction) 
  
  • Nodes Used:  
  
  o Partitioning Node: Splits data (80% training, 20% testing). 
  
  o Random Forest Learner / Decision Tree Learner: Trains models on past customer behaviors. 
  
  o Predictor Node: Applies trained models to predict discount usage likelihood. 
  
  o Scorer Node: Evaluates model accuracy using metrics like precision and recall. 
  
  • Target Variable: DiscountUsed (Yes/No) 
  
  • Features Used:  
  
  o Purchase behavior 
  
  o Customer demographics 
  
  o Cluster label from segmentation step 
  
  • Output: Predicted probability of discount redemption for each customer.
  
  ![image](https://github.com/user-attachments/assets/65a5e429-7520-4053-b0cd-161f0bbef8c5)


  ### Step 6: Personalized Discount Assignment 
  
  • Nodes Used:  
  
  o Rule Engine Node: Assigns discount categories based on customer segmentation and predicted discount usage. 
  
  • Example Rules:  
  
  o $Prediction(Cluster)$ = "cluster_0" => "High-Value" 
  
  o $Prediction(Cluster)$ = "cluster_1" => "Frequent Buyer" 
  
  o $Prediction(Cluster)$ = "cluster_2" => "At-Risk" 
  
  • Discount Rules:  
  
  o $Customer Segment$ = "High-Value" => "10% Off" 
  
  o $Customer Segment$ = "Frequent Buyer" => "Special Offer" 
  
  o $Customer Segment$ = "At-Risk" => "Retention Deal" 
  
  o $Customer Segment$ = "One-Time Buyer" => "Welcome Back" 
  
  • Output: Discount offers tailored to individual customer profiles.
  
  ![image](https://github.com/user-attachments/assets/80bb0075-8935-46a1-a1d4-238d18a7a3aa)


  ### Step 7: Data Visualization 
 
  • Nodes Used:  
  
  o Bar Chart / Pie Chart: Displays customer segment distribution. 
  
  o Stacked Bar Chart: Shows discount redemption rates across segments. 
  o Box Plot: Illustrates spending behavior variations. 
  o Heatmap: Visualizes revenue contributions by customer segment. 
  
  • Insights:  
  
  o Identify high-value segments. 
  
  o Evaluate discount effectiveness. 
  
  o Analyze customer spending trends. 

  ### Step 8: Email Automation for Personalized Offers 
  
  • Nodes Used:  
  
  o Row Filter Node: Selects customers based on criteria (e.g., email ID, purchase history). 
  
  o Rule Engine Node: Assigns personalized discount codes. 
  
  o Send Email Node: Sends tailored emails via SMTP configuration. 
  
  • Example Email Template:  
  
  • Subject: "Exclusive Discount Just for You!" 
  
  • Message: 
  
  Dear Customer, 
  
  We noticed you love shopping with us! Here's your special offer: 
  
  $Discount_Message$ 
  
  Enjoy your shopping! 
  
  Regards,   
  
  QUANTUM MULTIPOINTS 
  
  • Output: Automated email campaigns delivering personalized promotions.
  
  ![image](https://github.com/user-attachments/assets/828b03fb-2de9-4848-9bd5-c1d22e425aa5)


## 4. Final Workflow & Output 

The final output of the project includes: 

### 1. Real-Time Customer Segments: 

  o High-Value Customers → Spend frequently, get a 10% discount. 
  
  o Frequent Buyers → Visit often but spend moderately, get a special offer. 
  
  o At-Risk Customers → Haven't purchased recently, get a retention discount. 
  
  o One-Time Buyers → Low engagement, receive a welcome back offer.

  Output:
  
  ![image](https://github.com/user-attachments/assets/91d71761-fcc2-4d60-a6c5-57dfa5b9a061)


### 2. Personalized Discount Offers: 

  Predictions for Discount Usage (Based on Decision Tree/Random Forest Model) 
  
  o Customers likely to use discounts → More aggressive promotions. 
  
  o Customers unlikely to use discounts → Adjust strategy to increase engagement. 
  
  Output:
  
  ![image](https://github.com/user-attachments/assets/76428bc2-0148-4242-87fc-9df42e416ade)


### 3. Real-Time Dashboards: 

  o Customer segment distribution. 
  
  o Discount redemption rates. 
  
  o Revenue impact of personalized campaigns. 
  
  #### • Bar Chart / Pie Chart: Displays customer segment distribution. 
  
  ![image](https://github.com/user-attachments/assets/70cda3f4-bfe4-4ad0-a2e5-1d9b954f933b)
  
  ![image](https://github.com/user-attachments/assets/29d00e7f-90e8-4fda-8b70-e2454336d4d5)
  
  #### • Stacked Bar Chart: Shows discount redemption rates across segments.
  
  ![image](https://github.com/user-attachments/assets/e6fef1bc-956e-4b41-917d-bd303fb064c0)
  
  #### • Box Plot: Illustrates spending behavior variations.
  
  ![image](https://github.com/user-attachments/assets/c7b8a269-538a-4736-8cf6-24e69cc05c92)
  
  #### • Heatmap: Visualizes Category by customer segment.
  
  ![image](https://github.com/user-attachments/assets/caa584d7-7a5a-49a4-adbe-f47895b799ea)
  
  #### • Table View: Live updates of customer transactions and segmentation.
  
  ![image](https://github.com/user-attachments/assets/ea162146-8b0b-4239-91df-7f0362426f42)

## 4. Business Impact: 

  o Increased customer retention and loyalty. 
  
  o Higher conversion rates due to targeted offers. 
  
  o Improved revenue from upselling and cross-selling.
  
### Final Report:

- <a href="https://github.com/suriya2318/Real-Time-Customer-Segmentation-Personalized-Offers/blob/main/Real-Time%20Customer%20Segmentation%20%26%20Personalized%20Offers%20Project_Report.pdf"> Final Project Report</a>

### Final Workflow:
  
  ![image](https://github.com/user-attachments/assets/2100ad67-eb5e-411f-9d80-885aadfd6744)

## Final Conclusion

The KNIME-based real-time customer segmentation system offers a powerful tool for personalized marketing. It leverages customer data and predictive analytics to generate dynamic, tailored discount offers that improve engagement and drive business growth. This workflow provides an end-to-end solution, from data collection to customer communication, enhancing the retailer’s ability to compete in a data-driven market.
