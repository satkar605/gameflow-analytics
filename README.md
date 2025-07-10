# 🎮 GameFlow Analytics – Spark-Based Player Behavior Pipeline

## 📌 Project Overview

**GameFlow Analytics** is a Spark-optimized data pipeline designed to uncover player behavior patterns from multiplayer match data. This project emulates the kind of analysis a gaming company like 343 Industries (Halo), Riot Games, or Activision might use to improve **player engagement**, **map design**, and **matchmaking strategies**.

By answering core gameplay questions through aggregated metrics and efficient data processing, this project provides:

- Behavioral signals that help **improve user retention**
- Usage analytics to inform **game balancing and map redesign**
- Insights into **combat efficiency**, **playlist popularity**, and **medal earning patterns**

Ultimately, this pipeline allows game analysts and product teams to make **data-driven decisions** that enhance gameplay and player satisfaction.

---

## 🔧 Process Overview

This Spark pipeline was built using four main datasets:

- `match_details`: Player-level statistics for every match
- `matches`: Metadata per match, including playlist and map IDs
- `medals_matches_players`: Medal types awarded per player per match
- `medals`: Definitions and categories of medals
- `maps`: Map descriptions and identifiers

### ✅ Key Best Practices Applied

- **Broadcast Join Optimization**: Automatic broadcast joins disabled and small dimension tables (e.g., `maps`, `medals`) explicitly broadcasted for controlled performance.
- **Simulated Bucketed Joins**: All large fact tables repartitioned using `match_id` into 16 buckets, aligning partitions to reduce shuffle during joins.
- **Partition Sorting**: Used `.sortWithinPartitions()` on low-cardinality fields (like `playlist_id`, `mapid`) to evaluate storage efficiency and improve read performance.
- **Columnar Storage**: Final outputs written in Parquet format, leveraging columnar compression and Spark’s predicate pushdown features.

---

## 📊 Key Findings

### 1. **Top Players by Kill Efficiency**
- The player with the highest **average kills per game** exhibited consistent combat performance across multiple matches.
- These top performers likely indicate either high-skill users or imbalanced matchmaking.

### 2. **Most Played Playlists**
- A small set of playlists account for the majority of match activity, suggesting concentrated player interest or successful promotion of certain game modes.

### 3. **Most Popular Maps**
- Maps like *Construct* and *Guardian* surfaced as the most played.
- Their popularity may stem from favorable gameplay loops or positioning in matchmaking rotation.

### 4. **Killing Spree Medal Hotspots**
- Certain maps have disproportionately high counts of "Killing Spree" medals.
- This insight can help designers identify which maps enable streak-based domination, informing possible balancing efforts.

---

## 🔭 Conclusions and Future Directions

### 📌 Conclusions
- Spark's scalability enabled seamless analysis across millions of player-match interactions.
- Join optimization, partition design, and explicit broadcast control were essential for building a performant pipeline.
- The findings offer a solid behavioral foundation for **game mode tuning**, **content promotion**, and **player lifecycle modeling**.

### 🚀 Future Directions
- Add **session-level engagement tracking** to identify churn and reactivation patterns.
- Integrate **time-series retention analysis** for daily or weekly active users (DAU/WAU).
- Deploy as part of a **real-time dashboard** for live gameplay analytics.
- Incorporate **player cohorting** for personalized matchmaking experiments.

---

🏗️ *Built with Apache Spark, following best practices in distributed data engineering and user behavior analytics.*
