Women Access to Finance:

![Link](https://docs.google.com/spreadsheets/d/1wFr2hMAeeCkQQwfiymwKNS9gDPRxbTcu5mqWZYljNM8/edit?usp=sharing)

'
library(googlesheets4)
sheets_deauth() # only for public sheet

women_finance <- read_sheet("1wFr2hMAeeCkQQwfiymwKNS9gDPRxbTcu5mqWZYljNM8", 
                         sheet = 1) %>%
  janitor::clean_names() 
'

