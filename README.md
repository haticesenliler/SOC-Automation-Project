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

The goal of today's setup is to automate incident response using a SOAR workflow. When a Mimikatz-related alert is detected in Wazuh, the alert is sent to Shuffle, where it is processed, checked against VirusTotal, forwarded to TheHive to create an alert, and finally sent to a SOC analyst via email for investigation.

1. Mimikatz alert sent to shuffle
2. Shuffle receives mimkatz alert (extract sha256 hash from file)
3. Check reputation score w/virustotal
4. Send details to the thehive to create alert
5. Send email to soc analyst to begin investigation

What’s Working (The Success)
- Wazuh is talking to Shuffle: When Mimikatz runs on VM, Shuffle sees it. It successfully linked.
- Set up a process to "grab" the SHA256 hash from the messy log files so it can be used for searching.

What's not Working
- VirusTotal (The "URL Error"): I'm stuck here because of a small formatting mismatch. The node is looking for the hash, but because of a name or space error, it’s sending an empty request.
- I couldn't find the theHive app in the Shuffle library. This is likely a search or versioning quirk in the Shuffle interface.




