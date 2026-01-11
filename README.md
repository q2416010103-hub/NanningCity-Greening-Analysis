# NanningCity-Greening-Analysis
# Nanning City Greening Analysis Based on Google Earth Engine (GEE)

## Quick Links
- **GEE Script**: [View Full Code](https://code.earthengine.google.com/fdcf76e2953a86ad2b10c685fffd8c70)
- **Web Application**: [Live Demo](https://focal-lens-483706-u2.projects.earthengine.app/view/nanningcity-green-analysis)
- **GitHub Repository**: [Source Code](https://github.com/q2416010103/nanning-greening-analysis)

## Project Overview
This project utilizes Google Earth Engine (GEE) to analyze the greening degree in Nanning, Guangxi from 2021 to 2025. It accesses multi-temporal satellite imagery data on the GEE platform, applies vegetation indices like NDVI (Normalized Difference Vegetation Index) to identify and classify vegetation areas, and quantitatively evaluates greening status and changes in Nanning City.

## Features
- **Multi-year Analysis**: 2021-2025 annual greening assessment
- **NDVI Calculation**: Normalized Difference Vegetation Index computation
- **Interactive Web App**: User-friendly interface for data exploration
- **Data Export**: Export results as GeoTIFF and CSV formats
- **Zonal Statistics**: Calculate statistics for administrative boundaries
- **Time-series Analysis**: Track vegetation changes over time

## Resources
### Data Files
1. **Nanning City Boundary**: `users/q2416010103/NanningCity` (uploaded shapefile)
2. **Sentinel-2 Satellite Imagery**: COPERNICUS/S2_HARMONIZED collection

### Analysis Flow
1. Import and visualize feature layers
2. Process satellite image collections
3. Calculate NDVI and other vegetation indices
4. Perform zonal statistics analysis
5. Create interactive web application
6. Export and publish results

## Getting Started

### Prerequisites
1. Google Earth Engine account (sign up at https://earthengine.google.com/)
2. Google Chrome browser (recommended)
3. Basic knowledge of JavaScript

### Usage Instructions

#### 1. Access the Web Application
Visit: https://focal-lens-483706-u2.projects.earthengine.app/view/nanningcity-green-analysis

#### 2. Use the GEE Script
1. Open the GEE Code Editor: https://code.earthengine.google.com/
2. Paste the script from: https://code.earthengine.google.com/fdcf76e2953a86ad2b10c685fffd8c70
3. Click "Run" to execute the analysis
4. Use the control panel to interact with the application

#### 3. Control Panel Functions
- **Year Selection**: Choose analysis year (2021-2025)
- **Display NDVI**: Show vegetation index map
- **Calculate Statistics**: Compute mean NDVI and standard deviation
- **Export Data**: Download results in various formats

## Code Structure

### Main Components
```javascript
// 1. Import Nanning boundary
var nanning = ee.FeatureCollection('users/q2416010103/NanningCity');

// 2. Annual analysis function
function analyzeYear(year) {
  var s2 = ee.ImageCollection('COPERNICUS/S2_HARMONIZED')
    .filterBounds(nanning)
    .filterDate(year + '-03-01', year + '-11-30')
    .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 20));
  
  return s2.median()
    .normalizedDifference(['B8', 'B4'])
    .rename('NDVI_' + year);
}

// 3. Web application interface
var panel = ui.Panel({style: {width: '300px', padding: '10px'}});
ui.root.insert(0, panel);
```

### Key Functions
1. **Data Import**: Load Nanning boundary and Sentinel-2 imagery
2. **NDVI Calculation**: Compute vegetation index using B8 (NIR) and B4 (Red) bands
3. **Statistical Analysis**: Calculate mean, standard deviation, and zonal statistics
4. **Visualization**: Display results with color-coded maps
5. **Export**: Save results to Google Drive

## Methodology

### NDVI Calculation
```
NDVI = (NIR - Red) / (NIR + Red)
```
- **NIR Band**: Sentinel-2 Band 8 (842nm)
- **Red Band**: Sentinel-2 Band 4 (665nm)

### Analysis Steps
1. **Data Collection**: Sentinel-2 imagery for growing season (March-November)
2. **Preprocessing**: Cloud filtering (<20% cloud cover)
3. **Image Compositing**: Median composite for each year
4. **Index Calculation**: Compute NDVI for each pixel
5. **Statistical Analysis**: Calculate spatial statistics within Nanning boundary
6. **Visualization**: Create maps and charts for interpretation

## Results and Outputs

### Visual Outputs
- **NDVI Maps**: Annual vegetation index distribution
- **Greening Classification**: Vegetation density categories
- **Change Maps**: Year-to-year vegetation changes
- **Statistical Charts**: Time-series trends and comparisons

### Data Exports
1. **GeoTIFF Files**: Raster data for GIS analysis
2. **CSV Files**: Statistical tables for further analysis
3. **Interactive Maps**: Web-based visualization

### Key Findings
- **Annual Trends**: Track vegetation changes from 2021 to 2025
- **Spatial Patterns**: Identify high and low greening areas
- **Seasonal Variations**: Analyze growth patterns throughout the year
- **Urban-Rural Differences**: Compare vegetation density across different zones

## Applications

### Urban Planning
- Green space assessment and planning
- Urban expansion impact analysis
- Ecological corridor design

### Environmental Monitoring
- Vegetation health assessment
- Climate change impact evaluation
- Ecosystem services quantification

### Policy Support
- Greening policy effectiveness evaluation
- Environmental indicator development
- Sustainable development planning

## Limitations and Considerations
1. **Cloud Cover**: May affect data availability in certain periods
2. **Spatial Resolution**: 10m resolution may not capture small green spaces
3. **Atmospheric Effects**: Requires proper atmospheric correction
4. **Seasonal Variability**: Consider seasonal patterns in analysis

## Future Enhancements
1. **Additional Indices**: Include EVI, SAVI, and other vegetation indices
2. **Higher Resolution**: Incorporate higher resolution imagery where available
3. **Machine Learning**: Implement classification algorithms for vegetation types
4. **Real-time Monitoring**: Develop near-real-time analysis capabilities
5. **Comparative Analysis**: Compare Nanning with other cities

## Contact and Support
- **Project Developer**: q2416010103
- **GEE Profile**: https://code.earthengine.google.com/
- **Application URL**: https://focal-lens-483706-u2.projects.earthengine.app/view/nanningcity-green-analysis

## License and Citation
This project is developed for educational and research purposes. Please cite appropriately if used in publications.

## Acknowledgments
- Google Earth Engine for providing the platform and data
- European Space Agency for Sentinel-2 satellite imagery
- GEOM2138/2151 Cloud-based open-source GIS course for guidance

---

*For more information, please visit the web application or explore the GEE script directly.*
Name：Xiyuan Qin
Email:2416010103@s.upc.edu.cn
Github:q2416010103-Hub
