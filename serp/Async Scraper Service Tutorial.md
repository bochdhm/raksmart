
# Async Scraper Service Tutorial

## Introduction

ScraperAPI's new **Async Scraper endpoint** allows you to submit web scraping jobs at scale without worrying about timeouts or retries. The scraped data is sent directly to your webhook endpoint, making your scrapers more resilient even when dealing with complex anti-scraping systems.

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. 👉 [Start your free trial today!](https://bit.ly/Scraperapi)

---

## Asynchronous vs. Synchronous Scraping API

The primary difference between asynchronous and synchronous APIs lies in how requests are handled and when the data is returned.

- **Synchronous API**: Returns data immediately after the request. While faster, it might reduce the success rate for complex websites due to timeout issues or retries.
- **Asynchronous API**: Does not wait for the response. It submits multiple requests at once and processes them in the background, offering better success rates for difficult-to-scrape websites.

Using an asynchronous scraping API, you can scale up requests while giving the service more time to employ advanced anti-scraping bypass methods.

---

## When to Use the Async Scraper API

Use the **Async Scraper API** in the following scenarios:

1. **High success rate** is more important than fast response time.
2. Requests to certain websites are experiencing low success rates.
3. Scraping difficult or heavily protected websites.
4. Sending a massive volume of scraping requests simultaneously.

---

## Getting Started with ScraperAPI’s Async Scraper

### Submitting a Job

Here’s how to submit a scraping job using Python and the **Async Scraper endpoint**:

```python
import requests

url = "https://quotes.toscrape.com/"
api_key = "Your_API_KEY"

response = requests.post(
    url="https://async.scraperapi.com/jobs",
    json={"apiKey": api_key, "url": url}
)

print(response.json())
```

**Response Example:**
```json
{
  "id": "222cdaa5-efd1-4962-ad6c-c51e2eea59b7",
  "status": "running",
  "statusUrl": "https://async.scraperapi.com/jobs/222cdaa5-efd1-4962-ad6c-c51e2eea59b7",
  "url": "https://quotes.toscrape.com/"
}
```

---

### Checking Job Status

To check the status or retrieve results of a submitted job, use the `statusUrl` provided in the response:

```python
status_url = "https://async.scraperapi.com/jobs/222cdaa5-efd1-4962-ad6c-c51e2eea59b7"
response = requests.get(status_url)

print(response.json())
```

- If the job is still running:
```json
{
  "status": "running"
}
```

- Once the job is completed:
```json
{
  "status": "finished",
  "response": {
    "headers": {
      "content-type": "text/html; charset=utf-8"
    },
    "body": "<html>...</html>"
  }
}
```

---

### Parsing the Response Data

Once you receive the response, you can parse the HTML body using Beautiful Soup to extract the desired data.

```python
import requests
from bs4 import BeautifulSoup

status_url = "https://async.scraperapi.com/jobs/222cdaa5-efd1-4962-ad6c-c51e2eea59b7"
response = requests.get(status_url)
data = response.json()

soup = BeautifulSoup(data["response"]["body"], "html.parser")
quotes = soup.find_all("div", class_="quote")

for quote in quotes:
    print(quote.find("span", class_="text").text)
```

---

## Submitting Scraping Jobs in Bulk

For larger scraping tasks, you can use the `batchjobs` endpoint to submit multiple URLs simultaneously.

```python
import requests

urls = [f"https://quotes.toscrape.com/page/{i}/" for i in range(1, 11)]
api_key = "Your_API_KEY"

response = requests.post(
    url="https://async.scraperapi.com/batchjobs",
    json={"apiKey": api_key, "urls": urls}
)

print(response.json())
```

This approach allows you to process a large list of URLs efficiently.

---

## Advanced Functionalities of ScraperAPI

ScraperAPI offers additional features to enhance the Async Scraper's capabilities:

### Geo-Sensitive Scraping

For websites that show different data based on geolocation, add the `country_code` parameter to send requests from specific countries.

```json
{
  "apiKey": "Your_API_KEY",
  "apiParams": {
    "country_code": "us"
  },
  "url": "https://example.com"
}
```

### JavaScript Rendering

For websites that require JavaScript to load content, set `render` to `true` in your API parameters.

```json
{
  "apiKey": "Your_API_KEY",
  "apiParams": {
    "render": true
  },
  "url": "https://example.com"
}
```

### Full Parameter List

Here’s a list of parameters you can use with the Async Scraper:

```json
{
  "apiKey": "Your_API_KEY",
  "apiParams": {
    "autoparse": false,
    "binary_target": false,
    "country_code": "us",
    "device_type": "desktop",
    "follow_redirect": false,
    "premium": true,
    "render": false,
    "retry_404": false
  },
  "url": "https://example.com"
}
```

---

## Conclusion

The **Async Scraper API** is a game-changer for large-scale and complex scraping tasks. With features like webhook integration, geo-sensitive scraping, and JavaScript rendering, it simplifies the process of extracting data from difficult-to-scrape websites.

Get started today and experience hassle-free scraping at scale. 👉 [Start your free trial now!](https://bit.ly/Scraperapi)
