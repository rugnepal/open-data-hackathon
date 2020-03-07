

`

install.packages("jsonlite")

`

`
library(jsonlite)
library(tidyverse)
`

`
# # read remote json
json_file <- "http://realtime-api.opendatanepal.com/airquality/api/latest?id=5&params=pm25&coordinate=true"
json_data <- fromJSON(json_file, flatten=F, simplifyDataFrame = TRUE)
`

