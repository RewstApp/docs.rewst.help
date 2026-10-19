---
title: Untitled
---

<details>

<summary>Parse XML action</summary>

The Core Parse XML action in Rewst is designed to locate and extract specific elements or data from XML documents. This powerful tool, backed by an efficient Python library, facilitates precise data extraction from XML files, simplifying the process of parsing complex data structures. For additional understanding on XPath expressions, refer to this [w3schools article](https://www.w3schools.com/xml/xpath_intro.asp).

**Use cases**

Consider using the Parse XML action in these scenarios:

* **Data Extraction and Content Clean-Up:** Capture specific information or filter out necessary data from XML-formatted content. This is particularly useful in processing responses from HTTP requests or handling complex XML documents.
* **Web Scraping:** Automate the extraction of specific information from various XML sources using defined tags, attributes, or identifiers. It enables you to precisely target the data you need from web resources.

**Parameters**

* **XML**: The XML content that needs to be parsed. This could be XML content from an API response, obtained using the HTTP Request Core Action.
* **Attributes**: (Optional) Allows you to find XML elements based on their attribute key.
* **ID**: (Optional) Permits searching for XML elements based on their ID attribute.
* **Selector**: Determines the operation type. Options include:
  * find: Returns only the first instance of the defined XML tag.
  * find\_all: Returns all instances of the defined XML tag.
  * select: Enables the use of XPath expressions for nested XML tags or conditional searches.
* **String**: (Optional) Allows you to search for specific text within the XML content.
* **Value**: Specifies the tag or selector to search for in the XML content.

**Output**

* An array of matching string values is returned.

**Practical Use Case: Extracting Books from a Bookstore's XML Data**

Before diving into parsing XML data, you'll need to fetch the XML file. In this use case, the XML file is fetched from a public URL which contains bookstore data in XML format. The first task in the workflow, called `get_books`, uses the Core `HTTP Request` action to fetch this XML content:

**Input parameters:**

```yaml
url: http://books.toscrape.com/catalogue/category/books_1/index.html
request_method: GET
publish_result_as: get_books
```

The result from this task will look something like this:

```json
{
  "cookies": {},
  "data": "<bookstore>...</bookstore>",
  "headers": {...},
  "status_code": 200
}
```

The `data` field contains the XML content, which is the input for the `Parse XML` action. The XML content is passed using the Context (`CTX`) object as `CTX.books.data`.

**Finding the first book**

In this scenario, we are using the `find` operation to return the first `book` element in the XML:

**Input parameters:**

```yaml
input:
  xml: {{CTX.books.data}}
  selector: find
  value: book
```

The result from this task will look something like this:

```json
{
  "value": "<book category=\"cooking\"><title lang=\"en\">Everyday Italian</title><author>Giada De Laurentiis</author><year>2005</year><price>30.00</price></book>"
}
```

The output includes the first `book` element in the XML content.

**Selecting all 'Children' category books**

For a more complex operation, we can use the `select` operation with an XPath expression to extract all `book` tags where the `category` attribute is `children`.

**Input parameters:**

```yaml
xml: {{CTX.books.data}}
selector: select
value: book[category='children']
```

**Result:**

```json
{
  "value": "<book category=\"children\"><title lang=\"en\">Harry Potter</title><author>J K. Rowling</author><year>2005</year><price>29.99</price></book>"
}
```

The result includes all `book` tags where the `category` attribute is `children`.

</details>
