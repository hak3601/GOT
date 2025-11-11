# Game of Thrones Character Network Analysis

This project visualizes and analyzes the **Game of Thrones character interaction network** based on co-occurrence within the text.  
Each node represents a character, and each edge represents the frequency of their co-occurrence within 15 words of each other in the novel.

---

## 📊 Dataset Overview

| Property | Description |
|-----------|-------------|
| **Nodes** | 107 unique characters |
| **Edges** | 353 weighted, undirected relationships |
| **Edge weight** | Number of times two characters appear within 15 words |
| **Graph type** | Weighted, undirected, unimodal |

Files:
- `got-nodes.csv` – list of all characters
- `got-edges.csv` – pairwise co-occurrence relationships with weights

---

## 🧠 Methodology

Each character’s structural importance is evaluated using **three classic centrality measures**:

| Centrality | Meaning | Interpretation |
|-------------|----------|----------------|
| **Degree Centrality** | Number of distinct neighbors | Measures *popularity* or *activity* |
| **Weighted Betweenness** | Control over weighted shortest paths | Identifies *brokers* between storylines |
| **Eigenvector Centrality** | Importance based on connections to other important nodes | Measures *influence among elites* |

Community structure is detected using the **Louvain algorithm** (`python-louvain`), producing consistent color groupings across all visualizations.

---

## 🧩 Network Visualization Design

- **Node size** = centrality value (different per metric)
- **Node color** = community (consistent across all diagrams)
- **Edge thickness** = relationship strength (scaled 1–5)
- **Gray edges** = cross-community connections
- **Labels** = all character names (label size ∝ node size)

---

## 📈 Visual Results

### 1. Community-Colored **Degree Centrality**
Shows how many distinct characters each node interacts with.
- **Tyrion**, **Jon**, and **Sansa** are most connected.
- The **King’s Landing (blue)** cluster is the densest and most active.
- **Daenerys’s (orange)** cluster is internally strong but globally isolated.

---

### 2. Community-Colored **Weighted Betweenness**
Highlights brokers connecting otherwise separate storylines.
- **Robb Stark** ranks 1st: bridges the **North ↔ South** narrative.
- **Tyrion** and **Sansa** act as key intermediaries across factions.
- **Jon Snow** connects the Night’s Watch to the broader realm.
- **Daenerys** remains isolated — strong ties within her group, few cross-links.

---

### 3. Community-Colored **Eigenvector Centrality**
Reveals influence through connections with other influential nodes.
- **Tyrion** and **Sansa** lead again, linked to many high-status characters.
- **Cersei** and **Jaime** rise due to proximity to powerful figures.
- **Jon** drops despite high degree — his connections are local and less prestigious.
- **Daenerys** holds moderate EC within her own isolated cluster.

---

### 4. **Edge Betweenness Centrality**
Visualizes key bridging relationships between communities (red edges):
- **Jon ↔ Samwell**, **Robb ↔ Tyrion**, and **Robert ↔ Daenerys** are high-betweenness ties.
- Removing these edges would fragment the network most severely.

---

## 🏆 Rank Comparison (Top 10 Characters)

| Character | Degree Rank | Betweenness Rank | Eigenvector Rank | Notes |
|------------|--------------|------------------|------------------|-------|
| **Tyrion** | 1 | 2 | 1 | Dominates all metrics — politically and socially central |
| **Sansa** | 2 | 3 | 2 | Connects multiple elite groups, gaining social influence |
| **Robb** | 4 | 1 | 6 | Key broker linking northern and southern factions |
| **Jaime** | 5 | 5 | 3 | Core of Lannister elite |
| **Tywin** | 6 | 10 | 7 | Embedded power, low brokerage |
| **Jon** | 2 | 4 | 18 | Active local hub (The Wall) but isolated globally |
| **Cersei** | 7 | 13 | 5 | Political power within her court |
| **Arya** | 8 | 11 | 9 | Broad but shallow interactions across groups |
| **Joffrey** | 10 | 16 | 4 | Central via proximity to powerful elites |
| **Robert** | 10 | 6 | 16 | Legacy connector between major families |

---

## 💬 Interpretive Summary

| Observation | Implication |
|--------------|-------------|
| **Tyrion** dominates all metrics | Central protagonist both structurally and narratively |
| **Robb** high betweenness but moderate EC | Regional bridge leader, not part of power elite |
| **Sansa** strong in all metrics | Emerging connector between major factions |
| **Jon** active but isolated | Influential within peripheral community |
| **Daenerys** internally strong, globally distant | Independent storyline, isolated from Westeros politics |

---

## 🧩 Structural Insights

- **King’s Landing** cluster forms the *narrative core*.
- **Northern** and **Wall** clusters act as semi-independent modules linked through the Starks.
- **Daenerys’s** network is self-contained, forming an *isolated subgraph*.
- A handful of edges maintain *global cohesion* (high edge betweenness).

---

## 🛠️ Environment Setup

Create and activate a new Conda environment:

```bash
conda create -n gotnet python=3.10
conda activate gotnet
conda install -c conda-forge networkx python-louvain pandas numpy matplotlib seaborn
```
or using the included <requirements.txt>

```bash
conda create -n gotnet --file requirements.txt
```

## 🧩 Credits

- Dataset based on the Game of Thrones Character Network (A. Beveridge & J. Shan, 2016).
- Louvain community detection via python-louvain.
- Visualization built with NetworkX and Matplotlib.