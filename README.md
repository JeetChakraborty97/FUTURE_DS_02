# FUTURE_DS_02
Repository for Task 2 of the Data Science &amp; Analytics Internship at Future Interns
# Meta Ads Performance (Facebook & Instagram) Dashboard

<img width="1412" height="810" alt="Dashboard 1 SS" src="https://github.com/user-attachments/assets/3b1b98a7-561c-4540-8df6-8cbb5ca83966" />

<img width="1408" height="807" alt="Dashboard 2 SS" src="https://github.com/user-attachments/assets/3026a265-8f88-477d-aa60-f34b96f0579b" />

# Overview

## Business Objective

The objective of this analysis was to evaluate the performance of advertising campaigns across Meta platforms (Facebook & Instagram). The dashboards were designed to help stakeholders measure user engagement, identify the most responsive audience groups, analyze geographic reach, and understand which ad formats and timeframes contribute most to awareness and conversion. The insights aim to guide future budget allocation, audience targeting, and campaign strategy to maximize return on advertising spend.

## Data Overview

The analysis is based on campaign-level and event-level Meta ad performance data from the month of May to the month of August. The datasets include:

* Impressions, clicks, shares, comments, purchases, and engagement actions.
* Ad types, campaign details, and budget allocation.
* User demographics such as age, gender, and country.
* Time granularity for hourly and weekly trend analysis.

The data was integrated, cleaned, and transformed to support accurate performance measurement and platform-specific insights.

## Tools Used

* Microsoft Excel: Data Source.
* Microsoft Power BI: Data Cleaning, Transformation & Visualisation.

## Key Performance Indicators (KPIs) & DAX Formulas Used for Each

Separate dashboards were created for Facebook and Instagram to analyze each platform individually.

### Facebook KPIs

* Impressions: 216K
```DAX
Impressions = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Impression"))
```
* Clicks: 25.4K
```DAX
Clicks = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Click"))
```
* Shares: 1.3K
```DAX
Shares = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Share"))
```
* Comments: 2.6K
```DAX
Comments = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Comment"))
```
* Engagements: 29.3K
```DAX
Engagements = [Shares] + [Clicks] + [Comments]
```
* Purchases: 1.3K
```DAX
Purchases = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Purchase"))
```
* CTR (Click-Through Rate): 11.76%
```DAX
CTR (Click Through Rate) = DIVIDE([Clicks], [Impressions], 0)
```
* Engagement Rate: 13.56%
```DAX
Engagement Rate = DIVIDE([Engagements], [Impressions], 0)
```
* Conversion Rate (CR): 5.21%
```DAX
Conversion Rate = DIVIDE([Purchases], [Clicks], 0)
```
* Purchase Rate: 0.61%
```DAX
Purchase Rate = DIVIDE([Purchases], [Impressions], 0)
```
* Total Budget: $ 2,535.9K
```DAX
Total Budget = SUM(campaigns[total_budget])
```
* Avg. Budget/Campaign: $ 50.7K
```DAX
Avg. Budget per Campaign = AVERAGE(campaigns[total_budget])
```

### Instagram KPIs

* Impressions: 123.8K
```DAX
Impressions = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Impression"))
```
* Clicks: 14.7K
```DAX
Clicks = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Click"))
```
* Shares: 682
```DAX
Shares = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Share"))
```
* Comments: 1.5K
```DAX
Comments = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Comment"))
```
* Engagements: 16.8K
* Purchases: 708
* CTR (Click Through Rate): 11.86%
* Engagement Rate: 13.60%
* Conversion Rate: 4.82%
* Purchase Rate: 0.57%
* Total Budget: $ 2,535.9K
* Avg. Budget/Campaign: $ 50.7K
