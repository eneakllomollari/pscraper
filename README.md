# pscraper

## Overview

The goal of the project is to understand how the supply-side of vehicle availability affects the electric vehicle market. It tracks all vehicles that are available for sale at online marketplaces(Cars.com, Autotrader) across the country through a web scraper that takes advantage of publicly available data.

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

#### `pscraper.scraper`
Main package of the library that, among others, provides one main API, `scrape`, which performs the scraping process following the given parameters and saves it to the database. Every vehicle is processed in a sequential manner, and there is work in progress to change that to a multithreading approach for performance improvement.

The marketplace where data is scraped from are: [Cars.com](https://www.cars.com), and [AutoTrader](https://www.autotrader.com).

#### `pscraper.api`
This package has APIs that interact with the [endpoints](https://pscraper.herokuapp.com/api/v1/) provided by the backend application. It is used to create, update or retrieve records on a vehicle or seller.

#### `pscraper.utils`
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
