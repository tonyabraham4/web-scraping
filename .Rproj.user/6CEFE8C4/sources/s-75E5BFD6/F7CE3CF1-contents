# General-purpose data wrangling
library(tidyverse)  

# Parsing of HTML/XML files  
library(rvest)    

# String manipulation
library(stringr)   

# Verbose regular expressions
library(rebus)     

# Eases DateTime manipulation
library(lubridate)

library(V8)

# URL_ireland

ireland_equity_url <- "http://mandg.com/ireland/adviser/summary-of-asset-classes/equities/"

html <- read_html(ireland_equity_url)
# identified the tag for each of the 14 funds --> tag <a> and class ".page-content-link"


nodes_class_a <- html %>% 
  html_nodes(".page-content-link")
nodes_class_a


length(nodes_class_a)

