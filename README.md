# Actor - Google Search Scraper

## Google Search scraper

Since Google Search doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Google Search data scraper supports the following features:

-   Unlock Comprehensive Search Results - Gather every search result from Google, unfiltered and exhaustive.

-   Maximize Your Data Collection - Collect an extensive range of search results, including both organic and paid listings, with precision and efficiency.

-   Global Insights, Local Focus - Customize search results by country and language with ease, ensuring your data reflects the global and local perspectives you need.

-   Precision Location-Based Insights - Gather results for a specific location - down to the street level. Refine your search intelligence and understand how information varies across geographies.

-   Unleash the Power of "People Also Ask" - Discover related queries and expand your search intelligence, gaining deeper insights into user intent and content opportunities.

-   Expand Insights with Related Queries - Unlock valuable search trends and user interests with our feature to retrieve "Related Queries." Gain a deeper understanding of search intent and uncover hidden opportunities for your business or research.

-   Effortless Google Search Mastery - Harness the full potential of Google search, effortlessly retrieving the data you need to inform your strategies and decisions.

-   Data in Your Preferred Format - Export results in XML, JSON, CSV, or Excel, your choice! Tailor your data output to match your analysis and reporting needs effortlessly.


## Bugs, fixes, updates, and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/google-search-scraper/issues).


## Input Parameters

The input of this scraper should be JSON containing the list of pages on Google Search that should be visited. Required fields are:

- `startUrls`: (Optional) (Array) List of Google Search URLs. You should only include search URLs. It must be used if `queries` parameter is not used.

- `queries`: (Optional) (Array) Keywords you want to search on Google. It must be used if `startUrls` parameter is not used.

- `countryCode`: (Optional) (String) This option determines the Google search domain by the country code. It only applies to the search queries.

- `languageCode`: (Optional) (String) This option determines the language of the Google search results which is passed to Google Search as the `hl` URL query parameter.

- `locationUule`: (Optional) (String) The code for the exact location for the Google search. It's passed to Google Search as the uule URL query parameter. You can use the UULE code generator https://padavvan.github.io/.

- `maxItems`: (Optional) (Integer) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `resultsPerPage`: (Optional) (String) Number of search results for each Google result page. By default, Google Search returns 10 results per page. The allowed values are 10, 20, 30, 40, 50 and 100.

- `includeUnfilteredResults`: (Optional) (Boolean) If checked, the lower-quality results that Google normally filters out will be included. This usually consists of a few hundred extra results.

- `endPage`: (Optional) (Integer) The page number that you want to end with. By default there is no end page. This is applies to all search requests and startUrls individually.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as an argument and returns an object with data.

- `customMapFunction`: (Optional) (String) Function that takes each object's handle as an argument and returns the object with executing the function.

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that is explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor is optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detailed requests. If the actor doesn't block very often it'll scrape 100 listings in 2 minutes with ~0.04-0.45 compute units.

### Google Search Scraper Input example

```json
{
  "queries":[
    "sculpture"
  ],
  "endPage":2,
  "maxItems": 10,
  "startUrls":[
    "https://www.google.com/search?q=fitness"
  ],
  "countryCode": "us",
  "languageCode": "tr",
  "locationUule":"w+CAIQICIIaXN0YW5idWw=",
  "resultsPerPage":"20",
  "includeUnfilteredResults": true,
  "proxy":{
    "useApifyProxy":true
  }
}

```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with a failure state and output an explanation of what is wrong.

## Google Search Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any language (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Google Search actor.

## Scraped Google Search Properties

The structure of each item in Google Search looks like this:

### Item Detail

```json
{
	"url": "https://google.com/search?q=sculpture&gl=us&num=20&hl=tr&filter=0&uule=w%2BCAIQICIIaXN0YW5idWw%3D",
	"name": "sculpture - Google'da Ara",
	"paidResults": [
		{
			"title": "Steel Sculpture Manufacturer - Fabrication for World Sculptor",
			"url": "https://www.sinosculpture.com/case/stainless-steel-sculpture/LOVEME-MEXICO.html",
			"displayedUrl": "https://www.sinosculpture.com",
			"description": "Steel Sculpture Manufacturer - Fabrication for World Sculptorsinosculpture.comsinosculpture.comProviding fabrication, 3D modeling, mirror polishing for contemporary art metal sculpture. Installed in USA, UK, Singapore, Italy, UAE, Thai etc. for world sculptor and architect.",
			"siteLinks": [
				{
					"title": "Custom for Sculptor",
					"url": "https://www.sinosculpture.com/video/intl_report/"
				},
				{
					"title": "3D Tech Assistance",
					"url": "https://www.sinosculpture.com/service/"
				},
				{
					"title": "Superb Mirrored Sculpture",
					"url": "https://www.sinosculpture.com/case/stainless-steel-sculpture/"
				},
				{
					"title": "Sky mirror polish",
					"url": "https://www.sinosculpture.com/video/latest_program/"
				}
			],
			"type": "paid"
		}
	],
	"organicResults": [
		{
			"title": "Sculpture - Tate",
			"url": "https://www.tate.org.uk/art/art-terms/s/sculpture#:~:text=Three%2Ddimensional%20art%20made%20by,carving%2C%20modelling%2C%20casting%2C%20constructing",
			"displayedUrl": "https://www.tate.org.uk › art › art-terms › sculpture",
			"description": "",
			"siteLinks": [],
			"type": "organic",
			"position": 1
		},
		{
			"title": "Sculpture - Tate",
			"url": "https://www.tate.org.uk/art/art-terms/s/sculpture#:~:text=Three%2Ddimensional%20art%20made%20by,carving%2C%20modelling%2C%20casting%2C%20constructing",
			"displayedUrl": "https://www.tate.org.uk › art › art-terms › sculpture",
			"description": "",
			"siteLinks": [],
			"type": "organic",
			"position": 2
		},
		{
			"title": "Sculpture",
			"url": "https://en.wikipedia.org/wiki/Sculpture",
			"displayedUrl": "https://en.wikipedia.org › wiki",
			"description": "Sculpture is the three-dimensional art work which is physically presented in the dimensions of height, width and depth. It is one of the plastic arts. Durable ...",
			"siteLinks": [
				{
					"title": "Bronze sculpture",
					"url": "https://en.wikipedia.org/wiki/Bronze_sculpture"
				},
				{
					"title": "Classical sculpture",
					"url": "https://en.wikipedia.org/wiki/Classical_sculpture"
				},
				{
					"title": "Architectural sculpture",
					"url": "https://en.wikipedia.org/wiki/Architectural_sculpture"
				},
				{
					"title": "Butter sculpture",
					"url": "https://en.wikipedia.org/wiki/Butter_sculpture"
				}
			],
			"type": "organic",
			"position": 3
		}
	],
	"relatedQueries": [
		{
			"title": "Sculpture Parfüm",
			"url": "https://www.google.com/search?num=20&sca_esv=566249636&gl=us&hl=tr&q=Sculpture+Parf%C3%BCm&sa=X&ved=2ahUKEwimltiyg7SBAxXStTEKHZn7CIUQ1QJ6BQiAARAB"
		},
		{
			"title": "Sculpture art",
			"url": "https://www.google.com/search?num=20&sca_esv=566249636&gl=us&hl=tr&q=Sculpture+art&sa=X&ved=2ahUKEwimltiyg7SBAxXStTEKHZn7CIUQ1QJ6BQiBARAB"
		}
	],
	"searchQuery": {
		"query": "sculpture",
		"countryCode": "us",
		"languageCode": "tr",
		"resultsPerPage": "20",
		"domain": "google.com",
		"locationUule": "w+CAIQICIIaXN0YW5idWw="
	}
}
```

## Contact
Please visit us through [epctex.com](https://epctex.com) to see all the products that are available for you. If you are looking for any custom integration or so, please reach out to us through the chat box in [epctex.com](https://epctex.com). In need of support? [devops@epctex.com](mailto:devops@epctex.com) is at your service.
