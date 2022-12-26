# Analysis of Global Video Game Sales using SQL (Personal Project)

## Purpose
1) To provide an analysis of the global console video game sales since 2010
2) To serve as a platform to save and share my sql code

Table of contents
=================

* [Data Source](#Data-Source)
* [SQL Code and Analysis](#SQL-Code-and-Analysis)
  * [Sales by Regions](#Sales-by-Regions)
  * [Sales by Genre](#Sales-by-Genre)
  * [Sales by Platform](#Sales-by-Platform)
* [Conclusion and Recommendations](#Conclusions-and-Recommendations)
   
<!--te-->

## Data Source 
The dataset in the attached file "GlobalVideoGameSales.csv" contains a list of console video games with sales greater than 100,000 copies from 1980 to 2020. 
It is generated by a scrape of vgchartz.com. Data credited to Kaggle, an online community of data scientist.
The link is to the data is found at: https://www.kaggle.com/datasets/gregorut/videogamesales?resource=download

## SQL Code and Analysis

### Sales by Regions
North America (USD 1,113m / 44%) is the largest market for video game, followed by Europe (USD 839m / 33%), Japan (USD 299m / 12%) and the rest of the world (USD 270m / 11%) since 2010

<img width="698" alt="image" src="https://user-images.githubusercontent.com/121382980/209517964-2cdce15a-411d-49ad-9f1c-e94951019298.png">

```ruby
-- Identify Sales by Regions since Year 2010
SELECT 
Round(SUM(NA_Sales),0) AS North_America_Sales,
Round(SUM(EU_Sales),0) AS Europe_Sales,
Round(SUM(JP_Sales),0) AS Japan_Sales,
Round(SUM(Other_Sales),0) AS Other_Sales,
ROUND(SUM(Global_Sales),0) AS Global_Sales
FROM 
`Video_Game_Sales.Video_Game_Sales_1980_to_2020`
WHERE
CAST(Year AS INT64) >= 2010
```

<img width="748" alt="image" src="https://user-images.githubusercontent.com/121382980/209518574-93983959-e136-43ab-bc01-51e6b4c4cef2.png">

```ruby
-- Identify Sales by Regions as % since Year 2010
SELECT 
ROUND(SUM(NA_Sales)/SUM(Global_Sales)*100,0) AS North_America_Sales_Percentage,
ROUND(SUM(EU_Sales)/SUM(Global_Sales)*100,0) AS Europe_Sales_Percentage,
ROUND(SUM(JP_Sales)/SUM(Global_Sales)*100,0) AS Japan_Sales_Percentage,
ROUND(SUM(Other_Sales)/SUM(Global_Sales)*100,0) AS Other_Sales_Percentage,
ROUND(SUM(Global_Sales)/SUM(Global_Sales)*100,0) AS Global_Sales_Percentage
FROM 
`Video_Game_Sales.Video_Game_Sales_1980_to_2020`
WHERE
CAST(Year AS INT64) >= 2010
```

### Sales by Genre

The top four console gaming genres are action, shooter, sports and role-playing. 
These top four console gaming genres represent over 70% (USD 1,767m) of total console games sold since 2010

<img width="776" alt="image" src="https://user-images.githubusercontent.com/121382980/209519950-3f4181ce-decd-4f27-8025-ede59b39e0e0.png">

```ruby
-- Identify best selling game by genre since Year 2010
SELECT 
Genre,
Round(SUM(Global_Sales),0) AS Sum_of_Global_Sales
FROM 
`Video_Game_Sales.Video_Game_Sales_1980_to_2020`
WHERE
CAST(Year AS INT64) >= 2010
GROUP BY
Genre
ORDER BY
Sum_of_Global_Sales DESC
```

### Sales by Platform

The console gaming platforms are dominated by three main companies Sony (PS and PSP series), Microsoft (XBox Series), Nintendo (DS and Wii).

<img width="592" alt="image" src="https://user-images.githubusercontent.com/121382980/209521139-6d2e8caf-6035-4108-a6a2-9baaea7148ad.png">

```ruby
-- Identify best selling game by platform since Year 2010
SELECT 
Platform,
ROUND(SUM(Global_Sales)) AS Global_Sales
FROM 
`Video_Game_Sales.Video_Game_Sales_1980_to_2020`
WHERE
CAST(Year AS INT64) >= 2010
GROUP BY 
Platform
ORDER BY
Global_Sales DESC
```

## Conclusions and Recommendations

1) Largest portion of the marketing budget should be spent on North American region as this market (sales since 2010 USD 1,113m or 44% of global sales) represents the largest game console market
2) Unless a gaming company is able to carve out a niche market, the safer option is to focus effort on the devlopment of game for the top four best selling genre (i.e. action, shooter, sports and role-playing)
3) Sony, Microft and Nintendo dominate the platform for console gaming. It is extremely vital that gaming companies work closely and maintain good relationship these three companies
