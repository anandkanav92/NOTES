# GCP [course link](https://booking.udemy.com/course/learn-gcp-become-a-certified-data-engineer-express-course/)

### 
---
- Cloud Storage
    + OLTP is transactional and strong consistency. (For banking) while OLAP is more suited for historical querying purposes.
    + Types of cloud storage in gcp: 
        + Multi regional : frequent access
        + regional : frequent access
        + Nearline : once a month access
        + Coldline : once a year access 
    - Cloud storage can serve as a backup option for serving static websites. 
    - Life cycle policies
        + Delete an object after 365 days.
        + keep only 3 versions of an object and so on.
    - Bucket policy and ACLS:
        + File access permissions.
        + bucket is for whole bucket and every file inside it.
        + ACL is for each object. 
    - gsutil is a command line tool to interact with gcp APIs. 
        + copy : `gsutil cp local_location remote_location`
        + download: `gsutil cp remote_location local_location`
        + move: `gsutil mv remote_location_1 remote_location_2`
        + change class: `gsutil rewrite -s [class] object_location`
- BIGTABLE
    + low latency, nosql, easily scalable to petabytes, million of ops in a second.
    + storing time series data is a natural fit. Stores data as unstructures columns in rows. Identified by unique row number.
    + Retrieve : Either by row number or range of row number using wildcard.
    + Strongly consistent for one region. But if needs to replicate over multiple region becomes inconsistent.
    + `cbt` is the command line tool for bigtable.
        * can only delete, create, count etc with cbt. But not insert. insert must be done using google libraries via python java et al.
- BigQuery
    + data warehousing solution by google.
    + used heavily for analytics. Sql like syntax.
    + OLAP - no banking
    + It has low cost for storing data, almost as drive but high cost for processing. That's why partitioned table reduce the cost of processing as they reduce the size of tables.  
    + partition table limits: each partitioned table can have 2500 partitions. 2000 partions update per table per day.
    + 50 partition updates every 10 seconds
    + `_PARTITIONTIME` is a pseudo column that is added to every row to filter rows based on the timestamp they were added.
    + `REDUCING COST`
        * Use preview options. Don't run queries to explore data.
        * use query validator to validate the price of query before execution.
        * use partitioned tables.
        * no `select *` as it selects all columns and more money
        * hard limit project bytes in your account to give you an error after you cross it
        * hard limit members or users
    + `TEMPORARY TABLES`
        * every query store results in a table. if not given a name its called temporary tables.
        * Not charged
        * stays for 24 yours. 
    + `FILE FORMATS`
        * AVRO
        * JSON
        * CSV
        * PARQUET
        * ORC
    
- CloudSQL
    + not automatically replicated, auto-scaled, and highly available.
    + OLTP 
- Datastore
    + Nosql database, like MongoDB or DunamoDB in AWS.
    + Indexes:
        * helps you query faster.
        * automatically created for simple query like querying one property.
        * For complex -> add your query to index.yaml, use `datastore indexes create`. This looks at your local yaml and if index config are diff it will create the indexes again.
- Cloud spanner
    + relational DB with horizontal scaling.HOW???
    + low latency, highly available, autoscaling, strong transactional consistency - yes banking.
    + no downside? very pricey!
- Memorystore - Redis
    + highly available across two zones but not regions.
    + used for caching
    + start small and scale according to need.
    + uses redis protocal, so no need to change code.
    + 
- CLOUD DATA LAB
    + built on Jupyter notebooks
    + free unless processing data using bigquery
    + can use python, javascript, sql to process datasets
- CLOUD DATA STUDIO
    + a dashboard solution to generate and show reports to the clients
    + Tableau alternative but have less features
    + sources can come from bigquery, mysql, cloudsql, sheets, google analytics
    + update is automatic, that is, if data changes your dashboard gets updated
    + can be shared using google drive.
- CLOUD PUB/SUB
    + like kafka producer and consumers.
    + puv publishes to topic and it is stores in storage until sub ack that it recieved the message.
    + it guarantee that message will be delivered at least once
    + usecases: balance workloads, increases reliability,security (can encrypt the messages)
- HADOOP
    +     