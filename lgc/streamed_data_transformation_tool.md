# Stream data transformation tool

## Challenge

Transform the stored streamed data into a more accessible format for easier review and exploration. However, the numerous schema transformations make querying the data extremely challenging. The image below illustrates this situation.

![alt text](imgs/raw_to_transformed.png)

## Implementation (2022)

Tasks:

- Design a solution to solve this two problems.

- Support the implementation of that solution.

### Solution

To make the data more readable, the nested structures apart from lists were flatten and converted to columns at the root level of the table. Lists where transformed into separate tables with keys to connect back to the main table. Additionally, all "business" columns columns were converted into strings, while this approach adds extra cost for data consumers, it ensures that the data remains readable, even if column A was initially a datetime formatted string but on later stage starts receiving numbers.

![alt text](imgs/raw_to_transformed_2.png)

### Improvements:

#### Improvements (2023):

Due to the increase of volumes in certain tables the performance of theses jobs started to degrade, to address this issue some parts of the core were refactored.

Tasks:
- Cache data-frames that are reused in multiple stages.
- Refactor the code on specific components.
- Implement a python multi-thread pool to increase the number of tables that are transformed in parallel(this required extensive testing to be feasible).

#### Improvements (2024):

With the expansion support new data sources like APIs and other data producers, it became necessary to refactor the tool to handle diverse data inputs while maintaining consistent output.

Tasks:

- Design and develop a second version of the transformation tool that allows the definition of all necessary components for data transformation in a configuration file.
