---
layout: page
title: Tech Stacks
nav_order: 2
---

# Tech Stacks

## System Components 

![System Component](assets/images/system-component.png)
{: .prop}

HotstoneSEO consists of the following components:

- **HotStone**
  - **UI** : Dashboard which allow users to configure HotStone (rule, datasource, etc)
  - **Server** : Backend of **UI** to manage data
  - **Provider** : API backend of **HotStone Client** providing rule matching and retrieving tags data
- **HotStone Client** : Javascript library used by SSR web app to interact with **Provider**