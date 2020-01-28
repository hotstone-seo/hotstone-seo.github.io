---
layout: page
title: URL Pattern
nav_order: 2
---

# URL Pattern

## Examples

| Pattern | Matched |
|---|---|---|
| `/hotel` | `www.tiket.com/hotel`{: .text-green-100}<br>`www.tiket.com/hotels`{: .text-red-100} x|
| `/hotel/<country>/<city>` | `www.tiket.com/hotel/indonesia/jakarta`{: .text-green-100}<br>`www.tiket.com/hotel/thailand/bangkok`{: .text-green-100}   |
| `/hotel/*` | `www.tiket.com/hotel/indonesia/city/jakarta`{: .text-green-100}<br>`www.tiket.com/hotel/japan/region/tokyo`{: .text-green-100} | 
| `/flight/DPS-<flightNum:\d+>` | `www.tiket.com/flight/DPS-87`{: .text-green-100}<br>`www.tiket.com/flight/DPS-55`{: .text-green-100}<br>`www.tiket.com/flight/DPS-MESC`{: .text-red-100} x |



