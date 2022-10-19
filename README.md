# Past-Weather
A Dataset Documenting Past Weather in Salt Lake City, Utah

# Contents

This repository contains past weather collected in Salt Lake City over the past 26 days starting on Monday, September 19, 2022 and ending on Friday, October 14, 2022 just after noon. It focuses on key weather statistics that are interesting in analyzing patterns of weather changes that occur as the seasons change. Right now, it is transitioning into Fall and therefore we are most interested in finding out how that transition occurs in Utah and how gradual that is.

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
#read the page
page_html = Client.read()
#close the connection
Client.close()
#use beautiful soup to obtain the html code
page_soup = bs(page_html, "html.parser")


#experimentation with data
page_soup.h1
page_soup.findAll("div",{"id":"day1"})


#create a list of containers with tables that I want
containers = page_soup.findAll("table",{"class":"table table-bordered pastwx_grid"})

len(containers)


#perform data creation to format a correct table
n = 0
date = []
time = []
temp = []
hum = []
dew = []
speed = []
bar = []
data = { 'date':[], 'time':[], 'temp':[], 'hum':[], 'dew':[],'bar':[],'speed':[]}
for container in containers:
    n += 1
    for j in container.find_all('tbody'):
        data['date'].append(n)
        data['time'].append([container.text for container in j.find_all('td')][0])
        data['temp'].append([container.text for container in j.find_all('td')][1])
        data['hum'].append([container.text for container in j.find_all('td')][2])
        data['dew'].append([container.text for container in j.find_all('td')][3])
        data['bar'].append([container.text for container in j.find_all('td')][4])
        data['speed'].append([container.text for container in j.find_all('td')][5])
   
   
 #make this a dataframe and name columns  
df1 = pd.DataFrame(data)
df1.columns =['Date','Time','Temperature','Humidity','Dew Point','Bar. Pressure','Wind Speed']
   
   
#filter our data based on times of the day   
result = pd.DataFrame()
result = pd.concat([df1[df1.Time == '6:00 AM'],result])
result = pd.concat([df1[df1.Time == '8:00 AM'],result])
result = pd.concat([df1[df1.Time == '10:00 AM'],result])
result = pd.concat([df1[df1.Time == '12:00 PM'],result])
result = pd.concat([df1[df1.Time == '2:00 PM'],result])
result = pd.concat([df1[df1.Time == '4:00 PM'],result])
result = pd.concat([df1[df1.Time == '6:00 PM'],result])
result = pd.concat([df1[df1.Time == '8:00 PM'],result])
result = pd.concat([df1[df1.Time == '10:00 PM'],result])

result


#export results to a csv file
result.to_csv('weather.csv',index = False)


```


# Data
Data is shown in weather(1).csv file attached to this repository.
