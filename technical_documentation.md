# Technical Documentation: InnerSource Community Health Analysis

## Project Description
This project conducts an Exploratory Data Analysis (EDA) on a curated dataset of 1,052 public GitHub repositories to uncover the key metrics and activity patterns that define healthy InnerSource software communities. The goal is to provide actionable insights for organizations seeking to foster effective, sustainable, and collaborative technical teams.

## Project Structure
```
innersource-eda-project/
├── data/
│   ├── raw/              # Original unprocessed data
│   │   └── github_dataset.csv
│   │   └── repository_data.csv
│   └── processed/        # Processed data
│       └── github_dataset_analysis.csv
│       └── github_dataset_clean.csv
│       └── summary_statistics.csv
├── notebooks/            # Jupyter notebooks
│   └── InnerSource_EDA_Analysis.ipynb
├── utils/                # Utility functions for analytics
│   └── functions_eda.py
├── visualizations/       # Generated graphics
│ ├── bivariate_plots/
│ │ └── scatterplots/
│ │ └── Q2_contributors_vs_responsiveness.png
│ ├── correlation_heatmap/
│ │ └── correlation_heatmap.png
│ ├── segmentation_plots/
│ │ ├── health_activity_segmentation.png
│ │ ├── Q1_healthy_vs_unhealthy.png
│ │ └── Q3_metric_distributions.png
│ └── univariate_plots/
│ ├── boxplots/
│ │ ├── boxplot_contributors.png
│ │ ├── boxplot_forks_count.png
│ │ ├── boxplot_issues_count.png
│ │ ├── boxplot_pull_requests.png
│ │ └── boxplot_stars_count.png
│ └── histograms/
│ ├── histogram_contributors.png
│ ├── histogram_forks_count.png
│ ├── histogram_issues_count.png
│ ├── histogram_pull_requests.png
│ └── histogram_stars_count.png
├── InnerSourceCommunitiesHealthy.pdf # Final presentation
├── LICENSE
├── README.md
├── requirements.txt
└── technical_documentation.md
```

## Dataset
The main dataset (`github_dataset.csv`) contains 1,052 public GitHub repositories with the following fields:

| Column | Type | Description |
|--------|------|-------------|
| `repositories` | String | Full repo name (owner/project) |
| `stars_count` | Integer | Number of stars (social approval metric) |
| `forks_count` | Integer | Number of forks |
| `issues_count` | Integer | Open issues |
| `pull_requests` | Integer | Open pull requests |
| `contributors` | Integer | Unique contributors to the project |
| `language` | String | Main programming language |

**Data Source**: [TODO] [Kaggle - GitHub Dataset](https://www.kaggle.com/datasets/nikhil25803/github-dataset)

**Processing**: Raw data cleaned and processed to remove duplicates, handle missing values, and derive new features (health_score, activity_ratio, issues_per_contributor, prs_per_contributor).

## Dependencies
Requires Python 3.8+ with the following packages:
- **pandas**: Data manipulation and analysis
- **numpy**: Numerical computing
- **scipy**: Statistical analysis (zscore, skew, kurtosis)
- **matplotlib**: Graphics and plotting
- **seaborn**: Statistical data visualization

Install dependencies:
```bash
pip install -r requirements.txt
```

## Analysis Process

### 1. Data Loading and Cleaning
- Load raw dataset from CSV
- Standardize column names (lowercase, remove spaces, snake_case)
- Handle missing values (e.g., fillna for language → 'Unknown')
- Remove duplicate rows (80 duplicates removed → 972 repos)
- Validate numeric columns (remove negatives, impute with median)
- Reset index

### 2. Exploratory Data Analysis (EDA)
- Compute descriptive statistics per metric (mean, median, std, skewness, kurtosis)
- Identify outliers using z-score method (|z| > 3)
- Visualize distributions: histograms, boxplots for all numeric features
- Analyze pairwise correlations with heatmap (Pearson correlation)

### 3. Feature Engineering
- **health_score**: `(stars + forks - issues) / max(contributors, 1)`
  - Represents overall project health relative to active participants
- **activity_ratio**: `pull_requests / (issues + 1)`
  - Proxy for responsiveness to contributions vs. issues

### 4. Question-Specific Analysis
**Q1**: Key metrics distinguishing healthy communities
- Boxplots comparing healthy vs. unhealthy communities (threshold: median health_score)
- Metrics: stars_count, contributors, pull_requests, issues_count

**Q2**: Relationship between contributors and responsiveness
- Scatter: contributors vs. pull_requests

**Q3**: Actionable patterns for sustainable InnerSource
- Distribution plots by quadrant (health_score vs. activity_ratio)
- Repository segmentation visualization

### 5. Visualization
- All plots saved as PNG files (300 dpi) in `visualizations/`
- Organized by type: univariate (histograms, boxplots), bivariate (scatterplots), correlation matrices, segmentation plots
- Color schemes: seaborn coolwarm for heatmaps, red-green for health categories

## Results and Artifacts

### Data Artifacts
- **Raw**: `data/raw/github_dataset.csv` (1,052 repos)
- **Processed**: `data/processed/github_dataset_clean.csv` (972 repos after deduplication)
- **Features**: Additional columns in processed data (health_score, activity_ratio, outlier flags)

### Visualizations
**Correlation Matrix**:
- `correlation_heatmap.png` - Pearson correlations between InnerSource metrics

**Segmentation Plots**:
- `health_activity_segmentation.png` - Repository quadrants (health_score vs. activity_ratio)
- `Q1_healthy_vs_unhealthy.png` - Boxplots comparing community health
- `Q3_metric_distributions.png` - Distribution analysis by quadrant

**Bivariate Analysis**:
- `Q2_contributors_vs_responsiveness.png` - Scatterplot showing relationship

**Univariate Distributions**:
- Histograms and boxplots for: stars_count, forks_count, issues_count, pull_requests, contributors

### Notebook
- **Main**: `notebooks/InnerSource_EDA_Analysis.ipynb`
  - Full workflow: data load → clean → analyze → visualize
  - Commented code with explanations
  - Narrative flow aligned to key research questions

### Presentation
- **File**: `InnerSourceCommunitiesHealthy.pdf`
- **Slides**: Comprehensive presentation covering:
  - Project introduction and motivation
  - Dataset overview
  - Research questions
  - Key findings and insights
  - Recommendations for InnerSource success
  - Conclusions

## Version Control
This project is version-controlled with Git. Repository structure follows best practices:
- Data, notebooks, and visualizations in separate folders
- README for quick overview
- Technical documentation for deep dive
- `.gitignore` file excludes temporary files and system files

## Author(s)
- Ana Gamito

## License
MIT License - see [LICENSE](LICENSE) file for details.

## References
- [InnerSource Commons](https://innersourcecommons.org/) - Community and best practices
- [InnerSource Patterns](https://patterns.innersourcecommons.org/) - Proven solutions for InnerSource adoption
- [GitHub InnerSource Guide](https://github.com/resources/articles/innersource) - Introduction to InnerSource
- [CHAOSS Metrics](https://chaoss.community/) - Community health analytics for open source software

---

**Last Updated**: November 28, 2025
