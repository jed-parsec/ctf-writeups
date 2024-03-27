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

One of the sources observed in the Beacon frames is `02:00:00:00:05:00`, which appears to be formatted similarly to MAC addresses.
Hmmm, we don't see any signs of IP addresses... There must be something else going on. I figured I'd filter out the EAPOL to check for any 4-way handshakes which can be used to crack the pwd using aircrack-ng


![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/0b89c6f5-7343-4fc0-a6fe-a9f716dacbd9)

We found a 4-way handshake between 02:00:00:00:05:00 and 02:00:00:00:13:00, so i used aircrack-ng to get the PSK


![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/7a9d3ee6-d498-4bda-b42e-d485db3a6d08)

Cracking it was successful!

![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/615ca87a-2a2a-48dc-85e1-2ae6254d90a9)


Now that we got the pwd which is 12345678, i figured I'd use the pwd as a decryption key. Just go to Edit -> Preference -> Protocols -> IEEE 802.11 and then edit the decryption keys.

![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/2186a712-9f73-4981-9d0d-b0a2fdc4b109)
