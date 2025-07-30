# SQL-Server to Redshift CDC tool

## Challenge

Develop a new tool that could replace another low code tool that was doing the same job but at a higher cost.

### Implementation

Tasks:
- design the new tool with the support of one of the data engineers that was working with the old tool.

- Help in implementation.

#### Solution

This tool was design to combined tasks in airflow and spark. Airflow was responsible to identify what tables add changes that required synchronization and send this information to spark using SQS queues. Spark was responsible do fetch the changes from SQL-Server and send it to Redshift.

![alt text](imgs/cdc_tool.png)

