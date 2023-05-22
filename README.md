# Airbnb Data Analysis - Dublin

The dashboard “Airbnb Data Analysis – Dublin” is designed for individual property investors, as well as landlords, who want to analyze the Dublin Airbnb data, and hence, decide on whether to invest in buying a new property in Dublin and if so where and what kind of property to purchase. Also, the dashboard facilitates decision-making on the marketing strategy of the listings (e.g., naming, pricing, the minimum number of nights to let, etc.). This is an exploratory dashboard, which enables users to explore Airbnb data in an interactive and visual way. It also enables users to identify patterns and trends quickly and effectively. Thus, the user’s role with this dashboard is to explore and analyze the data to drive insights using various filtering and other interactive elements that the dashboard presents. Possible use case scenarios for this dashboard are indicated later in this report.

The KPIs that this dashboard presents are as follows:
* Occupancy rate - Percentage of booked nights for a listing in a given year, calculated as:
Booked nights per listing in a year/365 * 100

* Revenue per listing – The revenue made per listing in a given year, calculated as:
Booked nights per listing in a year * Price per listing

* Price – The average price of a listing per night;
* Number of listings – The number of listings in Dublin or a given neighborhood;
* Room Type – The type of the listing (e.g., Entire home/apartment, private room, shared room, or hotel room);
* Minimum nights required – The minimum nights required to be able to make a booking for each listing;
* Hosts by listing count – The number of listings each host has on the Airbnb website.

For this dashboard, I used listings.csv and calendar.csv files for Dublin, retrieved from http://insideairbnb.com/get-the-data/. Some of the data-cleaning steps include the following:
* I changed the name of the “id” column to “listing_id” in the listings.csv document so that it corresponds to the same column in the calendar.csv file.
* I deleted the minimum_nights, price, and adjusted_price columns in the calendar.csv file, in order to decrease the load of the file  (hence increase the speed of the Tableau dashboard) and to avoid duplication.
* I created a new column in the listings.csv file named “listings_per_host”. The formula used for the data in this column is as follows: =IF(N2<10, N2, "10") – here, N2 refers to the data in the “calculated_host_listings_count” column. The purpose behind this is to easily create a histogram, which has hosts that have more than 10 listings grouped into one bin. 
* I also created a new column in the listings.csv file named minimum_nights_per_listing. The formula used for the data in this column is as follows: =IF(J2<35, J2, "35") – here, J2 refers to the data in the “minimum_nights” column. The purpose behind this is to easily create a histogram, which has listings that have more than 35 as minimum required nights grouped into one bin.
* I checked for the nulls in the data in both files. I only came across null values in only last_review column. I decided to keep rows with these values since they might indicate that a property has recently been listed on the Airbnb website, and there is no reason to remove it from the analysis.  
* I named the cleaned and edited new CSV files as listings-edited.csv and calendar-edited.csv respectively.

Then, I added listings.csv and calendar.csv files to Tableau and joined them using Many to Many connection, where the related field is listing_id. To demonstrate some of the KPIs I have previously identified, I had to create some calculated fields in Tableau. They are as follows:
* Occupancy rate: (365 - [Availability 365])/365*100
* Revenue per listing: (365 - [Availability 365])*[Price]

In order to keep the dashboard as simple as possible, I decided to design it in a minimalistic way, with no background color or borders. However, to keep the dashboard visually consistent with Airbnb brand colors, I used the heading and one of the neighborhood colors in the map in Airbnb’s red color. I also added the brand logo to facilitate this association. The dashboard is designed to easily communicate relevant data to users and allow them to explore data on their own. Therefore, the most important metrics are placed on the top of the dashboard, while details are on the mid and bottom sections.

On the top side of the dashboard, I included a summary of the main KPIs, namely the average price per listing, average occupancy rate, average annual revenue per listing, and the number of listings. I made use of borders only in the summary part, to keep it separated from the rest of the dashboard and to ease the readability. There are 2 filters on the dashboard: one is based on Neighborhoods, and the other is based on Room Type. If any of the filters are activated, all the data in the dashboard will be automatically updated (including KPI summaries, the map, and tables). Both of the filters can be utilized simultaneously, or separately. 

On the left side, I included a map that shows the location of all the listings. They are differentiated by colors based on the neighborhoods, thus there are 4 colors on the map representing different neighborhoods: Dn Laoghaire-Rathdown, Dublin City, Fingal, and South Dublin. The legend for the map is located at the top right corner of the dashboard. 

By clicking on each of the dots (which represents individual listings), the users can see the following details about each listing: 
* Name
* Room Type
* Occupancy Rate
* Price
* Revenue per listing
* Minimum nights
* Number of reviews (in the past 12 months)

With the use of filters, users can see relevant data in the neighborhood and/or the room type of their choice, which provides valuable insights regarding the pricing, naming, type of property, etc. 

In addition, with the help of the “Room Type” bar chart, users can see the number of listings per room type, which can be very beneficial, especially with the neighborhood filter. Moreover, the number of listings per minimum night required bar chart is created with the help of bins, each with a size of 5, except for the last bin, which indicates the total number of listings with a minimum night requirement of at least 36. This bar chart can provide useful insights for hosts deciding on the minimum number of days they should let their property. By clicking on each bin, users can see the exact number of listings per bin. And finally, the Number of Hosts by Listing Count bar chart presents information about the number of hosts with the relevant number of listings. This bar chart was also created with the help of bins, each with a size of 1, except for the last one “10+”, which indicates the number of hosts with more than 10 listings. By clicking on each bin, users can see the number of hosts per number of listings they have. This table helps identify the competitors in the market.

### Potential use scenario #1:
If a host has private rooms to let in the Fingal area, they can select relevant filters to see only the similar listings in the area of interest. By doing so, they can learn about the average price, occupancy rate, annual revenue for this type of listing in Fingal, and the total number of private rooms in this neighborhood. They can then go to the map to see some of the names other hosts use to market their listings and see where the listings are primarily located. They can, then, move to the second table, and see how many minimum days hosts require to let their properties, which can help to identify their own listing strategy. And finally, with the last table, the users are able to see how many similar listings other hosts (i.e. their competitors) have in that region, which can help to identify potential investment areas. 

### Potential use scenario #2:
If a property investor is trying to decide where to buy a property to further let in Airbnb, they can do this by selecting different Neighborhood filters and analyzing each. By doing so, they will be able to identify the neighborhoods with maximum and minimum occupancy rates, profitability, and the number of listings in each neighborhood. Also, with the use of the number of hosts by listing count, investors can identify the market leaders, and hence, determine their own market entrance strategy. 

#### Screeshot of the dashboard:
![Screenshot of the dashboard](https://github.com/parvinnabili/Project4/blob/7d7d0f32b80725cbda19e5fb57508e91d5eba86f/Dashboard%20screenshot.png)
