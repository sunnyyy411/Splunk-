# Data Ingestion Guide for BOTS v3 Dataset

The **BOTS v3** dataset is designed for **SOC Analysts** to practice threat detection and incident response using Splunk. This guide provides step-by-step instructions for ingesting the dataset into Splunk.

---

## **Steps to Ingest Data into Splunk**

### **1. Download BOTS v3 Dataset**
- Clone or download the BOTS v3 dataset from GitHub:
  ```bash
  git clone https://github.com/splunk/botsv3.git ~/Downloads/botsv3_data_set
  ```

### **2. Extract the Dataset**
- If the dataset is downloaded as a ZIP file, extract it:
  ```bash
  unzip ~/Downloads/botsv3_data_set.zip -d ~/Downloads/botsv3_data_set
  ```

### **3. Ingest the Splunk Bucket Files**
- Copy the extracted **BOTS v3** directory to Splunk's index directory:
  ```bash
  sudo cp -r ~/Downloads/botsv3_data_set/var/lib/splunk/botsv3 /opt/splunk/var/lib/splunk/
  ```

### **4. Update `indexes.conf`**
- Open `indexes.conf` for editing:
  ```bash
  sudo nano /opt/splunk/etc/system/local/indexes.conf
  ```
- Add the following configuration:
  ```ini
  [botsv3]
  homePath = /opt/splunk/var/lib/splunk/botsv3/db
  coldPath = /opt/splunk/var/lib/splunk/botsv3/colddb
  thawedPath = /opt/splunk/var/lib/splunk/botsv3/thaweddb
  ```

### **5. Restart Splunk**
- Apply the changes by restarting Splunk:
  ```bash
  sudo /opt/splunk/bin/splunk restart
  ```

### **6. Verify the Data**
- Log in to the Splunk Web Interface.
- Run the following search query to confirm data availability:
  ```spl
  index=botsv3
  ```

✅ **Done!** The data should now be successfully ingested into Splunk, allowing you to perform **SOC analysis and threat hunting**. 🚀


