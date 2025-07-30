# Framework to accelerate Data Model implementation

## Challenge

The challenge here was not related with any technical limitation, it was more related with time constraint. What this means is that we add pressure to build a data model that was being design based on the data that we where receiving from kafka.

## Implementation

Tasks:

- Design and implement a framework that could in a simplified maner transform and move from one data storage (s3) into another (redshift).

### Solution

To mitigate time constrain issue I developed a framework that permitted the data engineers focus on the business components and the framework would provide the logging mechanisms, error handling, user authentication and access to environment variables.

The framework was composed by four components source, middleware, destination and custom. The first three components load transform and write data the last component exists for cases when its required to do some type of operation that is not supported natively by spark, like for example read from a API, execute a capitalize function on a complete name.

Below is a example of a configuration file that is loaded into the framework.

```yaml
  - format: custom.spark.udf.capitalize

  - format: source.csv
    options:
      header: false
      delimiter: ','
      columns: 'country, id, job, name'
      path: /samples/jobs_by_country.csv
    tmp_table: data
    filter_query: SELECT * FROM data
    cache: false

  - format: middleware
    tmp_table: musicians_by_country
    filter_query: 
        SELECT 
            country,
            CAPITALIZE(name) AS name
        FROM data
        WHERE job like '%music%'
    cache: false

  - format: destination.parquet
    options:
      path: /transformed/musicians_by_country
      savemode: overwrite
    query: 'SELECT * FROM musicians_by_country
```
