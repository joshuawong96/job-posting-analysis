# Analysis of Cloud Competencies in the Job Market 

This repository contains the data and Jupyter notebooks used for the analysis of job postings, which are used as a proxy of cloud skills and competencies in demand in the current job market. They were scraped from 3 local job portals: MonsterSG, LinkedIn and NodeFlair using the keyword `cloud` and `cloud computing` (for MonsterSG only).

> ✨ **Note:** The job postings were scraped once-off in March 2022, and are scraped periodically to be up-to-date. As job portals have to 
> keep their platform updated with listings that are open, we were unable to scrape job postings that date back more than 3 months.


### 📋 Data
These files are in the `data/cleaned` folder by default.
| Cleaned Data Files | Description |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Individual Platforms | Each file in this folder contains cleaned data for a platform (MonsterSG, LinkedIn and NodeFlair) with common data fields across all platforms                                                               |
| `combined_data.json` | Single JSON file of data from all 3 platforms, with standardised data fields and data format. Extracted information can also be found in this dataset.                               |
| `filtered_data.json` | JSON file of cleaned combined data after removing records of job roles that are not closely related to advanced cloud skills through text clustering | 
| Nodes and Edges | |

### 🧹 Data Cleaning and Processing

| Step  | Description |
| --------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Removing duplicates & Standardising data fields | Dropped duplicates for job postings that are identical based on Job Title, Company Name and Job Description. Each platform has different data fields that were scraped, thus data field names and data types were standardised. We reviewed all data fields and kept those that were useful. For fields which other platforms do not have, the relevant information was extracted. |
| Information Extraction: Education Qualifications | Map a dictionary of qualifications and field of study to standardise the qualification namings across all job listings. e.g. `{"PhD": ["phd", "doctor", "doctorate"]}` |
| Information Extraction: Sector/Industry | Used Selenium to search the company on Google and obtain the Industry Used Selenium to search the company on Google and obtain the sector.  Map a dictionary of the various sectors to standardise the sector namings across all job listings. e.g. `{"Financial Services": ["Fund management", "Cryptocurrency"]}` |
| Information Extraction: Tech Stack and Skills | Trained a custom `spaCy Named Entity Recognition (NER)` model to extract `'SKILLS'` as the entity by manually labelling ~100 sentences. The model was saved and applied on dataset to extract tech skills from the job descriptions |
| Information Extraction: Cloud Service Provider | Job posting will be assigned to the cloud service provider as long it mentions any variation of the naming. e.g. `{"aws": "aws", "amazon web services"}` |
| Removing Redundant Job Postings | Text Clustering was done based on the Job Titles and after interpreting the dominant cloud role for each cluster, clusters of job postings for roles that are not as relevant in using advanced cloud skills were removed. Roles such as Business Analyst and Data Scientist were removed. |

### ⚙ Analysis
These files are in the `analysis` folder by default, unless another path is stated.
| Notebook | Description |
| ------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| `/data cleaning/cleaning_job_postings.ipynb` | Code for data cleaning and processing steps mentioned [above](#-data-cleaning-and-processing)
| `ner_model.ipynb` | Training the custom `spaCy Named Entity Recognition (NER)` model to extract `'SKILLS'`. Model is saved in the folder `custom_ner_model`|
| `kmeans_text_clustering.ipynb` | Text Clustering analysis fore removing redundant job postings | 
| `visualisations_and_stats.ipynb` | EDA and visualisations created such as wordclouds, boxplots and barcharts | 

Network analysis was done using the software Gephi. 