---
title: "Product Innovation"
layout: single
toc: true
---


## Abstract
The Product Innovation project is a proof-of-concept toolkit that aims to enable the [North
American Industry Classification System (NAICS)](https://www.census.gov/naics/#:~:text=The%20North%20American%20Industry%20Classification,to%20the%20U.S.%20business%20economy.) to track innovation activities sustainably using
[opportunity data](https://hdsr.mitpress.mit.edu/pub/hnptx6lq/release/10). The toolkit accelerates [Really Simple Syndication (RSS)](https://en.wikipedia.org/wiki/RSS) queries and news
source text extraction using open-source modules and browser automation. The collected texts
are then piped to natural language processing (NLP) modules that detect business, product,
and innovation status.

## Introduction

## Method
<img src="https://lucid.app/publicSegments/view/e1fac901-5124-444a-9fbd-d051a79b5469/image.png" alt="">
We created two modules, the **rss-get** module, and the **news-get** module. We separate these because extracting information from news sites take a varying amount of time.

### Evaluation
We utilize a set of pharmaceutical key words as found on the NAICS website.

## Results
We extracted a set of source text and appended it to the url retrieved and made a dataset. Out of these urls, more than 80% of the data can be retrieved simply using ```get```.

## Contact
- Alan Wang (alanwang@virginia.edu)
- Steve Zhou (wz8ry@virginia.edu)
- Neil Kattampallil (nak3t@virginia.edu)
