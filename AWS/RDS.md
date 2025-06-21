# RDS

## What is RDS?

> Relational Database Service: A relational database service provided by AWS

<br/>

## Why use RDS?

- If you use an EC2 instance, there is very little automatic management for the DB, so the user must spend time **installing the DB engine, managing versions, and backing up data manually**.
- In addition, **availability and durability are not guaranteed**, so there is a higher chance that data stored in the DB will be lost or not used properly, and it is difficult to scale the DB as needed later.
- If you use RDS, **all DB maintenance tasks are automatically managed by RDS**. **Except for the initial setup, the only thing the user has to do is manage the data stored in the DB**, which provides great convenience.
- Another advantage is that **it offers a variety of DB engine choices**.
- Since each DB engine provides slightly different features, you can choose the DB engine that fits your needs and purpose to increase efficiency.
