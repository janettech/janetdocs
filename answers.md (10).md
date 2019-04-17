# Questions

## Setup the environment:
 
Initially, I tried to install Datadog agent on Docker on a **Windows** platform. The installation was successful and the Agent was working fine. 
But the issues I had faced were:
-I could not locate the file structure(config files) of the Agent on Windows platform. But I was able to see the Host Map on the UI.
So I dropped this path and installed the Agent on **macOS** where all my executions were performed.

## Collecting Metrics:

**Add tags in the Agent config file and show us a screenshot of your host and its tags on the Host Map page in Datadog.**

The Host Map along with the tags are shown.

![HostMap with tags](images/hostmap_mac.png)

**Install a database on your machine (MongoDB, MySQL, or PostgreSQL) and then install the respective Datadog integration for that database.**

PostgresSQL database was installed and integrated to the Agent as shown.

 ![Postgres integration](images/postgres_integration.png)

**Create a custom Agent check that submits a metric named my_metric with a random value between 0 and 1000.**

Custom_macmetric is created and I later created another metric named my_metric.

![Custom Metric](images/custom_macmetric_snapshot.png)   

**Change your check's collection interval so that it only submits the metric once every 45 seconds.**

In the config custom_macmetric.yaml file, the collection interval is increased to 45 seconds.

![Collection interval](images/collection_interval.png)

 **Bonus Question: Can you change the collection interval without modifying the Python check file you created?**

Changed the collection interval in the Agent UI.

![Collection interval in the Agent](images/collection_customintervallatest.png)


### Visualizing Data:


**Utilize the Datadog API to create a Timeboard that contains:**

**Your custom metric scoped over your host.**  

The image shows mymetric on the Dashboard.

![CustomMetricOnHost](images/mymetricoverhost.png)

**Any metric from the Integration on your Database with the anomaly function applied.**

I don't know how to apply the anomaly function on the postgres database integration. I tried a cURL command, but I got an error.

    curl  -X POST -H "Content-type: application/json" \
    -d '{
      "title" : "My Metric and POstgres max connections",
      "widgets" : [{
          "definition": {
              "type": "timeseries",
              "requests": [
	 	{
              		"q":"avg:mymetric{host:Ajis-MacBook-Pro.loc}, anomalies(avg:postgresql.max_connections{*}.as_count(), \"basic\", 2)"
	 	}
              ],
              "title": "My Metric and POstgres max connections"
          }
      }],
      "layout_type": "ordered",
      "description" : "A dashboard with My Metric and POstgres max connections."
     }' \ 
    "https://api.datadoghq.com/api/v1/dash?  api_key=${api_key}&application_key=${app_key}"

The error as shown below

    html>
    <head><title>301 Moved Permanently</title></head>
    <body bgcolor="white">
    <center><h1>301 Moved Permanently</h1></center>
    <hr><center>nginx</center>

The postgres integration metrics dashboard is seen below.

![Postgres metrics](images/postgresmetrics.png)

The Timeseries editor showing the params and the JSON editor to plot the graph.

![Timeseries](images/Timeseries_latest.png)

**Take a snapshot of this graph and use the @ notation to send it to yourself.**

![EmailAnnotate](images/Emailannotate.png)
