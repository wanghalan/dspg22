---
permalink: /product-innovation/
title: Product Innovation
layout: single
toc: true
toc_label: Product Innovation
toc_sticky: true
---

## Stakeholder(s)
Gary Andersen, National Center for Science and Engineering Statistics ([NCSES](https://ncses.nsf.gov/)) 

## Abstract
The Product Innovation project is a proof-of-concept toolkit that aims to track innovation activities sustainably using
[opportunity data](https://hdsr.mitpress.mit.edu/pub/hnptx6lq/release/10). The toolkit accelerates [Really Simple Syndication (RSS)](https://en.wikipedia.org/wiki/RSS) queries and news source text extraction using open-source modules and browser automation. The collected texts are then piped to natural language processing (NLP) modules that detect business, product, and innovation status.

## Introduction
Project started with the idea the the NCSES has a Business Research and Discovery Innovation Survey (BRDIS) Survey. They wanted us to explore alternative sources of data, to complement the findings of the survey with possibly more detail such as the name of the innovative product. In the process of looking for this data source, we realized that most sources were impracticel and expensive to access. This sourcing of data becomes a challenge for most researchers, and we began to think about possible alternatives through which we can obtain data in a free and open-source way. During the 2022 summer of the DSPG internship, we were able to make some progress towards this aim.

## Method
<img src="https://lucid.app/publicSegments/view/e1fac901-5124-444a-9fbd-d051a79b5469/image.png" alt="">
We created two modules, the **rss-get** module, and the **news-get** module. We separate these because extracting information from news sites take a varying amount of time.
- Using open source news source extractors:
  - [Newspaper3k](https://newspaper.readthedocs.io/en/latest/)
  - [Sumy](https://github.com/miso-belica/sumy)
- Approach is publisher friendly (lowest severity)

## Evaluation
We utilize a set of pharmaceutical key words as found on the NAICS website.

## Results
We extracted a set of source text and appended it to the url retrieved and made a dataset. Out of these urls, more than 80% of the data can be retrieved simply using ```get```.

## Future Work
The other steps to improve this system

## Broader Impacts
- News articles are rich sources of data that with the rise of natural language models, can be used to benefit government organizations?
- Allow for opportunity data in the form of news to be accessible to researchers
- Encourages research reproducibility

## Contact
- Alan Wang (alanwang@virginia.edu)
- Steve Zhou (wz8ry@virginia.edu)
- Neil Kattampallil (nak3t@virginia.edu)
