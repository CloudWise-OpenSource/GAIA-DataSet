GAIA
================
[Website](http://www.cloudwise.ai/) | [Docs](http://docs.aiops.cloudwise.com/zh/gaia/) | [Community & Forum](http://bbs.aiops.cloudwise.com/)

GAIA, with the full name Generic AIOps Atlas, is an overall dataset for analyzing operation problems such as anomaly detection, log analysis, fault localization, etc. 

# Quick start

**GAIA** contains the data from **MicroSS** (in **MicroSS** repository in Github link) and metrics from companions (in **Companion Data** repository in Github link). Statistically, the data from **MicroSS** contains more than 6,500 metrics, 7,000,000 log items and detailed trace data continuously collected for two weeks. In this scenario, we also simulate the anomalies that may happen in real systems and provide the record for all anomaly injections for fair evaluation of root cause analysis algorithms. This is achieved by controlling the users' behaviors and mimicking the wrong manipulations to the systems.

The data files are listed below.

|Git repository|Relevant repository|Download|
|---|---|---|
|MicroSS| metric \| trace \| business \| run |[MicroSS](https://github.com/CloudWise-OpenSource/GAIA-DataSet/tree/main/MicroSS)|
|Companion Data|metric_detection \| metric_forecast \| log|[Companion Data](https://github.com/CloudWise-OpenSource/GAIA-DataSet/tree/main/Companion_Data)|


## MicroSS

**MicroSS** rpeository contains all data in different types, selected from the business simulation system **MicroSS**. It comes from a scenario of logging-in with QR Code. The description of this scenario is also included in **MicroSS.**

### metric

In "metric" folder, each csv filename contains the node to which the file belongs, ip, and the corresponding indicator name and time period, reformulated from the raw data collected by Metricbeat. The data includes fields as follows.

|timestamp|value|
|---|---|
|1625133601000|34201179|

* timestamp: the time of data collection: 13-bit time stamp
* value: value of metric at the timestamp

### trace

In "trace" folder, each file contains the trace record, reformulated from the raw data collected by OpenTracing. The data includes fields as follows.

|      timestamp      | host_ip | service_name |     trace_id     |     span_id      |    parent_id     |         start_time         |          end_time          |                                                                                                url                                                                                                 | status_code |                       message                       |
| ------------------- | ------- | ------------ | ---------------- | ---------------- | ---------------- | -------------------------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | --------------------------------------------------- |
| 2021-07-01 10:54:23 | 0.0.0.4 | dbservice1   | c124e30fb40651dc | 58ac80ceea500f66 | 8b3e4a4003c5119c | 2021-07-01 10:54:22.632751 | 2021-07-01 10:54:22.632751 | [http://0.0.0.4:9388/db_login_methods?uuid=a3036736-da17-11eb-9811-0242ac110003&user_id=ToeLCkHR](http://0.0.0.4:9388/db_login_methods?uuid=a3036736-da17-11eb-9811-0242ac110003&user_id=ToeLCkHR) | 200         | request call function 1 dbservice1.db_login_methods |


* timestamp: string of time record with the form YYYY-MM-DD hh:mm:ss
* host_ip: the IP of the host running the service named service_name
* service_name: name of service or host 
* trace_id: UUID of the business trace
* span_id: UUID of the node in current trace
* parent_id: UUID of the parent node in current trace
* start_time:the time this call is created
* end_time: the time this call is closed
* url: the RPC url
* status_code: 200 for normal, and others for anomalies.
* message: the out-band message for this call

### business

In "business" folder, each file contains the business log of a node, reformulated from the raw data. The data includes fields as follows.

|      datetime       |  service   |                                                                                                                                                                                message                                                                                                                                                                                |
| ------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2021-07-01 00:00:00 | dbservice2 | 2021-07-01 14:11:54,950 \| INFO \| 0.0.0.2 \| 172.17.0.2 \| dbservice2 \| 12ef1025e43ec0ef \| 3b12f3fa-da33-11eb-875f-0242ac110003-JKrdHZDV-END!RH0>_qOJ token generate success<br>token=MTYyNTExOTkxNC45NTA0Njk1OjNiMTJmM2ZhLWRhMzMtMTFlYi04NzVmLTAyNDJhYzExMDAwM0pLcmRIWkRWRU5EIVJIMD5fcU9KOjE2MjUxMTk5NzQuOTUwNDc5NTpkZjk2YmIyOThmN2M4ZDg3N2NiYmY2MWZkYWM4ZjBlYw== |

* datetime: string of time record with the form YYYY-MM-DD hh:mm:ss
* service: the relevant node ID
* message: extra information in this log.

### run

In "run" folder, we provide system log and anomaly injection records. The data includes fields as follows, with the same meaning to files in "business" folder.

|  datetime  |  service   |                                                                                                  message                                                                                                   |
| ---------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2021-07-01 | dbservice1 | 2021-07-01 22:33:05,033 \| WARNING \| 0.0.0.4 \| 172.17.0.3 \| dbservice1 \| [memory_anomalies] trigger a high memory program, start at 2021-07-01 22:23:04.230332 and lasts 600 seconds and use 1g memory |



## Companion Data

**Companion Data** contains metric and log data provided by the companions of Cloudwise. All the data in **Companion Data** has achieved strict hyposensitization to protect users and companies' privacy. It contains a total of 406 anomaly detection and metric prediction data, including 279 label data, and covers the following types of time series data:

* Changepoint data
* Concept_drift_data
* Linear_data
* Low_signal-to-noise_ratio_data
* Partially_stationary_data
* Periodic_data
* Staircase_data

In terms of logs, the **Companion Data** contains log parsing, log semantics anomaly detection, and named entity recognition (NER) data. About 218,736 pieces of log data. Please refer to **Companion Data** for data description.

### metrc_detection

"metrc_detection" folder records the corresponding type of time series data under each subfolder. Notice that all metrics here are labeled, so that metric anomaly detection can be tackled with fair evaluation. The data includes fields as follows.

|   timestamp   |    value    | label |
| ------------- | ----------- | ----- |
| 1546272000000 | 168899765   | 0     |
| 1546272300000 | 168900938.6 | 0     |
| 1546272600000 | 168902112.2 | 0     |
| 1546272900000 | 168896334   | 0     |
| 1546273200000 | 168880129   | 0     |
| 1546273500000 | 168863924   | 0     |

* timestamp: the time of data collection:13-bit time stamp.
* value: metric value at the time.
* label: anomaly label. 0 for normal, and 1 for anomaly.

### metrc_forecast

"metrc_detection" folder records the corresponding type of time series data under each subfolder. Time series prediction algorithms can be trained on this data set. The data includes fields as follows.

|   timestamp   |    value    |
| ------------- | ----------- |
| 1546272000000 | 168899765   |
| 1546272300000 | 168900938.6 |
| 1546272600000 | 168902112.2 |
| 1546272900000 | 168896334   |
| 1546273200000 | 168880129   |
| 1546273500000 | 168863924   |


* timestamp: the time of data collection.
* value: metric value at the time.

### log

In "log" folder, three sub-folders are included, "log parsing", "log semantics anomaly detection", and "named entity recognition (NER)", serving for the tasks with the same names. Detailed descriptions of the files within can be found in each sub-folder.

# License
GAIA-DataSet is under the Apache 2.0 license. See the [LICENSE](./LICENSE) file for details.
