# Prometheus exporters

---

Prometheus is an open-source systems monitoring and alerting toolkit that allows a multi-dimensional data model with time series data retrieved over HTTP and identified by metric name and key pairs. We are using Prometheus exporter as a middleware to create time-based queries on the Salesforce API for maintaining a proper monitoring on our projects. 

Due to the high number of logs that are processed by this exporter, the exposed metric cache can become too big, the retrieval and processing time from the endpoint to Prometheus server takes too long, hence it can result in no data error. This is a normal behavior for a Prometheus exporter and there are two ways of overcoming the above scenario:

1.	Increasing the scrape_time interval for getting the metrics from the exporter into Prometheus. By doing this, we will prevent a new cycle of metrics being started while the previous cycle is already running and is not complete.
2.	Restarting the containers. This is the desired option as it takes less time that the first one and the exporter is independent, no other process will be impacted.

As we were struggling with multiple Grafana alerts due to no data error, a cronjob has been added having the purpose of restarting the container during night.
 
---

[Home](/wiki/Home.md)
