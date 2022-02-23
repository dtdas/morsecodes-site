---
title: FetchXML Liquid Tag for Read Operations in Power Apps Portals
Description: For when you want to display data rapidly, and don't want to set up the whole Web API
slug: fetchxml-liquid-tag-for-read-operations-portals
---

## Setup

There are a few ways in Portals to read records from Dataverse - built in lists and forms, Web API, and fetchxml. Fetchxml offers a simple way to list data using liquid tags directly in the Page Template.

<br>

At the top of the Page Template, include the xml code, replacing the sample names with the information from your table.

<br>

Entity name: the table you would like to display data from
Order attribute: order by any column name
Note: the following code includes all columns, but if you'd only like to include certain columns, you can specify them by replacing `all-attributes />` with `<attribute name="column1" />` for each column.

```{% fetchxml get_some_data %}
<fetch version="1.0" output-format="xml-platform" mapping="logical" distinct="false">
  <entity name="table_name">
    <all-attributes />
    <order attribute="attr1" descending="false" />
  </entity>
</fetch>
{% endfetchxml %}
{% assign query_results = get_some_data.results.entities %}
```

Use a for loop to iterate through the records and display the data. In this example, we list the column1 custom column for each record in the table. Include this code directly inside any html.

```{% for result in query_results %}
{{ result.column1 }}
{% endfor %}
```

We can take advantage of conditionals and operations within liquid tags as well. For example, let's say we want to subtract column2 from column1 and display the results as a whole number:

```{% for result in query_results %}
{{ result.column1 | minus: result.column2 | round }}
{% endfor %}
```
