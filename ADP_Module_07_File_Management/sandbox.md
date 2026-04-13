
2h comment sauvegarder des valeursl

Les types de fichiers classiques.

CSV: l'ancètre.
XML: le classique, voir fichier Word, Excel
Json: orienté JS, mais aussi, python


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

* native in Node-RED (`msg.payload`)
* easy to manipulate with JavaScript
* perfect for APIs and data feeds

**XML** remains important for:

* industry standards
* compatibility with existing systems

**CSV** remains useful for:

* export to **Microsoft Excel**
* simple reporting
* data recorder, continuous or asynchronous writing of a file.


