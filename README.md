This software, "Trax SQL Audit", is not free for commercial business use, to be deployed, or to be used to connect to any business database, without purchasing a license for "Trax SQL Audit" software from Andre Maree maree.andre@gmail.com. It is not allowed to copy the "Trax SQL Audit" dll, or the source code of "Trax SQL Audit", to use it as is, or to modify it, without purchasing a "Trax SQL Audit" license that allows this. Please see the included software license "TRAX_SQL_AUDIT_LICENSE.md"".

1 License per SQL database is needed at $19 per month or $99 per year. Contact Andre at maree.andre@gmail.com for more info.

# Welcome to Trax SQL Audit

The goal of Trax is to help your business save money and benefit from modern application development and data storage. Trax is a SQL Server auditing micro-service that copies SQL audit data to Azure storage reliably and securely. The primary benefits are that data in Azure storage is a lot cheaper than data in SQL Server, and audit data tend to be high volume because every change must be saved, so the other major benifit is better scalability. No server is required to run Trax, or for the saved data - this is a serverless NoSQL solution. Since no server vm, or destination SQL Server is needed, Trax is very easy to set up. Reliability is enforced by leveraging Durable Functions reliability. Source data can be any SQL Server table that needs to track every change to the data. Trax can also audit by an API call to log events that is not a SQL Server data change. This way all audit data can be in the same place and accessed the same way.

- It is required to set up your SQL audit tables and triggers.
- The data is saved to Azure storge. It can either be partitioned per month by audit date and SQL table name, or it can be bulk saved per month by SQL table name. If it bulk saved per month then the entire month`s data must be dowmload before a query can be made.

### High Level Cost Benefit Analysis

#### Compared to a solution that requires another SQL Server licence:

It is not straight-forward to compare Azure Table Storage vs Azure SQL data at rest costs. A reasonable cost for SQL Azure can be $5 per gig per month. A reasonable cost for Azure Table Storage can be 5c per gig per month. It is not unreasonable to estimate that Azure Table Storage cost is about a 100 times cheaper than Azure SQL for data at rest. It is very safe to assume that there is a massive price advantage for data at rest for Azure Table Storage, for any logical comparisons with different factors and features enabled that effects pricing.

#### Compared to a solution that requires another SQL Server licence, or for when the existing SQL Server is used to store audit data:

If SQL Server is the audit store, then it is recommended to export audit data to another SQl Server instance. However, id the same instance is used to store audit data, then there is only a slight data cost advantage in favour of Table Storage. A great benefit of Trax is it`s scalability by data partitioning, compared to a SQL index on audit data that was populated by trigger.

#### Compared to solution that uses the built in SQL auditing mechanism:

SQL Azure can log audit data to a file to disk on the database server. This can be used additionally if needed, however it is not query-able by API and can cause the server disk to become full. So it needs to be managed manually. Trax will, without any human intervention, supply end-user made change tracking history of SQL Server data that can either be queried by API or downloaded by API per month. Trax can remove the audit data from SQL Server if opted.

### Reliability

Trax is a Durable Function and therefor offers built in reliability.

### Security

Azure storage is secure and encrypted. Trax is secured by using Azure AD token based security and function keys. Azure Key Vault is used to securely store configuration.
