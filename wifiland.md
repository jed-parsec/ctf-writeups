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

Upon examining the wifiland.pcap file in Wireshark, I noticed a variety of network packets, including IEEE 802.11 Beacon frames. These frames contain crucial information about the Wi-Fi network, such as MAC addresses.

While inspecting the Beacon frames, I observed that one of the MAC addresses appeared as 02:00:00:00:05:00, resembling the typical MAC address format. Strangely, no IP addresses were evident. This led me to suspect there might be additional layers of network activity.

To delve deeper into the analysis, I decided to filter out the EAPOL frames to investigate any potential 4-way handshakes. These handshakes could be exploited for password cracking purposes using tools like aircrack-ng.



![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/0b89c6f5-7343-4fc0-a6fe-a9f716dacbd9)

After I found a 4-way handshake between the MAC addresses 02:00:00:00:05:00 and 02:00:00:00:13:00, I used a tool called aircrack-ng to get the Wi-Fi password.

![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/7a9d3ee6-d498-4bda-b42e-d485db3a6d08)

Cracking it was successful!

![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/615ca87a-2a2a-48dc-85e1-2ae6254d90a9)


Having obtained the password, which is "12345678," I decided to utilize it as the decryption key. To do so, We will navigate to the "Edit" menu, followed by "Preferences," and then select "Protocols" and "IEEE 802.11." From there, proceed to edit the decryption keys accordingly.


![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/2186a712-9f73-4981-9d0d-b0a2fdc4b109)



After using the acquired password for decryption, I noticed an ARP message originating from the source address 02:00:00:00:13:00. The message contained the inquiry "Who has 93.184.216.34? Tell 10.0.3.19."

This discovery revealed both the Client IP address (10.0.3.19) and the Target IP address (93.184.216.34)
![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/87ce8944-8c7f-46a6-a950-bc0dba862145)

Now that we have obtained the client IP and the target IP, we can utilize them as values for the variables in the get_flag.py to get the flag
![image](https://github.com/jed-parsec/ctf-writeups/assets/71179248/8e364114-5e23-47e4-b482-7cef5f7e0828)




