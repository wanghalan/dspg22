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

## Background
Previous works have used innovation indicators based on website information [^1]. 

[^1]: Axenbeck, Janna, and Patrick Breithaupt. "Innovation indicators based on firm websites—Which website characteristics predict firm-level innovation activity?." PloS one 16, no. 4 (2021): e0249583.

## Method
<img src="/assets/img/product-innovation_system-overview.svg" alt="Product innovation System Overview">

We created two modules, the **rss-get** module, and the **news-get** module. We separate these because extracting information from news sites take a varying amount of time.

### Search Engine Comparison
To find rss feeds, we looked towards some of the most popular search engines with the following two criteria: 1) the search engine should have keyword search capabilities, and 2) the rss should return a sentence snippet. We compiled the results of our search in following table:

|**Source**|**Type**|**Keyword**|**Snippet**|**Notes**|
|--|--|--|--|--|
|[Google](https://news.google.com/rss/search?q={0})|Search Engine|Y|Y|<ul><li>Successful RSS keyword extraction using: https://news.google.com/rss/search?q={0}</li><li>Column _summary_detail.value_ might contain one sentence description of the news</li></ul>|
|[Bing](https://www.bing.com/news/search?q={0}&format=rss)|Search Engine|Y|Y|<ul><li>Successful RSS keyword extraction using: https://www.bing.com/news/search?q={0}&format=rss</li><li>Column _summary_detail.value_ might contain 2-3 sentences of the news </li></ul>|
|[Baidu](?)|Search Engine|N|N|<ul><li>We found a website https://www.baidu.com/search/rss.html that seems to describe the existance of rss functioning. However, upon clicking into the keyword search field, I kept being returned the same news in non-RSS format</li></ul>|
|[Yahoo News](https://news.yahoo.com/rss)|News Channel|N|N|<ul><li>Does not seem to allow keyword searches. If you do a yahoo search with news it automatically returns search.yahoo.com.</li><li>You can manipulate the [URL](https://news.search.yahoo.com/search;_ylt=A2KIbMuIVJpipzUAhiNXNyoA;_ylu=Y29sbwNiZjEEcG9zAzEEdnRpZAMEc2VjA3Nj?p={KEYWORD}&fr=news) to do news page sources, but it does not seem like they will convert it into an RSS format for us </li></ul>
|[Yandex](https://yandex.com/)|Search Engine|N|N|<ul><li>robots.txt disallows /company/*.rss, /company/search. Returns results in Russian?</li><li>Upon searching [sitemaps](https://yandex.com/support/sitemap.xml), found an rss source at [https://zen.yandex.ru/](https://zen.yandex.ru/search?query={0}). However, to subscribe to any of the feeds require signing in</li></ul>|
|[Ask](https://www.ask.com/rss)|Search Engine|N|Y| <ul><li> Found https://www.ask.com/rss, but so far haven't found a way to add a keyword. </li> <li> Looked through: https://www.ask.com/sitemap_index.xml and https://www.ask.com/robots.txt but did not find anything rss-related</li><li>Column _metadescription_ contains 2 sentences </ul>|
|[ABC News](https://abcnews.go.com)|General Media|Y|N|<ul><li>Does not have usable rss feed. Web scraping with keyword search is possible, but most of the content seems to be videos without transcript.</li></ul>
---

### Source Text Extraction
Once we found a rss-feed search the avails us keywords and snippets, we realized that the snippets we find are mostly 1-2 sentences, which is less than the 3 we hoped that would allow us to run the Natural Language Processing (NLP) more effectively. As a result, we started to investigate the retrieval of source text directly.

#### Text Summarizer Comparison
In order to see which summarizers are the most effective, we manually checked a sample of the following news articles: [bloomberg](https://www.bloomberg.com/news/newsletters/2022-06-07/apple-s-troubles-in-china-aren-t-going-away-quickly), [usatoday](https://www.usatoday.com/story/tech/2022/06/06/wwdc-22-apple-pay-buy-now-pay-later/7534225001/), [reuters](https://www.reuters.com/markets/stocks/australias-bnpl-stocks-wilt-after-apple-announces-entry-2022-06-07/), [forbes](https://www.forbes.com/sites/davidphelan/2022/05/13/apple-iphone-15-insider-leaks-astonishing-design-change/), [appleinsider](https://appleinsider.com/articles/22/05/15/ios-16-will-have-refreshed-apple-apps-but-look-the-same).

For the following extractors:
  - [Newspaper3k](https://github.com/codelucas/newspaper), "News, full-text, and article metadata extraction in Python 3"
  - [Article Parser](https://github.com/myifeng/article-parser), "Extract article or news by url or html, parse the title and content, output in markdown format"
  - [Sumy](https://github.com/miso-belica/sumy), "Simple library and command line utility for extracting summary from HTML pages or plain texts"

The goal of the comparison is to elucidate common ways an extraction might fail more than using them as a metric for the efficacy of our extractor. We summarize our lessons below:

|**Package**|**Article**|**Status**|**Notes**|
|--|--|--|--|
|Newspaper3k| bloomberg | <span style="color:red"> Failed </span>| article.text returns a response: "Why did this happen? Please make sure your browser supports JavaScript and cookies and that you are not blocking them from loading. For more information you can review our Terms of Service and Cookie Policy." Likely additional work needs to be done in order to extract this data |
||usatoday|Passed|While the extraction has worked successfully, the parser cannot easily discern between the genuine article or the ads for different articles embedded|
---


#### Severity Levels
During our investigation, we realized that news sources have a varying degree of "friendliness" to being scraped. In other words, some websites intentionally resist source text from being extracted. We introduced the concept of _severity_ to our system so that we can navigate spending more computational power in order to access these more difficult websites. During our search, however, we realized that more than 80% of the websites are retrievable using the lowest severity level (a simple HTTP GET request was sufficient to retrieve the source text). To not cause undue burden to the content hosts, we did our evaluation of the system using only severity 0 source text. An example of a higher severity text extraction would be using Selenium to automate a browser and wait for specific CSS signatures to access the website.

## Evaluation
In order to evaluate our methods, we mind a set a pharmaceutical keywords directly from the NAICS website.

### Keyword Mining
Based on ```rss-get``` and the set of keywords, we arrived a set of the following articles:

[Plot of the articles per keywords here]

### NLP
Based on prior work from Neil, we did some things...

## Results
We extracted a set of source text and appended it to the url retrieved and made a dataset. Out of these urls, more than 80% of the data can be retrieved simply using [http get](https://www.w3schools.com/tags/ref_httpmethods.asp).

## Future Work
The other steps to improve this system

## Broader Impacts
- News articles are rich sources of data that with the rise of natural language models, can be used to benefit government organizations?
- Allow for opportunity data in the form of news to be accessible to researchers
- Encourages research reproducibility

## Contact
- Alan Wang (ahw9f@virginia.edu)
- Steve Zhou (wz8ry@virginia.edu)
- Neil Kattampallil (nak3t@virginia.edu)

---
