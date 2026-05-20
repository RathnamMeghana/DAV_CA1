# EV Transition Readiness Composite Index 2024

This project develops a country-level **EV Transition Readiness Composite Index for 2024**. The aim is to compare how ready different countries are for the transition to electric vehicles by looking at more than one factor.

EV readiness is not only about EV sales. A country may have high EV sales but still have weak charging infrastructure, low clean-energy readiness, or weaker national conditions to support long-term EV growth. Because of this, the index combines EV adoption, EV penetration, charging infrastructure, national readiness and clean energy readiness into one final score.

## Project Overview

The final index is built using **52 countries** and **11 indicators**. These indicators are grouped into five sub-indices:

1. **EV Adoption**
   - EV sales share
   - EV stock share

2. **EV Penetration**
   - EV stock per 1,000 people
   - Total public chargers per 1,000 EVs

3. **Charging Infrastructure**
   - Slow chargers per 100,000 people
   - Fast chargers per 100,000 people

4. **National Readiness**
   - GDP per capita PPP
   - Electric power consumption

5. **Clean Energy Readiness**
   - Low-carbon electricity share
   - Renewable installed capacity share
   - Renewable generation share

Each sub-index contributes **20%** to the final EV Transition Readiness Index.

## Data Sources

The project uses data from several public sources:

- International Energy Agency Global EV Data Explorer
- World Bank indicators
- Our World in Data
- CountryEconomy electricity generation data
- Ayvens Mobility Guide 2024
- World Economic Forum Energy Transition Index 2024
- Yale Environmental Performance Index 2024

The cleaned and imputed dataset used for the final index is:

```text
Cleaned_Datasets/EV_Index_Cleaned_Imputed_2024.csv
```

The imputation flags file is:

```text
Cleaned_Datasets/EV_Index_Imputation_Flags_2024.csv
```

The final generated outputs are:

```text
EV_Index_Normalised_2024.csv
EV_Index_Standardized_2024.csv
EV_Transition_Readiness_Index_2024.csv
```

## Main Steps

### 1. Data Cleaning and Imputation

The raw datasets were cleaned and merged into one country-level dataset. Country names were standardised, non-country rows were removed, and derived indicators were created.

Missing data was handled carefully. Countries with too many missing core values were removed. Remaining missing values were imputed using either the mean or median depending on skewness:

- Highly skewed indicators used median imputation.
- Less skewed indicators used mean imputation.

An imputation flags dataset was also created to show which values were filled.

### 2. Multivariate Analysis

Multivariate analysis was used to understand the structure of the data before building the final index.

This included:

- Descriptive statistics
- Correlation matrix
- Correlation heatmap
- Sub-index correlation checks
- Scatterplots with trend lines
- PCA
- K-Means clustering

The analysis helped check whether the selected indicators behaved sensibly and whether the five sub-index structure was suitable.

### 3. Standardisation and PCA

The indicators were standardised before PCA so that all variables had a mean close to 0 and a standard deviation close to 1. This was needed because PCA is sensitive to scale.

PCA was used to check the main patterns in the dataset. The first three principal components explained a large share of the variation:

- PC1 explained 47.6%
- PC2 explained 17.7%
- PC3 explained 10.9%

Together, the first three components explained about 76.2% of the variation.

### 4. K-Means Clustering

K-Means clustering was used to group countries with similar EV readiness profiles. The elbow method was used to support the cluster choice, and the clustering was visualised using PCA scores.

The clustering helped show which countries had similar strengths and weaknesses across the EV readiness indicators.

### 5. Normalisation

Min-Max normalisation was used to place all indicators on the same 0 to 1 scale. This made the variables comparable before weighting and aggregation.

Higher values were kept as stronger EV readiness values.

### 6. Weighting and Aggregation

The normalised indicator values were converted into 0 to 10 scores. Each sub-index was calculated first, and then the five sub-indices were combined into the final composite index.

Each sub-index was given an equal weight of 20%:

```text
Final EV Index =
20% EV Adoption
+ 20% EV Penetration
+ 20% Charging Infrastructure
+ 20% National Readiness
+ 20% Clean Energy Readiness
```

The final score was converted to a 0 to 100 scale.

### 7. Link to Other Indices

The final EV Transition Readiness Index was compared with existing external indices:

- Ayvens Mobility Guide 2024
- World Economic Forum Energy Transition Index 2024
- Yale Environmental Performance Index 2024

The strongest EV-focused comparison was with Ayvens Mobility Guide 2024. The relationship was strongly positive:

- Pearson correlation: 0.733
- Spearman correlation: 0.703

The WEF Energy Transition Index also showed a strong positive relationship:

- Pearson correlation: 0.721

This helped support the final index because countries that scored well in this constructed index also tended to perform well in recognised external measures.

## Final Results

The highest ranked countries in the final EV Transition Readiness Index were:

1. Norway
2. Iceland
3. Denmark
4. Sweden
5. Netherlands

Norway ranked first with a final score of **86.63**, while Iceland ranked second with **84.96**.

The Nordic countries performed strongly because they had balanced performance across EV adoption, infrastructure and clean energy readiness.

Lower-ranked countries usually had weaker charging infrastructure, lower EV penetration, weaker national readiness, or weaker clean-energy readiness.

## Visualisations

The notebook includes visualisations such as:

- Final EV readiness ranking chart
- Sub-index leader charts
- Sub-index contribution chart
- Spider/radar charts for selected countries
- Choropleth map of the final composite index
- Correlation heatmaps
- Scatterplots with trend lines
- PCA plots
- K-Means clustering plots
- External index comparison scatterplots

The visualisations were designed to keep the results clear and easy to interpret, following ideas from Tufte’s data visualisation principles.

## Repository Structure

```text
DAV_CA1/
│
├── index.ipynb
├── DataMining.ipynb
├── .gitignore
│
├── Datasets/
│   └── Source datasets used for the project
│
├── Cleaned_Datasets/
│   ├── EV_Index_Cleaned_Imputed_2024.csv
│   └── EV_Index_Imputation_Flags_2024.csv
│
├── EV_Index_Normalised_2024.csv
├── EV_Index_Standardized_2024.csv
└── EV_Transition_Readiness_Index_2024.csv
```

## Technologies Used

- Python
- pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Plotly
- Jupyter Notebook

## How to Run

1. Clone the repository.

```bash
git clone https://github.com/RathnamMeghana/DAV_CA1.git
```

2. Open the project folder.

```bash
cd DAV_CA1
```

3. Open the notebook.

```text
index.ipynb
```

4. Run the notebook cells from top to bottom.

The notebook will load the datasets, clean and impute the data, run the analysis, create the final index, compare it with external indices, and produce the visualisations.

## Limitations

Some limitations of this project are:

- Not every country had complete 2024 data.
- Some values had to use the closest available year.
- Imputation was needed for some missing values.
- Equal weighting is simple and clear, but different weighting choices could change the ranking.
- Per-capita indicators can sometimes favour smaller countries.
- The index does not include every possible EV policy, behavioural or affordability factor.
- External indices do not measure exactly the same thing, so comparisons are used as supporting checks rather than exact matches.

## References

The main references used include:

- International Energy Agency Global EV Data Explorer
- World Bank Data
- Our World in Data
- CountryEconomy
- OECD Handbook on Constructing Composite Indicators
- Ayvens Mobility Guide 2024
- World Economic Forum Energy Transition Index 2024
- Yale Environmental Performance Index 2024
- Edward Tufte, *The Visual Display of Quantitative Information*
