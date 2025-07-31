# Framework to accelerate Data Model implementation

## Challenge

The main challenge was not related with any technical limitation, but rather related to time constraints. This meant that there was significant pressure to start working on a data model that was being design based on the real-time data being received from Kafka.

## Implementation

Tasks:

- Design and implement a framework to simplify the transformation and movement of data from one storage system (s3) to another (Redshift).

### Solution

To address the time constraints, the framework needed to allow the data engineers to focus on business components while the framework handles logging mechanisms, error handling, user authentication, and access to environment variables.

The framework consists of four main components:

- Source: Extracts data from various sources.

- Middleware: Transforms the extracted data.

- Destination: Writes the transformed data to the target storage system.

- Custom: Provides functionality for operations not natively supported by Spark, such as reading from an API or executing custom functions (ex: capitalizing a complete name).

Below is an example of a configuration file.

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

NOTE: All client and project information was changed to respect privacy.

