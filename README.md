# Enterprise-NOC-Monitoring-Lab-with-Zabbix-7.0
This project documents the deployment and configuration of an enterprise-style Network Operations Center (NOC) monitoring environment using Zabbix 7.0 LTS within a multi-VM home lab.
The objective of this lab was to build centralized infrastructure monitoring capable of:

- Monitoring Windows, Linux, and firewall infrastructure
- Detecting infrastructure failures and service outages
- Visualizing operational health through dashboards
- Simulating real-world incidents and validating alerting workflows
- Building practical NOC administration and monitoring engineering skills


## Environment Architecture
#### Hypervisor
- Hyper-V
#### Infrastructure Components
Systems and	Purpose
- Ubuntu Server 24.04:	Zabbix Server
- Windows Server 2025:	Active Directory / DNS / Monitoring Target
- OPNsense: Firewall	Network Gateway / Security Appliance
- Windows 11 Host:	Administrative Workstation


## Technologies Used
- Zabbix 7.0 LTS
- Ubuntu Server 24.04
- Apache2
- PHP 8.3-FPM
- MySQL
- OPNsense
- Hyper-V
- Windows Server 2025
- Zabbix Agent 2

#### Objectives
- Monitoring Goals
- Centralize infrastructure monitoring
- Configure agent-based monitoring
- Build NOC-style dashboards
- Create operational alerting workflows
- Validate host availability monitoring
- Simulate infrastructure incidents
- Improve troubleshooting and observability skills


## Zabbix Server Deployment
#### Ubuntu Server Configuration

The Zabbix server was deployed on Ubuntu Server 24.04 using:

- Apache2
- PHP 8.3-FPM
- MySQL backend database
- Zabbix 7.0 LTS packages from the official repository
#### Key Deployment Tasks
- Installed Apache2 and PHP dependencies
- Configured PHP-FPM integration
- Created MySQL database for Zabbix
- Imported Zabbix database schema
- Configured Zabbix server database authentication
- Enabled and validated Zabbix services
<img width="1030" height="762" alt="77 install zabbix 7 4 repo" src="https://github.com/user-attachments/assets/1a1152c9-f281-40fb-b2cc-8841e2ece04d" />
<img width="1022" height="192" alt="78 install zabbix packages" src="https://github.com/user-attachments/assets/f8c36e1c-441a-417a-b63a-484d53e2a235" />
<img width="607" height="206" alt="79 create initial database mysql" src="https://github.com/user-attachments/assets/ada0e80e-7d35-4511-a0d0-a28964817ba2" />
<img width="1860" height="930" alt="80 zabbix 7 0 running" src="https://github.com/user-attachments/assets/fdd2dfab-5449-45a5-8f03-3156263515f9" />

## OPNsense Monitoring Configuration
#### Agent-Based Monitoring

The OPNsense firewall was integrated into Zabbix using the native Zabbix Agent plugin.

#### Configuration Steps
1. Installed:
- System → FirmwAgent-Based Monitoring:
The OPNsense firewall was integrated into Zabbix using the native Zabbix Agent plugin.
`System → Firmware → Plugins → os-zabbix-agent.`
<img width="3766" height="1600" alt="81 add zabbix agent to opnsense" src="https://github.com/user-attachments/assets/fd0723e0-1355-496b-b9c7-4502a306cc0a" />

2. Enabled Zabbix Agent:
- Services → Zabbix Agent
  
3. Configured:
- Zabbix server IP
- Hostname
- Agent port 10050
<img width="3772" height="1540" alt="82 configure zabbix agent on OPNSense" src="https://github.com/user-attachments/assets/d3854e0e-4bbc-4594-9e74-68eccba07348" />


4. Added OPNsense host to Zabbix using:
- Agent interface
- LAN IP address

5. Appropriate monitoring templates
<img width="3772" height="1528" alt="85 add free bsd template to opnsense host in zabbix" src="https://github.com/user-attachments/assets/734eb9de-2d70-476b-b6d1-65f08ca873cb" />
<img width="3765" height="1410" alt="86 successfully added opnsense as host in zabbix" src="https://github.com/user-attachments/assets/dec50f38-4811-4ce8-a6ab-4c382e70d12d" />


#### Connectivity Validation

Validated agent connectivity using:
`zabbix_get -s <OPNsense-IP> -k agent.ping`
<img width="970" height="280" alt="87 confirm connectivity to zabbix agent on opnsense vm and ws 2025 from zabbix server" src="https://github.com/user-attachments/assets/69970b0d-ff71-41fa-b24d-217268808188" />


## Windows Server 2025 Monitoring

#### Zabbix Agent 2 Deployment

Installed Zabbix Agent 2 on Windows Server 2025 for centralized monitoring.

#### Configuration Steps
- Installed Zabbix Agent 2 MSI package
- Configured Zabbix server IP
- Configured Windows firewall rule for TCP 10050
- Added Windows host to Zabbix
- Attached Windows monitoring template

#### Important Troubleshooting Lesson

An initial monitoring issue occurred due to a hostname mismatch between:
- Windows computer name
- Zabbix host configuration
This prevented monitoring data from being processed despite successful network connectivity, the issue was resolved by matching the Zabbix host name exactly to the Windows server computer name.

<img width="1507" height="1144" alt="88 download and install zabbix agent on windows server 2025" src="https://github.com/user-attachments/assets/6fcd7ea2-c6b2-4de0-932f-364b5ce6e90b" />
<img width="1525" height="1156" alt="89 zabix agent 2 installed on ws 2025 successfully" src="https://github.com/user-attachments/assets/514e7ebf-46cd-4238-af4b-b68d2d488c27" />
<img width="3775" height="1275" alt="90 successfully added windows server as host in zabbix gui" src="https://github.com/user-attachments/assets/4f9d3379-e09f-4cb2-8f4b-308338829c19" />
<img width="1513" height="1006" alt="91 enable zabbix agent via firewall on wins 25" src="https://github.com/user-attachments/assets/7993a884-fd47-4c98-b760-8e303147b20e" />
<img width="1861" height="737" alt="92 all hosts added to zabbix" src="https://github.com/user-attachments/assets/124fa4a3-a264-4c10-9279-cc12d81071d9" />


## Dashboard Development

#### Created a centralized NOC dashboard within Zabbix 7.0 to provide a single pane of glass for infrastructure monitoring.

#### Dashboard Widgets
- Problems
- Host Availability
- Top Hosts
- CPU Utilization Graphs
- Trigger Severity Summary
- Network Throughput Graphs
- Monitoring Goals

The dashboard was designed to provide:

- Real-time operational visibility
- Infrastructure health monitoring
- Rapid incident identification
- Centralized alert visualization

<img width="1850" height="915" alt="93 zabbix dashboard" src="https://github.com/user-attachments/assets/61cc6c4b-813b-4bab-8420-4368940e2397" />

## Trigger Engineering

Configured custom triggers for proactive alerting.

#### Implemented Triggers
- High CPU Usage: Monitored sustained CPU usage exceeding defined thresholds.

- Host Unavailability: Validated agent availability monitoring for infrastructure hosts.

- DNS Service Failure: Created custom service monitoring using:
  `service.info[DNS,state]`
Trigger alerts were configured to detect DNS service outages.


## Incident Simulation Exercises
1. CPU Spike Simulation
Objective: Validate trigger activation during high resource utilization.

Method:
- Created trigger for high CPU Utilization
- Generated sustained CPU utilization using PowerShell loops.
<img width="3778" height="1330" alt="94 create expression for trigger zabix" src="https://github.com/user-attachments/assets/925cfbc5-4ec2-49b3-aef0-e0831de4a30e" />
<img width="1734" height="918" alt="97 ps trigger" src="https://github.com/user-attachments/assets/a47f6ac4-9ed6-4785-bd20-24f1c816d992" />

Result:
- Zabbix trigger activated successfully
- Dashboard reflected elevated CPU usage
- Problem severity displayed in centralized alert panel
<img width="3532" height="1015" alt="95 trigger active" src="https://github.com/user-attachments/assets/1aa6bbe8-86e4-460d-b593-e9b5d79a696e" />
<img width="3534" height="981" alt="96 resolve cpu load after turning off load" src="https://github.com/user-attachments/assets/30bca21a-370e-4a4c-b285-108943dbd2c9" />



2. DNS Service Failure Simulation
Objective: Validate service-level monitoring.

Method:
- Stopped the Windows DNS service.
<img width="1396" height="1036" alt="101 dns service down trigger" src="https://github.com/user-attachments/assets/1ef2b8aa-c1d3-4e76-b249-78d37de5a116" />


Result:
- Zabbix detected service outage
- Alert generated successfully
- Incident appeared in Problems dashboard widget
<img width="3166" height="1141" alt="102 reenabled zabbix agent validate dns service down" src="https://github.com/user-attachments/assets/939705d5-f999-48ea-bea5-871156f14dab" />


- 
3. Agent Connectivity Failure
Objective: Validate host availability monitoring.

Method:
- Stopped the Zabbix agent service.
<img width="1732" height="922" alt="98 ps trigger to disable zabbix agent on win server" src="https://github.com/user-attachments/assets/aaac262b-6ceb-4116-afe3-b4ec92d34aee" />

Result:
- Host availability alerts generated
- Infrastructure visibility updated in real time
<img width="3526" height="1149" alt="99 validate zabbix agent unavailability" src="https://github.com/user-attachments/assets/1c6113ea-f31f-424b-a862-37decc75cc07" />

#### Operational Skills Demonstrated
- Infrastructure Monitoring
  - Cross-platform monitoring
  - Agent-based telemetry
  - Centralized observability
- Troubleshooting
  - PHP-FPM troubleshooting
  - Agent connectivity validation
  - Hostname mismatch resolution
  - Port and firewall validation
- Monitoring Engineering
  - Trigger creation
  - Alert tuning
  - Dashboard engineering
  - Service monitoring
- NOC Operations
  - Incident detection
  - Operational visibility
  - Infrastructure health monitoring
  - Alert validation workflows


#### Key Lessons Learned
- Enterprise monitoring depends heavily on proper hostname consistency
- Agent-based monitoring provides richer telemetry than SNMP alone
- Validating dependencies layer-by-layer simplifies troubleshooting
- Monitoring engineering requires meaningful, actionable alerting
- Centralized observability significantly improves operational awareness


## Future Improvements

Planned future enhancements include:
- Grafana integration
- Email/Slack alerting
- OPNsense SNMP monitoring
- WAN latency monitoring
- Packet loss alerting
- Integration with Wazuh SIEM
- Infrastructure inventory grouping
- Advanced dashboard customization

## Conclusion

This project successfully demonstrated the deployment of a centralized enterprise-style monitoring environment using Zabbix 7.0 LTS.
The lab provided hands-on experience with:

- Infrastructure monitoring
- Monitoring engineering
- Incident detection
- Dashboard creation
- Service monitoring
- Operational troubleshooting

The environment closely mirrors real-world NOC workflows and provides a foundation for future expansion into SIEM integration, security monitoring, and advanced observability engineering.


