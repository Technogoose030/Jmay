---
layout: default
---
<!--Forget.html-->
## Project 2: Network Traffic Analysis with Wireshark
### Objective: The primary goal of this project was to use Wireshark for monitoring and analyzing network traffic to identify and address performance and security issues.

### Preparation: Ensured all necessary tools and prerequisites were in place, including Wireshark installation and configuration.

## Setting up wireshark 
Installation: Downloaded and installed Wireshark from the official website, ensuring the installation of necessary components like WinPcap or Npcap for packet capturing on Windows.
Wireshark download: https://www.wireshark.org/download.html

Configuration: Launched Wireshark and configured the network interfaces. This involved selecting the correct interface (Ethernet, Wi-Fi) for capturing relevant network traffic.

<img src="docs/assets/Pasted image 20240904140653.png" style="width: 30vw; min-width: 330px;" />

##Start Capturing Traffic:
    
Click on the Start button (the shark fin icon) next to the selected network interface to begin capturing packets.

Next is to start monitoring traffic to look for common weak ports using these filters 

tcp.port == 21 for FTP traffic

Yielded no results as no devices on the network was trasferring using ftp 

tcp.port == 80 for HTTP traffic

Yielded no results as nothing on the network was using http so i simulated it 

First made a python server 

<img src="docs/assets/Hosting Server.png" style="width: 30vw; min-width: 330px;" />

Then ran a curl comand on another computer 

<img src="docs/assets/Curl request.png" style="width: 30vw; min-width: 330px;" />

From this i cancelled the wireshark scan to analyze the packets 

<img src="docs/assets/Get request.png" style="width: 30vw; min-width: 330px;" />

Doing this shows how to find the GET request for port 80. If you are to look deeper you would find all of the files in the directory that i hosted in plain text the same would not have happened if it was being hosted with the encrypted version of http which is https

tcp.port == 3389 for RDP traffic

[back](./)
