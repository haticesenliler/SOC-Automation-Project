# SOC-Automation-Project
Home Lab

## Day 1
An illustartion of the project and home lab.
<img width="856" height="782" alt="Screenshot 2026-03-04 170813" src="https://github.com/user-attachments/assets/f606a471-11da-4df2-b2fa-ad141d6e9120" />

<img width="1292" height="372" alt="Screenshot 2026-03-04 170827" src="https://github.com/user-attachments/assets/1bee424d-58f9-4bdf-b4fe-9e94d00d875f" />

## Day 2
Server Setup: Created two separate cloud servers: one dedicated to Wazuh and the other to TheHive.

Wazuh Installation: Downloaded and installed the Wazuh manager on the first VM to handle security monitoring.

TheHive Dependencies: Installed the required "stack" on the second VM: Java (to run the apps), Cassandra (for the database), and Elasticsearch (for the search engine).

TheHive 5 Installation: Installed the actual TheHive 5 application to act as the incident response platform.

## Day 3
Fixed the Networking: Swapped the default "localhost" IPs for the Public IP in the Cassandra and Elasticsearch configuration files so they could communicate.

Configured TheHive: Set up the main configuration file so TheHive knew exactly where to find its database and search engine.

Started Services in Order: Manually synced the startup sequence—Cassandra, then Elasticsearch, then TheHive—to prevent connection errors.

Integrated Wazuh: Connected TheHive and Wazuh so that security alerts would automatically flow into the incident response platform.
