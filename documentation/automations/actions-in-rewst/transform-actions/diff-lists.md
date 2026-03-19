---
description: Identify the differences between two input lists.
---

# Diff lists transform action

## Use case

You need to compare two lists and highlight the unique entries or entries exclusive to the first list, A transformation action that simplifies this complex comparison process is required.

## Overview

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-03-28 at 11.24.48 AM.png" alt=""><figcaption></figcaption></figure>

The `Diff Lists` transform is your solution for list comparison tasks. It uses two methods - `Anti-Join` and `Symmetric Difference` - to focus on unique or exclusive entries, thereby streamlining your data comparison process.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-03-24 at 10.59.50 AM.png" alt=""><figcaption></figcaption></figure>

## Parameters

Here are the parameters you have available to you within the action, and their descriptions:

<table><thead><tr><th width="192">Parameter</th><th width="438.3333333333333">Description</th><th data-type="checkbox">Required</th></tr></thead><tbody><tr><td>Difference Method</td><td>Choose the method to compute the differences between the lists. Options are <code>anti_join</code> and <code>symmetric_difference</code> (described below).</td><td>true</td></tr><tr><td>First List</td><td>Enter the first list to be compared.</td><td>true</td></tr><tr><td>First List's Key</td><td>Identify the key attribute for matching items in the first list.</td><td>true</td></tr><tr><td>Second List</td><td>Enter the second list to be compared.</td><td>true</td></tr><tr><td>Second List's Key</td><td>Identify the key attribute for matching items in the second list.</td><td>true</td></tr></tbody></table>

## Usage

### **Input lists**

For this transform, we will want to feed the action two separate lists, that we will then identify the fields in which we want to identify differences. Let's use these two lists as example:

**List 1:**

```json
list_1: [
  {"id": 1, "name": "John"},
  {"id": 2, "name": "Mary"}
]
```

**List 2:**

```json
list_2: [
  {"id": 1, "age": 30},
  {"id": 3, "age": 35}
]
```

### Difference methods

We have two options for the `Difference Method` you can pick to have the action perform, these method have slight differences that are quite helpful in various situations:

* **Anti-join:** for scenarios where you want to find entries that are exclusive to the first list.
* **Symmetric difference:** for comparing two sets of data and identifying unique records in each.

Take a look at examples of both below:

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td><img src="../../../../.gitbook/assets/image (2) (2).png" alt="" data-size="original"></td><td>The <code>Symmetric Difference</code> method is used when you want to identify entries that are unique to each list, i.e., items that exist in the one list and not in the other.</td><td></td></tr><tr><td></td><td><img src="../../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""></td><td>The <code>Anti Join</code> difference method is used when you want to determine the items in the first list that don't have a corresponding match in the second list.</td></tr></tbody></table>

***

<details>

<summary>Anti join</summary>

**Action Parameters:**

```yaml
diff_method: anti_join
list_1: List 1
list1_key: id
list_2: List 2
list2_key: id
```

**Jinja2 Equivalent:**

```django
{% set result = [] %}
{% for item1 in list_1 %}
  {% if all(item1[list1_key] != item2[list2_key] for item2 in list_2) %}
    {% do result.append(item1) %}
  {% endif %}
{% endfor %}


{{ result }}
```

</details>

<details>

<summary>Symmetric difference</summary>

**Action Parameters:**

```yaml
diff_method: symmetric_difference
list_1: {{ CTX.list_1 }}
list1_key: id
list_2: {{ CTX.list_2 }}
list2_key: id
```

**Jinja2 Equivalent:**

```django
{% set result = [] %}
{% for item1 in list_1 %}
  {% if all(item1[list1_key] != item2[list2_key] for item2 in list_2) %}
    {% do result.append(item1) %}
  {% endif %}
{% endfor %}
{% for item2 in list_2 %}
  {% if all(item2[list2_key] != item1[list1_key] for item1 in list_1) %}
    {% do result.append(item2) %}
  {% endif %}
{% endfor %}


{{ result }}
```

</details>

## Results output

The results of the two different diff methods can be seen as follows:

**Anti join:** only Mary's object from `list_1` is returned in the output, as she didn't have a correlating `id` in `list_2`.

```json
result: [
  {"id": 2, "name": "Mary"}
]
```

**Symmetric difference:** both Mary's object from `list_1` and the object in `list_2` that didn't have a correlating id in `list_1` were returned in the returned list.

```json
result: [
  {"id": 2, "name": "Mary"},
  {"id": 3, "age": 35}
]
```

***

With a grasp on the `Diff Lists` transform, you're ready to analyze and compare your lists for unique entries or entries exclusive to the first list. Understanding the differences between `Anti-Join` and `Symmetric Difference` methods will aid you in making effective data comparisons.
