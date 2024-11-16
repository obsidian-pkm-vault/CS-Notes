---
Author:
  - Xinyang YU
Author Profile:
  - https://linkedin.com/in/xinyang-yu
tags:
  - software_engineering
Creation Date: 2023-10-17T09:41:00
Last Date: 2024-11-16T16:50:53+08:00
References: 
description: Information regarding the resources used by a request at different part of the system.
---
## Abstract
---
- Traces help us track the **flow of requests** through various services and components of the system
- A trace is made up one or more [[Span]]
- Once we identify the span for latency, we can proceed with optimisation
- We can use tools like [[Datadog APM]], Tempo and Zipkin etc


## Terminologies
---

### Runtime Metrics
- Allow to view [[Address Space#Heap Segment]], non-heap memory usage and [[Garbage Collector]] activity of the app
- [[Datadog]] can have this enabled with `export DD_RUNTIME_METRICS_ENABLED=true` 
### Instrumented
- Code or tools have been added to the application to monitor, measure, or analyze its behavior during execution
- Provide insights into the application's performance, functionality, and other operational characteristics
- This is particularly useful for debugging, performance tuning, and monitoring purposes
### Pipeline
- [[Datadog]] example
![[datadog_trace_pipeline.png]]
#### Host-side
- We can tune the [[Sampling]]
	- *Library Sampling* overrides *Agent Sampling*
- *Trace Metrics* are the [[#Metrics]], directly connected [[#Instrumented]] application, calculated based on 100% of the app's traffic
#### Datadog backend side
- *Live Search* allows us to search [[Span]] using any tag or [[Span]]
- *Generate Custom [[Monitoring#Metric]]* from [[Span]]
- *Retention Filters* - how long we want to retain the trace
- *Dashboard* used to give a visual representation of the app for optimisation and debugging 