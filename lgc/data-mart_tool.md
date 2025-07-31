# Data-mart tool

## Challenge

Implement a mechanism to build data marts within the data warehouse, without moving data in or out of Redshift, due to the high computational cost associated with such transfers.

### Implementation

Tasks:
- Design and implement a solution that deals with Redshift's restrictions while maintaining flexibility for data engineers to configure the tool in a similar way to other applications.

#### Solution

For this case we followed a different approach, instead of developing a standalone application, we created a library that is loaded by Airflow DAG tasks. Each task loads a temporary procedure into Redshift and executes it. This approach ensures that all operations run within Redshift.

![alt text](imgs/data-marts.png)

NOTE: All client and project information was changed to respect privacy.
