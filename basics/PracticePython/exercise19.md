Decode A Web Page Two Solutions
Exercise 19
The How To Decode A Web Page Two exercise was a follow-up to the extremely challenging prelude, How To Decode A Web Page. The purpose of the original (and the follow-up exercise) was to give people a chance to poke around at a close-to-real application of Python.

A few people submitted solutions to this exercise (one example is given at the bottom of the page), and many of them used things that I haven’t yet talked about in the exercises. I will not go into extreme detail about how to solve this problem - I will just present the important points for one way you could solve this problem. For a more detailed solution to a similar problem, I encourage you to look at the solution to the previous exercise (How To Decode A Web Page).

And without further ado, a plan for achieving the solution:

Use the requests library to load the HTML of the page into Python
Find out which HTML tags contain the article text
Use BeautifulSoup to process HTML and extract the text of the article
Print the extracted text to the screen
In my opinion, the difficult part of this exercise is figuring out the elements on the page (whether that is through HTML or CSS selectors) that contain all the text of the article. It requires knowing or exploring a little bit about CSS selectors and reading documentation. Such is the way of working with web pages.

A few observations on that point:

The entire text of the article is on this single page - no need to move to another URL. The text is placed inside “hidden containers” that are just set to invisible.
It seems that article text comes inside p elements that are inside div elements of class body that are inside div elements that have classes parbase and cn_text. But it also seems that there are other things like hyperlinks and article comments also fall inside this structure.
When you select for this in BeautifulSoup, the first 7 elements that come out are links and the introduction, so we just want to ignore those.
Given these observations, this solution:

import requests
from bs4 import BeautifulSoup

base_url = "http://www.vanityfair.com/society/2014/06/monica-lewinsky-humiliation-culture"
r = requests.get(base_url)
soup = BeautifulSoup(r.text)

all_p_cn_text_body = soup.select("div.parbase.cn_text > div.body > p")

for elem in all_p_cn_text_body[7:]:
  print(elem.text)
view rawdecode-web-page-solutions-2.py hosted with ❤ by GitHub
prints to the screen the full text of the article.

The CSS selectors are complex, and it takes some practice to get comfortable with them. We’ll re-visit this later (perhaps much later), but for now I encourage you to poke around the internet and look at sources of websites, playing with BeautifulSoup and figuring out how CSS selectors behave.

Here is an example of a user-submitted solution that is not completely automated, and that does not use the exact article specified. However, it does show you that you can start solving your own problems using the techniques I am talking about on this blog.

"""
Using the requests and BeautifulSoup Python libraries, print to the screen the full text of the
article on this website: http://www.vanityfair.com/society/2014/06/monica-lewinsky-humiliation-culture.
http://www.practicepython.org/exercise/2014/07/14/19-decode-a-web-page-two.html
"""

import requests
from bs4 import BeautifulSoup

def print_to_text(base_url):
    """
    :param base_url: URL of article to scrape
    :return: naked content to text file
    """
    r = requests.get(base_url)
    soup = BeautifulSoup(r.text)
    with open("work less.txt", "w") as textfile:
        for paragraph in soup.find_all(dir="ltr"):
            textfile.write(paragraph.text.replace("<span>",""))

if __name__ == "__main__":
    #Chose my own article
    base_url = "http://www.theatlantic.com/business/archive/2014/08/to-work-better-work-less/375763/"
    base_url2 = "http://www.theatlantic.com/business/archive/2014/08/to-work-better-work-less/375763/2/"
    print_to_text(base_url)
    print_to_text(base_url2)
view rawexercise 19.py hosted with ❤ by GitHub