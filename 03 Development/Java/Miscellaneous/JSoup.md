# Jsoup

## Overview

**Jsoup** is a Java library used for:

- **Web scraping** (extracting data from web pages)
    
- **Parsing and manipulating HTML**
    
- Reading and working with HTML content **without using a browser**
    

---

## 1. Setup

**Add the following Maven dependency:**

```xml
<dependency>
  <groupId>org.jsoup</groupId>
  <artifactId>jsoup</artifactId>
  <version>1.17.2</version> <!-- Latest as of mid-2025 -->
</dependency>
```

---

## 2. Fetch a Basic Web Page

```java
package org.adarsh;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;

public class Main {
    public static void main(String[] args) {
        String url = "https://books.toscrape.com/";
        try {
            Document doc = Jsoup.connect(url)
                .userAgent("Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36")
                .header("Referer", "https://google.com")
                .get();

            String title = doc.title();
            System.out.println("Title: " + title);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

- **Document**: Represents the full HTML document.
    
- **userAgent**: Pretends the request is from a real browser.
    
- **header**: Add optional headers like `Referer`.
    

---

## 3. Selecting Elements (CSS Selectors)

```java
Elements links = doc.select("a"); // All <a> tags
for (Element link : links) {
    System.out.println(link.text());        // Text of the link
    System.out.println(link.attr("href")); // URL of the link
}
```
- **`Element`** represents a single HTML tag or node from the parsed HTML document.

---
## Common CSS Selectors

| Selector    | Meaning                           |
| ----------- | --------------------------------- |
| `a`         | All `<a>` tags                    |
| `#id`       | Element with specific `id`        |
| `.class`    | Element with specific `class`     |
| `tag[attr]` | Element with a specific attribute |
| `div > p`   | `<p>` directly inside `<div>`     |

---

## 4. Example: Scrape News Headlines

```java
Document doc = Jsoup.connect("https://news.ycombinator.com")
    .userAgent("Mozilla/5.0")
    .get();

Elements headlines = doc.select(".titleline > a");

for (Element headline : headlines) {
    System.out.println("Title: " + headline.text());
    System.out.println("Link: " + headline.attr("href"));
}
```

---

## Important Tips

- **Always use a User-Agent**: Some websites block unknown/bot requests.
    
- **Respect `robots.txt`**: Not all sites allow scraping.
    
- **Avoid spamming**: Add a delay between requests (`Thread.sleep(...)`).
    

---

## Advanced Usage

### 1. Simulate Login with POST Request

```java
Connection.Response loginResponse = Jsoup.connect("https://example.com/login")
    .data("username", "yourUsername")
    .data("password", "yourPassword")
    .method(Connection.Method.POST)
    .userAgent("Mozilla/5.0")
    .execute();

// Save session cookies
Map<String, String> cookies = loginResponse.cookies();

// Use cookies to access authenticated page
Document dashboard = Jsoup.connect("https://example.com/dashboard")
    .cookies(cookies)
    .userAgent("Mozilla/5.0")
    .get();

System.out.println(dashboard.title());
```

> Use browser dev tools (Inspect → Network tab → Login request) to inspect form fields and request URLs.

---

### 2. Add Headers and Cookies Manually

```java
Document doc = Jsoup.connect("https://example.com")
    .header("User-Agent", "Mozilla/5.0")
    .header("Accept", "text/html")
    .cookie("sessionid", "abc123xyz")
    .get();
```

Use this when:

- Pages require login/session tracking
    
- You are being blocked and need to simulate real requests
    

---

### 3. Scraping Paginated Data

```java
for (int i = 1; i <= 5; i++) {
    String url = "https://example.com/page=" + i;
    Document doc = Jsoup.connect(url)
        .userAgent("Mozilla/5.0")
        .get();

    Elements items = doc.select(".product-title");
    for (Element item : items) {
        System.out.println(item.text());
    }

    Thread.sleep(1000); // Delay between requests
}
```

---

### 4. When Jsoup Is Not Enough (Dynamic Content)

Jsoup **cannot render or execute JavaScript**. It can only parse static HTML.

Use **Selenium** or browser automation tools when:

- Data loads dynamically via JS/AJAX
    
- The site is built using frameworks like React, Angular, Vue
    

Example: Sites like Flipkart, Instagram, or Twitter often require Selenium.

---

## Practice Project Ideas

| Project                                    | Concepts Practiced            |
| ------------------------------------------ | ----------------------------- |
| Scrape Flipkart product data               | CSS Selectors, pagination     |
| Automate login and scrape user dashboard   | POST request, session cookies |
| Collect news headlines from multiple pages | Pagination, selectors         |
| Scrape job listings from a portal          | Structured data parsing       |

---