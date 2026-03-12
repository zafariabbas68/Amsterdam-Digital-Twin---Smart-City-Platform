
# 🏙️ Amsterdam Digital Twin - Smart City Platform

[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-CC--BY--4.0-green)](LICENSE)
[![PostGIS](https://img.shields.io/badge/PostGIS-3.0%2B-orange)](https://postgis.net/)
[![GeoServer](https://img.shields.io/badge/GeoServer-2.23%2B-brightgreen)](http://geoserver.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15%2B-yellow)](https://tensorflow.org/)

<div align="center">
  <img src="docs/images/dashboard_preview.png" alt="Amsterdam Digital Twin Dashboard" width="800"/>
  <p><em>Professional statistical dashboard with 16+ publication-quality visualizations</em></p>
</div>

## 📋 **Table of Contents**
- [Overview](#-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Installation](#-installation)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Output Files](#-output-files)
- [Screenshots](#-screenshots)
- [Contributing](#-contributing)
- [License](#-license)
- [Citation](#-citation)
- [Contact](#-contact)

## 🎯 **Overview**

The **Amsterdam Digital Twin** is a production-ready smart city platform that integrates multi-source urban data to create a comprehensive digital representation of Amsterdam. This system demonstrates professional-grade geoinformatics engineering, combining:

- 🏢 **3D City Model** - 400+ buildings with realistic attributes
- 🚗 **Real-time Traffic Simulation** - 672 traffic measurements across major arteries
- 🌍 **Environmental Monitoring** - 576 air quality measurements from 6 stations
- 📊 **Advanced Analytics** - Statistical validation, spatial analysis, scenario modeling
- 🗺️ **Interactive Visualization** - Professional dashboards and WebGIS maps

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

### 🗺️ **Visualization Suite**
- **16-Panel Statistical Dashboard**: Publication-quality matplotlib plots
- **Interactive Plotly Dashboard**: Hoverable, zoomable analytics
- **Fixed WebGIS Map**: Three-layer map with building, traffic, and air quality overlays

### 🗄️ **Database Integration**
- **PostGIS**: Full spatial database support with geometry columns
- **GeoServer Ready**: OGC API Features collections and GeoJSON exports
- **Spatial Indexing**: Optimized for spatial queries

### 🌍 **Standards Compliance**
- **OGC API Features**: Compliant metadata and endpoints
- **INSPIRE Directive**: EU spatial data infrastructure standards
- **FAIR Principles**: Findable, Accessible, Interoperable, Reusable

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

### Option 1: Conda Environment (Recommended)

```bash
# Clone the repository
[git clone https://github.com/yourusername/amsterdam-digital-twin.git](https://github.com/zafariabbas68/Amsterdam-Digital-Twin---Smart-City-Platform.git)
cd amsterdam-digital-twin

# Create conda environment
conda create -n amsterdam-twin python=3.10 -y
conda activate amsterdam-twin

# Install dependencies
pip install -r requirements.txt

# For TensorFlow support (optional)
pip install tensorflow
```

### Option 2: Pip Installation

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install geopandas pandas numpy scipy scikit-learn matplotlib seaborn plotly folium
pip install psycopg2-binary sqlalchemy geoalchemy2
```

### PostGIS Setup (Optional)

```sql
-- Create database with PostGIS
CREATE DATABASE amsterdam_twin_17;
\c amsterdam_twin_17
CREATE EXTENSION postgis;
```

## 🚀 **Quick Start**

### Run the Complete Digital Twin

```python
# In Jupyter Notebook or Python script
from amsterdam_digital_twin import main

# Execute the full pipeline
main()
```

### Or Run Step-by-Step

```python
# 1. Initialize data loader
loader = DutchDataLoader()
bbox = "4.85,52.33,4.95,52.40"

# 2. Load data
buildings = loader.load_3dbag_buildings(bbox)
traffic = loader.load_ndw_traffic()
air_quality = loader.load_rivm_air_quality()

# 3. Run spatial analytics
analytics = SpatialAnalytics(buildings)
buildings = analytics.calculate_traffic_exposure(traffic)
buildings = analytics.interpolate_air_quality(air_quality)

# 4. Statistical validation
stats = EnhancedStatisticalValidation.traffic_no2_correlation_with_ci(traffic, air_quality)

# 5. Run scenarios
engine = EnhancedScenarioEngine(traffic, air_quality, buildings)
scenarios = engine.run_all_scenarios()

# 6. Create visualizations
viz = EnhancedStatisticalVisualizer(traffic, air_quality, buildings, stats, scenarios)
viz.create_professional_dashboard()

# 7. Create web map
map_viz = FixedWebGISVisualizer(buildings, traffic, air_quality)
webmap = map_viz.create_fixed_map()
webmap.save('amsterdam_digital_twin.html')
```

## 📁 **Project Structure**

```
amsterdam-digital-twin/
│
├── 📂 data/
│   ├── buildings/          # Building data
│   ├── traffic/            # Traffic measurements
│   └── air_quality/        # Air quality data
│
├── 📂 src/
│   ├── __init__.py
│   ├── data_loader.py      # DutchDataLoader class
│   ├── analytics.py        # SpatialAnalytics class
│   ├── statistics.py       # Statistical validation
│   ├── scenarios.py        # Scenario engine
│   ├── visualizations.py   # Dashboard generators
│   └── postgis_manager.py  # Database connector
│
├── 📂 notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_spatial_analytics.ipynb
│   └── 03_full_pipeline.ipynb
│
├── 📂 docs/
│   ├── images/             # Screenshots and diagrams
│   └── api/                # API documentation
│
├── 📂 tests/
│   ├── test_analytics.py
│   └── test_statistics.py
│
├── requirements.txt
├── environment.yml
├── README.md
├── LICENSE
└── .gitignore
```

## 📊 **Output Files**

When you run the digital twin, the following files are generated:

| File | Description |
|------|-------------|
| `amsterdam_professional_dashboard.png` | 16 publication-quality statistical plots |
| `amsterdam_interactive_dashboard.html` | Interactive Plotly dashboard |
| `amsterdam_digital_twin_fixed.html` | WebGIS map with all three layers |
| `ogc_collections.json` | OGC API Features metadata |
| `buildings_sample.geojson` | GeoJSON sample for GeoServer |

## ✅ **Standards Compliance**

This project is designed to be compliant with international geospatial standards:

| Standard | Compliance | Implementation |
|----------|------------|----------------|
| **OGC API Features** | ✅ Full | JSON collections with links |
| **INSPIRE Directive** | ✅ Full | EU spatial data infrastructure |
| **CityGML / CityJSON** | ✅ Partial | Building attributes ready |
| **ISO 19115** | ✅ Full | Comprehensive metadata |
| **FAIR Principles** | ✅ Full | Findable, Accessible, Interoperable, Reusable |
| **BAG Register** | ✅ Compatible | Building data structure |
| **NDW Format** | ✅ Compatible | Traffic data structure |
| **RIVM Format** | ✅ Compatible | Air quality data structure |

## 📸 **Screenshots**

<div align="center">
  <img src="docs/images/dashboard_preview.png" alt="Statistical Dashboard" width="400"/>
  <img src="docs/images/map_preview.png" alt="WebGIS Map" width="400"/>
  <p><em>Left: Statistical Dashboard | Right: Interactive WebGIS Map</em></p>
</div>

<div align="center">
  <img src="docs/images/layers_preview.png" alt="Map Layers" width="800"/>
  <p><em>Three-layer map with Buildings, Traffic, and Air Quality overlays</em></p>
</div>

## 🤝 **Contributing**

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow PEP 8 style guide
- Add docstrings for all functions and classes
- Include unit tests for new features
- Update documentation as needed

## 📄 **License**

This project is licensed under the Creative Commons Attribution 4.0 International License (CC-BY-4.0) - see the [LICENSE](LICENSE) file for details.

This license allows for:
- ✓ Commercial use
- ✓ Modification
- ✓ Distribution
- ✓ Private use

With the condition that appropriate credit is given.

## 📝 **Citation**

If you use this project in your research or work, please cite:

```bibtex
@software{amsterdam_digital_twin_2025,
  author = {Zafari, Ghulam Abbas},
  title = {Amsterdam Digital Twin: Smart City Platform},
  year = {2025},
  publisher = {GitHub},
  url = {https://github.com/yourusername/amsterdam-digital-twin}
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
  <p>🏙️ <strong>Amsterdam Digital Twin</strong> - Building the future of smart cities, one dataset at a time.</p>
  <p>⭐ Star this repository if you find it useful!</p>
</div>
```

## 📂 **Repository Name Options**

```
amsterdam-digital-twin
amsterdam-smart-city
urban-digital-twin
city-digital-twin
smart-city-platform
```

## 🏷️ **GitHub Topics/Tags**

```
digital-twin
smart-city
gis
postgis
geoserver
amsterdam
urban-planning
data-science
python
visualization
spatial-analytics
ogc-standards
3d-city-model
environmental-monitoring
traffic-analysis
