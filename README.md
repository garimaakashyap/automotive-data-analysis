# Automotive Data Analysis

[![Python](https://img.shields.io/badge/Python-3.x-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-Latest-green.svg)](https://pandas.pydata.org/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📋 Overview

This repository contains a comprehensive analysis of automotive repair and service data. The dataset includes **100 vehicle repair records** with **52 attributes**, covering critical information such as repair age, vehicle mileage, causal parts, costs, and customer feedback. The goal of this project is to perform exploratory data analysis (EDA), data cleaning, visualization, and text-based tag generation to provide actionable insights for stakeholders in the automotive industry.

---

## 🎯 Project Objectives

- **Column-wise Analysis**: Perform detailed analysis of each column to understand data types, unique values, distributions, and overall significance for stakeholders
- **Data Cleaning**: Handle missing values, fix inconsistencies in categorical columns, and ensure numerical columns are properly formatted and free from outliers
- **Critical Column Identification**: Identify and analyze the top 5 most insightful columns for stakeholders
- **Data Visualization**: Generate meaningful visualizations (bar plots, histograms, boxplots, etc.) to represent insights effectively
- **Tag Generation**: Extract meaningful tags from free text fields (customer verbatim, correction verbatim) to summarize failure conditions and components
- **Actionable Insights**: Provide comprehensive summary, insights, and recommendations based on the analysis

---

## 📊 Dataset Information

### Source
- **File**: `DA -Task 2..xlsx`
- **Records**: 100 vehicle repair transactions
- **Columns**: 52 attributes
- **Memory Usage**: ~40.8 KB

### Key Fields

#### Identification & Transaction
- `VIN`: Vehicle Identification Number (100 non-null)
- `TRANSACTION_ID`: Unique transaction identifier (100 non-null)
- `REPAIR_DATE`: Date of repair (100 non-null, datetime)
- `SRC_TXN_ID`: Source transaction ID (100 non-null)

#### Vehicle Specifications
- `PLATFORM`: Vehicle platform (100 non-null)
- `BODY_STYLE`: Body style classification (100 non-null)
- `ENGINE`: Engine type (100 non-null)
- `ENGINE_DESC`: Engine description (100 non-null)
- `TRANSMISSION`: Transmission type (100 non-null)
- `TRANSMISSION_DESC`: Transmission description (100 non-null)
- `VIN_MODL_DESGTR`: VIN model designator (100 non-null)
- `LINE_SERIES`: Line series (99 non-null)

#### Repair & Service Information
- `REPAIR_AGE`: Age of vehicle at repair (100 non-null, int64)
- `KM`: Vehicle mileage in kilometers (100 non-null, int64)
- `CAUSAL_PART_NM`: Name of the causal part (95 non-null)
- `GLOBAL_LABOR_CODE`: Global labor code (100 non-null)
- `GLOBAL_LABOR_CODE_DESCRIPTION`: Labor code description (100 non-null)
- `TRANSACTION_CATEGORY`: Category of transaction (100 non-null)
- `COMPLAINT_CD`: Complaint code (100 non-null)
- `COMPLAINT_CD_CSI`: Complaint code CSI (100 non-null)

#### Cost Information
- `REPORTING_COST`: Reporting cost (100 non-null, float64)
- `TOTALCOST`: Total cost of repair (94 non-null, float64)
- `LBRCOST`: Labor cost (100 non-null, float64)

#### Location & Dealer Information
- `STATE`: State location (98 non-null)
- `PLANT`: Manufacturing plant (99 non-null)
- `BUILD_COUNTRY`: Country of build (100 non-null)
- `DEALER_NAME`: Repairing dealer name (100 non-null)
- `REPAIR_DLR_CITY`: Repair dealer city (100 non-null)
- `DEALER_REGION`: Dealer region code (100 non-null)
- `SALES_REGION_CODE`: Sales region code (100 non-null)

#### Text Fields (Free Text)
- `CUSTOMER_VERBATIM`: Customer complaint/feedback (100 non-null)
- `CORRECTION_VERBATIM`: Technician correction notes (100 non-null)

#### Additional Attributes
- `VPPC`: VPPC code (100 non-null)
- `COUNTRY_SALE_ISO`: Country sale ISO code (100 non-null)
- `MEDIA_FLAG`: Media flag indicator (100 non-null)
- `NON_CAUSAL_PART_QTY`: Non-causal part quantity (100 non-null)

### Data Types Summary
- **datetime64[ns]**: 1 column (REPAIR_DATE)
- **float64**: 6 columns (cost-related fields)
- **int64**: 12 columns (IDs, codes, age, mileage)
- **object**: 33 columns (categorical and text fields)

---

## 📈 Column-Wise Analysis

### Data Type Distribution
The dataset contains a mix of:
- **Categorical Fields**: Platform, Body Style, Engine, Transmission, State, Plant, etc.
- **Numerical Fields**: Repair Age, KM (mileage), Costs, Transaction IDs
- **Textual Fields**: Customer verbatim, Correction verbatim (free text)
- **Date Fields**: Repair date
- **Identifier Fields**: VIN, Transaction IDs (complete and unique)

### Missing Value Analysis
- **CAMPAIGN_NBR**: 100% null (0 non-null) - **Removed from analysis**
- **CAUSAL_PART_NM**: 5 missing values (95 non-null)
- **PLANT**: 1 missing value (99 non-null)
- **STATE**: 2 missing values (98 non-null)
- **TOTALCOST**: 6 missing values (94 non-null)
- **OPTN_FAMLY_CERTIFICATION**: 10 missing values (90 non-null)
- **ENGINE_SOURCE_PLANT**: 12 missing values (88 non-null)
- **TRANSMISSION_SOURCE_PLANT**: 12 missing values (88 non-null)

### Column Significance for Stakeholders

#### High-Impact Columns
1. **REPAIR_AGE**: Critical for understanding failure patterns and warranty analysis
2. **KM (Mileage)**: Essential for reliability analysis and maintenance scheduling
3. **TOTALCOST / REPORTING_COST**: Key financial metrics for cost analysis
4. **CAUSAL_PART_NM**: Identifies problematic components requiring attention
5. **CUSTOMER_VERBATIM / CORRECTION_VERBATIM**: Rich text data for sentiment and issue categorization

#### Medium-Impact Columns
- **PLATFORM / BODY_STYLE**: Vehicle segmentation analysis
- **ENGINE / TRANSMISSION**: Powertrain reliability insights
- **STATE / DEALER_REGION**: Geographic failure patterns
- **COMPLAINT_CD**: Standardized complaint categorization

#### Low-Impact Columns
- **VIN**: Unique identifier (no analytical value)
- **TRANSACTION_ID**: Transaction tracking (operational use)
- **CAMPAIGN_NBR**: 100% null (removed)

---

## 🧹 Data Cleaning Summary

### 1. Missing Value Treatment
- **CAMPAIGN_NBR**: Dropped entirely (100% null values)
- **CAUSAL_PART_NM**: Imputed with "UNKNOWN" for missing values
- **TOTALCOST**: Imputed with median value to preserve distribution
- **Categorical Fields**: Imputed with "UNKNOWN" or mode value
- **Numerical Fields**: Imputed with median to avoid mean bias

### 2. Categorical Data Standardization
- Converted all categorical text to uppercase for consistency
- Stripped leading/trailing whitespace
- Fixed inconsistent capitalization (e.g., "Engine" vs "ENGINE")
- Standardized abbreviations and codes

### 3. Numerical Data Cleaning
- **Outlier Treatment**: Used Interquartile Range (IQR) method for cost columns
  - Identified outliers beyond Q3 + 1.5*IQR and Q1 - 1.5*IQR
  - Capped extreme values at 95th percentile
- **Data Type Verification**: Ensured all numerical columns are in correct format
- **Negative Value Check**: Verified no negative costs or invalid numerical entries

### 4. Date Field Validation
- Verified `REPAIR_DATE` is in correct datetime format
- Checked for future dates or invalid date ranges
- Extracted additional features (year, month, day of week) if needed

### 5. Text Field Preprocessing
- Removed extra whitespace from verbatim fields
- Standardized encoding (UTF-8)
- Prepared text fields for tag extraction

---

## 🔍 Critical Columns Analysis

### Top 5 Critical Columns Identified

#### 1. **REPAIR_AGE** (Age of Vehicle at Repair)
- **Significance**: Indicates when vehicles typically require repairs
- **Insight**: Early failures may indicate manufacturing defects; late failures suggest wear patterns
- **Stakeholder Value**: Warranty planning, quality control, predictive maintenance

#### 2. **KM** (Vehicle Mileage)
- **Significance**: Correlates repair frequency with usage
- **Insight**: High mileage failures vs. low mileage failures indicate different root causes
- **Stakeholder Value**: Reliability analysis, maintenance scheduling, warranty terms

#### 3. **TOTALCOST** (Total Repair Cost)
- **Significance**: Financial impact of repairs
- **Insight**: Identifies high-cost failure modes requiring immediate attention
- **Stakeholder Value**: Budget planning, cost optimization, warranty cost analysis

#### 4. **CAUSAL_PART_NM** (Causal Part Name)
- **Significance**: Identifies problematic components
- **Insight**: Pareto analysis reveals which parts cause most issues
- **Stakeholder Value**: Quality improvement priorities, supplier management, design changes

#### 5. **CUSTOMER_VERBATIM / CORRECTION_VERBATIM** (Free Text Fields)
- **Significance**: Rich qualitative data on customer complaints and technician notes
- **Insight**: Natural language processing reveals common themes and failure modes
- **Stakeholder Value**: Customer satisfaction, issue categorization, automated complaint routing

---

## 📊 Visualizations

### Visualization 1: Repair Age Distribution
- **Type**: Histogram / Density Plot
- **Purpose**: Understand typical failure timing
- **Insights**: 
  - Early failures (low repair age) may indicate manufacturing issues
  - Normal distribution suggests expected wear patterns
  - Outliers indicate premature failures

### Visualization 2: Top 10 Causal Parts
- **Type**: Horizontal Bar Chart
- **Purpose**: Identify most problematic components
- **Insights**:
  - Pareto principle: 20% of parts cause 80% of issues
  - Focus improvement efforts on top failure parts
  - Supplier quality assessment

### Visualization 3: Total Cost Distribution
- **Type**: Box Plot / Violin Plot
- **Purpose**: Analyze cost trends and identify outliers
- **Insights**:
  - Median cost indicates typical repair expense
  - Outliers represent high-cost failure modes
  - Cost distribution helps in warranty reserve planning

### Visualization 4: Repair Age vs. Mileage Scatter Plot
- **Type**: Scatter Plot with Trend Line
- **Purpose**: Understand relationship between age and usage
- **Insights**:
  - High mileage, low age = heavy usage vehicles
  - Low mileage, high age = infrequently used vehicles
  - Correlation analysis for failure prediction

### Visualization 5: Cost by Causal Part
- **Type**: Grouped Bar Chart / Heatmap
- **Purpose**: Identify high-cost failure components
- **Insights**:
  - Parts with high frequency AND high cost = priority issues
  - Cost per failure analysis for ROI calculations

---

## 🏷️ Tag Generation from Free Text

### Methodology
Using **CountVectorizer** and **TF-IDF** from scikit-learn to extract meaningful tags from:
- `CUSTOMER_VERBATIM`: Customer complaint text
- `CORRECTION_VERBATIM`: Technician correction notes

### Tag Categories Generated

#### 1. Failure Condition Tags
- **Performance Issues**: "slow", "stalling", "rough idle", "acceleration"
- **Noise Issues**: "rattling", "knocking", "squeaking", "grinding"
- **Visual Issues**: "leak", "smoke", "warning light", "check engine"
- **Functional Failures**: "won't start", "won't shift", "overheating"

#### 2. Component Tags
- **Engine Components**: "engine", "cylinder", "spark plug", "fuel injector"
- **Transmission Components**: "transmission", "clutch", "gearbox"
- **Electrical Components**: "battery", "alternator", "wiring", "sensor"
- **Body/Chassis**: "brake", "suspension", "tire", "wheel"

#### 3. Severity Tags
- **Critical**: "complete failure", "total loss", "catastrophic"
- **Moderate**: "intermittent", "occasional", "sometimes"
- **Minor**: "slight", "minor", "cosmetic"

### Implementation
```python
# Example tag extraction code
from sklearn.feature_extraction.text import CountVectorizer

# Extract top keywords from customer verbatim
vectorizer = CountVectorizer(max_features=50, stop_words='english')
tags = vectorizer.fit_transform(df['CUSTOMER_VERBATIM'])
```

---

## 💡 Summary and Insights

### Key Findings

#### 1. Early Failure Patterns
- **Observation**: Significant number of repairs occur at low repair age (< 1 year)
- **Implication**: Potential manufacturing quality issues or design defects
- **Recommendation**: 
  - Conduct root cause analysis on early failures
  - Review supplier quality for affected components
  - Implement enhanced quality control measures

#### 2. Pareto Principle in Part Failures
- **Observation**: Top 10% of causal parts account for majority of complaints
- **Implication**: Focused improvement efforts can yield significant results
- **Recommendation**:
  - Prioritize redesign/improvement of high-failure parts
  - Engage suppliers for quality improvement initiatives
  - Consider alternative suppliers for critical components

#### 3. Cost Concentration
- **Observation**: High-cost repairs are concentrated in specific failure types
- **Implication**: Financial impact is not evenly distributed
- **Recommendation**:
  - Develop predictive maintenance for high-cost failure modes
  - Create warranty reserve models based on cost distribution
  - Negotiate supplier warranties for expensive components

#### 4. Geographic Patterns
- **Observation**: Certain states/regions show higher failure rates
- **Implication**: Environmental factors or regional usage patterns may influence failures
- **Recommendation**:
  - Analyze regional climate and usage patterns
  - Adjust warranty terms based on geographic risk
  - Regional quality improvement programs

#### 5. Text Analysis Insights
- **Observation**: Common keywords reveal recurring themes (noise, performance, leaks)
- **Implication**: Standardized complaint categorization is possible
- **Recommendation**:
  - Implement automated complaint categorization using NLP
  - Create knowledge base from verbatim text
  - Improve customer service with faster issue identification

### Discrepancies Identified and Approach

#### 1. Missing Values
- **CAMPAIGN_NBR**: 100% null - **Approach**: Removed column entirely
- **CAUSAL_PART_NM**: 5% missing - **Approach**: Imputed with "UNKNOWN" to preserve records
- **TOTALCOST**: 6% missing - **Approach**: Median imputation to maintain distribution
- **Other categorical**: **Approach**: Mode imputation or "UNKNOWN" category

#### 2. Data Quality Issues
- **Inconsistent Casing**: Fixed by standardizing to uppercase
- **Whitespace Issues**: Stripped leading/trailing spaces
- **Outliers in Costs**: Treated using IQR method and capping at 95th percentile

#### 3. Missing Primary Keys
- **VIN**: Complete (100 non-null) - No action needed
- **TRANSACTION_ID**: Complete (100 non-null) - No action needed
- **Verification**: Confirmed uniqueness of key identifiers

### Actionable Recommendations

#### For Quality Engineering
1. **Focus on Early Failures**: Investigate root causes of repairs within first year
2. **Part Improvement Priority**: Target top 5 causal parts for redesign/improvement
3. **Supplier Engagement**: Work with suppliers of high-failure components

#### For Financial Planning
1. **Warranty Reserve Modeling**: Use cost distribution to model warranty reserves
2. **Cost Optimization**: Identify high-cost failure modes for cost reduction initiatives
3. **ROI Analysis**: Calculate return on investment for quality improvements

#### For Operations
1. **Predictive Maintenance**: Develop models to predict failures based on age and mileage
2. **Regional Adjustments**: Adjust service strategies based on geographic patterns
3. **Dealer Training**: Focus training on high-frequency failure types

#### For Customer Service
1. **Automated Categorization**: Implement NLP-based complaint routing
2. **Knowledge Base**: Create searchable database from verbatim text
3. **Proactive Communication**: Use failure patterns to inform customers

#### For Data Management
1. **Data Quality Standards**: Implement validation rules for new data entry
2. **Missing Value Protocols**: Establish procedures for handling missing critical fields
3. **Text Field Guidelines**: Standardize verbatim text collection processes

---

## 📁 Folder Structure

```
automotive-data-analysis/
│
├── DA -Task 2..xlsx          # Original dataset
├── analysis.ipynb             # Jupyter notebook with full analysis
├── data_analysis.py           # Python script version (optional)
├── README.md                  # Project overview and documentation
├── requirements.txt           # Python dependencies
├── visuals/                   # Folder containing saved plots
│   ├── repair_age_distribution.png
│   ├── top_causal_parts.png
│   ├── cost_distribution.png
│   ├── age_vs_mileage.png
│   └── cost_by_part.png
└── results/                   # Generated outputs
    ├── cleaned_data.csv       # Cleaned dataset
    ├── tags_summary.csv       # Extracted tags
    └── insights_report.pdf    # Detailed insights report
```

---

## 🛠️ Tools & Libraries

### Core Libraries
- **Python 3.x**: Programming language
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computing

### Visualization
- **Matplotlib**: Basic plotting and visualization
- **Seaborn**: Statistical data visualization

### Text Processing
- **scikit-learn**: CountVectorizer, TF-IDF for tag extraction
- **NLTK** (optional): Advanced natural language processing

### Additional Tools
- **Jupyter Notebook**: Interactive development environment
- **Excel**: Data source format

---

## 🚀 How to Run

### Prerequisites
1. **Python 3.7+** installed on your system
2. **Jupyter Notebook** or **Jupyter Lab** (optional, for notebook version)

### Installation Steps

1. **Clone this repository** (if applicable):
   ```bash
   git clone https://github.com/garimaakashyap/automotive-data-analysis.git
   cd automotive-data-analysis
   ```

2. **Install required libraries**:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn openpyxl
   ```
   
   Or use the requirements file:
   ```bash
   pip install -r requirements.txt
   ```

3. **Prepare your data**:
   - Place `DA -Task 2..xlsx` in the project root directory
   - Ensure the file name matches exactly

4. **Run the analysis**:
   
   **Option A: Jupyter Notebook**
   ```bash
   jupyter notebook analysis.ipynb
   ```
   Then run all cells in the notebook.
   
   **Option B: Python Script**
   ```bash
   python data_analysis.py
   ```

5. **View results**:
   - Visualizations will be displayed and saved in the `visuals/` folder
   - Generated tags and cleaned data will be saved in the `results/` folder

---

## 📝 Code Structure

### Main Analysis Steps

1. **Data Loading**
   ```python
   import pandas as pd
   df = pd.read_excel('DA -Task 2..xlsx')
   ```

2. **Column Analysis**
   - Data type inspection
   - Missing value analysis
   - Unique value counts
   - Distribution analysis

3. **Data Cleaning**
   - Missing value imputation
   - Categorical standardization
   - Outlier treatment
   - Data type conversion

4. **Critical Column Analysis**
   - Statistical summaries
   - Distribution plots
   - Correlation analysis

5. **Visualization Generation**
   - Repair age distribution
   - Top causal parts
   - Cost analysis
   - Relationship plots

6. **Tag Extraction**
   - Text preprocessing
   - CountVectorizer application
   - Tag frequency analysis
   - Tag categorization

7. **Insights Generation**
   - Summary statistics
   - Key findings
   - Recommendations

---

## 📊 Expected Outputs

### Visualizations
- **Repair Age Distribution**: Histogram showing age at repair
- **Top 10 Causal Parts**: Bar chart of most frequent failure parts
- **Cost Distribution**: Box plot of repair costs
- **Age vs. Mileage**: Scatter plot with correlation
- **Cost by Part**: Grouped analysis of cost per component

### Generated Files
- **cleaned_data.csv**: Preprocessed dataset
- **tags_summary.csv**: Extracted tags with frequencies
- **column_analysis_report.txt**: Detailed column statistics
- **insights_summary.txt**: Key findings and recommendations

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

---

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

---

## 👤 Author

**Garima Kashyap**

- **Role**: Data Analyst
- **Skills**: Python | EDA | NLP | Data Visualization
- **LinkedIn**: [https://www.linkedin.com/in/garima-kashyap-75b1202b8/]
- **Email**: [garimakashyap2121@gmail.com]
- **GitHub**: [https://github.com/garimaakashyap]

---

## 🙏 Acknowledgments

- Dataset provided for analysis purposes
- Open-source community for excellent Python libraries
- Automotive industry stakeholders for domain insights

---

## 📚 Additional Resources

### Related Documentation
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [Matplotlib Gallery](https://matplotlib.org/stable/gallery/index.html)
- [Seaborn Tutorial](https://seaborn.pydata.org/tutorial.html)
- [scikit-learn Text Processing](https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction)

### Best Practices
- Data cleaning methodologies
- EDA best practices
- Visualization design principles
- NLP for automotive text analysis

---

## 📈 Future Enhancements

- [ ] Machine learning models fo
