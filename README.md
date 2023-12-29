# WebScrapping - Get desired links from a website

Beautiful soup is the common webscrapping library in python. It uses html tags for data retrival. 
Before getting into the code, answer the following questions.

What's the target?
To get only DP-203 related discussions links from all the pages.

How many pages are there?
1409

What's the link?
https://www.examtopics.com/discussions/microsoft/

Any pattern identified?
Yes. Page number is added at the end of the link.

Now let's get into the code.

-These lines import the necessary modules for web scraping (requests for making HTTP requests, BeautifulSoup for parsing HTML/XML, and timer for measuring the time taken by the script).

import requests
from bs4 import BeautifulSoup
from timeit import default_timer as timer

-This line starts the timer to measure the runtime of the script.

start = timer()

-This line initializes an empty list dp203_links where we will store the links that contain 'dp-203'.

dp203_links = []

-This line starts a loop that iterates from 1 to 1409.

for i in range(1,1410):

-Inside the loop, this line initializes an empty list k for storing links on the current page.

k=[]

-Constructs the URL for the current page based on the loop variable i.

page_link = 'https://www.examtopics.com/discussions/microsoft/'+str(i)+'/'

-Sends an HTTP GET request to the URL, retrieves the HTML content, and stores it in the link variable. The verify=False argument is used to ignore SSL certificate verification.

link = requests.get(page_link, verify=False).text

-Creates a BeautifulSoup object soup to parse the HTML content using the XML parser.

soup = BeautifulSoup(link,'xml')

-Finds all anchor (<a>) tags in the HTML content and stores them in the all_links variable.

all_links = soup.find_all('a')

-Iterates through all the anchor tags, extracts the 'href' attribute (link), and appends it to the k list.

for a_link in all_links:
  k.append(a_link.get('href'))

-Iterates through the links in the k list, checks if 'dp-203' is present in the link, and appends it to the dp203_links list if true.

for j in k:
      if(j):
          if 'dp-203' in j:
              dp203_links.append(j)

-Stops the timer and calculates the runtime of the script. Prints the total runtime.

end = timer()
print("Run Time: {}".format(end-start))

-Print the output

dp203_links

Time taken by this scrpit : 1.67 hr(approx)



