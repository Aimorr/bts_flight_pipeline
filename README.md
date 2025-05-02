# BTS Airline Delay Pipeline

This project builds a complete data pipeline to analyze flight delays in the United States using data from the Bureau of Transportation Statistics (BTS). The goal is to demonstrate reproducible data ingestion, cleaning, storage, and visualization using real-world tools and best practices.

---

## Project Pipeline

**1. Data Acquisition**
- Scraped from [BTS On-Time Statistics](https://www.transtats.bts.gov/OT_Delay/OT_DelayCause1.asp) using Selenium
- Selected all fields and retrieved delay summaries from **January 2020 to December 2024**
- Raw ZIP downloaded and unzipped to `data/raw/`

**2. Data Cleaning & Transformation**
- Combined year/month into a datetime column
- Dropped incomplete or duplicate rows
- Validated numerical types and ensured non-negative delay values
- Cleaned dataset saved to `data/cleaned/airline_delay_summary_clean.csv`

**3. NoSQL Storage**
- Uploaded cleaned data (~100k+ records) to **MongoDB Atlas**
- Stored in the `flight_delays` database under `airport_carrier_delays` collection

**4. Visualization**
- Pulled data from MongoDB using PyMongo
- Compared:
  - Total arriving flights (COVID vs post-COVID)
  - Delay causes (average per category)
  - Proportion of delayed vs on-time flights

---


## Technologies Used

- Python 3.10
- Selenium (automated scraping)
- Pandas (data processing)
- PyMongo (MongoDB integration)
- MongoDB Atlas (cloud NoSQL storage)
- Matplotlib + Seaborn (visualization)
- JupyterLab (Jetstream2 instance)

---

## Directory Structure

bts_flight_pipeline/
- data/ # raw and cleaned datasets
- notebooks/ # Jupyter notebooks for each phase
- README.md
- requirements.txt

---

## How to Reproduce

1. **Clone this repo and set up the environment:**

   ```bash
   git clone https://github.com/<your-username>/bts_flight_pipeline.git
   cd bts_flight_pipeline
   conda create -n bts_pipeline python=3.10 -y
   conda activate bts_pipeline
   pip install -r requirements.txt


2. Run notebooks in order

notebooks/1_download.ipynb         #Scrape BTS delay data using Selenium
notebooks/2_unzip_clean.ipynb      #Unzip, clean, and transform raw data
notebooks/3_upload_mongodb.ipynb   #Upload cleaned data to MongoDB Atlas
                                   #Edit the MongoDB URI in the notebook if needed
notebooks/4_visualize.ipynb        #Pull from MongoDB and generate visuals

   