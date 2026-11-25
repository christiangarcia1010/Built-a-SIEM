# Deployed-a-SIEM
SIEM Implementation and Log Analysis
## Objective

This project aimed to build a functional Security Information and Event Management (SIEM) environment using Wazuh to monitor and analyze security events across multiple operating systems. The lab involved deploying a Wazuh server on an Ubuntu virtual machine and configuring agents on both a Kali Linux virtual machine and a Windows 11 computer. I generated test telemetry by performing administrative tasks and installing software to observe how Wazuh collects, processes, and categorizes security events. This hands-on experience helped me better understand centralized security monitoring, endpoint security, vulnerability detection, and the responsibilities of a security operations center (SOC) analyst.

### Skills Learned

- Deployment and configuration of a SIEM environment.
- Installation and management of Linux and Windows security agents.
- Collection, analysis, and interpretation of security event logs.
- Understanding of centralized endpoint monitoring.
- Identification and analysis of software vulnerabilities.
- Security configuration assessments using CIS benchmarks.
- Familiarity with the MITRE ATT&CK framework.
- Generation of test telemetry through endpoint activity.
- Troubleshooting virtual machines, network connectivity, and Linux services.
- Understanding of security alert severity levels and event filtering.
- Development of threat hunting and security investigation skills.

### Tools Used

- Wazuh: Open-source SIEM and extended detection and response (XDR) platform used for security monitoring, log analysis, and vulnerability detection.
- VMware Workstation: Virtualization software used to create and manage the lab environment.
- Ubuntu Linux: Operating system used to host the Wazuh server.
- Kali Linux: Virtual machine used as a monitored Linux endpoint.
- Windows 11: Physical computer used as a monitored Windows endpoint.
- Windows PowerShell: Used to install the Wazuh agent and generate test security events.
- Windows Package Manager (WinGet): Used to initiate software installations and generate endpoint activity.
- Linux Bash: Used for system administration, agent installation, and privilege verification.

  ## Steps

  Step 1: Installing the Wazuh Server

I began by setting up an Ubuntu virtual machine in VMware Workstation and installing the Wazuh platform. The installation process included configuring the Wazuh indexer, generating security certificates, initializing the indexer cluster, and installing the Wazuh manager. These components provide the foundation for collecting, processing, storing, and displaying security events.

<img width="1900" height="796" alt="Screenshot 2026-11-24 152044" src="https://github.com/user-attachments/assets/9fcf4f2c-02a9-4893-b007-05f03842047e" />

Step 2: Accessing the Wazuh Dashboard

After completing the installation, I accessed the Wazuh dashboard through a web browser using the server's IP address. I verified that the dashboard was accessible and displaying security alerts. At this stage, no external endpoint agents had been registered.

The dashboard also provided access to several security features, including malware detection, file integrity monitoring, vulnerability detection, configuration assessments, and threat hunting.

<img width="1843" height="776" alt="Screenshot 2026-11-24 153420" src="https://github.com/user-attachments/assets/a780024a-0458-4f0f-a54f-1b5f9cb313fe" />

Step 3: Configuring a Linux Agent

Using the Wazuh dashboard, I navigated to the agent deployment section and selected the DEB amd64 installation package for my Kali Linux virtual machine. I configured the agent to communicate with the Wazuh server using its IP address.

This process allowed the Linux endpoint to communicate with the centralized SIEM environment.

<img width="1846" height="781" alt="Screenshot 2026-11-24 153503" src="https://github.com/user-attachments/assets/722fc9db-94b1-43ff-b440-07676abee4a0" />

Step 4: Verifying Linux Agent Connectivity

After installing and starting the Wazuh agent on Kali Linux, I returned to the dashboard to verify that the endpoint had successfully registered. The dashboard displayed the agent's IP address, operating system, software version, and active connection status.

This confirmed that the Wazuh server could communicate with the Linux endpoint.

<img width="1847" height="788" alt="Screenshot 2026-11-24 154146" src="https://github.com/user-attachments/assets/5d8843ef-d326-47ab-8702-406ef1afa9f1" />

Step 5: Generating Linux Administrative Activity

To generate administrative activity on the Linux endpoint, I used the terminal to elevate my privileges through the sudo command. I then executed the whoami command to verify that I was operating with root privileges.

Activities involving privilege elevation are important to security monitoring because unauthorized administrative access can indicate suspicious behavior or system compromise.

<img width="1626" height="841" alt="Screenshot 2026-11-24 154512" src="https://github.com/user-attachments/assets/7ab305d8-01d5-488a-bbc3-f2069eee0187" />

Step 6: Configuring a Windows Agent

To expand the lab into a multi-platform monitoring environment, I configured a second Wazuh agent for my Windows 11 computer. From the Wazuh dashboard, I selected the Windows MSI installation package and configured it to communicate with the same Wazuh server.

<img width="1812" height="577" alt="Screenshot 2026-11-24 154847" src="https://github.com/user-attachments/assets/99768d57-2fb6-4b2e-999a-71fd2b3eed02" />

Step 7: Installing the Windows Agent Using PowerShell

I opened Windows PowerShell with administrative privileges and executed the installation command provided by Wazuh. The command downloaded and installed the agent while configuring the server address and agent name.

After installation, I used the NET START Wazuh command to start the service and confirmed that it started successfully.

<img width="1211" height="672" alt="Screenshot 2026-11-24 161408" src="https://github.com/user-attachments/assets/317626ac-da3b-4f62-979d-ad629dfb2c57" />

Step 8: Verifying Both Endpoint Connections

After deploying both agents, I returned to the Wazuh dashboard to verify their connection statuses. Both the Kali Linux virtual machine and the Windows 11 computer were registered and displayed as active.

This demonstrated that the SIEM environment was capable of centrally monitoring endpoints running different operating systems

<img width="1768" height="270" alt="Screenshot 2026-11-24 161557" src="https://github.com/user-attachments/assets/72028221-cbde-4a99-831a-a79ab5021b5e" />

Step 9: Analyzing Vulnerabilities and Security Configurations

Once the Windows endpoint was connected, I explored the system inventory, vulnerability detection, and security configuration assessment features available in Wazuh.

The initial vulnerability assessment identified nine high-severity and three medium-severity vulnerability findings associated with installed software, including Steam, WinRAR, and Microsoft Photos.

The security configuration assessment also evaluated the Windows endpoint against the CIS Microsoft Windows 11 Enterprise Benchmark v3.0.0. The assessment returned a score of 26%, with 127 passed checks, 348 failed checks, and seven checks marked as not applicable.

Although the endpoint was running Windows 11 Home rather than Enterprise, the results provided a starting point for identifying potential security configuration improvements.

<img width="1782" height="665" alt="Screenshot 2026-11-24 161655" src="https://github.com/user-attachments/assets/26dcb337-fe7b-472e-a4af-1d59a526267a" />

Step 10: Generating Test Telemetry on Windows

To observe how Wazuh responds to endpoint activity, I used Windows PowerShell and the Windows Package Manager to initiate software installations. I successfully installed Claude and initiated the installation of Wireshark.

Software installations and changes to system services are examples of legitimate activities that security monitoring tools can record. Similar activities may also occur during unauthorized software installation or malicious activity, making them important events for security analysts to investigate.

<img width="1136" height="657" alt="Screenshot 2026-11-24 162229" src="https://github.com/user-attachments/assets/430c4866-3192-4829-8c47-374d2c1d10c7" />

Step 11: Threat Hunting and Security Log Analysis

After generating endpoint activity, I navigated to the Threat Hunting section of the Wazuh dashboard and filtered the events to display logs associated with the Windows endpoint.

I reviewed the event timestamps, rule descriptions, severity levels, and rule identification numbers to better understand how Wazuh categorizes security-related activity.

The dashboard displayed 489 matching events, including:

Windows software installation activity.

Changes to service startup configurations.

Wazuh agent startup and shutdown events.

Security configuration assessment results.

Windows update configuration findings.

Reviewing these events helped me understand how normal system activity is recorded and how security analysts can use centralized logs to investigate potentially suspicious behavior.

<img width="1817" height="736" alt="Screenshot 2026-11-24 162817" src="https://github.com/user-attachments/assets/f6a2f27b-e7f6-45d0-8dd9-3d0394753df8" />

## Conclusion

This project provided hands-on experience building and operating a centralized SIEM environment. By deploying Wazuh and connecting both Linux and Windows endpoints, I gained a better understanding of how organizations monitor systems, collect security logs, identify vulnerabilities, and assess system configurations.

Generating test telemetry and reviewing the resulting security events also helped me understand how routine endpoint activity can be used during security investigations. This project established a foundation for future labs involving attack simulations, incident response, custom detection rules, and more advanced threat hunting techniques.

