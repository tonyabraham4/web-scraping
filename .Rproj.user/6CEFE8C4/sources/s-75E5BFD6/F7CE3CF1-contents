# General-purpose data wrangling
library(tidyverse)  

# Parsing of HTML/XML files  
library(rvest)    

# String manipulation
library(stringr)   

### URL_ireland
## Identify all the URLs and fund names for equity 

ireland_equity_url <- "http://mandg.com/ireland/adviser/summary-of-asset-classes/equities/"

html <- read_html(ireland_equity_url)

# identified the tag for each of the 14 funds --> tag <a> and class ".page-content-link"
# Attribute class(class="page-content-link") gives the fund name and 

fund_names <-read_html(ireland_equity_url )%>%
  html_nodes(".page-content-link") %>% 
               html_text()


# href gives each fund link
fund_links <- html %>% 
  html_nodes(".page-content-link") %>% 
  html_attr("href")
fund_links

# Number of funds
length(fund_names)

# Extract the lu number from href


lu <-fund_links %>% 
  str_extract("[lu]+[0-9]+")




## FollOw each of the links and create a data frame/tibble with "FUND NAMES", "PERFORMANCE COMPARATOR", "



