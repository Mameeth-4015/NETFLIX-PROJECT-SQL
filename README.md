<p align="center"> <img src="./banner.png"...)
  <img src="./banner.png" alt="Netflix SQL Data Analysis Project banner" width="100%">
</p>

<h1 align="center">Netflix Movies & TV Shows Data Analysis (SQL)</h1>

<p align="center">
A SQL portfolio project analyzing Netflix's content library to uncover patterns in content type, ratings, genres, release trends, and contributor activity using PostgreSQL.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/SQL-PostgreSQL-blue" alt="PostgreSQL">
  <img src="https://img.shields.io/badge/status-completed-brightgreen" alt="Status">
  <img src="https://img.shields.io/badge/dataset-8807%20titles-e50914" alt="Dataset size">
</p>

---

## 📌 Overview

This project explores the [Netflix Titles dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows) using PostgreSQL to answer real-world business questions about Netflix's catalog — such as content distribution by type, top genres, country-wise output, actor appearances, and content categorization based on description keywords.

The goal is to demonstrate practical SQL skills including:
- Aggregations & grouping
- Window functions (`RANK()`)
- String/array functions (`UNNEST`, `STRING_TO_ARRAY`, `SPLIT_PART`)
- Date functions (`TO_DATE`, `EXTRACT`, `INTERVAL`)
- Subqueries & CTEs
- Conditional logic (`CASE WHEN`)

---

## 🗂 Dataset

| | |
|---|---|
| **File** | `netflix_titles.csv` |
| **Rows** | ~8,807 titles |
| **Source** | Netflix content listings (Kaggle) |

**Columns:**

| Column | Description |
|---|---|
| `show_id` | Unique ID for each title |
| `type` | Movie or TV Show |
| `title` | Name of the title |
| `director` | Director(s) of the title |
| `cast` | Cast members |
| `country` | Country/countries of production |
| `date_added` | Date the title was added to Netflix |
| `release_year` | Year the title was originally released |
| `rating` | Content rating (e.g., PG-13, TV-MA) |
| `duration` | Movie runtime or number of seasons |
| `listed_in` | Genre(s) / category |
| `description` | Short synopsis |

---

## 🛠 Tools Used

- **Database:** PostgreSQL
- **Client:** pgAdmin / psql
- **Language:** SQL

---

## 🚀 Setup

1. Clone this repository
   ```bash
   git clone https://github.com/<your-username>/netflix-sql-project.git
   cd netflix-sql-project
   ```
2. Create the database table and load the dataset using the schema in [`NETFLIX_PROJECT.sql`](./NETFLIX_PROJECT.sql)
3. Import `netflix_titles.csv` into the `netflix` table (via `\copy` in psql or pgAdmin's import tool)
4. Run the queries in your SQL client of choice

```sql
CREATE TABLE netflix (
    show_id        VARCHAR(6),
    type           VARCHAR(10),
    title          VARCHAR(150),
    director       VARCHAR(208),
    casts          VARCHAR(1000),
    country        VARCHAR(150),
    date_added     VARCHAR(50),
    release_year   INT,
    rating         VARCHAR(15),
    duration       VARCHAR(15),
    listed_in      VARCHAR(100),
    description    VARCHAR(250)
);
```

---

## ❓ Business Questions Answered

1. Count the total number of movies vs TV shows
2. Find the most common rating for movies and TV shows
3. List all movies released in a specific year (e.g., 2020)
4. Find the top 5 countries with the most content on Netflix
5. Identify the longest movie
6. Find content added in the last 5 years
7. Find all titles directed by **Rajiv Chilaka**
8. List all TV shows with more than 5 seasons
9. Count the number of titles in each genre
10. Find the average number of titles released by India each year (top 5 years by % of total Indian content)
11. List all movies that are documentaries
12. Find titles with no director listed
13. Find how many movies actor **Salman Khan** appeared in over the last 10 years
14. Find the top 10 actors with the most appearances in Indian-produced content
15. Categorize content as **"Good"** or **"Bad"** based on keywords (`kill`, `violence`) in the description, and count each category

---

## 🔍 Sample Insight

```sql
-- Top 5 countries by content volume
SELECT
    UNNEST(STRING_TO_ARRAY(country, ',')) AS new_country,
    COUNT(show_id) AS total_content
FROM netflix
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5;
```

This query splits multi-country entries (e.g., `"United States, India"`) into individual rows before aggregating — a common real-world data cleaning step.

---

## 📁 Repository Structure

```
├── netflix_titles.csv      # Raw dataset
├── NETFLIX_PROJECT.sql     # All SQL queries (schema + analysis)
├── banner.png              # README banner
└── README.md               # Project documentation
```

---

## 📈 Key Learnings

- Handling **comma-separated values** in a single column using `UNNEST` + `STRING_TO_ARRAY`
- Using **window functions** to rank results within groups
- Extracting and converting **inconsistent date formats** with `TO_DATE`
- Writing **CTEs** for content categorization based on text pattern matching

---

## 🤝 Contributing

Feel free to fork this repo, raise issues, or submit a PR with additional queries or improvements.

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

⭐ If you found this project helpful, consider giving it a star!
