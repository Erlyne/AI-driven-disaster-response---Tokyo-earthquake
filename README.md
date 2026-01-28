# AI-Driven Disaster Response Triage: Sumida Ward Deployment

**Author:** AYADEN Lina  
**Date:** January 2026

---

## 1. Problem and Context
This project models a disaster response scenario in Tokyo following a Magnitude 7.3 earthquake in Sumida Ward. The primary objective is to resolve "information saturation" at the Honjo Fire Station Command Center, which is typically overwhelmed by civilian alerts and sensor data immediately following a disaster. The system utilizes a triage algorithm to rank incoming signals within a 5-kilometer radius to ensure critical structural failures and life threats are prioritized.

## 2. Geographic Risk Modeling
The deployment area is partitioned into five distinct zones based on structural material and historical vulnerability:

| Zone | Base Risk | Primary Material | Strategic Risk Profile |
| :--- | :--- | :--- | :--- |
| **Kyojima** | 9.0 | Wooden | Highest priority; dense post-war housing with high fire-spread risk. |
| **Kinshicho** | 7.0 | Concrete | Commercial hub; risks include population density and falling glass. |
| **Skytree** | 5.0 | Steel | Safe engineering; primary risks are internal panic and elevator entrapments. |
| **Kameido** | 4.0 | Concrete | Modern apartment blocks; relatively stable compared to older districts. |
| **Park** | 2.0 | Open Ground | Structurally safe; secondary Tsunami risk due to river proximity. |

## 3. Decision Model: ELECTRE III
The system employs the **ELECTRE III** method because it is non-compensatory, ensuring that a high score in a secondary category cannot hide a critical life-threatening disaster.

### 3.1 Ranking Criteria ($g_{1} - g_{6}$)
The model utilizes a 39-point system to weigh alerts:

* **Veto Trigger (10 Points):** A safety override for critical "Kill Words" like *Tsunami* using a veto threshold of $v=0.9$.
* **Severity ($g_{1}$) (9 Points):** Direct physical threat to life determined via NLP classification.
* **Zone Vulnerability ($g_{4}$) (8 Points):** Strategic risk based on neighborhood material (e.g., wooden vs. concrete).
* **Proximity ($g_{3}$) (5 Points):** Distance from the fire station to optimize response time.
* **Battery Life ($g_{5}$) (3 Points):** Priority given to victims before device power is lost and GPS signal is cut.
* **Panic ($g_{2}$) (2 Points):** Urgency based on crowd distress, shouting, and punctuation in messages.
* **Accessibility ($g_{6}$) (2 Points):** Logistical difficulty; slightly lowers priority if roads are reported as blocked.

## 4. Methodology
* **Data Processing:** Human text alerts go through an NLP engine, while IoT sensor data is trusted immediately.
* **Thresholds:** Each criterion is assigned Indifference ($q$), Preference ($p$), and Veto ($v$) thresholds to define outranking relations.
* **Ranking:** The script calculates a **Net Flow Score**, representing the difference between alerts an alternative outranks and those that outrank it.

## 5. Results and Analysis
The model was tested using a 25-second snapshot of data post-earthquake.

### 5.1 Kyojima Sector (High Risk)
In the high-risk wooden sector, the AI successfully prioritized confirmed life threats and active fires:
* **Rank #1:** Active fire reported at a convenience store.
* **Rank #3:** Sustained flooding from water line rupture.
* **Rank #5:** Trapped elderly person due to collapsed stairs.

### 5.2 Park Sector (Low Risk)
In the open ground zone, the model correctly isolated the single critical threat:
* **Rank #16:** Tsunami risk identified by unusual river wave motion.
* **Standard Triage:** Vague distress calls and low battery reports were ranked lower without being deleted.

## 6. Conclusion
The ELECTRE III model successfully balances immediate life threats with strategic geographic risks. While occasional false positives occur, such as flagging the Tokyo Skytree for swaying, the system effectively filters information overload to protect the most vulnerable sectors during the first critical minutes of a disaster.
