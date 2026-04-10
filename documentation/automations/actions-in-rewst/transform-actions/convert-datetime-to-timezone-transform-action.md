# Convert DateTime to timezone transform action

## Use case

You are working with an API that returns a time in UTC, you would like to localize this value to your timezone or a specific timezone.

## Overview

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-04-18 at 2.38.40 PM.png" alt="" width="191"><figcaption></figcaption></figure>

Convert a DateTime to a different timezone.

## Parameters

<table><thead><tr><th width="217">Parameter</th><th width="417.3333333333333">Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>DateTime to convert</td><td>Use <a href="https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior">https://docs.python.org/2/library/datetime.html#strftime-and-strptime-behavior</a> for various options</td><td>true</td></tr><tr><td>Timezone to convert</td><td>Use https://en.wikipedia.org/wiki/List_of_tz_database_time_zones for various options not listed</td><td>true</td></tr></tbody></table>

{% hint style="info" %}
Some timezone values are timezone naive, such as EST. If you would like to use a timezone aware value then, as an example, you should use America/New\_York or US/Eastern.
{% endhint %}

## Usage

<details>

<summary>Example: Convert a UTC timestamp to EST/EDT</summary>

Inputs:

**DateTime to convert:** 2025-04-16T09:00:30.000Z

**Timezone to return:** US/Eastern

</details>

## Results output

Result of Example:

```json
"2025-04-16T05:00:30-04:00"
```
