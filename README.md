# Google Sheets -> BigQuery pipeline  
This repo accompanies [this blog post](https://dlthub.com/docs/blog/google-sheets-to-data-warehouse-pipeline) and contains a deployed `dlt` pipeline that loads data from Google Sheets into BigQuery. To set up your own `dlt` Google Sheets pipeline, first create a Google Sheet that you want to load, and then follow the steps below:  
  
1. Clone this repo.  
2. Install necessary requirements using `pip install -r requirements_github_action.txt`.  
3. Create a file `.dlt/secrets.toml` and insert credentials for Google Sheet and BigQuery:
    1. Follow the steps listed [here](https://dlthub.com/docs/pipelines/google_sheets#get-api-credentials) to get credentials for your Google Sheet, and the steps [here](https://dlthub.com/docs/destinations/bigquery) to get credentials for BigQuery.
    2. Add the credentials that you get from step 1 inside `.dlt/secrets.toml`:
        ```T
        [sources.google_spreadsheet.credentials]
        project_id = "set me up" # GCP Source project ID!
        private_key = "set me up" # Unique private key !(Must be copied fully including BEGIN and END PRIVATE KEY)
        client_email = "set me up" # Email for source service account
        location = "set me up" #Project Location For ex. “US”
        [destination.bigquery.credentials]
        project_id = "set me up" # GCP Source project ID!
        private_key = "set me up" # Unique private key !(Must be copied fully including BEGIN and END PRIVATE KEY)
        client_email = "set me up" # Email for source service account
        location = "set me up" #Project Location For ex. “US”
        ```
4. Enable sharing of your Google Sheet data (see [these steps](https://dlthub.com/docs/pipelines/google_sheets#share-the-google-sheet-with-the-api) for a guide on how to do this).
5. Follow [these](https://dlthub.com/docs/pipelines/google_sheets#add-spreadsheet-id-and-url) steps to get the ID for your spreadsheet and add it inside `.dlt/config.toml`:
    ```T
    [sources.google_sheets]
    spreadsheet_identifier = "spreadsheet_identifier" # Add your Spreadsheet ID here
    ```
6. Finally, run the pipeline using: `python google_sheets_pipeline.py`. This loads your Google Sheets data into BigQuery.  
7. To deploy this pipeline to regularly load data from your Google Sheet into BigQuery, follow the steps on [how to deploy a `dlt` pipeline](https://dlthub.com/docs/walkthroughs/deploy-a-pipeline).