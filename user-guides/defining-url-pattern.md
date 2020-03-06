---
layout: page
title: Defining URL Pattern
parent: User Guides
nav_order: 4
---

# Defining URL Pattern

## Match Exact URL

| URL Example | Matched |
|---|---|
| `/hotel` | `www.tiket.com/hotel`{: .text-green-100}<br>`www.tiket.com/hotels`{: .text-red-100} x|

## Set Parameter

| URL Example | Matched |
|---|---|
| `/hotel/<country>/<city>` | `www.tiket.com/hotel/indonesia/jakarta`{: .text-green-100}<br>`www.tiket.com/hotel/thailand/bangkok`{: .text-green-100}   |


## Wild Card 

| URL Example | Matched |
|---|---|
| `/hotel/*` | `www.tiket.com/hotel/indonesia/city/jakarta`{: .text-green-100}<br>`www.tiket.com/hotel/japan/region/tokyo`{: .text-green-100} | 

## Regular Expression (RegEx)


| URL Example | Matched |
|---|---|
| `/flight/DPS-<flightNum:\d+>` | `www.tiket.com/flight/DPS-87`{: .text-green-100}<br>`www.tiket.com/flight/DPS-55`{: .text-green-100}<br>`www.tiket.com/flight/DPS-MESC`{: .text-red-100} x |
