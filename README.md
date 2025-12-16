# http-log-analysis-splunk





























## Steps to Analyze HTTP Log Files in Splunk SIEM


### 1. Search for HTTP Events
- Open Splunk interface and navigate to the search bar.
- Enter the following search query to retrieve HTTP events:
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
```

### 3. Analyze Web Traffic Patterns
- Determine the distribution of request methods (GET, POST, etc.) to understand web traffic patterns.
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| stats count by method
```
- Identify top URLs or endpoints accessed by users.
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| top limit=10 uri
```
- Analyze response codes to identify errors or successful requests.
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| stats count by status
```

### 4. Detect Anomalies
- Look for unusual patterns in file transfer activity.
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| timechart span=1h count by _time
```
- Analyze high volumes of error responses:
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| stats count by status
| where status >= 400
```
- Investigate file transfers to or from suspicious IP addresses.
```
index=<your_http_index> sourcetype=<your_http_sourcetype>
| search src_ip="suspicious_ip"
```
