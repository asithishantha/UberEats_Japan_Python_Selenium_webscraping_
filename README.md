 #Uber-Eats Web Scraping script Using Selenium in Python 
 
 For this project,Python 3.8 will be used.
 
 For Windows installations, when installing Python make sure to check “PATH installation”. PATH installation adds executables to the default Windows Command Prompt executable search. Windows will then recognize commands like “pip” or “python” without requiring users to point it to the directory of the executable (e.g. C:/tools/python/…/python.exe). If you have already installed Python but did not mark the checkbox, just rerun the installation and select modify. On the second screen select “Add to environment variables”.
 
 _Getting to the libraries_
 
*  is widely used to parse the HTML files
 
*  Pandas is used to create structured data

*  Selenium provides browser automation

To install these libraries, start the terminal of your OS. Type in:
    
    pip install BeautifulSoup4 pandas selenium
    
    
_WebDrivers and browsers_

Every web scraper uses a browser as it needs to connect to the destination URL. For testing purposes i highly recommend using a regular browser.

To get started, use your preferred search engine to find the “webdriver for Chrome” (or Firefox). Take note of your browser’s current version. Download the webdriver that matches your browser’s version.

for chrome driver : https://chromedriver.chromium.org/

_Finding a cozy place for our Python web scraper_

If you already have Visual Studio Code installed, picking this IDE would be the simplest option. Otherwise, I’d highly recommend PyCharm


_Importing and using libraries_

    import openpyxl
    from selenium import webdriver
    from selenium.webdriver.common.keys import Keys
    import time
    from selenium import webdriver
    from selenium.webdriver.common.by import By
    from selenium.webdriver.support.ui import WebDriverWait
    from selenium.webdriver.support import expected_conditions as EC
    import csv


We should begin by defining our browser. Depending on the webdriver we picked back in “WebDriver and browsers” we should type in:

    driver = webdriver.Chrome(executable_path='c:\path\to\windows\webdriver\executable.exe')

    OR

    driver = webdriver.Firefox(executable_path='/nix/path/to/webdriver/executable')
 
 
_Picking a URL_

Before performing our first test run, choose a URL. As this web scraping tutorial is intended to create an elementary application, I highly recommended picking a simple target URL:

    driver.get("https://www.google.com/")

In this program, we are reading restaurants' name from excel sheet.
to read that excel sheet 

    obj = openpyxl.load_workbook("nagoya.xlsx")

after that we have to get restaurants' name from excel sheet one by one 

below code is written.

    sheet_obj = obj.active
    # print(sheet_obj)

    m_row = sheet_obj.max_row

    for i in range(1, m_row):
        cell_obj = sheet_obj.cell(row=i, column=1)
        restaurantname = cell_obj.value  # take the restaurant name in first cell
        driver.get("https://www.google.com/")
        search = driver.find_element_by_name("q")  # google search box element name by name, we can use class name,
        # tag name and any other locate element methods.
        search.send_keys(restaurantname)  # search the restaurant name
        search.send_keys(Keys.RETURN)  # press search


_Get elements_

To get mobile number from the google. get element by x path is used.
We can use any locating method for that.
To know about locating methods.
   https://www.youtube.com/watch?v=mQ7-mPJYJ5A&t=973s
   
If you don't know how to write the x path for the target element, there is a google plugin, which generate the x path for any element .
 
  for more details : https://www.youtube.com/watch?v=VvZEsZ3cGmc


    number2 = driver.find_element_by_xpath("//span[@class='LrzXr zdqRlf kno-fv']/a[1]/span[1]")


_for write the output data to the csv_ 

    
    def write_csv(resturant):
        with open('nagoya_res.csv', 'a', encoding='utf8') as csvfile:
            writer = csv.writer(csvfile)

            row = [resturant['name'], resturant['address'], resturant['number'], url]

            writer.writerow(row)


    write_csv(resturant)
    # write to the csv file. please give the csv file name accordingly, you wish to write the scraped data
    print(resturant)
    
