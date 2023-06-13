# Solr - Backup
Solr can have 2 types of storages:
1. HDFS (comes with the dataproc cluster)
2. GCS bucket ([persistent volume](https://cloud.google.com/dataproc/docs/concepts/components/solr))

## Backup with HDFS(Hadoop File System)
> **Chatgpt question:** How to take backup for solr deployed on google cloud dataproc cluster that uses hdfs as the storage?

To take a backup of Solr deployed on a Google Cloud Dataproc cluster that uses HDFS as the storage, you can follow these general steps:
1. Connect to the master node of the Dataproc cluster:
    - Use the gcloud command-line tool to SSH into the master node:
    ```
    gcloud compute ssh --zone=<zone> <cluster-name>-m
    ```
    - Once connected to the master node, you'll have access to the HDFS file system.
2. Export the Solr collection data:
    - Use the hadoop or hdfs command to export the Solr collection data to a backup location in HDFS. For example:
    ```
    hdfs dfs -cp /solr/<collection-name> /solr-backup/<collection-name>-backup
    ```
    - Replace <collection-name> with the name of your Solr collection. This command will create a backup copy of the collection's data directory in HDFS.
3. Validate the backup:
    - You can use the hdfs command to verify that the backup was successfully created. For example:
    ```
    hdfs dfs -ls /solr-backup
    ```
    - This command lists the contents of the /solr-backup directory and should display the backup directory for your collection.
4. (Optional) Copy the backup to an external storage location:
    - If you want to create an additional backup copy outside of the Dataproc cluster, you can use the hadoop or hdfs command to copy the backup to an external storage location, such as a Cloud Storage bucket or another HDFS cluster.
  
Remember to adjust the commands according to your specific setup and environment, including the paths, collection names, and backup locations.
It's also worth noting that taking regular backups is essential for data protection. Consider automating the backup process using scripts or scheduling the backup tasks to ensure data consistency and availability in case of any issues or failures.
