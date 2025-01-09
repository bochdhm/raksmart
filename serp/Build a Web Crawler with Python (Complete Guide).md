
# Build a Web Crawler with Python (Complete Guide)

## Introduction

Web crawling is a powerful technique to automatically navigate through multiple URLs and collect large amounts of data. By crawling web pages, you can extract valuable information from various domains and analyze it for purposes such as price comparisons, indexing, and more.

Search engines like **Google**, **Yahoo**, and **Bing** heavily rely on web crawling to rank websites and suggest relevant search results to users. In this guide, we will explore:

1. The **difference between web scraping and web crawling**.
2. How to create a **basic web crawler** using Python libraries like `requests` and `BeautifulSoup`.
3. Building a **production-ready web crawler** with the Scrapy framework.

---

## What is Web Crawling?

Web crawling involves using an automated bot to visit multiple URLs on a website, downloading their HTML content, and parsing it to extract valuable data. The process starts with a **seed URL**, which acts as the entry point for the crawler. From there, links to other pages are discovered and visited recursively.

Common use cases for web crawling include:
- **Search Engine Indexing**
- **Price Comparison**
- **Monitoring Changes on Websites**

The extracted data can contain links to other pages on the same domain, enabling the crawler to navigate through an entire website. This recursive process allows it to gather comprehensive information.

---

## Web Crawling vs. Web Scraping

Though often used interchangeably, **web crawling** and **web scraping** are distinct:

- **Web Crawling**: Involves visiting multiple pages, following links recursively, and gathering data from an entire domain.
- **Web Scraping**: Focuses on extracting data from a single page without exploring additional links.

---

## Creating a Basic Web Crawler

We will start with a simple Python-based web crawler using the libraries `requests` and `BeautifulSoup`. This basic implementation will give you a solid understanding of web crawling fundamentals.

### Requirements

Before we begin, install the following libraries:
- `requests`
- `beautifulsoup4`

Both can be installed via `pip`:
```bash
pip install requests beautifulsoup4
```

Additionally, we’ll use the `urllib.parse` module from Python's standard library for URL handling.

### Code Example: Basic Crawler

Below is a Python script for a basic web crawler:

```python
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin

# URL of the website to crawl
base_url = "https://books.toscrape.com/"

# Set to store visited URLs
visited_urls = set()

# List to store URLs to visit next
urls_to_visit = [base_url]

# Function to crawl a page and extract links
def crawl_page(url):
    try:
        response = requests.get(url)
        response.raise_for_status()  # Raise an exception for HTTP errors

        soup = BeautifulSoup(response.content, "html.parser")
        
        # Extract links and enqueue new URLs
        links = []
        for link in soup.find_all("a", href=True):
            next_url = urljoin(url, link["href"])
            links.append(next_url)
        
        return links

    except requests.exceptions.RequestException as e:
        print(f"Error crawling {url}: {e}")
        return []

# Crawl the website
while urls_to_visit:
    current_url = urls_to_visit.pop(0)  # Dequeue the first URL

    if current_url in visited_urls:
        continue

    print(f"Crawling: {current_url}")

    new_links = crawl_page(current_url)
    visited_urls.add(current_url)
    urls_to_visit.extend(new_links)

print("Crawling finished.")
```

### How It Works:
1. **Fetch HTML Content**: The `requests.get()` method retrieves the HTML content of a page.
2. **Parse HTML**: `BeautifulSoup` is used to parse the content and extract links.
3. **Recursive Crawling**: Extracted links are visited recursively to crawl the entire site.

### Limitations:
- **No Parallelism**: Crawls pages sequentially, which can be slow for large websites.
- **Error Handling**: Basic exception handling is implemented but not comprehensive.
- **Lack of Scraping Logic**: While it crawls pages, it does not extract structured data.

---

## Advanced Web Crawling with Scrapy

To address the limitations of the basic crawler, we’ll use **Scrapy**, a powerful web scraping and crawling framework.

### Why Scrapy?
- Supports **parallelism** for faster crawling.
- Handles **errors** gracefully.
- Flexible and extensible for production-grade crawling and scraping.

### Installation

Install Scrapy using `pip`:
```bash
pip install scrapy
```

### Setting Up a Scrapy Project

Run the following command to create a new Scrapy project:
```bash
scrapy startproject learncrawling
```

This will generate a project folder structure. The most important directory is `spiders`, where we’ll define our custom crawlers.

### Creating a Scrapy Spider

Create a new file in the `spiders` directory (e.g., `crawling_spider.py`) and define the spider:

```python
from scrapy.spiders import CrawlSpider, Rule
from scrapy.linkextractors import LinkExtractor

class CrawlingSpider(CrawlSpider):
    name = "mycrawler"
    allowed_domains = ["toscrape.com"]
    start_urls = ["https://books.toscrape.com/"]

    # Define rules for crawling
    rules = (
        Rule(LinkExtractor(allow="catalogue/category")),
        Rule(LinkExtractor(allow="catalogue", deny="category"), callback="parse_item")
    )

    def parse_item(self, response):
        yield {
            "title": response.css(".product_main h1::text").get(),
            "price": response.css(".price_color::text").get(),
            "availability": response.css(".availability::text").get().strip()
        }
```

### Running the Spider

Run the following command to execute the spider:
```bash
scrapy crawl mycrawler
```

To save the scraped data to a JSON file:
```bash
scrapy crawl mycrawler -o results.json
```

---

## Handling Anti-Scraping Mechanisms

Many websites employ anti-scraping measures such as:
- **IP Blocking**
- **CAPTCHAs**
- **User-Agent Blocking**

To bypass these challenges, you can use **ScraperAPI** to manage proxies, retries, and headers seamlessly.

### Why Choose ScraperAPI?
1. **Automatic Proxy Rotation**: Avoid IP bans with a pool of rotating proxies.
2. **CAPTCHA Handling**: Automatically solve CAPTCHAs for uninterrupted scraping.
3. **Unlimited Bandwidth**: Scale your scraping operations without restrictions.

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Conclusion

In this guide, we explored the basics of web crawling and built a simple crawler using Python libraries. We then advanced to creating a robust, production-grade crawler using Scrapy. By leveraging tools like **ScraperAPI**, you can overcome challenges like IP bans and CAPTCHAs, making your crawling process faster and more efficient.

Start building your crawler today, and unlock the power of automated data collection!

👉 [Try ScraperAPI for free now!](https://bit.ly/Scraperapi)
