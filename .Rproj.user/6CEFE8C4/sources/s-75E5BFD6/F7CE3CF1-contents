# General-purpose data wrangling
library(tidyverse)  

# Parsing of HTML/XML files  
library(rvest)    

# String manipulation
library(stringr)   

### URL_ireland
## Identify all the URLs and fund names for equity 


url <- "http://mandg.com/ireland/adviser/summary-of-asset-classes/equities/"

### FUnction to retrieve equity weblinks from Ireland.
get_fund_list <- function(url){
  html <- read_html(url)
  
  # identified the tag for each of the 14 funds --> tag <a> and class ".page-content-link"
  # Attribute class(class="page-content-link") gives the fund name and 
  fund_names <- html %>%
    html_nodes(".page-content-link") %>% 
    html_text()
  
  # href gives each fund link
  fund_links <- html %>% 
    html_nodes(".page-content-link") %>% 
    html_attr("href")
  
  
  # Extract the lu number from href
  isin <-fund_links %>% 
    str_extract("[lu]+[0-9]+")
  
  fund_list <- tibble(fund_names = fund_names, fund_links = fund_links,isin = isin)  
  message(paste("Total number of funds found ", dim(fund_list)[1], sep = ":"))
  fund_list
  
  # TODO 2 Extract country name in another column.
  # TODO 3 Extract "lux" and "non lux" and add a flag.
  # TODO 4 Check for any timestamp present to associate - "Last update time" etc.
}

url_funds_ireland <- get_fund_list("http://mandg.com/ireland/adviser/summary-of-asset-classes/equities/")
url_funds_ireland
# Checking
class(url_funds_ireland)
dim(url_funds_ireland)
summary(url_funds_ireland)
length(url_funds_ireland)

###########################################################################################################################################

### TODO 1 Lets find the number of Share Classes for each fund. Find a way to extract the li id = that "contains shareclass.
page <- read_html("https://www.mandg.com/ireland/adviser/funds/mg-lux-asian-fund/lu1670618187/overview")

share_class_list <- page %>% 
  html_nodes("ul") %>% 
  html_attr(".dropdown-menu share-class")
### TODO 1 Ends here.


###########################################################################################################################################

### Function to follow the above links and fetch the "Performance Comparator", "Benchmark", "Objectives", "Risk", "Cost", "Past Performance", etc.)

#fund_page <- read_html("https://www.mandg.com/ireland/adviser/funds/mg-lux-asian-fund/lu1670618187/overview")

get_fund_wording <- function(fund_page){
  
  fund_page <- read_html(fund_page)
  
  
  # Extracting the umbrella fund name and share class
  
  umbrella_fund_name <-fund_page %>% 
    html_nodes(css = "#MainContentPlaceHolder_BreadCrumb_BreadCrumb_BreadCrumbLabel_1") %>% 
    html_text()
  share_class <-fund_page %>% 
    html_nodes(css = "#MainContentPlaceHolder_BreadCrumb_BreadCrumb_BreadCrumbLabel_2") %>% 
    html_text()
  
  # Extracting the text in the form of XML nodes
  
  div_left<- fund_page %>% 
    html_nodes(".column") %>% 
    html_text() %>% 
    paste(collapse = " ")
  
  
  #right can be ignored sinceleft is picking it already!!!
  # div_right <- page %>% 
  #   html_nodes(".column.right") %>% 
  #   html_text()
  
  div_bottom <- fund_page %>% 
    html_nodes(".disclaimer") %>% 
    html_text() %>% 
    paste(collapse = " ")
  # Combining
  fund_wording <- paste(div_left ,div_bottom, collapse = "")
  # Removing white spaces
  fund_wording <-  gsub("\\s+"," ", fund_wording )
  
  fund_list1 <- tibble(umbrella_fund_name = umbrella_fund_name, share_class = share_class, fund_wording = fund_wording)
  fund_list1
  
}



###################################################################




