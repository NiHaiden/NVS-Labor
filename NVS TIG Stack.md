# TIG Stack 
## Influx 
(https://docs.influxdata.com/influxdb/v2.1/reference/key-concepts/design-principles/)

### Overview
- written in Go, self contained binary, includes WebUI for managing some parts of the software
- Open-Source
- Time-series database: optimised for storing sensor data, monitoring data from IT systems
- Uses Flux as query language 
- Strict update & delete permissions 
- Fast read and write queries
- Schemaless design, prioritize performance over consistency 
- Data with the ssame value is assumed as a duplicate

### Flux
- Written in Go
- Open Source, functional data scripting language 
- Designed for 
		- querying 
		- analyzing 
		- acting
   on data. 
- Supports data sources such as: Time Series (Influx), Relational SQL DB, CSV Files 
	- Default language in Influx since Release v2.0

```Flux
from(bucket: "example-bucket")
    |> range(start: -1d)
    |> filter(fn: (r) => r._measurement == "example-measurement")
    |> mean()
    |> yield(name: "_results")
```

## Grafana 
- Backend written in Go and Frontend written in TypeScript
- Open Source 
- Analytics and interactive visualization application 
- Support for numerous data sources, such as PostgreSQL and InfluxDB 
- does not ingest data, gets it from the data source and displays it in a variety of ways 
- Multiple types of panels to visualize data: 
	- Time Series Panel
	- Pie Charts / other Charts 
	- Tables
- Panels are organised into dashboards, which are shareable with other people, and organizable into folders
- Custom alerts for certain data points, such as HDD space running low 
- Transformations allow for calculations on data on multiple data sources at once 

## Telegraf
- Written in Go
- Open Source 
- Collect, process, aggregate and write metrics 
- Plugin-driven -> small core, depends on community to create plugins for it 
- there are 4 distinct types of plugins 
	- Input Plugins to collect data from (e.g. system, services, 3rd party)
	- Processor Plugins to transform, filter data
	- Aggregator plugins for calculations using aggregate functions like (min, max, quantile, etc.)
	- Output Plugins to write metrics to various destinations 
- About 300 plugins

