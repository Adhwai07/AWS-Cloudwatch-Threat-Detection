# AWS-Cloudwatch-Threat-Detection
Detect anomalies and uncover potential cyber threats using AWS CloudWatch traffic data.

**Overview**

This project focuses on the analysis of AWS CloudWatch traffic dataset to uncover suspicious web threat interactions. Through data preprocessing, exploratory analysis, and machine learning techniques, the goal is to identify anomalies that could signify potential cybersecurity threats.

****The key questions addressed:****

**Which source IPs and countries generate the most traffic?**

**What time of day sees peak activity?**

**Are there signs of unusual or suspicious behavior?**

**How can machine learning (Isolation Forest) aid in anomaly detection?**

**Dataset Overview**

- Rows: 282

- Columns: 20

**Important Fields:**

- creation_time, end_time, time — Session timestamps

- bytes_in, bytes_out — Traffic volume

- src_ip, dst_ip, src_ip_country_code — Source/Destination info

**Data Preparation & Feature Engineering**

- Datetime Conversion: Parsed timestamp fields to enable time-based operations.

- Session Duration: end_time - creation_time

- Average Packet Size: total bytes / session duration

- Hour of Day: Extracted to detect temporal trends.

**Data Cleaning**

- No missing or duplicate values.

- Outliers in bytes_in, bytes_out, and session_duration retained to preserve security-related anomalies.

**Exploratory Data Analysis (EDA)**

- Traffic Distribution: Visualized bytes transferred and session durations.
  ![image](https://github.com/user-attachments/assets/19bfad2a-e6f4-40e1-89d2-d26c72a80542)


- Top Source Countries: Identified highest traffic contributors.
  ![image](https://github.com/user-attachments/assets/521aa5ef-e430-4dbe-83c2-6a8e4e482cb5)


- Hourly Trends: 9 AM peak in session activity.
  ![Screenshot 2025-04-26 200622](https://github.com/user-attachments/assets/1f1dc586-44f6-4fac-8a34-869c5d593949)


- Frequent IPs: Ranked source IP addresses by frequency.
  ![Screenshot 2025-04-26 200704](https://github.com/user-attachments/assets/054b6cef-cb81-4c48-9005-940d4e30b718)


**Anomaly Detection**

- Algorithm: Isolation Forest

- Selected Features: bytes_in, bytes_out, session_duration, avg_packet_size

- Contamination: 10% assumed anomalous

Output: Sessions labeled as 'Normal' or 'Highly Suspicious'

**Additional Engineering:**

- interaction_count: Number of sessions per source IP

- src_ip_country_code: One-hot encoded

- Standardization via StandardScaler

**Results**

**Suspicious IPs:**
![image](https://github.com/user-attachments/assets/b0f9fd61-bcaa-4ee9-8633-5a31a98d77be)


- 155.91.45.242 (Most suspicious)

- 165.225.240.79 (Second most)

**Top Suspicious Countries:**
![image](https://github.com/user-attachments/assets/b1c80e0a-ddf0-4ea3-a135-4b054dbb7483)


- United States: 62.1% of anomalies

- Netherlands: 37.9%

Session Consistency: All sessions lasted 600 seconds and used port 443 (HTTPS)


**Conclusion**

- Clear behavioral patterns were observed in normal traffic.

- Anomaly detection flagged real deviations that align with potential security threats.

- These findings support more targeted monitoring and response strategies for IPs and regions showing high suspicious activity.
