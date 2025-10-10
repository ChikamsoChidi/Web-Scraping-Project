# ✂️ Squire Barber Shop Data Scraper (UK)

###  Project Overview

This project is a dedicated web scraping solution designed to systematically extract location and contact information for barber shops listed on the **getsquire.com/discover/united-kingdom** marketplace. Utilizing the **Selenium** framework, the script navigates the UK-based discovery pages to gather data from individual city listings, ultimately compiling a comprehensive dataset for market analysis.

###  Objective

The primary goal is to collect structured data for all accessible barber shops across the United Kingdom listed on the Squire platform. This data can be utilized for:

* **Market Analysis:** Understanding geographical distribution and concentration of Squire-listed shops across UK provinces and cities.
* **Business Intelligence:** Informing strategy development, target marketing, or competitive analysis.
* **Data Science:** Serving as a clean dataset for further data processing or machine learning tasks.

###  Technology Stack

| Component | Library/Tool | Purpose |
| :--- | :--- | :--- |
| **Scraping Engine** | `selenium` | Browser automation for dynamic content loading and navigation. |
| **Data Handling** | `pandas` | Structuring, cleaning, and exporting the extracted data. |
| **Driver** | `webdriver (Chrome)` | The browser interface used by Selenium to execute the scraping logic. |
| **Utilities** | `time`, `WebDriverWait` | Managing explicit waits and synchronizing the script with page loading. |

###  How the Script Works (Process Breakdown)

The Python notebook executes a four-phase scraping process:

1.  **Initialization and Navigation:**
    * The script initializes a Chrome WebDriver instance.
    * It navigates to the main UK discovery page: `https://getsquire.com/discover/united-kingdom`.
    * An explicit wait is used to ensure the main content (province listings) is fully loaded.

2.  **Province and City Discovery:**
    * It identifies the major UK provinces (`England`, `Scotland`, `Northern Ireland`, `Wales`) using `h3` tags.
    * For each province, it extracts a list of all available cities.
    * A custom function (`city_url`) is used to construct the direct, crawlable URL for each city (e.g., `.../england/london`).

3.  **Data Extraction Loop:**
    * The script iterates through the list of generated city URLs.
    * For each city URL, it waits for the shop listing "cards" (`data-automationid='shopcard'`) to become visible.
    * A `parser` function then extracts the following data points for **each barber shop card**:
        * `Name` (`<h2>` tag)
        * `Address` (`<p>` tag)
        * `Link` (`<a>` tag `href` attribute)
        * `City` (derived from the URL) [cite: user_uploaded
