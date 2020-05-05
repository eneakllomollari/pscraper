# pscraper

## Overview

The goal of the project is to understand how the supply-side of vehicle availability affects the electric vehicle market. It tracks all vehicles that are available for sale at online marketplaces across the country through a web scraper that takes advantage of publicly available data.

The main variables that are tracked are:
|  Variable        | Description                                         |
|------------------|-----------------------------------------------------|
| `first_date`     | Date this vehicle was first available for sale      |
| `last_date`      | Date this vehicle was last available for sale       |
| `duration`       | Number of days this vehicle was available for sale  |
| `price`          | Price of the vehicle, all price changes are tracked |
| `seller_id`      | Seller of the car, all seller changes are tracked   |

## Components
There are 4 main project components

### Django Backend Application
This is a backend app written in Python3.7 using Django3 and Django Rest Framework. It provides access to a MySQL database that contains the data, through 3 main [API endpoints](https://pscraper.herokuapp.com/api/v1/). The backend app is hosted on [Heroku](https://www.heroku.com/) and the MySQL database is hosted on [Cloud SQL](https://cloud.google.com/sql). 

It has 3 main models, vehicle, seller and history. 
1. The vehicle model has the most up to date information on the vechile such as VIN, Make, Model, Price, etc.
2. The seller model has infomation on the sellers such as name, address, etc.
3. The history model is used to track changes in price and seller.

For more information on this project see [pscraper-db](https://www.github.com/eneakllomollari/pscraper-db)

### Python Library
This is a python library with three packages:

#### [`pscraper.scraper`](https://github.com/eneakllomollari/pscraper-lib/#pscraperscraper)
Main package of the library that, among others, provides one main API, [`scrape`](https://github.com/eneakllomollari/pscraper-lib/#function-scrape), which performs the scraping process following the given parameters and saves it to the database.
Every vehicle is processed in a sequential manner, and there is work in progress to change that to a multithreading approach for performance improvement.

The marketplace where data is scraped from are: [Cars.com](https://www.cars.com). Soon [Autotrader](https://www.autotrader.com) and [CarMax](https://www.carmax.com) will be added with more to come after.

#### [`pscraper.api`](https://github.com/eneakllomollari/pscraper-lib/#pscraperapi)
This package has APIs that interact with the [endpoints](https://pscraper.herokuapp.com/api/v1/) provided by the backend application. It is used to create, update or retrieve records on a vehicle or seller.

#### [`pscraper.utils`](https://github.com/eneakllomollari/pscraper-lib/#pscraperutils)
Provides several miscellaneous helpers used for the scraping and reporting process..

Since the scraping function is designed to be autonomous, the functions are configured so that if any failure occurs a slack message will be sent to a specific channel.


For more information on this project see [pscraper-lib](https://www.github.com/eneakllomollari/pscraper-lib).

### Daily Scraping Tool
This project contains the script that performs web-scraping daily. At the end of the scraping process a report is build a send to a slack channel.
The command to start the scheduled scraping is:
```bash
$ nohup ./scrape.py &
```
This is run inside a tmux session on a [Google Cloud Compute Engine](https://cloud.google.com/compute) so that the process can run without any supervision.

For more information on this project see [pscraper-tool](https://www.github.com/eneakllomollari/pscraper-tool).


### Data Dashboard <img src="https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg" width="32" height="32">
WIP

A frontend dashboard, build with ReactJS. There might be more uses for it later but at the moment it's planned to be used mainly as a data visualization tool. Users are authenticated using the Django framework that's already set up, and it will have different views/layout based on the user's permissions.
#### Sneak Peek:
<img src="/dashboard.png">
<img src="/map.png">
<img src="/dashboard_white.png">
<img src="/map_white.png">

## Tools/Services Used
<p>
  <img src="https://juststickers.in/wp-content/uploads/2019/07/django-shapecut.png" width="253" height="201" alt="Django3"/> 
  <img src="https://www.django-rest-framework.org/img/logo.png" width="454" height="200" alt="Djano Rest Framework (DRF)"/>
</p>
<p>
  <img src="https://brand.heroku.com/static/media/heroku-logotype-spacing-horizontal.7594cf7f.svg" width="330" height="145" alt="Heroku"/>   
  <img src="https://cdn.worldvectorlogo.com/logos/mysql.svg" width="201" height="145" alt="MySQL"/>
</p>
<p>
  <img src="https://funthon.files.wordpress.com/2017/05/bs.png?w=772" width="351" height="151" alt="BeautifulSoup4"/>
  <img src="https://pluralsight.imgix.net/paths/python-7be70baaac.png" width="152" height="152" alt="Python3.7"/>
  <img src="https://cdn.clipart.email/d9e4929a152eaf98c98d78feda3d7fa8_google-maps-png-transparent-google-mapspng-images-pluspng_900-916.png" width="147" height="150" alt="Google Maps API"/>
</p>
<p>
  <img src="https://venturebeat.com/wp-content/uploads/2019/10/google-cloud-platform.png?fit=800%2C400&amp;strip=all" width="370" height="185" alt="Google Cloud Platform (GCP)"/>
  <img src="https://upload.wikimedia.org/wikipedia/commons/1/1d/Cloud-SQL-Logo.svg" width="183" height="183" alt="Cloud SQL"/>
  <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/d8/Google-Compute-Engine-Logo.svg/1200px-Google-Compute-Engine-Logo.svg.png" width="183" height="183" alt="Compute Engine"/>
  <img src="https://cdn4.iconfinder.com/data/icons/logos-3/600/React.js_logo-512.png" width="174" height="174" alt="ReactJS"/>
</p>
