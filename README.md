---
layout: post
title: "IP Geo-Heatmap with Python"
date: 2021-01-19 19:41:30 -0800
categories: python networking heatmap

---

## Overview

A lot of different things can be readily prototyped and done with Python, particularly because of the massive communities behind all of it's packages.

In this article I'll be explaining how to setup a quick python environment, install everything we need with PIP and finally create a simple application with Python + Folium + Flask that shows us a webpage with a navigateable map of earth with heatmaps of IP addresses we have.

Note: I'll be doing all most of the setup through a linux terminal, but you can follow along with [Jupyter Notebooks](/python/jupyter_notebooks_) if you prefer.

## Use Cases

Maybe you want to analyze malware and see all of the targets that it's trying to connect to and attack.

Maybe you want to see where the vast majority of your clients are connecting to your servers from.

Maybe you just like generating maps from meaningless data.

## Setup

Create a project folder and navigate into it

```bash
mkdir ip_heatmap
cd ip_heatmap
```

Create a virtual environment and activate it (explanation [here](/blog/python/virtual_environments_))

```bash
python3 -m venv .env
```

Install all necessary modules

```bash
pip install folium flask ...
```

## List of IP Addresses

Maybe you work in a field where it is possible for you to harvest a large amount of valid IP addresses and create this heat map from real data. I was looking into some malware samples, but I still couldn't find a satisfyingly large enough list of IP addresses to make this map interesting looking.

So I had to generate a bunch of my own fake addresses, so the following script will do that for you. Alternatively you can download a list of IP addresses I already generated from [here]({{ site.baseurl }}{% link /assets/iplist.txt %}).

```python
import random

# Declare Constants
EXPORT_FILE = "iplist.txt"
IP_NUMBERS = 1000

# Generate unique IP addresses
ip_list = []
for i in range(0, IP_NUMBERS):
    new_ip = "%d.%d.%d.%d." % (random.int(0,255), random.int(0,255), random.int(0,255), random.int(0,255))
    if new_ip not in ip_list:
        ip_list.append(new_ip)

# Write generate IP addresses to file
with open(EXPORT_FILE, 'w') as f:
    f.write('\n'.join(ip_list))
```

## Requesting Geo-Information for an IP address

The next thing we need to do - after reading each ip address - is to request geographical information about said IP address.

```python
import ...
```
