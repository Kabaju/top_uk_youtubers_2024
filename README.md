# Data Portfolio: Excel to Power BI

This is my portfolio website!

![First Image](assets/images/youtube_logo.png)

# Table of Contents

- [Heading 1](#First Header)
  - [Subheading_1](##First Subheader)

😁😁



# First Header
This is just me testing out all the stuff basically


## First Subheader

###### Smallest Header Possible

# Cleaning the data in SQL
'''sql
/*
STEPS 

1. Define the variables
2. Create a CTE that rounds the average views per video
3. Select the columns necessary for our analysis
4. Filter the results by the YouTube channels with the highest subscriber bases
5. Order by net profit (from highest to lowest)


*/


-- Step 1
DECLARE @conversionRate FLOAT = 0.02;		-- The conversion rate of 2%
DECLARE @productCost MONEY = 5.0;			--The product cost of $5
DECLARE @campaignCost MONEY = 50000.0;	-- The campaign cost of $ 50,000

-- Step 2
WITH ChannelData AS (
	SELECT
		channel_name,
		total_views,
		total_videos
		/*
		ROUND(CAST(total_views AS FLOAT)/total_videos,-4) AS rounded_avg_views_per_video,
		ROUND(CAST(total_views AS FLOAT)/total_videos *@conversionRate,-2) AS rounded_potential_sales_per_video,
		ROUND(CAST(total_views AS FLOAT)/total_videos * @conversionRate * @productCost,-3) AS rounded_potential_revenue_per_video,
		ROUND(CAST(total_views AS FLOAT)/total_videos * @conversionRate * @productCost - @campaignCost,-3) AS rounded_net_profit_per_video
		*/
	FROM
		dbo.view_uk_youtubers_2024
)

-- Step 3

SELECT
	channel_name,
	total_views,
	total_videos,
	ROUND(CAST(total_views AS FLOAT)/total_videos,-4) AS avg_views_per_video,
	ROUND(CAST(total_views AS FLOAT)/total_videos * @conversionRate,-2) AS potential_sales_per_video,
	ROUND(total_views/total_videos * @conversionRate * @productCost,-3) AS potential_revenue_per_video,
	ROUND(total_views/total_videos * @conversionRate * @productCost - @campaignCost,-3) AS net_profit
FROM 
	ChannelData
WHERE
	channel_name 
	IN
		('24 News HD','Sky News','BBC News ????' )
ORDER BY
	total_videos DESC
'''
