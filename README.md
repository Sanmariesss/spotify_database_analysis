# Spotify Music Database Design & Analysis

**Course:** Databases & Big Data — Luiss Guido Carli (2024/25)
**Team:** Sabina Nurseitova, Ziyi Dong, Ceyla Kaya, Assima Amangeldina
**Type:** Database Design & ETL Pipeline | Team Project

---

# Introduction

This project designs and implements a relational database for Spotify streaming data, covering tracks from Spotify, Apple Music, Deezer, and Shazam. The goal was to build a normalized database schema, load real-world data through a Python ETL pipeline, and enable interactive querying through a Tkinter GUI.

---

# Dataset

- **Source:** Spotify Most Streamed Songs dataset (Kaggle)
- **File:** `Spotify_Most_Streamed_Songs.csv`
- **Key fields:** `track_name`, `artist(s)_name`, `streams`, `release_date`, `bpm`, `danceability_%`, `energy_%`, `in_spotify_playlists`, `in_apple_charts`, `in_deezer_charts`, `in_shazam_charts`

---

# Methods

## Tools and Environment
- **Language:** Python 3, SQL
- **Libraries:** `pandas`, `mysql-connector-python`, `pymysql`, `tkinter`
- **Database:** MySQL
- **Environment:** Any Python 3 environment with MySQL installed
- **To install dependencies:** `pip install pandas mysql-connector-python pymysql`

## Database Schema

The database is organized into 5 normalized tables following a relational schema designed with an ER diagram:

| Table | Description |
|---|---|
| `Artist` | Stores unique artist names |
| `Track` | Stores track name, artist count, and release date |
| `Artist_Track` | Junction table for the many-to-many relationship between artists and tracks |
| `StreamingMetrics` | Stores stream counts and playlist/chart appearances across platforms |
| `MusicalAttributes` | Stores audio features: BPM, key, mode, danceability, energy, valence, etc. |

## ETL Pipeline — `data_loading.py`

The ETL pipeline handles the full data flow from raw CSV to MySQL:

1. **Extract** — reads `Spotify_Most_Streamed_Songs.csv` using pandas
2. **Transform** — removes rows with missing track or artist names, cleans numeric columns (removes commas, converts to integers), handles missing values
3. **Load** — inserts data into MySQL using cached inserts to avoid duplicate entries and minimize redundant queries

Artist and track IDs are cached in dictionaries during loading to avoid querying the database repeatedly.

## Tkinter GUI — `interface.py`

A desktop interface built with Tkinter that allows users to select and run predefined SQL queries from a dropdown menu. Results are displayed in a Treeview table inside the app.

**Available queries:**
- Top 10 artists by total stream count
- Top 10 songs by stream count
- Most collaborated artists
- Artists appearing most in playlists (Spotify + Apple + Deezer)
- Artists appearing most in charts (all platforms)
- Most streamed track per year
- Popularity score of artists (normalized)
- Average danceability and energy across all tracks
- Top acoustic tracks by acousticness and streams
- Tracks with minimum speechiness

---

# Results

- Successfully designed a normalized relational schema covering 4 streaming platforms
- Loaded and cleaned the full Spotify dataset into MySQL with error handling for duplicates and missing values
- Built 10 analytical SQL queries covering artist collaborations, cross-platform chart performance, and audio feature analysis
- Delivered an interactive GUI enabling non-technical users to run queries without writing SQL

---

# How to Run

1. Clone the repository
2. Install dependencies:
```bash
pip install pandas mysql-connector-python pymysql
```
3. Set up the database schema in MySQL:
```bash
mysql -u your_username -p < spotify_database.sql
```
4. Update the credentials in `data_loading.py` and `interface.py` with your MySQL username and password
5. Load the data:
```bash
python data_loading.py
```
6. Launch the interface:
```bash
python interface.py
```

---

## Repository Structure

```
├── spotify_database.sql              # Database schema (tables + relationships)
├── data_loading.py                   # ETL pipeline (CSV → MySQL)
├── interface.py                      # Tkinter GUI for query execution
├── Spotify_Most_Streamed_Songs.csv   # Dataset
├── ERDiagram.graphml                 # ER diagram source file
├── databases.pdf                    # Project presentation
└── README.md
```
