# Amazon-Web-Scraper-Project
Anaconda: https://www.anaconda.com/products/ind...

Find Your User-Agent: https://httpbin.org/get
# Required Tools
Anaconda: Download and install Anaconda to manage your Python environment.
Jupyter Notebooks: We will be using Jupyter Notebooks for this project. Launch it after installing Anaconda.
# Project Overview
In this project, we will scrape data from Amazon based on a poll where a majority of participants expressed interest in Amazon data. We will focus on extracting product titles and prices from a specific product page. Future projects will cover more advanced topics, such as scraping multiple items and traversing through multiple pages.

# Setting Up the Environment
Import Libraries: We will be using several libraries for this project:

BeautifulSoup for parsing HTML.
requests for making HTTP requests.
csv for handling CSV file operations.
datetime for timestamping our data.
Here’s how to import the necessary libraries:

import requests
from bs4 import BeautifulSoup
import csv
from datetime import datetime
Connecting to the Website: We need to specify the URL of the Amazon product page we want to scrape. Additionally, we will set up headers to mimic a browser request.

url = 'YOUR_PRODUCT_URL'
headers = {'User-Agent': 'YOUR_USER_AGENT'}
page = requests.get(url, headers=headers)
Scraping Data
Parsing HTML Content
Once we have the page content, we will use BeautifulSoup to parse the HTML:

soup = BeautifulSoup(page.content, 'html.parser')
Extracting Product Title and Price
To extract the product title and price, we will identify the HTML elements containing this information. For example:

product_title = soup.find(id='productTitle').get_text(strip=True)
product_price = soup.find(id='priceblock_ourprice').get_text(strip=True)
Cleaning the Data
After extracting the data, we may need to clean it up. For instance, we can remove any unwanted characters or whitespace:

product_price = product_price.strip().replace('$', '')
Saving Data to CSV
To store the scraped data, we will create a CSV file. Here’s how to do it:

with open('amazon_scraper_data.csv', mode='w', newline='', encoding='utf-8') as file:
    writer = csv.writer(file)
    writer.writerow(['Title', 'Price'])  # Writing headers
    writer.writerow([product_title, product_price])  # Writing data
Automating the Scraping Process
To automate the scraping process, we can set up a loop that runs at specified intervals. For example, to check the price every 5 seconds:

import time
while True:
    check_price()  # Function that contains the scraping logic
    time.sleep(5)
Conclusion
In this guide, we have covered the basics of web scraping using Python, focusing on Amazon as our target site. We learned how to extract product data, clean it, and save it into a CSV file. Additionally, we explored how to automate the scraping process to continuously monitor product prices.
