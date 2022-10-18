# Past-Weather
A Dataset Documenting Past Weather in Salt Lake City, Utah

# Contents
Weather plays an important factor in decision making whether we consciously choose to ignore it or not. Thus an analysis of the past weather can be valuable. This is of great interest to many people as it can help predict how certain holidays such as Halloween or Thanksgiving might play out. Will it be too warm or too cold to eat outside? Does there appear to be much wind during these transition months? All of these questions and more we hope to be able to explain with this dataset. 



This repository contains past weather collected in Salt Lake City over the past 26 days. It focuses on key weather statistics that are interesting in analyzing patterns of weather changes that occur as the seasons change. Right now, it is transitioning into Fall and therefore we are most interested in finding out how that transition occurs in Utah and how gradual that is.

Below will be posted the code that I used to scrape the website https://www.localconditions.com/weather-salt-lake-city-utah/84101/past.php. 

# Code 
```
#import packages
import numpy as np
import pandas as pd
from bs4 import BeautifulSoup as bs
import requests
from urllib.request import urlopen as uReq 


#import website
myurl = 'https://www.localconditions.com/weather-salt-lake-city-utah/84101/past.php'
myurl


#use uReq to open url
Client = uReq(myurl)
```

