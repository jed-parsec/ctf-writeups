# CTF Challenge Writeup: [wifiland]

## Challenge Details
- **Category:** [network, wireless]
- **Points:** [380]

## Description
Are you larping in the wifiland? Get me the client and target IP address!

## Approach
This challenge involves analyzing network traffic captured in a pcap file named `wifiland.pcap`. We are provided with a Python script named `get_flag.py`. The objective is to extract the flag from the network traffic using the client and target ip address.

Analyzing the wifiland.pcap
![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/bc058627-18db-4a6d-8bae-93579631c7de)

Upon opening `wifiland.pcap` in Wireshark, we observed various network packets, including IEEE 802.11 Beacon frames. These frames contain information about the Wi-Fi network, including MAC addresses.

One of the MAC addresses observed in the Beacon frames is `02:00:00:00:05:00`, which appears to be formatted similarly to MAC addresses.
