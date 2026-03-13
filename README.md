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


## Day 4

I configured Wazuh to collect telemetry from a Windows endpoint and created a custom alert to detect Mimikatz activity.

A significant portion of the project involved installing and troubleshooting the Wazuh agent and Sysmon on the Windows VM to ensure proper data collection.

I used Mimikatz, a common Red Team tool for extracting credentials, to simulate a real-world attack.

I authored a custom Wazuh rule specifically to identify and flag the unique behavior of Mimikatz.

To run the test, I had to configure Windows Defender to allow the download of a "dangerous" file and set up a folder exclusion so the tool wouldn't be deleted during execution.

Once these configurations were in place, I successfully ran the attack and confirmed that the security events were visible in the Wazuh dashboard.

<img width="1932" height="66" alt="image" src="https://github.com/user-attachments/assets/8a8e46b1-caca-4648-ae5c-47d86bb1bdea" />



## Day 5

Connect Shuffle (SOAR)
Send alert to TheHive
Send to SOC Analyst via Email
