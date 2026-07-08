# STELLAR-Log-Analyzer-Web-Tool
Stellar WiFi Analyzer is a comprehensive, browser-based network troubleshooting and forensic
analysis tool purpose-built for Stellar WiFi Access Points, the Stellar Access Points are property
of Alcatel-Lucent Enterprise (ALE). It connects directly to one or more APs via SSH and
provides a rich set of real-time diagnostic tools — all from a single web browser tab, with no
agents or additional software required on the APs themselves.
The tool was designed and developed by Fernando Rivasplata, a Network Architect at ALE with
+20 years of deep expertise in WiFi. It encodes years of operational knowledge about how
Stellar APs behave internally, making expert-level troubleshooting accessible to any engineer
who uses it.
Key Capabilities
Function What It Does
-Device Signal Monitor Live RSSI, noise, SNR, retransmissions and CU with CWAP-level
-RF analysis, Follow Roaming, and Anomaly detection Channel Utilization Monitor Real-time per-band airtime congestion monitoring across 2.4 / 5 / 6GHz with continuous trending
-CCI & ACI Detection Co-channel and adjacent-channel interference scan with signalweighted impact scoring and per-channel noise floor
-Locate a Device Find any connected client across all APs by MAC, IP, hostname, RSSI, or SNR
-RTT & Jitter Monitor Continuous round-trip latency and jitter measurement from AP to any destination host
-Multicast/Broadcast Monitor Real-time multicast and broadcast rate monitoring with dangerousrate alerting and remediation guidance
-Ethernet Capture Run tcpdump directly on AP ethernet interfaces and download .pcap files
-AP Information Hardware, firmware, radio, SSID, and health snapshot for any AP
-Config Files Browser Browse, view, and download AP configuration and system files directly from the SSH shell
-Roaming Neighbors Query the live roaming domain database from each AP’s perspective
-Log Analysis Filter, analyze, and visualize wam.log with 802.11 reason/status code enrichment
-Remote Script Executor Execute shell scripts across an entire AP fleet simultaneously

Installation & Getting Started
2.1 Prerequisites
Before deploying Stellar WiFi Analyzer, ensure the following requirements are met:
• Virtualization platform (VMware, Hyper-V, Proxmox, or equivalent) — if deploying via the VM option.
• Docker Engine installed and running on the host — if deploying via the container option. No Python or system dependencies need to be installed manually; everything is bundled inside the container image.
• Network connectivity (TCP port 22 / SSH) from the SWA host to the Stellar WiFi Access Points.
• A modern web browser (Chrome, Firefox, Edge, Safari) to access the SWA web interface.
• Root SSH credentials for the Stellar APs. Most diagnostic features require root access.
ℹ Recommended Deployment
The VM option is the recommended deployment method. It arrives pre-configured with Docker and the SWA container image already loaded, requiring only a network IP change before use.
2.2 Install the Application

Option A — Virtual Machine (Recommended)
The VM is the fastest path to a working deployment. It ships as an OVF/VMDK package (VMware / Proxmox) or as a VHD (Hyper-V), with the Alpine Linux OS and the SWA Docker container pre-installed.
• Download the distribution archive:
◦ VMware / Proxmox (OVF + VMDK): https://drive.google.com/file/d/1lBAhKxWBj7izzo5RVACdiEDi_jPC4SO/view
◦ Hyper-V (VHD): https://drive.google.com/file/d/1ATk4d38xXqAwCjx_2L_YLYi64kB4q1sw/view
• Unzip the archive.
1. VMWARE/Proxmox: The folder named SWA-VM-OVF will contain the .ovf and one
or more .vmdk files.
2. Hyper-V: The hyper-v disk files will be available
• Import or Create the VM into your virtualization platform:
  1. VMWARE: Import the VM using the standard OVF import process.
  2. Hyper-V: Create a new VM using the Generation-1 type and make sure to create 2 disks using the disk files available within the zip file
• VM default resource allocation:
  ◦ 2 vCPUs
  ◦ 8 GB RAM
  ◦ Disk 1: 1 GB (Alpine OS)
  ◦ Disk 2: 32 GB (SWA Application data)
• Power on the VM. The default network configuration is:
  ◦ IP Address: 192.168.13.55 / 24
  ◦ Gateway: 192.168.13.1
  ◦ DNS: 1.1.1.1
• Change the IP address to match your network. Use the hypervisor console to connect to the new VM and edit the file “/etc/network/interfaces” as root (see the credentials few lines below). To edit the file use the command “vi /etc/network/interfaces” and then change the address, netmask and gateway values
  auto eth0
  iface eth0 inet static
  address x.x.x.x
  netmask 255.255.255.0
  gateway x.x.x.1
Default SSH credentials for the VM: username root, password G0dL0vesY0u (zeros in place of the letter O).
• Reboot the VM after saving the network configuration. Once rebooted, open your browser and navigate to: http://x.x.x.x:3005
Replace x.x.x.x with the IP address you assigned to the VM.

Option B — Docker Container
If you prefer to run SWA on an existing Linux server or workstation, use the Docker container. The image bundles all dependencies (Python, Flask, Paramiko, ReportLab, and all supporting libraries) — no manual package installation is required.
Pull and start the container with a single command:
docker run -d \
--name log-viewer \
-p 3005:3005 \
--restart always \
fernandorivasplata/log-viewer:latest

The -p 3005:3005 flag maps port 3005 on the host to the container. The --restart always flag ensures the container restarts automatically after a host reboot or Docker daemon restart.

2.3 Update the Application
VM Option — Automatic Updates
When running the Stellar WIFI Analyzer (SWA) tool in a VM, updates occur each night at midnight to check for updates. The VM must have internet access and must be operative at that time.

Docker Option — Manual Update
To update to the latest version, run the following three commands in sequence:
# Step 1: Pull the latest image
docker pull fernandorivasplata/log-viewer:latest
# Step 2: Stop and remove the running container
docker stop log-viewer && docker rm log-viewer
# Step 3: Start a new container from the updated image
docker run -d --name log-viewer -p 3005:3005 --restart always
fernandorivasplata/log-viewer:latest
⚠ Note
Updating removes the old container. Any data or logs stored inside the container will be lost. If you
need to preserve session data, save it before updating.

2.4 Starting the Application
VM Option
The container starts automatically when the VM boots. Simply open a browser and navigate to:
http://x.x.x.x:3005
Docker Option
Verify the container is running:
docker ps | grep log-viewer
You should see log-viewer listed with status Up. Once confirmed, navigate to:
http://<ipaddress>:3005Stellar WiFi Analyzer | User Guide | V1.1.5-build-9.10 Page 10 of 25

If running Docker on your local machine, use http://localhost:3005 or http://127.0.0.1:3005. If
running on a remote server, use that server's IP address.

Changes or Improvements

V0.3.0-build-3
Differentiating Radius Authentication than Radius Accounting

V0.3.0-build-4
Differentiating 4-Way-Handshake messages 1/1 to 1/4

V0.3.0-build-5
Analyze both Aps button added

V0.3.0-build-6
Time elapsed between Flows is calculated and shown

V0.3.0-build-7
Channel utilization as a Gauge

V0.3.0-build-8
CCI logic improved and using a Gauge

V0.3.0-build-9
Network Events analysis improvements

Refetch logs button fix

V0.3.0-build-10
Tx Power obtained in real time from the 2.4, 5 or 6Ghz radio adapter when using the CCI function

From now on you can change the tx power on the radio adapter for troubleshooting purposes

V0.3.0-build-11
Split screen fullscreen

V0.3.0-build-12
Improved analysis logic

Network analysis page can be closed pressing the escape key

V0.3.0-build-13
Improved Network Events Analysis

V0.3.0-build-14
Improved Clients Connected search function

V0.3.0-build-15
Improved Flow reconstruction analysis, now you can see the Virtual Adapter used allowing you to identify if the roaming is happening among different bands likes roaming form 5Ghz to 6Ghz or any other scenario.

V0.3.0-build-16
Improved Flow reconstruction analysis, now you can see the roaming events and the destination AP ip address where the client device is roaming to.

V0.3.0-build-17
Neighbor AP's: Now you can see the list of the Neighbor APs. Being capable to check if a given AP mac address or ip address is part of the neighborship is critical when troubleshooting roaming problems. 

V0.3.0-build-18 and build-19
Connection reconstruction and analysis improvement: 

When a result_code different than 0 is detected after an ipv4 address has been negotiated the tool will calculate the time lapsed beween these 2 events.

When an event with result code different than 0 (whihc means a problem occurred) happens after the connection flow reached an ipv4 address then that is not considered a flow issue but an important event to be considered.

V0.4.0-build-1

Graphical Summary per MAC address added to the Network Events Analysis page

Dte and Time filter added to the Network Events Analysis page

V0.4.0-build-2

You can now analyze up to 4 APs simultaneously

Graphical Summary per MAC address visual improvement

V0.4.0-build-3

Improvements on the Roaming Neighbors AP details and accounting. Being capable to see in real time the neighbor APs details is important when troubleshooting roaming issues.

V0.4.0-build-4

Top 5 mac addresses with the highest number of failed connection flows and Top 5 mac addresses with the highest number of succesful connections flows.

V0.4.0-build-5

Association Requests and Responses are clearly differentiated in the connection flow details

Top 5 MAC addresses are now clickable and when clicked are automatically selected to be analyzed.

V0.4.0-build-6

Connection flows details are now folded for an easy general view. You can unfold the flows clicking on each flow.

V0.4.0-build-7

Improved MAC and 802.1x failure detection

V0.4.0-build-8

Top 5 issues detected within the logs

V0.4.0-build-9

When clicking on the Top 5 issues you can see some of the log lines associated

V0.4.0-build-10

When applying a zoom in or zoom out on any AP full screen page the same font size will be enforced on every other AP page.

V0.4.0-build-11

Improved capacity to recognize a failure at the Auth stage

V0.5.0-build-12

Improved capacity to differentiate an association with a disassociation event in the timeline.

V0.5.0-build-1

When fetching logs you will see the time window this log file is including. This is very helpful when trying to understand why you are not seeing all the information since the logs within the APs are not in synch meanng that each AP has a different starting date/time.

Monitor Mode has been added to allow you to have an aligned starting date/time on every AP. Monitor Mode starts a new log file on each AP at the same starting time. From that point, the program appends only the new log lines every minute so all AP monitor logs stay aligned in time. These monitor logs are shown in the webpage and support the same actions such as zoom, save, refetch/recheck, and analysis. This mode is useful when you want to capture a fresh troubleshooting window from multiple APs without mixing older log history. When Monitor Mode is stopped, the captured files are downloaded to your computer and removed from the server.

V0.5.0-build-2

Added the capacity to upload and analyze up to 4 local log files (offline analysis)

V0.5.0-build-3

Increased the capacity to process upto 10 APs simultaneously instead of just 4. 

V0.5.0-build-4

Improved the Monitor Mode capacity to automatically stop the monitor mode after 30 minutes and save all the logs gathered for a later analysis. You can stop manually the Monitor Mode or jst leave it and the system will stop automatically after 30 minutes, you need to accept the message to save the log files.

V0.5.0-build-5

Easier log navigation by date and time. From now on there is no need to enter manually any Date and time filter. The date and time filter can now be selected from a calendar or clicking on some predefined filters like the last 1, 2 .. hours

