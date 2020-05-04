# pscraper

## Overview

The goal of the project is to understand how the supply-side of vehicle availability affects the electric vehicle market. It tracks all vehicles that are available for sale at dealerships across the country through a web scraper that takes advantage of publicly available data.

The main variables that are tracked are:
| Tracked Variable | Description                                         |
|------------------|-----------------------------------------------------|
| `first_date`     | Date this vehicle was first available for sale      |
| `last_date`      | Date this vehicle was last available for sale       |
| `duration`       | Number of days this vehicle was available for sale  |
| `price`          | Price of the vehicle, all price changes are tracked |
| `seller_id`      | Seller of the car, all seller changes are tracked   |
