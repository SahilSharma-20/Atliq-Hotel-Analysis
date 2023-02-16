# Atliq-Hotel-Analysis

AtliQ Grands is a well-established hospitality company that owns multiple five-star hotels across India. The company has been in the industry for the past 20 years and is known for its luxury and business hotels.

## Problems we are trying to Solve

In recent times, AtliQ Grands has faced a decline in its market share and revenue due to strategic moves from competitors and ineffective decision-making in management. To tackle this issue, the managing director of AtliQ Grands has decided to incorporate "Business and Data Intelligence" to regain its market share and revenue. However, the company does not have an in-house data analytics team to provide insights from its historical data.

## Main Goal

Their revenue management team had decided to hire a 3rd party service provider to provide them with insights from their historical data.

# Business Requirement Document and Data Gathering

The input file given to us contains all the meta information regarding the columns described in the CSV files. we have provided 5 CSV files:

1) dim_date.
2) dim_hotels.
3) dim_rooms.
4) fact_aggregated_bookings.
5) fact_bookings.
To know more about Table details. Kindly visit to meta_data_hospitality.txt

# Mockup and solution design Metrics


So, our goal is to make similar kind of dashboard.

## Important Business Jargons / key metrics
### RevPar( Revenue Per Available room ) : To get Revpar : the formula is : Total Revenue / Total Rooms Available to sell. Another formula is : ADR x Occupancy
Occupancy formula is : Total Rooms Occupied / Total Rooms Available Example : As number of rooms sold or utilized by the customers divided by number of available rooms so say you have a 100 room Hotel on Monday you had 50 customers check out so for your occupancy for Sunday would be 50 50 rooms sold divided by 100 available right that is as simple as that.

### ADR (Average Daily Rate) : To get ADR : the formula is:
Total Rooms Renveue / Number of Rooms sold.

This metric is basically the rooms you sold what is the average rate you sold in them simple so if you sold 50 rooms and each room was worth thousand rupees your average daily rate is thousand period.

Note : If your occupancy is 100 your ADR and RevPar will always be equal.

Total Available rooms in hospitality domain are SRN (Sellable Room night) or DSRN(Daily Sellable Room Night). This is another metric that would be very helpful to look at this would help us look at any specific issues room blocking issues maintenance issues in the future.
For example right so let's assume another example of 100 room hotel and let's assume there is no issue in the hotel it's a fantastic Hotel everything is maintained perfectly so every day you have 100 Rooms to sell correct so if you say June has 30 days that means every day you have 100 Rooms to sell so for the entire month you had three thousand rooms to sell correct 30 into 100 that is 3000 rooms to sell so that would be the sellable room nights for June and if you want to look at the dairy level you would divide it by 30 and that number would be 100 so that would be DSR end in that case these are daily sellable room lights okay which one would be more beneficial for you to look at DSR and or srn I would like to look at DSR in this current view that would be really helpful.

So, Our Key metrics are :

RevPar.
Occupancy.
DSRN.
Revenue.
ADR
To get Realization we have two new matrics :

### URN (Utlized Room Nights) : For example if you have a hundred room hotel and 100 available rooms and on say Sunday 50 rooms were booked and customer stayed so those would be the 50 URLs or 50 utilized room lights so when the customer ends up staying at your hotel we treat it as a utilized roadmap

### BRN (Booked Room Night) :for example you have a 100 room Hotel 60 customers made bookings all right and 50 ended up staying so there is a gap of 10. these 10 would either be cancellations because customers do have the right to cancel right yes and the second split is generally called no shows they are very common in our industry wherein a customer does make a booking but it doesn't end up staying right due to any reason we could have multiple reservations with different hotels just plans could change you could not cancel in time so basically books booked room nights contains utilized room lights no shows and cancellations


### To get Realization the formula is : URN/BRN we want to see against the bookings we received how many customers actually stayed because that is the revenue realization percentage kind of helps you understand uh you know what is the actual Revenue you know that you have realized from the bookings because cancellations happen and uh yes a lot of other things happen great all

### Point to be noted: Weekends in hospitility domain are friday and saturday and sunday to thurday are weekdays

Thing to include in dashboard : Channel level split which channels the booking comes from if there is a channel level issue we can identify it only looking at that data so if you have that that is going to be fantastic very very helpful right we can add that and folks we have been using level one level.

### Types of level in dashboard designing :

### Level one Analysis : Level one Analysis to know uh where the water is leaking right you just you just look at the level one right and uh so level one metrics are kind of tell you there is a problem or not so when there is no problem you don't have to look at level two and there is a problem so then you have to look it's

### Level two Analysis : Level two Analysis is when you problems and try to identified it : like you know peeling an onion so you you look at the onion at some part it is having a problem then you peel it to the next level you know where exactly the onion is bad so you just fix only that part you don't have to put the throw the entire onion out of the you know to the basket and and the level two metrics is where you know like you understand okay which process is having a problem or which channel is having a problem or which city is having a problem let's say your revenue is so bad and only one city is causing that so you can fix only that City so you can talk to that particular city manager so that's level two So

# Data Transformation and Data Modeling

## Data Loading and Power Query Documentation

Create a folder in Desktop and store all the csv files related to hospitality challenge.

Open a Power BI file, and In "Get Data", select the option as folder and browse through the folder containing csv files.

Then go to Tranform data to expand each and every dataset.

Now, duplicate the data source 4 times and in each one, expand one dataset by clicking on "Binary" option. also, rename the tables accordingly.

## Power Query steps for tables:

dim_date:

remove the column 'day_type'
we are deleting this because, we got a feedback from the mock dashboard review that Friday and Saturday are
considered as weekends in the industry and not sunday. But In our datasets, saturday and sunday are considered
as weekends. So we delete this column and re-create day_type using calculated columns.
dim_rooms

The column names are not captured here. We need to select "Use First Row as Headers" option .
Data Modeling



# Building DAX

## Calculated Column

Our first Calculated column is to get number from week_no column of dim_date into week_number and the formula is :
week_number = WEEKNUM(dim_date[date])

Our Second Calculated column to get day_type from dim_date table. So, as we know in hospitality domain weekdays are Sunday to Thursday and weekends are Friday and Saturday. So, the formula to get day_type is : day_type =
var wkd = WEEKDAY(dim_date[date])
return if(wkd>5,"Weekend","Weekday")

## Measures

### Revenue : To get the total revenue_realized : formula : Revenue = SUM(fact_bookings[revenue_realized]) : and the table is fact_bookings.

### Total Bookings : To get the total number of bookings happened: Formula : Total Bookings = COUNT(fact_bookings[booking_id]): and the table is fact_bookings.

As, there are 26 measures. To check the detail of all measures visit metrics_list.xlxs

## Dashboarding and insight Generation

Dashboard Design




Dashboard Insights

Mumbai generates the highest revenue (669 M) followed by Bangalore, Hyderabad and Delhi.
AtliQ Exotica performs better compared to all 7 type of properties with 320 Million revenue, rating 3.62, occupancy percentage 57 and cancellation rate as 24.4%.
AtliQ Bay has the highest occupancy of 66%.
Week 24 recorded the highest revenue among all, which is 139.6 Million.
Delhi tops both in occupancy and rating followed by Hyderabad, Mumbai, Bangalore.
AtliQ lost around 298 Million in cancellation.
Elite type rooms has the most booking and as well higher cancellation rate.

