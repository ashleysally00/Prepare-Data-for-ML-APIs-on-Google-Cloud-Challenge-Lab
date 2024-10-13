# Prepare Data for ML APIs on Google Cloud Challenge Lab

## Task 1: Run a simple Dataflow job

1. Create a BigQuery dataset called **BigQuery Dataset Name**.

   Run the following in the Cloud Shell to download the schema file:
   ```bash
   gsutil cp gs://cloud-training/gsp323/lab.schema .
   ```
---
2. Create a table in BigQuery:
   a. In the dropdown menu of the Source section, select **Google Cloud Storage**.
   b. In "Select file from GCS bucket" enter:  
      ```
      gs://cloud-training/gsp323/lab.csv
      ```
   c. In the Destination section, for "Table name" enter:  
      ```
      customers
      ```
   d. Toggle the button that says enable:  
      ```
      Edit as text
      ```
   e. Copy the JSON data from the `lab.schema` file to the text area in the Schema section:
      ```json
      [ ]
      ```
   f. Click the button to **Create**.
----
3. Create a Cloud Storage Bucket:
   a. - In the Cloud Console, click on **Navigation Menu > Storage**.
   b. - Click **CREATE BUCKET**.
   c. - Copy your **GCP Project ID** to name your bucket.
   d. - Click **CREATE**.

4. Create a Dataflow job:
   a. In the Cloud Console, click on **Navigation Menu > Dataflow**.
   b. Click **CREATE JOB FROM TEMPLATE**.
   c. The job name can be anything you want that works.
   d. From the dropdown under **Dataflow template**, select **Text Files on Cloud Storage to BigQuery** under **"Process Data in Bulk (batch)"**. (**DO NOT** select the item under "Process Data Continuously (stream)")

   For the **Required parameters**, enter the following:
   1. - FieldValueJavaScript **UDF path** in Cloud Storage: `gs://cloud-training/gsp323/lab.js`
   2. - **JSON path**: `gs://cloud-training/gsp323/lab.schema`
   3. - JavaScript **UDF name**: `transform`
   4. - **BigQuery output table**: `YOUR_PROJECT:lab.customers`
   5. - **Cloud Storage input path**: `gs://cloud-training/gsp323/lab.csv`
   6. - **Temporary BigQuery directory**: `gs://YOUR_PROJECT/bigquery_temp`
   7. - **Temporary location**: `gs://YOUR_PROJECT/temp`

   Replace **YOUR_PROJECT** with your project ID.

   e. Click **RUN JOB**.

*While you are waiting for this to complete, do the other tasks or the lab will time out.*

-----------

## Task 2: Run a simple Dataproc job

1. Create a Dataproc cluster:
   a. In the Cloud Console, click on **Navigation Menu > Dataproc > Clusters**.
   b. Click **CREATE CLUSTER**.
   c. Make sure the cluster is going to create in the `region us-central1`.
   d. Click **Create**.
   e. After the cluster has been created, go to **vm instances**.
   f. Click the **SSH button** in the row of the **master instance**.

2. In the SSH console, run:
   ```
   hdfs dfs -cp gs://cloud-training/gsp323/data.txt /data.txt
   ```

3. Submit a job:
   a. Click **SUBMIT JOB** in the cluster details page.
   b. Select **Spark** from the dropdown of "Job type".
   c. Copy `org.apache.spark.examples.SparkPageRank` to "Main class or jar".
   d. Copy `file:///usr/lib/spark/examples/jars/spark-examples.jar` to "Jar files".
   e. Enter `/data.txt` to "Arguments".
   f. Click **CREATE**.

*While you are waiting for this to complete, do the other tasks or the lab will time out.*

-----------

## Task 3: Run a simple Dataprep job

1. Import runs.csv to Dataprep:
   - a. In the Cloud Console, click **Navigation menu > Dataprep**.
   - b. Enter the home page of Cloud Dataprep, click the **Import Data** button.
   - c. In the Import Data page, select **GCS** in the left pane.
   - d. Click on the pencil icon under "Choose a file or folder".
   - e. Copy `gs://cloud-training/gsp323/runs.csv` to the textbox, and click the **Go** button next to it.
   - f. Preview of runs.csv showing in the right pane.
   - g. Click on the **Import & Wrangle** button.

2. Transform data in Dataprep:
   - a. After launching the **Dataprep Transformer,** scroll right to the end and *select* **column10.**
   - b. In the Details pane, click **FAILURE** under *Unique Values* to show the "context menu."
   - c. **Right-click** ***FAILURE,*** select **Delete rows** with selected values to **Remove all rows** with the *state* of "FAILURE."
   - d. **Click** the **downward arrow** next to *column9,* choose **Filter rows > On column value > Contains.**
   - e. In the *Filter rows* pane, enter the ``` regex ``` pattern `/(^0$|^0\.0$)/` to "Pattern to match."
   - f. *Select* **Delete matching rows** under the *Action section,* then **click** the **Add** button.
   - g. Rename the columns to be: runid, userid, labid, lab_title, start, end, time, score, state.
   - h. Click **Run Job.**

*Green Check will take time. Do Other Tasks*

-----------

## Task 4: AI

For the options below, YOUR_PROJECT must be replaced with your lab project name.

You have the option to complete one of the tasks below:

1. Use Google Cloud Speech API to analyze the audio file `gs://cloud-training/gsp323/task4.flac`. Once you have analyzed the file, you can upload the resulting analysis to `gs://YOUR_PROJECT-marking/task4-gcs.result`.

2. Use the Cloud Natural Language API to analyze the sentence from text about Odin. The text you need to analyze is "Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." Once you have analyzed the text, you can upload the resulting analysis to `gs://YOUR_PROJECT-marking/task4-cnl.result`.

3. Use Google Video Intelligence and detect all text on the video `gs://spls/gsp154/video/train.mp4`. Once you have completed the processing of the video, pipe the output into a file and upload to `gs://YOUR_PROJECT-marking/task4-gvi.result`.

Here's a demonstration of the 2nd option: Cloud Natural Language API to analyze the sentence from text about Odin.

In cloud shell:

```bash
gcloud iam service-accounts create my-natlang-sa \
  --display-name "my natural language service account"

gcloud iam service-accounts keys create ~/key.json \
  --iam-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com

export GOOGLE_APPLICATION_CREDENTIALS="/home/$USER/key.json"

gcloud auth activate-service-account my-natlang-sa@${GOOGLE_CLOUD_PROJECT}.iam.gserviceaccount.com --key-file=$GOOGLE_APPLICATION_CREDENTIALS

gcloud ml language analyze-entities --content="Old Norse texts portray Odin as one-eyed and long-bearded, frequently wielding a spear named Gungnir and wearing a cloak and a broad hat." > result.json

gcloud auth login
# (Copy the token from the link provided)

gsutil cp result.json gs://$GOOGLE_CLOUD_PROJECT-marking/task4-cnl.result
```



