
# Instagram Crawler: A Complete Guide

## Introduction

Instagram Crawler is a powerful Ruby gem that allows you to download Instagram photos, posts, and videos with ease. This tool simplifies the process of crawling Instagram content and offers several features to enhance your downloading and logging experience.

[![Gem Version](https://badge.fury.io/rb/instagram-crawler.svg)](https://badge.fury.io/rb/instagram-crawler)  
[![Maintainability](https://api.codeclimate.com/v1/badges/a1625a5a812f515bdd91/maintainability)](https://codeclimate.com/github/mgleon08/instagram-crawler/maintainability)  
[![Build Status](https://travis-ci.org/mgleon08/instagram-crawler.svg?branch=master)](https://travis-ci.org/mgleon08/instagram-crawler)  
[![Coverage Status](https://coveralls.io/repos/github/mgleon08/instagram-crawler/badge.svg?branch=master)](https://coveralls.io/github/mgleon08/instagram-crawler?branch=master)  
[![Security](https://hakiri.io/github/mgleon08/instagram-crawler/master.svg)](https://hakiri.io/github/mgleon08/instagram-crawler/master)

---

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Instagram, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Features

- Download Instagram photos, posts, and videos.
- Show all file links for a given username.
- Filter downloads by date.
- Proxy support for safer crawling.
- Generate log files to track downloads.
- Docker compatibility for easy setup and usage.

---

## Installation

To install the Instagram Crawler gem, use the following command:

```bash
gem install instagram-crawler
```

## Setting Up Your Environment

To use the crawler, you need to set your Instagram `sessionid` as an environment variable:

```bash
export sessionid=[your_instagram_sessionid]
```

You can obtain the `sessionid` by inspecting your browser’s cookies when logged into Instagram.

---

## Getting Started

Here’s a quick demo of how Instagram Crawler works:

![Instagram Crawler Demo](https://rubydoc.info/gems/screenshots/instagram_crawler_demo.gif)

### Show All File Links

To show all file links for a given username, use:

```bash
instagram-crawler -u <user_name>
```

### Download Files After a Specific Date

To download files posted after a specific date (format: YYYYMMDD):

```bash
instagram-crawler -u <user_name> -d -a 20181120
```

### Download Files Before a Specific Date

To download files posted before a specific date:

```bash
instagram-crawler -u <user_name> -d -b 20181120
```

### Generate Log Files

To generate a log file during the download process:

```bash
instagram-crawler -u <user_name> -l
```

### Using Proxies

For added privacy and safety, Instagram Crawler supports proxy usage:

```bash
instagram-crawler -u <user_name> -P http://example.com -p 1234
```

### Help Menu

To view all available options and their descriptions, use the help command:

```bash
instagram-crawler -h
```

---

## Using Instagram Crawler with Docker

Instagram Crawler can also be run in a Docker container for an isolated and portable setup.

1. **Pull the Docker Image**  
   ```bash
   docker pull mgleon08/instagram-crawler
   ```

2. **Run the Container**  
   Replace `<sessionid>` with your session ID and `<user_name>` with the Instagram username:
   ```bash
   docker run -it --rm -v $PWD/instagram-crawler:/instagram-crawler -e sessionid=$sessionid --name crawler mgleon08/instagram-crawler -u <user_name> -a 20181124 -d -l
   ```

---

## Terms of Use

Please note the following restrictions from Instagram’s Terms of Use:

1. **You must not access Instagram's private API by any other means other than the Instagram application itself.**
2. **You must not crawl, scrape, or otherwise cache any content from Instagram, including but not limited to user profiles and photos.**

For more information, visit [Instagram Terms of Use](https://www.instagram.com/about/legal/terms/before-january-19-2013/).

---

## Contributing

This gem is open-source and available under the [MIT License](https://opensource.org/licenses/MIT). Contributions are welcome! Feel free to submit issues or pull requests on the [GitHub repository](https://github.com/mgleon08/instagram-crawler).

## Conclusion

Instagram Crawler is a straightforward yet powerful tool for downloading and managing Instagram content. With features like proxy support, date filtering, and Docker compatibility, it simplifies the task of crawling and organizing Instagram posts.

For large-scale scraping needs or to bypass complex anti-scraping mechanisms, consider using [ScraperAPI](https://bit.ly/Scraperapi) for effortless data extraction.

