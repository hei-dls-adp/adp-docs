<h1>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br> Automation in development and production
    <h2>Interfaces</h2>
  <br>
</h1>

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

<b style='color:red;'>Draft</b>

# Module 10, URS, FS, DS


In a **GMP (Good Manufacturing Practice)** environment, the documents **URS, FS, and DS** are part of the **validation and lifecycle documentation** used to ensure that computerized systems and equipment are **designed, built, and operated in compliance with regulatory expectations**. They form a **traceable specification chain** from user needs to technical implementation.

This lifecycle is emphasized in regulations such as **EU GMP Annex 11** and **GAMP 5**.

---

## 1. URS — User Requirements Specification

The **URS** describes **what the user needs the system to do** from a business and GMP perspective.

Typical contents:

* Intended use of the system
* Process requirements
* Regulatory requirements (data integrity, audit trail, electronic signatures)
* Performance expectations
* Security and access control
* Interfaces with other systems

Example:

* “The system shall record all batch data with a complete **audit trail**.”
* “Operators shall authenticate with unique user accounts.”

**Role in GMP**

* The URS ensures the system supports **GMP compliance**, including data integrity (ALCOA+ principles).
* It is typically written by **process owners, QA, and validation teams**.

---

## 2. FS — Functional Specification

The **FS** explains **how the system will fulfill the URS requirements functionally**.

Typical contents:

* Functional descriptions
* Software behavior
* Process logic
* User interface functions
* Alarm handling
* Data recording logic

Example:

* URS: “The system shall record temperature.”
* FS: “The PLC shall read temperature from sensor T01 every 1 second and store it in the historian.”

**Role in GMP**

* Provides the **bridge between user needs and technical implementation**.
* Used to prepare **functional testing (OQ)**.

---

## 3. DS — Design Specification

The **DS** (sometimes SDS: Software Design Specification) defines the **technical implementation**.

Typical contents:

* Hardware architecture
* Software modules
* PLC programs
* Network architecture
* database schema
* tag lists
* configuration details

Example:

* PLC variable definitions
* OPC UA node structure
* database table schema

**Role in GMP**

* Demonstrates that the **system design supports the required functions**.
* Used to prepare **installation and technical verification (IQ)**.

---

## 4. Relationship in the GMP Validation Lifecycle

The documents form a **traceability chain**:

```
URS  →  FS  →  DS  →  Implementation  →  Testing
       |     |
       |     └─ Design Qualification / IQ
       |
       └─ OQ functional testing
```

More complete validation flow:

```
URS
  ↓
Functional Specification (FS)
  ↓
Design Specification (DS)
  ↓
Implementation / Configuration
  ↓
IQ – Installation Qualification
OQ – Operational Qualification
PQ – Performance Qualification
```

Traceability matrix example:

| URS    | FS    | DS    | Test  |
| ------ | ----- | ----- | ----- |
| URS-01 | FS-03 | DS-05 | OQ-02 |

This ensures **every GMP requirement is implemented and tested**.

---

## 5. Why Regulators Care

Regulators expect this structure because it proves:

* The system was **designed intentionally**
* **User needs were defined before development**
* **All requirements are tested**
* The system is **fit for intended GMP use**

This concept is explicitly referenced in **EU GMP Annex 11**, which requires **documented specifications and validation based on risk**.

---

✅ **In short**

| Document | Question it answers                     |
| -------- | --------------------------------------- |
| URS      | What does the user need?                |
| FS       | What functions will the system provide? |
| DS       | How will it be technically implemented? |

---

If you want, I can also explain **how URS/FS/DS relate to automation layers (PLC, SCADA, MES)** or how they map to **ISA-88 / MTP / modular automation**, which is often where things get interesting in biotech systems.




<!--End of file-->