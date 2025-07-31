# kafka streaming tool

## Challenge

Each topic contained different data sources and the schema of each data source will evolve in time in terms of adding, removing and change the data type of columns.

### Implementation


Tasks:
- Design the tool that would consume the data taking in consideration the way the data is sent by each topic.

- Implement the first prototype.

- Help with the implementation of the application.

Below is a image that illustrates how the application works.

![alt text](imgs/streaming_tool_img1.png)

### Improvements:

We determined that was necessary to modify how certain components worked because the application workers started to fail as the volume of events in specific topics increased.

#### Improvements (2023):

Tasks:

- Readjust the limits on max events per topic.
- Cache frequently used data frames from specific stages.
- Implement additional metrics to monitor the execution time of each individual topic's data source.

#### Improvements (2024)

Tasks:

- Design and develop a auxiliary tool that uses a scheduling algorithm to automatically groups topics by workers according to the execution time that each topic was taking.

    Below is a visual representation of how topics would be distributed by four streaming worker jobs, along with an representation of how the workers extract data from topics.

    ![alt text](imgs/scheduler_optimization.png)

    ![alt text](imgs/scheduler_optimization_1.png)

NOTE: All client and project information was changed to respect privacy.
