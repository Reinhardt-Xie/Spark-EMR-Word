# Word Count Experiment by Leveraging Pyspark on AWS EMR

### Create an Amazon S3 Bucket

In this use case, we will use Amazon S3 bucket to store our Spark application jar, logs, input and output files.

1. Open the Amazon S3 console
2. Choose Create bucket
3. Type a name for your bucket (ex : my-first-emr-bucket) and choose its AWS Region then click next.
4. On the Set properties page, you can configure some properties for the bucket. In this tutorial we don’t need any specific properties, click next.
5. On the Set permissions page, you manage permissions that are set on the bucket that you are creating. We will use the default permissions, click next.
6. On the Review page, verify the settings and choose Create bucket.

### Upload files on Amazon S3

Now that our S3 bucket is created, we will upload the Spark application wordcount.py and an input file on which we will apply the wordcount.

1. On the Amazon S3 console click on the bucket you just created
2. Choose Create folder, enter the name of the folder (ex : tutorialEMR), the encryption setting (ex : None) and save
3. Click on the folder you just created, then choose upload to upload the Spark application jar and the input text file on which you want to apply the wordcount

### Create an Amazon EMR cluster & Submit the Spark Job

In this step, we will launch a sample cluster running the Spark job and terminating automatically after the execution.

1. Open the Amazon EMR console
2. On the right left corner, change the region on which you want to deploy the cluster
3. Choose Create cluster
4. On the General Configuration section, enter the cluster name, choose the S3 bucket you created (the logs will be stored in this bucket) and check Cluster.
5. On the Add steps section, select Spark application, and configure the Spark-submit options and arguments.
6. On the Software Configuration section, use the default release 
7. On the Hardware configuration section, choose the instance type and the number of instances
8. On the Security and access section, use the Default values.
9. Click on Create cluster
10. Click on the refresh icon to see the status passing from Starting to Running to Terminating — All steps completed

### Creating wordcount.py on the Master node in terminal

1. Now on our created cluster page (Cluster list->our cluster)
2. Near the "Master public DNS:" field click the SSH button
3. Follow the instructions and SSH on the master node
4. In /home/hadoop create wordcount.py (vi wordcount.py)
5. Copy over the contents from wordcount.py in this repo
5. In wordcount.py change the input file s3 url to point to input.txt in your bucket, created above

### Executing wordcount.py in terminal

1. Go through the code in wordcount.py and checkout what it does
2. Execute the script using "spark-submit wordcount.py | tee output.txt"
3. This will also generate output.txt with a copy of the logs
4. You may have the output file copied to your s3 bucket by using the cmd "aws s3 cp output.txt s3://my_bucket/my_folder/"
5. You should see the result of your code among other logs, should look like

### Results

And: 2;
on: 1;
then: 1;
Aberbrothok: 2;
bell: 1;
that: 1;
of: 2;
knew: 1;
Had: 1;
placed: 1;
Abbot: 2;
they: 1;
worthy: 1;
blest: 1;
Rock: 2;
Inchcape: 1;
the: 3;
The: 1;
perilous: 1;

### Terminate the cluster

Don't forget to terminate your cluster after you're done!

