<h1>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br> Automation in development and production
    <h2>Interfaces</h2>
  <br>
</h1>

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

<b style='color:red;'>Draft</b>

# Module 07 File Management

This module is integrated in [DLS lab 04](https://github.com/hei-dls-adp/adp_lab_04_2026).

## Overview

This module covers file management operations in Node-RED, focusing on CSV and JSON formats.

### Plan

1. **CSV File Management**
  - Reading CSV files
  - Parsing CSV data
  - Writing CSV files
  - Data transformation

2. **JSON File Management**
  - Loading JSON files
  - Serializing and deserializing JSON
  - Writing JSON data
  - Validating JSON structure

3. **File Operations**
  - File I/O basics
  - Error handling
  - Working with file paths

---

## Common file types.

[CSV](#csv-files): the original.
[XML](#xml-files): the classic, see Word and Excel files.
[JSON](#json-files): primarily used with JavaScript, but also compatible with Python.

---

## CSV files

A **CSV file**, **C**omma-**S**eparated **V**alues file, is a simple text file used to store **tabular data**—like a spreadsheet or database table.

### Basic idea

* Each **line = one row**
* Each **value = one column**
* Values are separated by a **delimiter** (usually a comma `,`)

### Example

```
Name,Age,Country
Alice,30,Switzerland
Bob,25,France
Charlie,35,Germany
```

### What this means

* First row → column headers
* Each next row → a record
* Commas separate the fields

### Variations

* Sometimes the separator is not a comma:

  * `;` (very common in Europe)
  * `\t` (tab → called TSV)
* Text values can be wrapped in quotes:

```
"Smith, John",40,"USA"
```

### Why CSV is widely used

* Very **simple and lightweight**
* Works with many tools:

  * Excel / LibreOffice
  * Databases
  * Programming languages (JavaScript, Python, etc.)
  * Industrial tools like Node-RED, PLC data logging, etc.

### Limitations

* No formatting (no colors, formulas, etc.)
* No data types (everything is basically text)
* No hierarchy (just flat tables)

---

## XML files

An **XML file** (eXtensible Markup Language) is a structured text format used to store and transport data in a **hierarchical (tree-like)** way.

### Basic idea

XML uses **tags** , like HTML, to describe data:

```xml
<Person>
    <Name>Alice</Name>
    <Age>30</Age>
    <Country>Switzerland</Country>
</Person>
```

### Key characteristics

* Data is **self-describing** (tags explain meaning)
* Supports **nested structures** (unlike CSV)
* Strict syntax (must be well-formed)

---

### XML vs CSV

| Feature     | CSV                | XML                   |
| ----------- | ------------------ | --------------------- |
| Structure   | Flat table         | Hierarchical, *tree*   |
| Readability | Very simple        | More verbose          |
| Flexibility | Low                | High                  |
| Use case    | Simple data tables | Complex data exchange |

:bulb: XML can perhaps be considered more robust, in the sense that it is more complicated to mix data. Below you can see that it is not possible to confuse different values, but also that it is simpler for a human reader to identify them.

Example with XML

```xml
<ArrayOfSensors>
    <Sensor>
        <Value>23.5</Value>
        <LimitLow>5.1</LimitLow>
        <LimitHigh>120</LimitHigh>
    </Sensor>
    <Sensor>
        <Value>23.5</Value>
        <LimitLow>52.1</LimitLow>
        <LimitHigh>120</LimitHigh>
    </Sensor>
</ArrayOfSensors>
```

The same with CSV

```csv
Value,LimitLow,LimitHigh
23.5, 5.1, 120
23.5, 52.1, 120
```

---

### Can Excel use XML files?

**Yes — Excel supports XML**, and in multiple ways.

#### 1. Open XML directly

You can open an `.xml` file in **Microsoft Excel**:

* Excel tries to **interpret the structure**
* It may create a table automatically

#### 2. Import with XML mapping *more advanced*

Excel can:

* Map XML elements → columns
* Use an **XSD schema** for structured import

#### 3. Excel’s native format is XML-based

Modern Excel files `.xlsx` are actually:

* A collection of XML files inside a ZIP container

---

### Example: XML usable in Excel

```xml
<People>
    <Person>
        <Name>Alice</Name>
        <Age>30</Age>
    </Person>
    <Person>
        <Name>Bob</Name>
        <Age>25</Age>
    </Person>
</People>
```

Excel can turn this into:

| Name  | Age |
| ----- | --- |
| Alice | 30  |
| Bob   | 25  |

---

### ⚠️ Things to watch out for

* Complex nesting → harder to import cleanly
* Requires consistent structure
* Sometimes needs an XSD schema for best results

---

### 💡 When to use XML instead of CSV

Use XML if:

* You need **hierarchical data**, e.g. machines → modules → sensors
* You exchange data between systems, e.g. OPC UA, MES, ERP
* You need **metadata or structure**

Use CSV if:

* You just need a **simple table export/import**

---

## JSON files

**JSON perfectly complements CSV and XML**, and today it is often the most used format in computing and automation.

---

### What is JSON?

**JSON** **J**ava**S**cript **O**bject **N**otation*, is a text format for representing **structured** data, based on key/value objects.

### Example

```json
{
  "Name": "Alice",
  "Age": 30,
  "Country": "Switzerland"
}
```

### With a more complex structure

```json
{
  "People": [
    { "Name": "Alice", "Age": 30 },
    { "Name": "Bob", "Age": 25 }
  ]
}
```

---

### JSON Characteristics

* **Hierarchical** structure (like XML)
* **Simple and lightweight** syntax
* Very easy to use in programming (especially JavaScript, Node-RED, APIs)
* Native types: numbers, strings, booleans, arrays, objects

---

## 🆚 Comparaison JSON vs CSV vs XML

| Criteria | CSV | XML | JSON |
| ------------- | --------------- | --------------------- | -------------------- |
| Structure | Table (flat) | Tree (hierarchical) | Tree (hierarchical) |
| Readability | Very simple | Verbose | Clear and compact |
| Size | Very lightweight | Heavyweight | Lightweight |
| Typing | ❌ No | ⚠️ Partial (via XSD) | ✅ Yes |
| Complexity | Low | High | Medium |
| Modern use | Simple data | Industry standards | APIs, IoT, apps |

:bulb: note that the table format of this md file could be imported like a CSV file with ``|`` as a delimiter with little transformation.

---

## When to use what?

### CSV → simplicity

* Excel export
* Simple logs (PLC, sensors)
* Tabular data

**Example**: temperature history

---

### 🏗️ XML → structure + standardization

* Industrial systems
* Standards, OPC UA.
* Complex data with validation

**Example**: complete description of a piece of equipment

---

### JSON → Modern and practical

* Web APIs
* Node-RED
* Communication between systems
* Modern IoT / automation

**Example**: Message between machines

```json
{
  "sensor": "temperature",
  "value": 22.5,
  "unit": "°C",
  "timestamp": "2026-04-13T10:00:00Z"
}
```

---

## Simple Summary

* **CSV** = Excel spreadsheet, **simple**
* **XML** = structured document, **rigorous** but resource-intensive
* **JSON** = modern structure **simple** + structure.

---

## In automation context / Node-RED / OPC UA.

**JSON** is often the best choice:

* native in Node-RED, `msg.payload`
* easy to manipulate with JavaScript
* perfect for APIs and data feeds

**XML** remains important for:

* industry standards
* compatibility with existing systems

**CSV** remains useful for:

* export to **Microsoft Excel**
* simple reporting
* data recorder, continuous or asynchronous writing of a file.


### Résumé

In the lab, we will learn how to handle CSV and JSON files in Node-RED using built-in and community nodes. You will learn to read, parse, transform, and write both formats, enabling integration of file-based data sources and outputs in automation workflows.


<!-- End of file -->