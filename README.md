# 🧼 Eat Safe, Love: UK Food Hygiene Data Analysis

## Overview

This project analyzes food hygiene ratings from establishments across the United Kingdom using MongoDB and PyMongo. The data was provided by the UK Food Standards Agency and evaluated per the requirements of a fictional food magazine, *Eat Safe, Love*.

The goal was to set up a NoSQL database, clean and update the data, and perform exploratory analysis to uncover insights for food journalists and critics.

---

## 📁 Files

- `NoSQL_setup_starter.ipynb` – Connects to MongoDB, loads and cleans the data, inserts new records, and prepares it for analysis.
- `NoSQL_analysis_starter.ipynb` – Contains the exploratory analysis to answer key questions.

---

## 🧪 Part 1: Setup Summary

- Used `mongoimport` to load `establishments.json` into a new database: `uk_food`, collection: `establishments`
- Confirmed database and collection exist using PyMongo
- Printed a sample document using `pprint`

---

## 🛠 Part 2: Database Update Summary

- ✅ Inserted a new halal restaurant: **Penang Flavours**
- ✅ Found and updated its correct `BusinessTypeID`: **1**
- ✅ Deleted all records from the **Dover** local authority
  - **Documents deleted:** 994
- ✅ Converted data types:
  - `geocode.latitude` and `geocode.longitude`: string → decimal
  - `RatingValue`: string → integer
  - Non-numeric `RatingValue` values (like "Pass", "AwaitingInspection") were set to `null`

---

## 🔍 Part 3: Exploratory Analysis & Findings

### 1. Establishments with a hygiene score of 20
- **Total results:** 41
- These establishments have poor hygiene and may be unsafe for consumers.
- Sample entry:
  ```json
  {
    "BusinessName": "Ali Baba",
    "scores": { "Hygiene": 20, ... },
    ...
  }
```
## 2. London establishments with a RatingValue ≥ 4

- **Total found:** 33  
- Indicates a small subset of high-rated establishments among London's food scene.  
- Used `$regex` to match `"London"` in `LocalAuthorityName`.

## 3. Top 5 best-rated establishments near "Penang Flavours"

**Criteria:**
- `RatingValue = 5`
- Within ±0.01 degrees of **latitude = 51.490142**, **longitude = 0.083840**
- Sorted by **lowest hygiene score**

These are the safest and highest-rated options near Penang Flavours for food critics to visit.

**Sample result:**

```json
{
  "BusinessName": "Charlton Kebabish",
  "scores": { "Hygiene": 0 },
  "Distance": 4599.12
}
```
## 4. Top 10 Local Authorities with Most Establishments Scoring 0 in Hygiene

This indicates areas with the greatest concentration of hygiene concerns.

| LocalAuthorityName | Establishments with Hygiene Score 0 |
|--------------------|-------------------------------------|
| Thanet             | 1130                                |
| Greenwich          | 882                                 |
| Maidstone          | 713                                 |
| Newham             | 711                                 |
| Swale              | 686                                 |

---

## 💻 Technologies Used

- MongoDB (Compass & Server)
- PyMongo
- Jupyter Notebook
- Pandas
- Python 3
