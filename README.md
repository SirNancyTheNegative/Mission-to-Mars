# Mission to Mars

## Purpose

### An Infatuation with Mars
In this project, we scrape data concerning the red planet Mars off of the internet and consolidate it in a single website. In order to do this, we need to write not only code for data scraping but also code for hosting the site in Flask and receiving the data as well as HTML that comprises the site and various other components. From the web we pull the latest news pertaining to Mars, various facts about Mars in comparison to the Earth, and a most recent picture of Mars landscape, as well as four hemispheric pictures that encapsulate the entirety of the red planet.

## Process

### Scraping
In order to have data to put into the site, we need to find it, pull from any source site's html, and save it to a database. This process, otherwise known as scraping, starts with the tools: for this purpose, we make use of BeautifulSoup to read HTML to find pertinent data, and ChromeDriveManager and splinter's Browser methods in order to do so automatically. From the sites chosen for this project, we seek out the most specific tags we can find that relate to our data, and grab the data from there. Sometimes it's text, but when we have to grab images, it's easy enough to read the source tag and use that.

Whenever we have to switch websites, we have to re-read the new site's HTML into BeautifulSoup, otherwise we don't get the information we're looking for. In order to remedy this, we can write:
```
html = browser.html
mars_soup = soup(html, 'html.parser')
```

This is assuming, of course, we have since aliased BeautifulSoup as "soup" and we have our browser initialized as "browser". In order to not clutter our code, all of the scraping code is left in "scraping.py", with a function "scrape_all()" that runs all the scraping functions one at a time, compiles the data we want into a dictionary, and returns that dictionary.

### The Website and the Database
Now that we have a way to get the information, we need to utilize it. This is where the website comes into play. Using MongoDB, we can use the website to not only pull from a database made specifically to hold the information we want, but also call the functions defined in "scraping.py" in order to push new information into the database. In order to do this, we set up a button that will call the function "scrape_all()" and push the dictionary into the database, before redirecting to the main page once more. This is done through Flask: the file "app.py" contains the basic pathing of the website, with instructions on how to render the site on different paths. For our purposes, we need only two: A home page with the most recent data, or "/", and the one that activates our scraping function and redirects the user to the home page again, or "/scrape". This simple action allows us to display the most recent data, and also allows us to update the data within our database at the push of a button.

In order to have better readability, some text was centered in places using the class tag ".text-center", and the table we have on the site was changed to include the ".table-hover" tag, which causes an entire row to darken slightly whenever one of its cells is moused over. It also makes the site look better cosmetically, though that is merely a personal opinion, and not necessarily a fact.
