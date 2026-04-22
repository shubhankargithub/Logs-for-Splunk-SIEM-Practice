# Log for Splunk SIEM Practice

This repository contains **synthetic log files** designed for practicing with **Splunk SIEM** (Security Information and Event Management) and performing various **log analysis tasks**. These logs are generated with realistic formats, representing common log categories like **authentication logs**, **web server logs**, **firewall logs**, and **system logs**. They are intended for learning and experimenting with Splunk's query language and features.

### Table of Contents
- [Log Categories](#log-categories)
- [Log Formats](#log-formats)
- [How to Use These Logs](#how-to-use-these-logs)
- [Customizing the Logs](#customizing-the-logs)


## Log Categories

The repository contains the following log categories:

### 1. Authentication Logs
These logs simulate user login attempts, both successful and failed. They are in a typical **Syslog format** and include random IP addresses and usernames.

Example:
```
Feb 21 10:15:34 server01 sshd[27967]: Accepted password for user1 from 192.168.0.25 port 22 ssh2
Feb 21 10:17:01 server01 sshd[27969]: Failed password for root from 192.168.0.100 port 22 ssh2
```

### 2. Web Server Logs
These logs simulate web server (Apache-style) access logs, with random IP addresses, URLs, and HTTP status codes. Useful for testing web traffic analysis.

Example:
```
203.0.113.50 - - [21/Feb/2025:10:15:34 +0000] "GET /index.html HTTP/1.1" 200 532
192.168.1.25 - - [21/Feb/2025:10:17:02 +0000] "POST /login HTTP/1.1" 200 150
```

### 3. Firewall Logs
These logs simulate firewall traffic data, showing allowed and denied network traffic. These logs include source and destination IPs, protocols (TCP, UDP, ICMP), and actions (ACCEPT, DENY).

Example:
```
Feb 21 10:15:45 fw01 kernel: IN=eth0 OUT= MAC=00:1a:2b:3c:4d:5e SRC=192.168.1.10 DST=192.168.1.20 PROTO=TCP ACTION=ACCEPT
Feb 21 10:16:50 fw01 kernel: IN=eth0 OUT= MAC=00:1a:2b:3c:4d:5e SRC=192.168.1.12 DST=192.168.1.22 PROTO=UDP ACTION=DENY
```

### 4. System Logs
These logs simulate Linux system service logs, with events such as service starts, stops, and restarts.

Example:
```
Feb 21 10:15:50 server01 systemd[1]: Starting Daily Cleanup of Temporary Directories...
Feb 21 10:17:01 server01 systemd[1]: Started Daily Cleanup of Temporary Directories.
```

## Log Formats

Each category follows a different log format to match real-world logs you might encounter in production environments:

- **Authentication Logs**: Standard **Syslog** format.
- **Web Server Logs**: **Apache-style** access log format.
- **Firewall Logs**: **Syslog** format with network-related fields.
- **System Logs**: **Systemd** log format.

## How to Use These Logs

Once you have the log files, you can use them for practicing with **Splunk** or any other SIEM tools. 

1. **Ingest the Logs into Splunk**:
   - Go to **Data Inputs** in Splunk and add the generated log files (`auth_logs.txt`, `web_logs.txt`, etc.) as data sources.
   - You can use **file monitoring** or **manual file upload** for this.

2. **Perform Queries**:
   You can start exploring the logs with queries such as:
   - **Failed login attempts**: 
     ```spl
     index=auth_logs "Failed password"
     ```
   - **404 Errors**:
     ```spl
     index=web_logs status=404
     ```
   - **Firewall Denied Traffic**:
     ```spl
     index=firewall_logs action=DENY
     ```
   - **System Service Starts**:
     ```spl
     index=system_logs "Started"
     ```

3. **Learn Querying in Splunk**: Practice writing more complex queries to explore trends, identify anomalies, and analyze events across different categories.

## Customizing the Logs

If you want to adjust the log generation for your needs, you can:
1. Modify the `generate_logs.py` script to generate a different number of logs.
2. Change the range of IP addresses, usernames, or other log field values.
3. Generate logs for different scenarios, like security incidents, traffic spikes, etc.
