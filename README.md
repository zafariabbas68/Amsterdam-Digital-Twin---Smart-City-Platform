

# 🏙️ Amsterdam Digital Twin -Smart City Platform v5.3

[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-CC--BY--4.0-green)](LICENSE)
[![PostGIS](https://img.shields.io/badge/PostGIS-3.0%2B-orange)](https://postgis.net/)
[![GeoServer](https://img.shields.io/badge/GeoServer-2.23%2B-brightgreen)](http://geoserver.org/)
[![Folium](https://img.shields.io/badge/Folium-0.19%2B-yellow)](https://python-visualization.github.io/folium/)

<div align="center">
  <img src="amsterdam_ultimate_dashboard.png" alt="Amsterdam Digital Twin Ultimate Dashboard" width="900"/>
  <p><em><b>Figure 1:</b> Ultimate Statistical Dashboard - 20 Publication-Quality Visualizations</em></p>
</div>

## 📋 **Table of Contents**
- [Overview](#-overview)
- [Key Features](#-key-features)
- [Visualization Gallery](#-visualization-gallery)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Output Files](#-output-files)
- [Interactive Map](#-interactive-map)
- [Contributing](#-contributing)
- [License](#-license)
- [Citation](#-citation)
- [Contact](#-contact)

## 🎯 **Overview**

The **Amsterdam Digital Twin v5.3** is a production-ready, research-grade smart city platform that integrates multi-source urban data to create a comprehensive digital representation of Amsterdam. This system demonstrates professional geoinformatics engineering, combining:

- 🏢 **3D City Model** - 400+ buildings with realistic attributes (height: 3-180m)
- 🚗 **Real-time Traffic Simulation** - 672 traffic measurements across 7 major arteries
- 🌍 **Environmental Monitoring** - 576 air quality measurements from 6 stations (NO₂, PM10, PM2.5, O₃)
- 📊 **Advanced Analytics** - Bootstrap confidence intervals, Monte Carlo uncertainty propagation
- 🗺️ **Interactive Visualization** - 20+ professional plots + interactive WebGIS map

## ✨ **Key Features**

### 📊 **Data Integration**
- **Buildings**: 3DBAG-compatible building footprints with height, function, and energy labels
- **Traffic**: NDW-style traffic data with 15-minute temporal resolution
- **Air Quality**: RIVM-compatible measurements (NO₂, PM10, PM2.5, O₃)

### 🔬 **Spatial Analytics**
- **Haversine Distance Calculation**: Accurate geodesic distances between buildings and roads
- **Inverse Distance Weighting (IDW)**: Spatial interpolation of air quality
- **Traffic Exposure Modeling**: Building-level exposure scores based on road proximity

### 📈 **Statistical Validation**
- **Bootstrap Confidence Intervals**: 95% CI for correlation estimates
- **Monte Carlo Uncertainty**: Scenario simulations with uncertainty propagation
- **Regression Diagnostics**: Residual plots, Q-Q plots, R² analysis

### 🗄️ **Database Integration**
- **PostGIS**: Full spatial database support with geometry columns
- **GeoServer Ready**: OGC API Features collections and GeoJSON exports
- **Spatial Indexing**: Optimized for spatial queries

### 🌍 **Standards Compliance**
- **OGC API Features**: Compliant metadata and endpoints
- **INSPIRE Directive**: EU spatial data infrastructure standards
- **FAIR Principles**: Findable, Accessible, Interoperable, Reusable

## 🖼️ **Visualization Gallery**

### Ultimate Statistical Dashboard (20 Plots)

<div align="center">
  <img src="amsterdam_ultimate_dashboard.png" alt="Ultimate Statistical Dashboard" width="1000"/>
  <p><em><b>Figure 2:</b> Complete 20-panel dashboard showing traffic patterns, air quality, correlation analysis, spatial distribution, and policy impacts</em></p>
</div>

### Interactive Plotly Dashboard

<div align="center">
  <a href="amsterdam_interactive_dashboard.html">
    <img src="amsterdam_interactive_dashboard copy.html" alt="Interactive Dashboard Preview" width="800"/>
  </a>
  <p><em><b>Figure 3:</b> Interactive Plotly dashboard with 9 linked plots - hover, zoom, and explore</em></p>
</div>

### WebGIS Interactive Map

<div align="center">
  <a href="amsterdam_digital_twin_ultimate.html">
    <img src="amsterdam_digital_twin_ultimate.html" alt="WebGIS Map Preview" width="800"/>
  </a>
  <p><em><b>Figure 4:</b> Interactive Folium map with three layers: 🏢 Buildings (colored by height), 🚗 Traffic locations (colored by intensity), and 🌍 Air quality stations</em></p>
</div>

## 📊 **Sample Results from Latest Run**

```
📊 DATA SUMMARY:
   • Buildings: 330 (3DBAG LoD2.2)
   • Traffic: 672 measurements (15-min intervals)
   • Air Quality: 576 measurements (hourly)

🔬 VALIDATION (95% CI):
   • Traffic-NO₂ correlation: r = 0.938 [0.917, 0.962]
   • R² = 0.880
   • Mean building height: 18.7m

🔮 SCENARIO (20% LEZ with 95% CI):
   • NO₂ reduction: 2.05 [1.62, 2.51] µg/m³
   • CO₂ savings: 9.8 [7.5, 12.2] tons/day
```

## 🏗️ **System Architecture**

```
┌─────────────────────────────────────────────────────────────┐
│                    DATA LAYER                               │
├───────────────┬─────────────────┬───────────────────────────┤
│  Buildings    │    Traffic      │     Air Quality           │
│  (3DBAG)      │    (NDW)        │     (RIVM)                │
├───────────────┴─────────────────┴───────────────────────────┤
│                    ANALYTICS LAYER                           │
├─────────────────────────────────────────────────────────────┤
│  • Spatial Analytics (Haversine, IDW)                        │
│  • Statistical Validation (Bootstrap, Monte Carlo)           │
│  • Scenario Simulation (LEZ 10-40%)                          │
├─────────────────────────────────────────────────────────────┤
│                    DATABASE LAYER                            │
├─────────────────────────────────────────────────────────────┤
│  • PostGIS (buildings_3d, traffic_measurements, air_quality)│
│  • GeoServer OGC API Features                                │
├─────────────────────────────────────────────────────────────┤
│                    VISUALIZATION LAYER                       │
├───────────────┬─────────────────┬───────────────────────────┤
│  Matplotlib   │    Plotly       │      Folium               │
│  Dashboard    │    Dashboard    │      WebGIS               │
└───────────────┴─────────────────┴───────────────────────────┘
```

## 🛠️ **Technology Stack**

| Category | Technologies |
|----------|-------------|
| **Core** | Python 3.10+, NumPy, Pandas, GeoPandas |
| **Spatial** | Shapely, PyProj, Fiona, Rtree |
| **Analytics** | SciPy, Scikit-learn, Statsmodels |
| **Statistics** | Bootstrap, Monte Carlo, Linear Regression |
| **Visualization** | Matplotlib, Seaborn, Plotly, Folium |
| **Database** | PostgreSQL, PostGIS, SQLAlchemy, Psycopg2 |
| **Standards** | OGC API Features, INSPIRE, ISO 19115 |
| **Development** | Jupyter, Git, Conda |

## 📦 **Installation**

### Prerequisites
- Python 3.10 or higher
- PostgreSQL with PostGIS extension (optional)
- Conda (recommended) or pip

### Quick Install with Conda

```bash
# Clone the repository
git clone https://github.com/zafariabbas68/Amsterdam-Digital-Twin---Smart-City-Platform.git
cd Amsterdam-Digital-Twin---Smart-City-Platform

# Create conda environment
conda create -n amsterdam-twin python=3.10 -y
conda activate amsterdam-twin

# Install dependencies
pip install -r requirements.txt

# For TensorFlow support (optional)
pip install tensorflow
```

### PostGIS Setup (Optional)

```sql
-- Create database with PostGIS
CREATE DATABASE amsterdam_twin_17;
\c amsterdam_twin_17
CREATE EXTENSION postgis;
```

## 🚀 **Quick Start**

```python
# In Jupyter Notebook or Python script
from amsterdam_digital_twin import main

# Execute the full pipeline (generates all plots and maps)
main()
```

## 📁 **Output Files Generated**

When you run the digital twin, these files are created in your working directory:

| File | Description | Preview |
|------|-------------|---------|
| `amsterdam_ultimate_dashboard.png` | 20 publication-quality statistical plots | ✅ [View Above](#visualization-gallery) |
| `amsterdam_interactive_dashboard.html` | Interactive Plotly dashboard with 9 plots | ✅ [Interactive](#visualization-gallery) |
| `amsterdam_digital_twin_ultimate.html` | WebGIS map with all three layers | ✅ [Interactive](#visualization-gallery) |
| `ogc_collections.json` | OGC API Features metadata | 📄 JSON |
| `buildings_sample.geojson` | GeoJSON sample for GeoServer | 📄 GeoJSON |

## 🗺️ **Interactive Map Features**

The WebGIS map includes three fully interactive layers:

### 🏢 **Buildings Layer**
- 330+ building footprints
- Color-coded by height (dark red >50m, red 30-50m, blue 15-30m, green <15m)
- Popup with height, type, year, energy label

### 🚗 **Traffic Locations Layer**
- Sampled traffic points (100 locations)
- Color-coded by intensity (red >3000, orange 2000-3000, yellow <2000)
- Popup with intensity and location

### 🌍 **Air Quality Stations Layer**
- 6 monitoring stations across Amsterdam
- Popup with NO₂ and PM10 averages
- Green marker icons

## ✅ **Standards Compliance**

| Standard | Compliance | Implementation |
|----------|------------|----------------|
| **OGC API Features** | ✅ Full | JSON collections with links |
| **INSPIRE Directive** | ✅ Full | EU spatial data infrastructure |
| **CityGML / CityJSON** | ✅ Partial | Building attributes ready |
| **ISO 19115** | ✅ Full | Comprehensive metadata |
| **FAIR Principles** | ✅ Full | Findable, Accessible, Interoperable, Reusable |

## 📝 **Citation**

If you use this project in your research or work, please cite:

```bibtex
@software{amsterdam_digital_twin_2025,
  author = {Zafari, Ghulam Abbas},
  title = {Amsterdam Digital Twin: Ultimate Smart City Platform v5.3},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/zafariabbas68/Amsterdam-Digital-Twin---Smart-City-Platform}
}
```

## 📬 **Contact**

**Ghulam Abbas Zafari** - Geoinformatics Engineer

- 📧 Email: [ghulamabbas.zafari@gmail.com](mailto:ghulamabbas.zafari@gmail.com)
- 🔗 LinkedIn: [ghulamabbaszafari](https://linkedin.com/in/ghulamabbaszafari)
- 🐙 GitHub: [zafariabbas68](https://github.com/zafariabbas68)
- 🌐 Portfolio: [personal-website-gaz.onrender.com](https://personal-website-gaz.onrender.com)

---

<div align="center">
  <p>🏙️ <strong>Amsterdam Digital Twin v5.3</strong> - 20 Visualizations • Monte Carlo Uncertainty • Bootstrap CI • PostGIS • GeoServer • WebGIS</p>
  <p>⭐ Star this repository if you find it useful!</p>
  <p>📊 <strong>Latest Results:</strong> r = 0.938 | R² = 0.880 | 20% LEZ: 2.05 µg/m³ NO₂ reduction</p>
</div>
