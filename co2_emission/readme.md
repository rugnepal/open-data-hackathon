# Food Consumption and CO2 Emissions

The data comes from [nu3](https://www.nu3.de/blogs/nutrition/food-carbon-footprint-index-2018) and was contributed by [Kasia Kulma](https://r-tastic.co.uk/post/from-messy-to-tidy/).

### Get the data here

```{r}
# Get the Data

food_consumption <- readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-18/food_consumption.csv')

```
### Data Dictionary

# `food_consumption.csv`

|variable      |class     |description |
|:-------------|:---------|:-----------|
|country       |character | Country Name |
|food_category |character | Food Category |
|consumption   |double    | Consumption (kg/person/year) |
|co2_emmission |double    | Co2 Emission (Kg CO2/person/year) |

