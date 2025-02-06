Using InfluxDB 2 as a Grafana Data Source
Follow these steps to configure InfluxDB 2 as a data source in Grafana:

1. Open Grafana and Navigate to Data Sources
In the Grafana Navigation Pane, go to Connections > Data sources.
Click Add new data source and select InfluxDB.
2. Set the Name for the Data Source
Enter a descriptive Name for the data source (e.g., InfluxDB_Metrics).
3. Configure Connection Settings
In the Query Language field, select Flux.
Under the HTTP section:
Set the URL to your InfluxDB instance:
cpp
Copy
Edit
http://<INFLUXDB_IP>:8086
Leave Auth and Custom HTTP Headers as default unless additional configuration is required.
4. Set InfluxDB Details
Enter your Organization, Token, and Default Bucket.
5. Save & Test
Click Save & Test to verify the connection.
6. Use Flux Query in Grafana
Once configured successfully, navigate to the Explore section in Grafana.
Select InfluxDB as the data source.
Use Flux Query to explore and visualize your data.
Now you can start creating dashboards with InfluxDB 2 in Grafana!
