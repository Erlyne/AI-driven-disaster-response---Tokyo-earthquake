# AI-Driven Disaster Response Triage: Sumida Ward Deployment

[cite_start]**Author:** AYADEN Lina [cite: 6]  
[cite_start]**Date:** January 2026 [cite: 7]

---

## 1. Problem and Context
[cite_start]This project models a disaster response scenario in Tokyo following a Magnitude 7.3 earthquake in Sumida Ward[cite: 9]. [cite_start]The primary objective is to resolve "information saturation" at the Honjo Fire Station Command Center, which is typically overwhelmed by civilian alerts and sensor data immediately following a disaster[cite: 10, 11]. [cite_start]The system utilizes a triage algorithm to rank incoming signals within a 5-kilometer radius to ensure critical structural failures and life threats are prioritized[cite: 13].

## 2. Geographic Risk Modeling
[cite_start]The deployment area is partitioned into five distinct zones based on structural material and historical vulnerability[cite: 18, 20]:

| Zone | Base Risk | Primary Material | [cite_start]Strategic Risk Profile [cite: 21, 23, 24, 25, 26] |
| :--- | :--- | :--- | :--- |
| **Kyojima** | 9.0 | Wooden | [cite_start]Highest priority; dense post-war housing with high fire-spread risk[cite: 21, 22]. |
| **Kinshicho** | 7.0 | Concrete | [cite_start]Commercial hub; risks include population density and falling glass[cite: 23]. |
| **Skytree** | 5.0 | Steel | [cite_start]Safe engineering; primary risks are internal panic and elevator entrapments[cite: 24]. |
| **Kameido** | 4.0 | Concrete | [cite_start]Modern apartment blocks; relatively stable compared to older districts[cite: 25]. |
| **Park** | 2.0 | Open Ground | [cite_start]Structurally safe; secondary Tsunami risk due to river proximity[cite: 26]. |

## 3. Decision Model: ELECTRE III
[cite_start]The system employs the **ELECTRE III** method because it is non-compensatory, ensuring that a high score in a secondary category cannot hide a critical life-threatening disaster[cite: 59, 60, 61].

### 3.1 Ranking Criteria ($g_{1} - g_{6}$)
[cite_start]The model utilizes a 39-point system to weigh alerts[cite: 30]:

* [cite_start]**Veto Trigger (10 Points):** A safety override for critical "Kill Words" like *Tsunami* using a veto threshold of $v=0.9$[cite: 32, 33, 34].
* [cite_start]**Severity ($g_{1}$) (9 Points):** Direct physical threat to life determined via NLP classification[cite: 35, 48].
* [cite_start]**Zone Vulnerability ($g_{4}$) (8 Points):** Strategic risk based on neighborhood material (e.g., wooden vs. concrete)[cite: 36, 52].
* [cite_start]**Proximity ($g_{3}$) (5 Points):** Distance from the fire station to optimize response time per hour[cite: 38, 51].
* [cite_start]**Battery Life ($g_{5}$) (3 Points):** Priority given to victims before device power is lost and GPS signal is cut[cite: 39, 54].
* [cite_start]**Panic ($g_{2}$) (2 Points):** Urgency based on crowd distress, shouting, and punctuation in messages[cite: 40, 42, 49].
* [cite_start]**Accessibility ($g_{6}$) (2 Points):** Logistical difficulty; slightly lowers priority if roads are reported as blocked[cite: 43, 44, 55].

## 4. Methodology
* [cite_start]**Data Processing:** Human text alerts go through an NLP engine, while IoT sensor data is trusted immediately[cite: 46].
* [cite_start]**Thresholds:** Each criterion is assigned Indifference ($q$), Preference ($p$), and Veto ($v$) thresholds to define outranking relations[cite: 63, 64, 65, 66].
* [cite_start]**Ranking:** The script calculates a **Net Flow Score**, representing the difference between alerts an alternative outranks and those that outrank it[cite: 67].

## 5. Results and Analysis
[cite_start]The model was tested using a 25-second snapshot of data post-earthquake[cite: 47, 69].

### 5.1 Kyojima Sector (High Risk)
In the high-risk wooden sector, the AI successfully prioritized confirmed life threats and active fires:
* [cite_start]**Rank #1:** Active fire reported at a convenience store[cite: 83].
* [cite_start]**Rank #3:** Sustained flooding from water line rupture[cite: 83].
* [cite_start]**Rank #5:** Trapped elderly person due to collapsed stairs[cite: 83].

### 5.2 Park Sector (Low Risk)
In the open ground zone, the model correctly isolated the single critical threat:
* [cite_start]**Rank #16:** Tsunami risk identified by unusual river wave motion[cite: 88, 89].
* [cite_start]**Standard Triage:** Vague distress calls and low battery reports were ranked lower without being deleted[cite: 88, 90].

## 6. Conclusion
[cite_start]The ELECTRE III model successfully balances immediate life threats with strategic geographic risks[cite: 97]. [cite_start]While occasional false positives occur—such as flagging the Tokyo Skytree for swaying—the system effectively filters information overload to protect the most vulnerable sectors during the first critical minutes of a disaster[cite: 93, 99, 100].
