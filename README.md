This software, "Trax SQL Audit", is not free for commercial business use, to be deployed, or to be used to connect to any business database, without purchasing a license for "Trax SQL Audit" software from Andre Maree maree.andre@gmail.com. It is not allowed to copy the "Trax SQL Audit" dll, or the source code of "Trax SQL Audit", to use it as is, or to modify it, without purchasing a "Trax SQL Audit" license that allows this. Please see the included software license "TRAX_SQL_AUDIT_LICENSE.md"".

1 License per SQL database is needed at $99 per month. Contact Andre at maree.andre@gmail.com for more info.

The Trax source code repository is not publicly available.

# Welcome to Trax SQL Audit

The goal of Trax is to help your business save money and benefit from modern application development and data storage. Trax is a SQL Server auditing micro-service that copies SQL audit data to Azure Table Storage. The primary benefit is that data in Azure Table Storage is a lot cheaper than data in SQL Server, and audit data tend to be high volume because every change must be saved. No server is required to run Trax, or for the saved data - this is a serverless NoSQL solution. Since no server vm, or destination SQL Server is needed, Trax is very easy to set up. Reliability is enforced by leveraging Durable Functions reliability. Source data can be any SQL Server table that needs to track every change to the data.

- Set up your SQL audit tables and triggers to populate these tables.
- Set the audit tables to copy from in Trax config.
- Specify an interval for Trax to run.
- Trax will select the SQL audit data on this interval and copy it to table storage.
- Upon successful saving of a batch, the batch data will then be deleted from the SQL audit table.
- The data is saved to table storge partitioned by month and SQL table name.
- The table storage rowkey is set to the audit UTC date descending, for fast retrieval by date filter.

### High Level Cost Benefit Analysis:

It is not straight-forward to compare Azure Table Storage vs Azure SQL data at rest costs. A reasonable cost for SQL Azure can be $5 per gig per month. A reasonable cost for Azure Table Storage can be 5c per gig per month. It is not unreasonable to estimate that Azure Table Storage cost is about a 100 times cheaper than Azure SQL for data at rest. It is very safe to assume that there is a massive price advantage for data at rest for Azure Table Storage, for any logical comparisons with different factors and features enabled that effects pricing.

### Reliability:

Trax is a Durable Function and therefor offers built in reliability, but if there ever is a problem when processing a batch, then:

- the error will be logged
- audit data will not be deleted from the source SQL Server
- or copied to table storage
- Trax will continue to process new data
 
This allows for safe problem resolution if the need ever arises.

### Alerts:

Trax does not have any alerts at the moment. It is in the development pipeline to add alerting functionality for errors.
