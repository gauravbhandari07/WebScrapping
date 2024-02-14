from bs4 import BeautifulSoup

# The requests module allows user to send HTTP requests using Python.
import requests

# CSV is a simple file format used to store tabular data, such as a spreadsheet or database.
import csv

# store the URL of the webpage in a variable ‘products_url’
products_url = "https://www.reliancedigital.in/redmi-note-13-5g-128-gb-6-gb-ram-black-smartphone/p/494351914"
# requests we GET content from the webpage
responses = requests.get(products_url)
responses.status_code
# we store the content of the page in page_contents variable
page_contents = responses.text
# using Beautiful Soup we parse the html and store it in a variable named ‘doc’.
doc = BeautifulSoup(page_contents, "html.parser")
# we use all the classes and store them in variable corresponding to class of what we’re looking for here we are searching for name.
heading_class = "_4rR01T"
# The findAll function takes 2 arguments i.e., the tag the data is stored under (in the case of the name of the product
# it is stored under the <div>) and the name of the class of the data we wish to extract (in this case which we have stored
# under ‘heading_class’) and store the data received in a list called ‘heading_tags’.
heading_tags = doc.findAll("div", class_=heading_class)
# with the extraction of every tag we have also initialized n list with identifiers like ‘name_text’, ‘price_text’ and so on.
# These lists will be used later to hold the exact information we want, that is without the <div> tags and all the
# unnecessary things.
name_text = []
heading_tags[:4]
price_class = "_30jeq3 _1_WHN1"
price_tags = doc.findAll("div", class_=price_class)
price_text = []
# we only check the first four because the structure of the rest will be same.
price_tags[:4]
stars_class = "_3LWZlK"
stars_tags = doc.findAll("div", class_=stars_class)
stars_text = []
stars_tags[:4]
reviews_class = "_2_R_DZ"
reviews_tags = doc.findAll("span", class_=reviews_class)
reviews_text = []
reviews_tags[:4]
url_class = "_1fQZEK"
#'base_url' using which stored the missing part of the URL as on inspecting we saw that the <a> tags didn’t store the
# complete URL of the webpage of the product
base_url = "https://www.flipkart.com"
url_tags = doc.findAll("a", class_=url_class)
url_product = []
# we iterate through every URL tag and using append function and append the ‘base_url’ with the ‘href’ part of the
# ‘url_tags’ and store it in ‘url_products’ list.
for i in range(len(url_tags)):
    url_product.append(base_url + url_tags[i]["href"])
# After coming out of the for loop this list will have the exact URL to the product.
# we iterate through every tag and using append function we extract the data for name, price, stars, reviews and ratings.
for i in range(len(reviews_tags)):
    price_text.append(price_tags[i].text)
    name_text.append(heading_tags[i].text)
    stars_text.append(stars_tags[i].text)
    reviews_text.append(reviews_tags[i].text)
    reviews_text[i] = reviews_text[i].replace("\xa0", " ")
# In the reviews and ratings, we were getting some part in the i.e., “\xa0” so we replace it with “ ”.
# We store all the data in a dictionary. We store the lists under their respective headings.
product_dict = {
    "name": name_text,
    "price": price_text,
    "stars": stars_text,
    "reviews": reviews_text,
    "url": url_product,
}
# We import the Pandas library to convert the dictionary to a dataframe
import pandas as pd

# we display the first 4 items of data extracted to the dataframe to verify if we the data extracted is correct or not.
products_df = pd.DataFrame.from_dict(product_dict, orient="index")
products_df = products_df.transpose()
products_df[:4]
# we export the data in csv file which is created in the same directory as the project.
products_df.to_csv("products.csv")
from google.colab import drive

drive.mount("/content/drive")
