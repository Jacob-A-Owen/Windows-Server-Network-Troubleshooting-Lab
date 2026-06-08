\# Windows Server Network Troubleshooting and Connectivity Restoration Lab



\## Overview



This project demonstrates a structured troubleshooting methodology used by Systems Administrators to identify, diagnose, and resolve network connectivity issues in a Windows Server environment.



The lab was performed using Windows Server 2022 running in VirtualBox. During testing, the server was unable to communicate with external resources due to an incorrect virtual network configuration. Multiple diagnostic tools were used to investigate the issue, identify the root cause, implement corrective action, and verify successful resolution.



\## Technologies Used



\* Windows Server 2022

\* VirtualBox

\* Windows PowerShell

\* TCP/IP

\* DNS

\* Ping

\* Nslookup

\* Route Table Analysis

\* Event Viewer

\* Netstat



\---



\## Problem Identification



Initial testing revealed that the server could not communicate with external resources.



\### Connectivity Failure



Basic network testing was performed to verify internet access and DNS functionality.



The server was unable to successfully reach external hosts, indicating a network configuration issue requiring further investigation.



!\[Connectivity Failure](screenshots/01-network-connectivity-failure.png)



\---



\## IP Configuration Analysis



The first troubleshooting step was to examine the server's TCP/IP configuration.



\### Network Configuration Review



Command:



```powershell

ipconfig /all

```



This output was used to verify the server's IP address, subnet mask, default gateway, DNS servers, and DHCP configuration.



The review confirmed that network configuration information could be collected for further analysis.



!\[IP Configuration Review](screenshots/02-ip-configuration-review.png)



\---



\## DNS Resolution Testing



After verifying IP configuration, DNS functionality was tested.



\### DNS Name Resolution



Command:



```powershell

nslookup google.com

```



The query successfully returned both IPv4 and IPv6 addresses for Google.



This confirmed that DNS services were functioning properly and that hostname resolution was available.



!\[DNS Resolution Test](screenshots/03-dns-resolution-test.png)



\---



\## Routing Table Verification



The server routing table was reviewed to validate network path information.



\### Route Analysis



Command:



```powershell

route print

```



The routing table displayed a valid default route directing traffic through gateway 10.0.2.2.



This verified that outbound traffic had a valid path to external networks.



!\[Routing Table Review](screenshots/04-routing-table-review.png)



\---



\## Network Adapter Validation



The operational state of the network adapter was verified.



\### Adapter Status Review



Command:



```powershell

Get-NetAdapter

```



The Ethernet adapter was confirmed to be operational and actively connected.



This eliminated hardware and adapter state issues as a potential cause of the problem.



!\[Network Adapter Status](screenshots/05-network-adapter-status.png)



\---



\## DNS Server Configuration Review



DNS client configuration was reviewed to verify name resolution settings.



\### DNS Server Assignment



Command:



```powershell

Get-DnsClientServerAddress

```



The server displayed valid DNS server assignments, confirming that DNS requests had a valid destination for name resolution.



!\[DNS Server Configuration](screenshots/06-dns-server-configuration.png)



\---



\## Connectivity Validation



Additional testing was performed to validate network communication.



\### End-to-End Connectivity Test



Command:



```powershell

Test-NetConnection google.com

```



The test successfully validated network communication and DNS resolution.



Results confirmed that the server could communicate beyond the local network.



!\[Test NetConnection](screenshots/07-test-netconnection.png)



\---



\## Event Log Investigation



System logs were reviewed to identify potential operating system or network-related events.



\### System Event Review



Command:



```powershell

Get-EventLog -LogName System -Newest 20

```



Recent system events were reviewed as part of the troubleshooting process.



Event logs provide administrators with visibility into service failures, warnings, hardware issues, and operating system activity.



!\[System Event Log Review](screenshots/08-system-event-log-review.png)



\---



\## Active Network Connection Analysis



Active ports and network services were reviewed.



\### Network Service Verification



Command:



```powershell

netstat -ano

```



The output showed active listening ports including DNS and Active Directory-related services.



This confirmed that critical infrastructure services were available and accepting network traffic.



!\[Active Network Connections](screenshots/09-active-network-connections.png)



\---



\## Connectivity Restoration Verification



After corrective action was implemented, final testing was performed.



\### Successful Connectivity Test



Command:



```powershell

ping google.com

```



The server successfully resolved the hostname and received replies from the remote host with 0% packet loss.



This verified that DNS resolution, routing, and internet connectivity were functioning correctly.



!\[Connectivity Restored](screenshots/10-connectivity-restored.png)



\---



\## Root Cause Analysis



Initial testing revealed that the server could not communicate with external hosts.



Investigation determined that the VirtualBox network adapter had been configured incorrectly, preventing the server from obtaining proper network connectivity.



The adapter configuration was corrected and the virtual machine was restarted. Once a valid IP address, default gateway, and DNS configuration were obtained, connectivity testing confirmed successful communication with external resources.



\---



\## Skills Demonstrated



\* Windows Server Administration

\* Network Troubleshooting

\* DNS Troubleshooting

\* TCP/IP Analysis

\* Connectivity Testing

\* Event Log Analysis

\* Root Cause Analysis

\* PowerShell Administration

\* VirtualBox Administration

\* Systems Troubleshooting Methodology



\---



\## What I Learned



This project reinforced the importance of following a structured troubleshooting methodology when diagnosing infrastructure issues. By validating connectivity, reviewing network configuration, testing DNS services, examining routing information, and analyzing system logs, I gained practical experience identifying and resolving network problems in a Windows Server environment.

