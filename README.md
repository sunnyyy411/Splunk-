# Splunk for SOC Analysts

## Introduction
Splunk is a powerful Security Information and Event Management (SIEM) tool widely used in Security Operations Centers (SOCs) for real-time monitoring, threat detection, and incident response. As an aspiring SOC Analyst, mastering Splunk can significantly enhance your ability to analyze logs, detect anomalies, and investigate security incidents efficiently.

## Why Splunk?
- **Real-time log analysis**: Helps monitor and analyze security events in real time.
- **Threat detection**: Uses correlation rules and alerts to identify security threats.
- **Incident investigation**: Provides detailed logs and dashboards for efficient analysis.
- **Automation & reporting**: Automates security workflows and generates insightful reports.
- **Integration with various security tools**: Works seamlessly with firewalls, IDS/IPS, endpoint security, and more.

## Splunk Architecture and Components
Splunk's architecture consists of the following key components:

### 1. **Forwarders**
- Collects logs and sends them to the Indexer.
- Types: **Universal Forwarder (UF)** and **Heavy Forwarder (HF)**.

### 2. **Indexers**
- Stores and processes incoming log data.
- Enables fast searching and retrieval.

### 3. **Search Head**
- Allows users to perform searches and create reports/dashboards.
- Distributes search queries to multiple Indexers in a distributed setup.

### 4. **Deployment Server**
- Manages configurations and app deployments across multiple Splunk instances.

### 5. **License Manager**
- Ensures compliance with Splunk’s licensing model and monitors data ingestion.

### 6. **Cluster Master** (for distributed setups)
- Manages index replication and high availability.

### 7. **Splunk Web Interface**
- Provides a user-friendly UI for searching, monitoring, and visualization.


## Key Learning Areas
- **Installation & Setup**: Setting up Splunk on a local or cloud instance.
- **Indexing & Searching**: Understanding Splunk's indexing mechanism and using SPL (Search Processing Language) for data retrieval.
- **Dashboard & Visualization**: Creating dashboards for better threat analysis.
- **Alerts & Correlation Rules**: Setting up alerts for security events.
- **Log Analysis for SOC**: Analyzing logs from different sources like Windows, Linux, firewalls, and IDS/IPS.
- **Use Cases for SOC**:
  - Detecting brute-force attacks
  - Monitoring failed logins
  - Analyzing malware activity
  - Investigating suspicious network traffic

## Basic SPL Commands

### 1. Search Command
- Basic search syntax: `index=<index_name> sourcetype=<sourcetype>`
- Filtering events: `search <keyword>`
- Using wildcards: `*`

### 2. Time Range
- Specifying time ranges: `earliest`, `latest`
- Relative time: `-15m`, `-1h`, `-7d`
- Absolute time: `"01/01/2023:00:00:00"`

### 3. Fields
- Extracting fields: `fields <field_name>`
- Renaming fields: `rename <old_field> as <new_field>`
- Removing fields: `fields - <field_name>`

## Filtering and Sorting

### 1. Where Command
- Filtering based on conditions: `where <field> <operator> <value>`
- Example: `where status="404"`

### 2. Search Filters
- Using Boolean operators: `AND`, `OR`, `NOT`
- Example: `status="404" AND method="GET"`

### 3. Sort Command
- Sorting results: `sort <field>`
- Sorting in ascending/descending order: `sort +<field>`, `sort -<field>`

## Data Aggregation

### 1. Stats Command
- Basic aggregation: `stats count by <field>`
- Common functions: `count`, `sum`, `avg`, `min`, `max`
- Example: `stats count by src_ip`

### 2. Chart Command
- Creating charts: `chart count by <field1>, <field2>`
- Example: `chart count by src_ip, dest_ip`

### 3. Timechart Command
- Time-based aggregation: `timechart count by <field>`
- Example: `timechart count by status`

### 4. Dedup Command
- Removing duplicates: `dedup <field>`
- Example: `dedup src_ip`

## Data Transformation

### 1. Eval Command
- Creating new fields: `eval <new_field> = <expression>`
- Example: `eval response_time = end_time - start_time`
- Using functions: `if()`, `case()`, `round()`, `tonumber()`, `tostring()`

### 2. Rex Command
- Extracting fields using regex: `rex field=<field> "<regex_pattern>"`
- Example: `rex field=_raw "user=(?<user>\w+)"`

### 3. Regex Command
- Filtering using regex: `regex <field>="<regex_pattern>"`
- Example: `regex user="admin.*"`

## Joining and Combining Data

### 1. Join Command
- Joining two datasets: `join <field> [<dataset>]`
- Example: `join src_ip [search index=firewall]`

### 2. Append Command
- Combining results: `append [<search_query>]`
- Example: `append [search index=ids]`

## Advanced SPL for Security Use Cases

### 1. Transaction Command
- Grouping events into transactions: `transaction <field>`
- Example: `transaction src_ip`

### 2. Lookup Command
- Enriching data with lookup tables: `lookup <lookup_table> <field>`
- Example: `lookup threat_intel src_ip`

### 3. Risk Score Analysis
- Calculating risk scores: `eval risk_score = <expression>`
- Example: `eval risk_score = if(status="404", 10, 0)`

### 4. Threat Hunting
- Searching for IoCs: `search src_ip IN (<list_of_IoCs>)`
- Example: `search src_ip IN ("1.1.1.1", "2.2.2.2")`

## Creating Alerts and Reports

### 1. Alert Creation
- Setting up alerts: `search <query> | alert`
- Example: `search status="404" | alert`

### 2. Scheduled Reports
- Scheduling reports: `search <query> | save <report_name>`
- Example: `search status="404" | save report_404_errors`

## Visualization and Dashboards

### 1. Table Command
- Displaying results in a table: `table <field1>, <field2>`
- Example: `table src_ip, dest_ip, status`

### 2. Visualization Commands
- Creating charts: `chart`, `timechart`
- Example: `timechart count by status`

### 3. Dashboard Creation
- Building dashboards in Splunk
- Adding panels and visualizations

## Deployment Plan
I plan to document my Splunk learning journey through:
- **Practical Labs**: Hands-on exercises and real-world scenarios.
- **Custom Dashboards & Queries**: Sharing SPL queries for SOC-related use cases.
- **Incident Investigation Case Studies**: Analyzing real-world security incidents using Splunk.
- **Automation & Alerting Scripts**: Implementing automation techniques for proactive security monitoring.

## How to Use This Repository?
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/splunk-soc.git
   ```
2. Explore different folders for use cases, dashboards, and queries.
3. Implement the use cases in your own Splunk environment.
4. Contribute by adding new security use cases and improvements.

## Conclusion
Splunk is a must-have skill for SOC Analysts, and this repository aims to provide a structured approach to mastering it. Whether you're a beginner or an advanced user, feel free to explore, learn, and contribute!


