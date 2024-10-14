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

This project taught me that, virtually at every step of data processing, bias can occur and could lead to misleading analyses. There are so many decision points along a data processing journey, and each of these can potentially introduce bias:

1. Choice of data source
2. Management of duplicated information
3. Dealing with mismatched data
4. Handling missing data

These decisions have to be cautiously taken and well-investigated to reduce the risk of biases. This project highlights how extensive research or due diligence in all aspects is necessary to minimize the loss of data integrity or bias.

### What biases did you expect to find in the data (before you started working with it), and why?

Prior to working with the data, two main sources of bias were anticipated:

1. Article Quality Rating Bias: Since the API, ORES, does quality prediction based on English Wikipedia pages, a set of potential bias was against politicians from countries whose English is not their first language. Their articles may get low scores while the corresponding pages in their native languages are very informative.

2. Sampling Bias: The politicians_by_country list wasn't considered to be comprehensive. Not every politician from any different country could get an equal opportunity to land in the dataset.

### What (potential) sources of bias did you discover in the course of your data processing and analysis?

Following are some of the potential biases identified during data processing and analysis:

1. Inadequacy of Data: Input data lacked comprehensive information on politicians for most countries, which further reduced the scope and reliability of the analysis.

2. Quality Issues: The data had duplication and misalignment issues, together with data loss; any of these issues, if not treated properly, might lead to biased analysis.

3. ORES Prediction System: Going through the documentation, it was noted that the ORES system evaluates article quality much more in terms of structure than its content. This is biased in assessing the quality of articles.

These results highlight how complex an exercise it is to work with large datasets and how crucial critical examination is at every step in a data science pipeline. They also further reiterate the fact that methodological transparency and declaration of limits are required when presenting the results of such analyses.

### What might your results suggest about the internet and global society in general?

These findings of this analysis on Wikipedia articles of politicians from different countries and regions have some interesting implications for the internet and society as a whole:

1. Digital divide persists: Large differences in online presence between regions suggest that access to and use of the internet continue to be unequal.

2. Language barriers matter: The predominance of English on Wikipedia is likely to contribute to skewed coverage towards English-speaking nations or countries that have historical links to English-speaking nations.

3. Size factor does not always work in determining coverage: In general, smaller states normally receive disproportionately high coverage, perhaps due to the relative prominence of their politicians.

4. Information inequality exists: This is shown in the difference in the quality of the coverage, revealing unequal access in respect to well-researched political information around the world.

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
