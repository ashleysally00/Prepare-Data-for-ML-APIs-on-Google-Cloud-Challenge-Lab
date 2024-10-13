# Prepare Data for ML APIs on Google Cloud Challenge Lab

## Task 1. Run a simple Dataflow job

1. Create a BigQuery dataset called BigQuery Dataset Name

Run ``` gsutil cp gs://cloud-training/gsp323/lab.schema .``` in the Cloud Shell to download the schema file.

View the schema by running ``` cat lab.schema ```.

2. Go back to the Cloud Console, select the new dataset lab and click **Create Table**.

In the Create table dialog:

1. In the dropwdown menu of the Source section, select Google **Cloud Storage**. 
2. In "Select file from GCS bucket" enter``` gs://cloud-training/gsp323/lab.csv ```.
3. In the Destination section, for “Table name” enter ``` customers ```. 


Create a Cloud Storage Bucket called Cloud Storage Bucket Name.
