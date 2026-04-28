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

:warning: using both example of a structure with Node-RED, we have this kind of prolem.

Converting a JSON object to a string, we get

**With JSON**

```json
    {"ID":2001,
     "Name":"Axes Velocity",
     "Unit":"m/s",
     "Value":0.1
    },
    {"ID":2002,
     "Name":"Axes Acceleration",
     "Unit":"m/s2",
     "Value":0.5
    },
```

**With XML**

```xml
<value>
  <ID>2003</ID>
  <Name>Axes Deceleration</Name>
  <Unit>m/s2</Unit>
  <Value>0.5</Value>
</value>
<value>
  <ID>2004</ID>
  <Name>Axes Jerk</Name>
  <Unit>m/s3</Unit>
  <Value>5</Value>
</value>
```
<b style='color:red;'>With XML we have lost the distinction between strings and number</b> this can be a problem when reading back parameters to send them to a PLC!

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

### Finally with AI

Short answer: **you can’t—at least not in plain XML itself.**

XML is just a **text format**. Everything between tags is treated as a **string of characters** unless you add an external mechanism.

---

# 🧠 Why there is no native type

In XML:

```xml
<Value>45.3</Value>
<Value>Hello</Value>
```

Both are simply **text nodes**. The parser (like in Node-RED using xml2js) has **no built-in way** to know:

* if `"45.3"` is a number
* or just a string that looks like a number

---

# 🧩 How to differentiate types (real solutions)

## 1. Use an XML Schema (XSD) ✅ (the “proper” way)

You define the type explicitly using XML Schema (XSD):

```xml
<xs:element name="SensorOne" type="xs:float"/>
```

Then:

```xml
<SensorOne>45.3</SensorOne>
```

👉 A validator knows it's a **number**

🔴 But:

* Node-RED does **not automatically enforce XSD**
* You’d need a validation step

---

## 2. Add type attributes manually (common in practice)

```xml
<SensorOne type="float">45.3</SensorOne>
<SensorTwo type="string">Hello</SensorTwo>
```

Then in Node-RED:

```json
{
  "SensorOne": {
    "_": "45.3",
    "$": { "type": "float" }
  }
}
```

👉 You can interpret it yourself in a Function node.

---

## 3. Use conventions (most common in Node-RED flows)

Just assume:

* numeric-looking strings → numbers
* others → strings

Example logic:

```javascript
let val = Number(x);
return isNaN(val) ? x : val;
```

👉 This is what most people do in practice.

---

## 4. Use a typed XML format (less common but powerful)

Some XML-based standards embed typing, for example:

* OPC UA XML Encoding
* SOAP XML Schema types

Example:

```xml
<Value xsi:type="xs:float">45.3</Value>
```

👉 Now type is explicit—but requires compatible tooling.

---

# ⚠️ Important takeaway

* XML itself = **no types**
* Types come from:

  * schema (XSD)
  * attributes
  * conventions
  * or application logic

---

# 💡 In your Node-RED context

The **best pragmatic approach** is:

1. Disable arrays (`explicitArray = false`)
2. Convert types in a Function node

Because:

* simple
* robust
* no dependency on schema validation

---

If you want, I can show you a **smart type inference function** (booleans, integers, floats, timestamps) instead of just `Number()` 👍

## Conclusion
On peut utiliser du XML pour un store restore de paramètres, mais ce n'est vraiment pas la manière la plus simple.

Pour aller vite au but: JSON
Si on a du temps pour faire quelque chose de vraiment robuste: XML.

<!-- End of file -->