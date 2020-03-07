
Airpollution data csv : ![Link](http://realtime.opendatanepal.com/)


`
install.packages("jsonlite")
`

`
library(jsonlite)
`

`
library(tidyverse)
`

`
json_file <- "http://realtime-api.opendatanepal.com/airquality/api/latest?id=5&params=pm25&coordinate=true"
`

`
json_data <- fromJSON(json_file, flatten=F, simplifyDataFrame = TRUE)
`

