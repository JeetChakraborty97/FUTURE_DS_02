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
```DAX
Engagements = [Shares] + [Clicks] + [Comments]
```
* Purchases: 708
```DAX
Purchases = COUNTROWS(FILTER(ad_events, ad_events[event_type] = "Purchase"))
```
* CTR (Click Through Rate): 11.86%
```DAX
CTR (Click Through Rate) = DIVIDE([Clicks], [Impressions], 0)
```
* Engagement Rate: 13.60%
```DAX
Engagement Rate = DIVIDE([Engagements], [Impressions], 0)
```
* Conversion Rate: 4.82%
```DAX
Conversion Rate = DIVIDE([Purchases], [Clicks], 0)
```
* Purchase Rate: 0.57%
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

## Other DAX Formulas Used for Other Measures, Calculated Columns & Tables

### 1. Select Dynamic Measure
```DAX
Select Dynamic Measure = {
    ("Impressions", NAMEOF('ad_events'[Impressions]), 0),
    ("Engagements", NAMEOF('ad_events'[Engagements]), 1),
    ("Clicks", NAMEOF('ad_events'[Clicks]), 2),
    ("Shares", NAMEOF('ad_events'[Shares]), 3),
    ("Comments", NAMEOF('ad_events'[Comments]), 4),
    ("Purchases", NAMEOF('ad_events'[Purchases]), 5)
}
```

### 2. Dynamic Title
```DAX
Dynamic Title = IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 0, "Impressions",
                IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 1, "Engagements",
                IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 2, "Clicks",
                IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 3, "Shares",
                IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 4, "Comments",
                IF('Select Dynamic Measure'[Select Dynamic Measure Order] = 5, "Purchases", "Other"
                ))))))
```

### 3. Gender Donut Chart Title
```DAX
Gender Donut Chart Title = SELECTEDVALUE('Select Dynamic Measure'[Dynamic Title]) & " by Gender"
```

### 4. Age Stacked Column Chart Title
```DAX
Age Stacked Column Chart Title = SELECTEDVALUE('Select Dynamic Measure'[Dynamic Title]) & " by Age"
```

### 5. Country Map Chart Title
```DAX
Country Map Chart Title = SELECTEDVALUE('Select Dynamic Measure'[Dynamic Title]) & " by Country"
```

### 6. Event Date
```DAX
Event Date = DATEVALUE(ad_events[timestamp])
```

### 7. Calendar Table
```DAX
Calendar Table = CALENDAR(MIN(ad_events[Event Date]), MAX(ad_events[Event Date]))
```

### 8. Month Name
```DAX
Month Name = FORMAT('Calendar Table'[Date], "mmm")
```

### 9. Day Name
```DAX
Day Name = FORMAT('Calendar Table'[Date], "ddd")
```

### 10. Day Number
```DAX
Day Number = FORMAT('Calendar Table'[Date], "d")
```

### 11. Weekday
```DAX
Weekday = WEEKDAY('Calendar Table'[Date], 2)
```

### 12. Week Number
```DAX
Week Number = WEEKNUM('Calendar Table'[Date], 2)
```

### 13. Calendar Matrix Visual Title
```DAX
Calendar Matrix Visual Title = "Analysis by Month"
```

### 14. Weekly Stacked Column Chart Title
```DAX
Weekly Stacked Column Chart Title = "Weekly " & SELECTEDVALUE('Select Dynamic Measure'[Dynamic Title]) & " Trend"
```

### 15. Event Hour
```DAX
Event Hour = HOUR(ad_events[timestamp])
```

### 16. Hourly Area Chart Title
```DAX
Hourly Area Chart Title = "Hourly " & SELECTEDVALUE('Select Dynamic Measure'[Dynamic Title]) & " Trend"
```

### 17. Calendar Matrix 2 Visual Title
```DAX
Calendar Matrix 2 Visual Title = "Analysis by Ad Type"
```

## Data Modelling

A Snowflake Schema was created where:

* Established a relationship between "campaigns" & "ads" tables with 'one to many' cardinality via "campaign_id" where the cross-filter direction is 'single'.
* Established a relationship between "ads" & "ad_events" tables with 'one to many' cardinality via "ad_id" where the cross-filter direction is 'single'.
* Established a relationship between "users" & "ad_events" tables with 'one to many' cardinality via "user_id" where the cross-filter direction is 'single'.
* Established a relationship between "Calendar Table" & "ad_events" tables with 'one to many' cardinality via "Event Date" where the cross-filter direction is 'single'.
* No physical relationship established between "Select Dynamic Measure" & other tables. Instead, it is used as a disconnected table to enable dynamic measure selection in charts, slicers and DAX logic.

## Key Insights

