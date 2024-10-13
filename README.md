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

1. In the Cloud Console, click on **Navigation Menu > Dataflow**.
2. Click **CREATE JOB FROM TEMPLATE**
3. The job name can be anything you want that works.
4. From the dropdown under **Dataflow template**, select **Text Files on Cloud Storage to BigQuery** under **“Process Data in Bulk (batch)”.** (**DO NOT** select the item under “Process Data Continuously (stream)”)

For the **Required parameters,** enter the following:
1. FieldValueJavaScript **UDF path** in Cloud Storage ``` gs://cloud-training/gsp323/lab.js ```
2. **JSON path**``` gs://cloud-training/gsp323/lab.schema ```
2. JavaScript **UDF name**: ``transform``
3. **BigQuery output table**: ``` YOUR_PROJECT:lab.customers ```
4. **Cloud Storage input path**: ``` gs://cloud-training/gsp323/lab.csv ```
5. **Temporary BigQuery directory**: ``` gs://YOUR_PROJECT/bigquery_temp ```
6. **Temporary locationgs**: ```//YOUR_PROJECT/temp```
Replace **YOUR_PROJECT** with **your project ID.**
7. Click **RUN JOB.**

*While you are waiting for this to complete... do the other tasks or the lab will time out*:

Task 2: Run a simple Dataproc job

Create a Dataproc cluster
