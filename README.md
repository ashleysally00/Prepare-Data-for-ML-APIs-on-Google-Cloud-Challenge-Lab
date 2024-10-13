# Prepare Data for ML APIs on Google Cloud Challenge Lab

## Task 1. Run a simple Dataflow job

1. Create a BigQuery dataset called **BigQuery Dataset Name**.

   Run the following in the Cloud Shell to download the schema file:
   ```bash
   gsutil cp gs://cloud-training/gsp323/lab.schema .


2a. In the dropdown menu of the Source section, select **Google Cloud Storage**.

2b. In "Select file from GCS bucket" enter:  
    ``` gs://cloud-training/gsp323/lab.csv ```

2c. In the Destination section, for “Table name” enter:  
    ``` customers ```

2d. Toggle the button that says enable:  
    ``` Edit as text ```

2e. Copy the JSON data from the `lab.schema` file to the text area in the Schema section:
   `[ ]`

2f. Click the button to **Create**.

3. ## Create a Cloud Storage Bucket called Cloud Storage Bucket Name ##

3a. In the Cloud Console, click on **Navigation Menu > Storage**.

3b. Click **CREATE BUCKET**.

3c. Copy your **GCP Project ID** to name your bucket.

3d. Click **CREATE**.

---

4. ## Create a Dataflow job ##


