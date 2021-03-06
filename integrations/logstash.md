---
title: Logstash Data Integration
tags: [integrations list]
permalink: logstash.html
summary: Learn about the Wavefront Logstash Data Integration.
---
# Logstash Integration

Usually the best way to send metrics to a monitoring system is to use a metrics library. However, sometimes you have a legacy system, or a system that is difficult to modify, and you want to garner metrics from Logstash logs. 

Wavefront supports sending log data to your Wavefront proxy with Filebeat. This method is supported in Wavefront proxy 4.4 and higher. Once your data arrives at the proxy, the proxy converts your Logstash log data to metrics by parsing log lines with grok patterns (regular expressions) that you specify in a proxy configuration file.



## Logstash Log Data Setup



### Step 1. Set up Wavefront Proxy

If you do not have a [Wavefront proxy](https://docs.wavefront.com/proxies.html) installed on your network, install a proxy.


### Step 2. Configure the Wavefront Proxy to Ingest Log Data and Set up Data Flow

Follow the instructions in [Log Data Metrics Integration](https://docs.wavefront.com/integrations_log_data.html) for configuring the grok patterns to extract metrics from log data and sending data using Filebeat.

