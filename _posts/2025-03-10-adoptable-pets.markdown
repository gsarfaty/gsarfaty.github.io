---
layout: post
title: Exploring Montgomery County's Adoptable Pets
date: 2025-03-10
description: Pulling data from data.gov on adoptable pets, in MoCo, MD and visualizing. # Add post description (optional)
img: zero-dog.jpg # Add image post (optional)
fig-caption: Meet Zero! A 7 year old pit mix who was among those availble at the time of the data pull # Add figcaption (optional)
tags: [API,keyring,purr,json,opendata,ggplot]
---
For this exercise, I decided to mix my passions: dogs and data! I went to <a href="https://catalog.data.gov/" target="_blank">data.gov</a> and  saw that Montgomery County, Maryland had data on their currently available adoptable pets. It was a match made in heaven.

## Pulling data into R from the API & preparing for analysis
In order to pull data from the data.gov API you have to first request an <a href="https://api.data.gov/signup/" target="_blank">API Key.</a> Once I had a key, I stored it securely in my code using keyring. I was then able to make a query, and extract the content of that query. The data were in a nested list format, which if you've not encountered before can take some getting used to. I was able to leverage the purr package to get the data in a tidy format. I added some API and nested list resources that I found helpful to the <a href="https://github.com/gsarfaty/playground/wiki/Resources" target="_blank">wiki</a> of my repo, lovingly named "playground."


-  **Raw input data:** The data were sourced from Montgomery County MD via data.gov <a href="https://catalog.data.gov/dataset/adoptable-pets" target="_blank">here</a>.
-  **Processed output data:** The tidy data output was stored <a href="https://github.com/gsarfaty/playground/blob/main/Dataout/2025-03-02_AdoptablePets.csv" target="_blank">here</a>.
-  **My code:** My code for this project is <a href="https://github.com/gsarfaty/playground/tree/main/Scripts/Adoptable_Pets" target="_blank">here</a>


## Key questions & their answers visualized

### 1. What kinds of animals are available for adoption?

Somewhat unsurprisingly, most of the available pets were dogs. But there were a few birds and other animals available too. 

![Adoptable animals](https://raw.githubusercontent.com/gsarfaty/playground/main/Images/MD_County_AdoptablePets_Animal_Type.png)

### 2. Which days are most popular, or unpopular, for pet intake?

Normally, I would sort a bar chart by something meaningful like the volume, but as humans I think we are accustomed to seeing the days of the week in the order that they occur so I made the choice to order them chronologically. My initial assumption was that weekends would be the most popular but Tuesday was actually the most common intake day (for those animals that were at the shelter at the time of the data pull), with volume high Fri, Sat, Mon and Tues. Wednesday turned out to be the least popular day for surrender or intake.

![Intake Days](https://raw.githubusercontent.com/gsarfaty/playground/main/Images/MD_County_AdoptablePets_Popular_Intake_Days.png)


### 3. Which dog breeds are a surrendered by their owners most?
I was then curious which dog breeds made up the highest proportion of those available. This was a fun opportunity to do a waffle chart! And, I found that just over 70% of the available dogs were pit bulls or pit bull mixes.  

![Dog Breeds](https://raw.githubusercontent.com/gsarfaty/playground/main/Images/MD_County_AdoptablePets_DOG_BREEDs.png)


### 4. How old are the available dogs?
Next, my thought was about how old the dogs were. Are they older dogs or were pets being surrendered or found as younger animals? Approaching this question took some data cleaning because the dataset provided was **MESSY.** The column for pet age had both numeric and text values AND had multiple units both months and years. Yikes.

<img src="/assets/img/dog-ages-messy.png"> 

To address this, I extracted the values before the word months and the values before the word years and made columns for these respectively. I then made a total months column along with a total years column that converted total months to years.

<img src="/assets/img/dog-ages-clean.png">

Once I had the total years column created, I was able to assess the age of each dog. The average age of the dogs was about 3 years old, but there were some outliers, especially among the pit/pit mixes with a dog as old as 12.

![Dog Ages](https://raw.githubusercontent.com/gsarfaty/playground/main/Images/MD_County_AdoptablePets_DOG%20AGES_BoxPlot.png)