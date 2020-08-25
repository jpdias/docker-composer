# Docker Composer Replication Package

Replication package of the user study conducted to validate the **Docker Composer** visual approach for working with Docker Compose in comparison with conventional textual `docker-compose.yml` files.

## Contents

* `/data` - Contains the raw data as well as the complete dataset resulting from the aggregation of all data sources (main.csv).
* `/forms`-  Contains the procedure instructions provided to participants.
* `/tasks` - Contains the task materials provided for each of the tasks.

## Methodology

Controlled user study with two treatments - control and experimental. Participants in both groups were tasked with solving a set of 4 orchrestration related tasks with Docker Compose. The control group used the conventional toolchain (textual editor + shell) while the experimental group used the Docker Composer tool.

## Procedure

The intructions were provided to the participants as a Google Form (available in `/forms`). The procedure is organized as follows: 

1. Background questionnaire - set of questions to establish the participant's background.
2. Tutorial - brief tutorial covering some basics of Docker Compose.
3. Tasks - set of 4 orchestration related tasks with stack analysis, debugging and implementation goals.
4. Assessment questionnaire - set of questions to evaluate confounding factors and perception-based metrics.

## Findings

The results of the experiment conducted with 16 5th year Informatics and Software Computing MSc students suggest the following: 

* Significant reduction of time spent reading documentation resources.
* Reduction of development time in the debugging and implementation tasks.
* Reduction of error-proneness in the implementation tasks.
* Generally more streamlined workflow with less context switches.
* More favorable perception of ease of usability than with the conventional toolchain.
* Positive perception of usefulness for the tool in general and its individual features.
* High intention to use.
