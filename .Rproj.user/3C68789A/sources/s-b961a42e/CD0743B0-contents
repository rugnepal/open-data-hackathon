# Australia Fires

This week's data is all about Australia, including it's climate over time and recent fires. A good article currently is from the [New York Times](https://www.nytimes.com/interactive/2020/01/02/climate/australia-fires-map.html). The BBC also has an [article](https://www.bbc.com/news/world-australia-50951043) with maps and news, but I am not 100% convinced their use of scale for fire points is 100% appropriate. It is using the NASA FIRMS data.

A group of `#rstats` contributors have put together a list of resources for community help for those affected, please take a look at it [here](https://github.com/AusNZOpenRes/AusFires).

## Fire Data

This is an ongoing situation, and the goal of sharing data here is to spread awareness of the Australian fires. PLEASE be cautious when plotting maps of ongoing fires - there are many considerations when using the NASA "Active Fires Dataset" via FIRMS - potential pitfalls are outlined [here](https://mobile.twitter.com/maartenzam/status/1214150089117224960?s=12) and at the source from [NASA](https://earthdata.nasa.gov/earth-observation-data/near-real-time/firms/active-fire-data). It is nuanced in interpretation and plotting (1 km estimations). There is a very long [user guide](http://modis-fire.umd.edu/files/MODIS_C6_Fire_User_Guide_A.pdf) if you want to look further. It is apparently suggested to use nighttime data for most accuracy, but I have never used this data before.

A live update of the fires from NASA can be seen [here](https://firms.modaps.eosdis.nasa.gov/map/#z:6;c:146.8,-32.3;t:adv-points;d:2019-12-29..2020-01-05;l:firms_viirs,firms_modis_a,firms_modis_t)

A safer dataset to use is from the New South Wales Rural Fire Service - this JSON file can be rapidly turned into a map, courtesy of [Dean Marchiori](https://twitter.com/deanmarchiori/status/1212899902465822720).

`url <- "http://www.rfs.nsw.gov.au/feeds/majorIncidents.json"` contains the newest updated data, I downloaded it for today (2020-01-06).

I also found some [The Guardian](https://github.com/guardian/aus-fires-maps-2019/tree/master/processing) fire data, but it has not been updated. Some shapefiles/json/geojson though.

### Climate Data

[Nicholas Tierney](https://twitter.com/nj_tierney) has a good overview of plotting Australian climate data on [GitHub](https://github.com/njtierney/ozviridis). THe original heatmap is [here](http://www.bom.gov.au/jsp/awap/temp/index.jsp).

The overall climate of Australia can be found on [Wikipedia](https://en.wikipedia.org/wiki/Climate_of_Australia). The list of cities by population is [here](https://en.wikipedia.org/wiki/List_of_cities_in_Australia_by_population).

For climate data, temperature and rainfall was gathered from the Australian [Bureau of Meterology (BoM)](http://www.bom.gov.au/?ref=logo). A number of weather stations were chosen, based on their proximity to major Australian cities such as Sydney, Perth, Brisbane, Canberra, and Adelaide. The South East region of Australia appears to be the most affected.

Rainfall data was sourced from:  
[Subiaco](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=009151&p_startYear=),  [Sydney](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=066062&p_startYear=),  [Melbourne](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=086232&p_startYear=), [Brisbane](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=040383&p_startYear=), [Canberra](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=070351&p_startYear=), [Adelaide](http://www.bom.gov.au/jsp/ncc/cdio/weatherData/av?p_nccObsCode=136&p_display_type=dailyDataFile&p_stn_num=023011&p_startYear=)  

Temp min/max data was sourced from:  
* [BoM Climate Data Online](http://www.bom.gov.au/climate/data/index.shtml??zoom=1&lat=-26.9635&lon=133.4635&layers=B0000TFFFFFFFFFTFFFFFFFFFFFFFFFFTTT&dp=IDC10001&p_nccObsCode=201&p_display_type=dailyDataFile)

### Get the data here

```{r}
# Get the Data

rainfall <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-01-07/rainfall.csv')
temperature <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-01-07/temperature.csv')

# IF YOU USE THIS DATA PLEASE BE CAUTIOUS WITH INTERPRETATION
nasa_fire <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-01-07/MODIS_C6_Australia_and_New_Zealand_7d.csv')

# For JSON File of fires
url <- "http://www.rfs.nsw.gov.au/feeds/majorIncidents.json"

aus_fires <- sf::st_read(url)

# Or read in with tidytuesdayR package (https://github.com/thebioengineer/tidytuesdayR)

# Either ISO-8601 date or year/week works!

# Install via devtools::install_github("thebioengineer/tidytuesdayR")

tuesdata <- tidytuesdayR::tt_load('2020-01-07') 
tuesdata <- tidytuesdayR::tt_load(2020, week = 2)


rainfall <- tuesdata$rainfall
```
### Data Dictionary

Please note that all weather station locations and metadata are in `weather_station_ids.txt`.

# `temperature.csv`

|variable    |class     |description |
|:-----------|:---------|:-----------|
|city_name   |character | City Name|
|date        |double    | Date |
|temperature |double    | Temperature in Celsius |
|temp_type   |character | Temperature type (min/max daily) |
|site_name   |character | Actual site/weather station|

# `rainfall.csv`

|variable     |class     |description |
|:------------|:---------|:-----------|
|station_code |character | Station Code |
|city_name    |character | City Name |
|year         |double    | Year |
|month        |character | Month |
|day          |character | Day |
|rainfall     |double    | rainfall in millimeters|
|period       |double    | how many days was it collected across |
|quality      |character | Certified quality or not |
|lat          |double    | latitude |
|long         |double    | longitude |
|station_name |character | Station Name |

# `MODIS_C6_Australia_and_New_Zealand_7d.csv`

| variable| description|
|:---| :--- |
| latitude| Center of 1km fire pixel but not necessarily the actual location of the fire as one or more fires can be detected within the 1km pixel.|
|longitude | Center of 1km fire pixel but not necessarily the actual location of the fire as one or more fires can be detected within the 1km pixel. |
| brightness| Channel 21/22 brightness temperature of the fire pixel measured in Kelvin.|
| scan| The algorithm produces 1km fire pixels but MODIS pixels get bigger toward the edge of scan. Scan and track reflect actual pixel size. |
| track | The algorithm produces 1km fire pixels but MODIS pixels get bigger toward the edge of scan. Scan and track reflect actual pixel size. |
| acq_date| Date of MODIS acquisition.|
| act_time| Time of acquisition/overpass of the satellite (in UTC).|
| satellite| A = Aqua and T = Terra. |
| confidence| This value is based on a collection of intermediate algorithm quantities used in the detection process. It is intended to help users gauge the quality of individual hotspot/fire pixels. Confidence estimates range between 0 and 100% and are assigned one of the three fire classes (low-confidence fire, nominal-confidence fire, or high-confidence fire). |
| version| Version identifies the collection (e.g. MODIS Collection 6) and source of data processing: Near Real-Time (NRT suffix added to collection) or Standard Processing (collection only). "6.0NRT" - Collection 6 NRT processing."6.0" - Collection 6 Standard processing. Find out more on collections and on the differences between FIRMS data sourced from LANCE FIRMS and University of Maryland. |
| bright_t31 | Channel 31 brightness temperature of the fire pixel measured in Kelvin.|
|frp | Depicts the pixel-integrated fire radiative power in MW (megawatts).|
|day_night| D = Daytime, N = Nighttime |
