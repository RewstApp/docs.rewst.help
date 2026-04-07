# Core actions

_Core actions_ in Rewst are your gateway to the platform's vast array of intrinsic functionalities. These actions, usable right out of the box, offer features ranging from ad-hoc HTTP requests to document parsing.&#x20;

Core actions are used in the same way as regular actions within workflows. They are selected from the list of available actions, configured based on their parameters, and then added to the workflow at the appropriate place.

{% hint style="info" %}
Expand each of the action types below to see their individual information. Actions are listed alphabetically in both this doc and the Rewst platform.
{% endhint %}

<details>

<summary>Await Webhook Request action</summary>

Waits for a request to a created one-off webhook. Once a request is received, the workflow continues.

* **Parameters**: This action only requires the ID of the webhook created from the `Create Webhook` action.
* **Output**: The output includes the HTTP method, query params, headers, JSON or form/multipart data in the body of the request, and the timestamp when the request was received.
* To access the results of a webhook, publish a [data alias](../workflows/data-aliases.md) with a value of `{/{ RESULT }/}.` You cannot merely publish the results as or use task.

</details>

<details>

<summary>Compare Strings Set Ratio action</summary>

This action calculates the ratio of how many words from the smaller string are found in the larger string. It's designed for measuring string similarity based on word overlap rather than character-by-character comparison. This action is particularly useful when you need to determine how similar two text strings are based on shared words, making it ideal for scenarios where exact string matching is too strict but you still need to measure content similarity.

**Use Cases**:

* Fuzzy matching between text strings
* Duplicate detection in datasets
* Content similarity analysis
* Partial string matching scenarios

**Parameters**:

* **original\_string** (required): The original string to compare
* **comparison\_string** (required): The comparison string that is being compared to

**Output**: Returns an integer representing the ratio of word overlap between the two strings. Higher values indicate greater similarity.



</details>

<details>

<summary>Confirmation Email action</summary>

Send a confirmation email with reply options to a specified recipient. \
This action pauses the workflow and places it in an `Awaiting-User-Input` state. The workflow will not proceed until the confirmation email is interacted with via buttons, or the task times out. You can configure task timeout on the **Advanced** tab of the action. Task time out means that the action fails. Note that this setup means that buttons are required for the workflow to proceed. \
\
![](<../../../.gitbook/assets/image (83).png>)

* **Parameters:** This action requires the recipient's email address (`to`), the subject of the email (`subject`), the title of the email (`title`), and the message body (`message`). It also offers user interaction buttons (`buttons`) and has the option to render markdown as HTML (`render_markdown`).
  * The parameters have several optional settings:
    * Custom Button CSS - Custom CSS to be applied to the buttons
    * Custom Footer - Custom footer to be displayed in the email. If not provided, this will default to the Rewst footer unless the footer is set to be removed.
    * Custom Title CSS - Custom CSS to be applied to the title
    * Logo Link - URL to go to if the logo is clicked. If not provided, this will default to [https://rewst.io](https://rewst.io/)
    * Logo URI - String value URI of the logo to be displayed in the email. If not provided, this will default to the Rewst logo image. This is essentially providing a value for the src param of a img tag. You could also provide a base64 encoded value. The file format for your hosted file will need to follow the guidance for your particular email client, which is independent of Rewst. For example, Outlook does not accept PNG formatted files. For broader guidance for all email clients, we recommend using this resource called [caniemail](https://www.caniemail.com/features/).&#x20;
    * Remove Footer - Removes the Rewst footer from the email
    * Render Markdown - Renders markdown as HTML when set to **True**
* **Output:** If the action is correctly executed, a confirmation email will be sent. Output variable `inquiry_result` is an output of the task and can be used to route the workflow in a specific path. `Inquiry_result` 's value is that of the button clicked, and is configured as a string value on the action itself in the workflow builder.

<figure><img src="../../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

* **Confirmation email class and confirmation examples**
  * Button classes:
    * Primary; primary
    * Default; default
    * Danger; danger
  * Title class:
    * Title; title
* #### Example custom button CSS

```css
a,

a:visited,

a:hover,

a:active {

color: inherit !important;

}

table, td, div, h1, p {

font-family: "Times New Roman", Times, serif;

}

.primary {

background: #4d7c0f;

}

.default {

background: #365314;

}

.danger {

background: #dc2626;

}
```



*   #### Example custom footer



    ```
    <tr>

    <td

    style="text-align:center;padding:30px 0 30px 0;background-color:#1a2e05;color:#ffffff;">

    <p style="display:inline-block;margin-right:10px;">&copy; The Dougnut {% now 'local', '%Y' %}</p>

    <p style="display:inline-block;margin-right:10px;"><a

    href="https://rewst.io/terms-of-service/">Order</a></p>

    <p style="display:inline-block;margin-right:10px;"><a href="https://rewst.io/privacy-policy/">Contact Us</a></p>

      

    <p style="display:inline-block;margin-right:10px;color:#84cc16"><a href="mailto:support@rewst.io">Need

    Delivery?</a></p>

      

    <p style="display:inline-block;margin:0px 4px 0 4px;vertical-align:middle;"><a href="https://www.linkedin.com/company/rewst"><img

    src="https://rewst-splash.s3.us-east-2.amazonaws.com/linkedin.png" width="24" height="24"

    alt="linkedin"></a></p>

      

    <p style="display:inline-block;margin:0px 4px 0 4px;vertical-align:middle;"><a href="https://twitter.com/rewst_dot_io"><img

    src="https://rewst-splash.s3.us-east-2.amazonaws.com/twitter.png" width="24" height="24" alt="twitter"></a>

    </p>

      

    </td>

    </tr>
    ```
* #### Example custom title CSS

```
.title {

font-size: 20px;

line-height: 16px;

font-weight: 700;

font-style: normal;

color: #0c0a09;

text-decoration: none;

letter-spacing: 0px;

padding: 25px 30px 0 30px;

}
```

* #### Example logo link

```
https://google.com
```

* #### Example logo URI

```
https://www.svgrepo.com/download/533811/donuts-cake.svg
```

</details>

<details>

<summary>Create Pending Task action</summary>

This action creates a pending task that pauses workflow execution and requires manual intervention through the Rewst UI. It's designed for scenarios where human approval, confirmation, or decision-making is needed within an automated workflow.

**Use Cases**:

* Manual approval workflows
* User confirmation before critical actions
* Decision points requiring human judgment
* Interactive workflow processes
* Quality control checkpoints

**Parameters**:

* **message** (required): The message to display in the pending task that explains what action is needed from the user
* **buttons** (required): An array of button objects that users can click to respond. Each button has:
  * **label**: The text displayed on the button
  * **style**: Visual style (`default`, `primary`, `danger`)
  * **value**: The value returned when the button is clicked

**Output**: The workflow pauses at this task until a user interacts with it via the Rewst UI. When a button is clicked, the action returns the corresponding button value, allowing the workflow to continue based on the user's choice.

This action is essential for creating interactive workflows that require human oversight or decision-making at specific points in the automation process.

</details>

<details>

<summary>Create Webhook action</summary>

Allows for the creation of a one-off webhook for which can then be used by the `Await Webhook` action.

**Parameters**: This action requires the methods allowed to access the webhook, the response status, response headers, response body, and an expiration timeout.

**Output**: The output of this action is the webhook ID and the full URL of the webhook.

</details>

<details>

<summary>Debug action</summary>

The `Debug` action is a utility feature in our workflow system, specifically designed to assist with debugging and logging purposes. This action can help in understanding the flow of data within your workflows, troubleshoot problems, and generally help you understand what's happening at a certain point in the workflow execution. It logs the input parameters it receives and returns the same as its output.

**Use cases**

You might want to use the `Debug` action in the following scenarios:

* When developing workflows, to see how data is flowing between tasks and actions.
* If you're troubleshooting an issue, to inspect the data that's being passed around.
* When you want to log specific information for auditing or reporting purposes.

**Input Parameters**

The `Debug` action accepts the following parameters:

* **text:** This is a general-purpose text field that will be logged and returned by the `Debug` action.
* **template:** This field takes a reference to a template in your environment that will be rendered and used as part of the action's input. The system will replace any variables in the template with its actual value at the time of template rendering.

**Example Usage**

Let's say we have a template named "Greeting Message" with content `# Hey there {{ CTX.name }}`.

We can use this template in the `Debug` action with the following parameters:

```yaml
text: Testing Debug Action
template: Greeting Message
```

Assuming `CTX.name` is set to `Rewsty`, the rendered template would be `# Hey there Rewsty`.

The `Debug` action will log these parameters and also return them as its output. The results of the action on the workflow results page would look like this:

**Output:**

```json
{
  "template": "# Hey there Rewsty",
  "text": "Testing Debug Action"
}
```

This tells us that `CTX.name` was set to`Rewsty`, and the text provided with this action was `Testing Debug Action`. Using this, you can better understand the state of your workflow at the point this `Debug` action was executed.

</details>

<details>

<summary>DNS Query action</summary>

Queries a nameserver for DNS records associated with a given URL.

* **Parameters:** The URL to query the Nameserver for, the field to query from the nameserver, timeout for the DNS Query (optional, default 60), and the nameserver to use for the query (several options available including Google, Cloudflare, OpenDNS).
* **Output:** The specified DNS records associated with the given URL from the queried nameserver.

</details>

<details>

<summary>Generate Password V2 action</summary>

An upgrade from the deprecated password generation action. It crafts a cryptographically secure password with user-specified values. (_This is recommended for use over the deprecated Password Action due to its upgraded structure.)_

* **Parameters:** length, minimum counts of numeric and capital letter characters, and optional punctuation characters.
* **Output:** the generated password is presented under the "password" key in the output.

</details>

<details>

<summary>HTTP Request action</summary>

Performs an HTTP request to a specified URL, supporting a variety of methods, body content types, and configurations. This is useful for interacting with APIs or other web services within a workflow, or for performing any other tasks that involve HTTP requests.

**Parameters**

* **URL**: The URL to which the HTTP request is sent.
* **Request Method**: The HTTP method to use for the request. You can select from the dropdown options (`HEAD`, `GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`, `TRACE`, `PATCH`, `PURGE`).
* **Auth Username**: The username for basic HTTP Authentication, if needed.
* **Auth Password**: The password for basic HTTP Authentication, if needed. _(This parameter is secret to ensure security.)_
* **Allow Redirects**: Specifies whether the HTTP request will follow redirects. By default, it's set to `true`.
* **Body**: The body to send with the request. This parameter is not required if `JSON` or `Files` is provided.
* **JSON**: The JSON body to send with the request. This field is not required if `Body` or `Files` is provided.
* **Files**: Here, you can add files to be uploaded with the HTTP request using `multipart/form-data`. Each file requires the following information:
  * **Field Name**: The name of the form field (not the filename).
  * **File Name**: The name of the file.
  * **File Contents**: Contents of the file to upload.
  * **File URL**: A publicly-accessible URL to the file contents to upload.
  * **Content Type**: The MIME type of the file to include in the multipart field.
* **Cookies**: Input the cookies to send with the request. You can add more than one cookie by clicking on the `+` icon.
* **Headers**: Specify the custom HTTP headers to be sent with the request. You can add more than one header by clicking on the `+` icon.
* **Params**: Enter the query parameters to be used with the HTTP request. You can add more than one parameter by clicking on the `+` icon.
* **Timeout**: Enter the timeout for the HTTP request in seconds. The default value is `5`.
* **Require Success Status**: If you check this box, the task will fail if a non-2xx HTTP status code is returned. This is useful for identifying and handling HTTP errors during the task's execution.

**Output**: The action returns the content returned by the server in response to the HTTP request. This could be a success message, a failure message, a data object, or any other content that the server sends as a response.

_<mark style="color:blue;">**Note**</mark><mark style="color:blue;">:</mark>_ _If you need more advanced security around calling particular endpoints, you can also use a_ [_Custom Integration_](../../integrations/custom-integrations/) _in addition to this HTTP Request action. This allows for enhanced security and customization when interacting with your external APIs._

</details>

<details>

<summary>Delay Workflow For Period action</summary>

Pauses the workflow for a specified duration.

* **Parameters:** The number of days, hours, minutes or seconds to delay the workflow.
* **Output:** No specific output, the workflow resumes after the specified delay.

</details>

<details>

<summary>Delay Workflow Until Date/Time action</summary>

Pauses the workflow until a specified date and time.

* **Parameters:** The date and time when the workflow should resume.
* **Output:** No specific output, the workflow resumes at the specified date and time.

</details>

<details>

<summary>Mock action</summary>

The `Mock` action is designed to provide you with the capability to simulate the result of a not yet implemented action. This is particularly useful during workflow development and testing phases as it allows you to simulate responses from services that are not yet available or are impractical to call during the development process.

**Use cases**

The `Mock` action comes in handy in scenarios such as:

* When designing new workflows where certain steps are not fully implemented.
* In testing stages, to simulate conditions without making actual calls to the services.
* To create controlled conditions in your workflow for troubleshooting issues.

**Input Parameters**

The `Mock` action accepts the following parameter:

* **Mock Result:** This parameter should contain the key / value pairs that you want to be returned by this action. You can press the `+` to add as many objects as necessary.

**Example Usage**

You are developing a workflow that is expected to interact with a service which is not yet implemented. You know the expected format of the response, and you want to build and test your workflow logic based on that response.

Let's say you know the response will look something like this:

```json
{
  "name": "Rewsty",
  "valid": true,
  "message": "Successfully completed the task."
}
```

You can simulate this response using the `Mock` action as follows:

```yaml
mock_result:
  name: {{ CTX.name }}
  valid: true
  message: Successfully completed the task.
```

While using the `Mock` action, the values can be literal Jinja expressions like `{{ CTX.name }}`above. The action will return this exact input structure wrapped inside a `data` object, and the Jinja expressions will not be evaluated but returned as is. The result of the action on the workflow results page would look like:

**Output:**

```json
{
  "data": {
    "name": "{{ CTX.name }}",
    "valid": true,
    "message": "Successfully completed the task."
  }
}
```

This can be useful for catching issues early in the development phase such as incorrect Jinja expression usage, understanding how the workflow will handle dynamic data, or verifying that your workflow is properly constructed to handle the expected responses from services. It's a way to ensure that your workflow behaves as expected when it starts receiving actual dynamic data.

</details>

<details>

<summary>No-Operation (Noop) action</summary>

A noop action does nothing. It's often used for logic or as a placeholder in the workflow.

* **Parameters:** None.
* **Output:** None

</details>

<details>

<summary>Parse HTML action</summary>

The Parse HTML action is a versatile tool within Rewst, geared to pinpoint and extract specific elements or data from HTML documents. It leverages the power of BeautifulSoup, a Python library recognized for extracting data from HTML and XML files effectively.

**Use cases**

This action is particularly beneficial in these situations:

* **Data Extraction**: capturing specific information from the response of an HTTP request.
* **Content Clean-Up**: sieving out only the necessary data from complex HTML content.
* **Web Scraping**: automating the extraction of specific information from various web pages using defined tags, classes, or identifiers.

**Action Parameters**

The `Parse HTML` action accepts the following parameters:

* **HTML**: The HTML content to be parsed. This could be HTML content from a webpage, obtained using the `HTTP Request` Core Action.
* **Class**: Optionally finds HTML elements based on their `class` attribute.
* **ID**: Optionally searches for HTML elements based on their `ID` attribute.
* **Query**: Employs [BeautifulSoup filters](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#kinds-of-filters) to specify the operation type:
  * `find_all` returns all instances of the defined HTML tag.
  * `find` returns only the first instance of the defined HTML tag.
  * `select` enables the use of CSS selectors for nested HTML tags.
* **String**: Optionally searches for specific text within the HTML content.
* **Value**: Identifies the tag or selector to search for in the HTML content. For example, `a` would find all anchor (`<a>`) tags in the HTML content.

**Practical Use Case: Extracting Links from 'Hacker News'**

This example involves making a `GET` request to the `Hacker News` website and parsing the returned HTML to extract all `<a>` links.

The first step uses the Core `HTTP Request` action to fetch the HTML content:

```yaml
publish_result_as: news
request_method: GET
URL: https://news.ycombinator.com
```

You can then use the `Parse HTML` action to extract all `<a>` links. The parameters for this action would be set as follows:

```yaml
html: {{ CTX.news }}
style: find_all
value: a
```

**Example Workflow Results**

Here's an example of how the `Parse HTML` action's input and output might look like on the workflow results page:

**Input from the HTTP Request:**

```json
html: {
  cookies: {},
  data: "<html>...</html>",
  headers: {...},
  status_code: 200
},
query: {
  style: "find_all",
  value: "a"
}
```

**Result:**

```yaml
[
  "<a href=\"https://news.ycombinator.com\"><img height=\"18\" src=\"y18.svg\" style=\"border:1px white solid; display:block\" width=\"18\"/></a>",
  "<a href=\"news\">Hacker News</a>",
  "<a href=\"newest\">new</a>",
  "<a href=\"front\">past</a>",
  "<a href=\"newcomments\">comments</a>",
  "<a href=\"ask\">ask</a>",
  "<a href=\"show\">show</a>",
  "<a href=\"jobs\">jobs</a>",
  "<a href=\"submit\">submit</a>",
  "<a href=\"login?goto=news\">login</a>"
]
```

This result contains all `<a>` tags found in the HTML content.

To further refine this output, returning only links for externally referenced pages, use the `select` query style, along with advanced CSS filters:

```yaml
html: {{ CTX.news }},
style: select
value: .titleline a[href^='https://']
```

The result is a list of strings containing all `<a>` tags that meet the newly specified criteria:

```json
[
  "<a href=\"https://arxiv.org/abs/2308.00676\" rel=\"noreferrer\">Electronic Structure of LK-99</a>",
  "<a href=\"https://www.science.org/content/blog-post/room-temperature-superconductor-new-developments\" rel=\"noreferrer\">A room-temperature superconductor? New developments</a>",
  "<a href=\"https://sophiehoulden.com/randomstuff/epitime/?revised\" rel=\"noreferrer\">Epicycle Clock</a>",
  "<a href=\"https://howardism.org/Technical/Emacs/new-window-manager.html\" rel=\"noreferrer\">Emacs is my new window manager</a>",
  "<a href=\"https://ploum.net/2023-08-01-splitting-the-web.html\" rel=\"noreferrer\">Splitting the Web</a>",
  "<a href=\"https://twitter.com/zebulgar/status/1686498517227814912\" rel=\"noreferrer\">Unconfirmed video showing potential LK-99 sample exhibiting the Meissner effect</a>",
  "<a href=\"https://magicloops.dev\" rel=\"noreferrer\">Show HN: Magic Loops – Combine LLMs and code to create simple automations</a>",
  "<a href=\"https://arxiv.org/abs/2307.08378\" rel=\"noreferrer\">eGPU: A 750 MHz Class Soft GPGPU for FPGA</a>"
]
```

To further understand CSS selectors, you can refer to this [w3schools article](https://www.w3schools.com/cssref/css_selectors.php).

_**Tip**: Parse HTML's functionalities include finding elements by tags (`<h1>`), class (`class_="abc"`), text (`string="The content"`), or id (`{"id": "abc"}`). When `string` is the sole argument, only the text is returned, not the whole element, which can help you fine-tune data extraction._

</details>

<details>

<summary>Parse XML action</summary>

The Core Parse XML action in Rewst is designed to locate and extract specific elements or data from XML documents. This powerful tool, backed by an efficient Python library, facilitates precise data extraction from XML files, simplifying the process of parsing complex data structures. For additional understanding on XPath expressions, refer to this [w3schools article](https://www.w3schools.com/xml/xpath_intro.asp).

**Use cases**

Consider using the Parse XML action in these scenarios:

* **Data Extraction and Content Clean-Up:** Capture specific information or filter out necessary data from XML-formatted content. This is particularly useful in processing responses from HTTP requests or handling complex XML documents.
* **Web Scraping:** Automate the extraction of specific information from various XML sources using defined tags, attributes, or identifiers. It enables you to precisely target the data you need from web resources.

**Action parameters**

The Core Parse XML action requires the following parameters:

* **XML**: The XML content that needs to be parsed. This could be XML content from an API response, obtained using the HTTP Request Core Action.
* **Attributes**: (Optional) Allows you to find XML elements based on their attribute key.
* **ID**: (Optional) Permits searching for XML elements based on their ID attribute.
* **Selector**: Determines the operation type. Options include:
  * `find`: Returns only the first instance of the defined XML tag.
  * `find_all`: Returns all instances of the defined XML tag.
  * `select`: Enables the use of XPath expressions for nested XML tags or conditional searches.
* **String**: (Optional) Allows you to search for specific text within the XML content.
* **Value**: Specifies the tag or selector to search for in the XML content.

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

<details>

<summary>Send Mail action</summary>

Allows for the sending of an email.

* **Parameters:** This action requires a sender prefix (`sender`), with multiple options available, the recipient's email address (`to`), the subject of the email (`subject`), the title of the email (`title`), and the message body (`message`). It also has the option to render markdown as HTML (`render_markdown`). You can also fully control the HTML of the email with `(Custom HTML)`. This can also reference a template using the `{{ template(“guid”) }}` function.&#x20;
  * Note that if you're using the `Custom HTML` field, the message and title fields will be ignored. \
    ![](<../../../.gitbook/assets/Screenshot 2026-03-03 at 9.44.26 AM.png>)
  * You cannot upload images to Rewst, so any image will need to be externally referenced via URL. The file format will need to follow the guidance for your particular email client, which is independent of Rewst. For example, Outlook does not accept PNG formatted files. For broader guidance for all email clients, we recommend using this resource called [caniemail](https://www.caniemail.com/features/).&#x20;
  * Emails will still be sent from the rewst.io domain.
* **Output:** The task doesn't yield an output upon success. It will fail if there are any errors during the process of sending the email.

</details>

<details>

<summary>Send SMS action</summary>

Allows you to send a text message to a specified phone number.

*   **Parameters**: This action requires the recipient's phone number (`phone_number`) and the text message (`message`) to be sent. All phone numbers must be provided using the E.164 international format, which includes the country code. Improperly formatted numbers may result in validation errors or delivery failures.

    Example: `+14155552671`
* **Output**: The output of this action will depend on the implementation details. Usually, it will return a confirmation message or an error message.

#### Sending number origin

The `core_send_sms` action sends messages from a US-based phone number owned and managed by Rewst.

Due to this setup:

* SMS delivery is most reliable for United States phone numbers
* Some international carriers restrict or block messages originating from US long-code numbers
* Certain countries require locally registered sender IDs or approved messaging routes

These limitations are imposed by telecommunications carriers and regional messaging regulations.

#### When to use your own messaging account

If you need to send SMS messages to a region that is not supported by the shared Rewst sending number, you can set up your own messaging account and use it through Rewst’s [Twilio integration](../../integrations/integration-guides/twilio-integration-setup.md).

Using your own account allows you to:

* Purchase local phone numbers in supported countries
* Configure which countries your numbers can send messages to
* Register country-specific sender IDs
* Meet regional compliance requirements

#### Delivery behavior

When the `core_send_sms` action is executed, it returns the **current delivery status** for the message. This status reflects the system's understanding of the message state after it has been sent to the carrier networks. Even when a message is reported as sent, final delivery still depends on external telecom carrier networks and the recipient device.

Because SMS delivery involves multiple third-party carriers, failures may still occur due to:

* Carrier filtering
* Regional messaging restrictions
* Unreachable devices
* Network congestion
* Recipient opt-outs

#### Common SMS error responses

* SMS service is temporarily unavailable, please try again later
* Invalid phone number format
* SMS cannot be sent to this region - geographic permissions not enabled
* This recipient has opted out of receiving messages
* SMS cannot be delivered to this number due to carrier or regional restrictions
* This number is a landline and cannot receive SMS messages
* The phone is currently unreachable (switched off or no signal)
* This phone number is unknown or may no longer exist
* This number cannot receive SMS messages (likely a landline or unsupported carrier)
* Network congestion - please try again in a few minutes

#### Error scenario: Carrier or regional restrictions

This situation occurs when the destination carrier or region doesn't allow messages from the sending number.

Possible causes include:

* Sender ID restrictions in the destination country – Some countries limit which numbers, shortcodes, or alphanumeric sender IDs can be used.
* Sender ID restrictions on the destination network – Certain networks may block messages from shortcodes or restrict MMS messages from longcodes that originate outside the country.
* Alphanumeric sender IDs – If you are using an alphanumeric sender ID, the destination country must support it, and some countries may require pre-registration.
* Number formatting – The “To” or “From” number may not be in the proper international format (E.164). Check that numbers are correctly formatted.
* Destinations with no connectivity – Some carriers or regions may not have messaging routes available for your sending number.
  * This error is more common when sending international messages from a US-based number. If you need to reliably reach a destination with restrictions, consider using your own messaging account via the Twilio integration, where you can configure allowed countries, local numbers, and sender IDs.

#### Error scenario: Messaging geo-permissions disabled

This situation occurs when an SMS or MMS message is sent to a country or region that the Rewst-managed sending number is not authorized to send messages to.

Possible causes:

* The destination country is not included in the allowed countries for the Rewst sending number
* The region is not supported for SMS delivery from the Rewst-managed sending number
* Messaging to that region is restricted by telecom regulations
  * If you need to send messages to a country that is not supported, consider using your own Twilio account via the Twilio integration, where you can configure allowed countries and sender IDs.

#### Error scenario: Recipient has opted out

The recipient has opted out of receiving messages from the sending number.

#### Error scenario: Landline number

The destination phone number is a landline and cannot receive SMS messages.

#### Error scenario: Phone unreachable

The destination device cannot currently be reached. Retrying later may resolve the issue.

Possible causes:

* Device powered off
* No cellular signal
* Temporary carrier network issues

#### Error scenario: Unknown or unreachable numbers

The destination number may not exist, cannot receive SMS, or is otherwise unreachable due to carrier restrictions.

#### Error scenario: Network congestion

The carrier network is currently congested. Retrying the message later may resolve the issue.

</details>

<details>

<summary>Test All Parameter Types action</summary>

This action serves as a comprehensive example and testing tool that showcases all the different input field types that can be used in Rewst actions. It's primarily used for:

* UI testing and validation
* Demonstrating parameter field capabilities
* Training and educational purposes
* Testing form rendering and validation

**Inputs**

The task accepts a wide variety of input parameters representing every field type available in Rewst:

**Basic fields:**

* `simple_string` (required) - Basic text input
* `optional_string` - Optional text field
* `string_with_default` - Text with default value "default\_value"
* `simple_integer` (required) - Whole number (default: 42)
* `simple_number` - Decimal number (default: 3.14)
* `simple_boolean` - Toggle switch (default: false)
* `required_boolean` (required) - Required toggle

**Advanced string fields:**

* `string_enum` (required) - Dropdown with options (option\_1, option\_2, option\_3)
* `string_enum_objects` - Dropdown with custom labels and descriptions
* `radio_selection` (required) - Radio button group
* `secret_string` - Password/masked field
* `multiline_text` - Large text area
* `textarea_content` - Code editor area

**Date/Time fields:**

* `date_field` - Date picker
* `time_field` - Time picker
* `datetime_field` - Date and time picker

**Array fields:**

* `simple_array` - Array of strings
* `array_with_enum` - Multi-select dropdown
* `array_of_objects` - List of complex objects with name, enabled, and quantity fields

**Object fields:**

* `simple_object` - JSON object field
* `nested_object` - Complex nested object with host, port, SSL settings, and credentials

**Special fields:**

* `number_with_range` - Integer between 1-100 (default: 50)
* `local_reference_template` - Reference to local templates
* `remote_reference_example` - Reference to remote API options
* `remote_reference_with_dependency` - Dependent reference field

**UI state fields:**

* `tooltip_field` - Field with helpful tooltip
* `hidden_field` - Hidden from UI
* `disabled_field` - Cannot be edited
* `readonly_field` - Read-only display
* `deprecated_field` - Marked as deprecated
* `staff_only_field` - Only visible to staff users

**Outputs**

The action returns a simple object with two properties:

* `message` (string) - A test result message describing the outcome
* `success` (boolean) - Whether the test execution was successful

</details>

<details>

<summary>UUID action</summary>

Generates a new UUID (Universally Unique Identifier).

* **Parameters:** UUID type (options include `uuid1` and `uuid4`, defaults to `uuid4`).
* **Output:** The generated UUID.

</details>
