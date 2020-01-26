---
layout: home
title: URL Pattern
nav_order: 2
---

# URL Pattern

## Static URL

```
/hotel
```

Matched:
```
www.tiket.com/hotel
```

Not Matched:
```
www.tiket.com/hotels
```

## Dynamic URL

```
/hotel/<country>/<city>
```

Matched:
```
www.tiket.com/hotel/indonesia/jakarta
www.tiket.com/hotel/thailand/bangkok
```

## Regex

### Wildcard

```
/hotel/*
```

Matched:
```
www.tiket.com/hotel/indonesia/city/jakarta
www.tiket.com/hotel/japan/region/toky
```

### Pattern of parameter

```
/flight/DPS-<flightNum:\d+>
```

Matched:
```
www.tiket.com/flight/DPS-87
www.tiket.com/flight/DPS-55
```

Not matched:
```
www.tiket.com/flight/DPS-MESC
```