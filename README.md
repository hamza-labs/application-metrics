---------------------------- 
### Applications Metrics in Microservices Architectures.

Prometheus is an open source tool for monitoring systems by collecting metrics from target systems as time series data. 
It supports multiple approaches for instrumenting the application codes. 

In this document, we will demonstrate how to use Prometheus to monitor a spring boot web application.


--------------------
### Table of Contents 

- [Why We Monitor](#why-we-monitor)  
- [What We Monitor](#what-we-monitor)  
- [What is Prometheus](#what-is-prometheus)  
- [Prometheus does not do](#prometheus-does-not-do)  
- [Prometheus Architecture](#prometheus-architecture)  
- [Monitoring Spring Application](#monitoring-spring-application)
- [Bugs and Feedback](#bugs-and-feedback)  
- [Sources](#sources)

---------------------------------
### Why We Monitor

```bash
- Analyzing long-term trends
- Comparing over time or experiment groups
- Alerting
- Building dashboards
- Conducting ad hoc retrospective analysis
```

### What we Monitor 

```bash
- Hosts (CPU, Memory, I/O, Network, Filesystem)
- Containers (CPU, Memory, I/O, Restarts, Throttling)
- Applications (Throughput, Latency)

```

---------------------------------
### What is Prometheus

Prometheus benefits:

```bash 
- Monitoring system and Timeseries Database
- Instrumentation
- Metrics collection and storage
- Quering
- Alerting
- Dashboard / Graphing / Trending
```
Promotheus focue on:

```bash
- Dynamic cloud environments
- Operational systems monitoring
```

--------------------------
### Prometheus does not do 

```bash
- Raw log / event collection (use ELK stack)
- Tracing (Use Jaeger)
- User /Auth Management
- Automatic Horizontal Scaling 
```
---------------
### Prometheus Architecture 

<img src="https://prometheus.io/assets/architecture.svg" width='600' >


----------------------------------------
### Monitoring Spring Application

- Run Prometheus via Docker

```bash
docker run -p 9090:9090 prom/prometheus
```

```bash
localhost:9090
```

- Add a Gradle Dependencies

```bash
   compile 'io.prometheus:simpleclient_spring_boot:0.0.21'
   compile 'io.prometheus:simpleclient_servlet:0.0.21'
   compile 'io.prometheus:simpleclient_hotspot:0.0.21'
```

- Configuring the Prometheus endpoint (application.yml)

```bash
endpoints:
  prometheus:
    path: "prometheus-metrics"
```

- Instrument your SpringApp.java

```bash
@EnablePrometheusEndpoint // the endpoint will be available at localhost:XXXX/prometheus
@EnableSpringBootMetricsCollector // What about metrics 
```

- Endpoint Metrics

```bash 
localhost:xxxx/promotheus-metrics
```

----------------------------
### Bugs and Feedback

For bugs, questions and discussions please use the [Github Issues](https://github.com/microservices-stack/Application-Metrics/issues).


----------------------------
### Sources 

- http://container-solutions.com/microservice-monitoring-with-prometheus/
- https://www.slideshare.net/brianbrazil/prometheus-overview?ref=https://thenewstack.io/prometheus-microservice-monitor-reports-production/
- https://raymondhlee.wordpress.com/2016/09/24/monitoring-spring-boot-applications-with-prometheus/
- https://raymondhlee.wordpress.com/2016/09/24/monitoring-spring-boot-applications-with-prometheus/
- https://raymondhlee.wordpress.com/2016/09/24/monitoring-spring-boot-applications-with-prometheus/
