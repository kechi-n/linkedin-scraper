# LinkedIn Scraper

Scrapes Experience, Education, top three skills and visible interests on a user's LinkedIn page 

## Getting Started

Clone the repo locally to your machine.

### Prerequisites

Install chromedriver, and set your chromedriver location by running the following in the terminal

```bash
export CHROMEDRIVER=~/chromedriver
```

### Installing

Import the class

```python
from linkedin_scraper import Person
from request import REQUEST
```

Import webdriver using the path from which chromedriver is running and assign it to the driver object, example: 

```python
from selenium import webdriver
driver = webdriver.Chrome(executable_path=r'/Users/kechup/chromedriver') 
```

## Insert the public profile URL and scrape the data from the page.

```python
person = Person(linkedin_url="https://www.linkedin.com/in/kech-up/", experiences = [], educations = [], skills=[], interests = [], driver = driver, scrape = False)
person.scrape()
person
```

### Scraping sites where login is required first
1. Run `ipython` or `python`
2. In `ipython`/`python`, run the following code (you can modify it if you need to specify your driver)
3. 
```python
from linkedin_scraper import Person
from selenium import webdriver
driver = webdriver.Chrome()
person = Person("https://www.linkedin.com/in/kech-up", driver = driver, scrape=False)
```
4. Login to Linkedin
5. [OPTIONAL] Logout of Linkedin
6. In the same `ipython`/`python` code, run
```python
person.scrape()
```

The reason is that LinkedIn has recently blocked people from viewing certain profiles without having previously signed in. So by setting `scrape=False`, it doesn't automatically scrape the profile, but Chrome will open the linkedin page anyways. You can login and logout, and the cookie will stay in the browser and it won't affect your profile views. Then when you run `person.scrape()`, it'll scrape and close the browser. If you want to keep the browser on so you can scrape others, run it as 

**NOTE**: Scraping can also occur while logged in. Beware that users will be able to see that you viewed their profile.

```python
person.scrape(close_on_complete=False)
``` 
so it doesn't close.


## API

### Person
Overall, to a Person object can be created with the following inputs:

```python
Person(linkedin_url=None, experiences = [], educations = [], driver = None, scrape = True)
```
#### `linkedin_url`
This is the linkedin url of their profile

#### `experiences`
This is the past experiences they have. A list of `linkedin_scraper.scraper.Experience`

#### `educations`
This is the education they have. A list of `linkedin_scraper.scraper.Education`

#### `skills`
This is the top three skills they have. A list of `linkedin_scraper.scraper.Skills`

#### `educations`
This is the interests that show up when their poage is loaded. A list of `linkedin_scraper.scraper.Interests`

#### `driver`
This is the driver from which to scraper the Linkedin profile. A driver using Chrome is created by default. However, if a driver is passed in, that will be used instead.

For example
```python
driver = webdriver.Chrome()
person = Person("https://www.linkedin.com/in/kech-up", driver = driver)
```

#### `scrape`
When this is **True**, the scraping happens automatically. To scrape afterwards, that can be run by the `scrape()` function from the `Person` object.


### `scrape(close_on_complete=True)`
This is the meat of the code, where execution of this function scrapes the profile. If *close_on_complete* is True (which it is by default), then the browser will close upon completion. If scraping of other profiles are desired, then you might want to set that to false so you can keep using the same driver.



## Authors and Acknowledgements
 
* Kechi Nwudu
* Hat tip to [joeyism]https://github.com/joeyism 
* Inspiration - *Initial work* - https://github.com/joeyism/linkedin_scraper
