# STELLAR-Log-Analyzer-Web-Tool
Stellar Log analyzer is a real-time wireless diagnostics and RF analysis platform  designed specifically for senior wireless engineers, NOC teams, and escalation specialists.  The system enables deep inspection of WiFi client lifecycle events, RF channel utilization,  and other features.

Install:

docker run -d -p 3005:3005 --restart always --name log-viewer frivasplata/log-viewer:latest

Update:

docker pull frivasplata/log-viewer:latest

docker stop log-viewer

docker rm log-viewer

docker run -d -p 3005:3005 --restart always --name log-viewer frivasplata/log-viewer:latest


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
