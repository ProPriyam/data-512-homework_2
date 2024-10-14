# Data 512 - Homework 2: Considering Bias in Data

## Project Overview

This project explores the concept of bias in data using Wikipedia articles about political figures from different countries. The analysis combines a dataset of Wikipedia articles with country population data and uses the ORES machine learning service to estimate article quality. The goal is to examine how the coverage and quality of Wikipedia articles about politicians vary among countries and regions.

## Repository Structure

```
DATA-512-HOMEWORK_2
├── input_data/
│   ├── politicians_by_country_AUG.2024.csv
│   └── population_by_country_AUG.2024.csv
├── intermediate_data/
│   ├── error_log.txt
│   ├── politicians_with_quality_and_revisions.csv
│   └── population_by_country_with_region.csv
├── output_data/
│   ├── wp_countries-no_match.txt
│   └── wp_politicians_by_country.csv
├── data_analysis.ipynb
├── data_fetch.ipynb
├── data_merge.ipynb
├── LICENSE
└── README.md
```

## Data Sources

1. Wikipedia articles: `input_data/politicians_by_country_AUG.2024.csv`

   - Source: Wikipedia Category:Politicians by nationality
   - Contains: List of Wikipedia article pages about politicians from various countries

2. Population data: `input_data/population_by_country_AUG.2024.csv`

   - Source: Population Reference Bureau's world population data sheet
   - Contains: Country populations and regional aggregates

3. ORES API: Used for predicting Wikipedia article quality
   - Documentation: [ORES API Documentation](https://www.mediawiki.org/wiki/ORES)

## Files in the Repository

### Input Data

- `politicians_by_country_AUG.2024.csv`: Input data of Wikipedia articles
- `population_by_country_AUG.2024.csv`: Input data of country populations

### Intermediate Data

- `error_log.txt`: Log of errors encountered during ORES API fetch
- `politicians_with_quality_and_revisions.csv`: Collected data including article quality and revision IDs
- `population_by_country_with_region.csv`: Processed population data with lowest hierarchical region information

### Output Data

- `wp_countries-no_match.txt`: List of countries with no matches between datasets
- `wp_politicians_by_country.csv`: Consolidated dataset after merging

### Notebooks

- `data_fetch.ipynb`: Jupyter notebook for adding regions in the population set and fetching data from ORES API
- `data_merge.ipynb`: Jupyter notebook for merging and processing datasets
- `data_analysis.ipynb`: Jupyter notebook containing analysis code and results

### Documentation

- `LICENSE`: License file for the project
- `README.md`: This file, containing project documentation

## Data Schema

### wp_politicians_by_country.csv

- country: Name of the country
- region: Geographic region of the country
- population: Population of the country (in millions)
- article_title: Title of the Wikipedia article
- revision_id: Revision ID of the article
- article_quality: Predicted quality class of the article

## Results

The analysis produces six tables:

1. Top 10 countries by coverage (total articles per capita)
2. Bottom 10 countries by coverage (total articles per capita)
3. Top 10 countries by high-quality articles (per capita)
4. Bottom 10 countries by high-quality articles (per capita)
5. Geographic regions ranked by total coverage (articles per capita)
6. Geographic regions ranked by high-quality coverage (articles per capita)

These tables are embedded in the `data_analysis.ipynb` notebook.

## Research Implications

Through this project, it became evident that bias can emerge at nearly every stage of data processing, potentially leading to misleading analyses. The data processing journey involves numerous decision points, each carrying the potential for introducing bias:

1. Selecting data sources
2. Handling duplicate information
3. Addressing mismatched data
4. Managing missing data

These decisions require careful consideration and thorough investigation to mitigate potential biases. The project underscored the importance of conducting comprehensive research and due diligence to maintain data integrity and minimize bias.

### What biases did you expect to find in the data (before you started working with it), and why?

Prior to working with the data, two main sources of bias were anticipated:

1. Article Quality Rating Bias: Given that the ORES API provides quality predictions based on English Wikipedia pages, there was an expectation of potential bias against politicians from non-English speaking countries. Their articles might receive lower scores even if the corresponding pages in their native languages are highly informative.

2. Sampling Bias: The comprehensiveness of the politicians_by_country list was questioned. There was a concern that not all politicians from different countries would have an equal probability of inclusion in the dataset.

### What (potential) sources of bias did you discover in the course of your data processing and analysis?

During the data processing and analysis phases, several potential sources of bias were identified:

1. Data Insufficiency: The input data lacked comprehensive information on politicians for numerous countries, limiting the scope and reliability of the analysis.

2. Data Quality Issues: Problems such as data duplication, missing data, and data mismatches were encountered, all of which could contribute to biased analysis if not properly addressed.

3. ORES Prediction System: Upon reviewing the documentation, it was noted that the ORES system tends to evaluate article quality with a stronger emphasis on structure rather than content. This approach could introduce bias in the quality assessment of articles.

These findings highlight the complex nature of working with large datasets and the importance of critical examination at every stage of the data science process. They also emphasize the need for transparency in methodology and acknowledgment of limitations when presenting results based on such analyses.

### What might your results suggest about the internet and global society in general?

The results from this analysis of Wikipedia articles about politicians across different countries and regions provide some interesting insights into the internet and global society:

1. Digital divide persists: Significant disparities in online representation between regions reflect ongoing inequalities in internet access and digital engagement.

2. Language barriers matter: English dominance on Wikipedia likely skews coverage towards English-speaking countries or those with historical ties to English-speaking nations.

3. Size doesn't always determine coverage: Smaller states often have disproportionately high coverage, possibly due to the relative prominence of their politicians.

4. Information inequality exists: Variations in coverage quality suggest uneven access to well-researched political information globally.

## Dependencies

- Python 3.x
- Jupyter Notebook
- Pandas
- Requests
- tabulate

## Running the Analysis

1. Clone this repository
2. Install the required dependencies
3. Run the `data_fetch.ipynb` notebook to retrieve data from the ORES API
4. Run the `data_merge.ipynb` notebook to process and merge the datasets
5. Run the `data_analysis.ipynb` notebook to generate the analysis tables and results

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- ORES API for providing article quality predictions
- Wikipedia for the article data
- Population Reference Bureau for the population data
