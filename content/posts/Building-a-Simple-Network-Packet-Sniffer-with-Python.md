+++
title = 'Building a Simple Network Packet Sniffer With Python'
date = 2024-09-21T10:39:05+02:00
draft = false
tags = ["programming", "python", "networking"]
+++

If you're interested in understanding how data flows through your network or need a tool for network diagnostics, creating a packet sniffer can be an exciting project.
In this post, I'll guide you through a Python-based packet sniffer that captures, decodes, and analyzes network packets.
This project is perfect for anyone wanting to learn more about networking and Python's ability to interact with low-level protocols.

## Project Overview

The goal of this packet sniffer is to capture and analyze packets at the Ethernet frame level.
By using Python's raw socket capabilities, it inspects Ethernet, IPv4, ICMP, TCP and UDP protocols.
This is ideal for understanding how these protocols work or for performing basic network diagnostics.

## Features of the Packet Sniffer

-   **Raw Socket Capture**: This sniffer uses raw sockets to intercept network traffic, allowing it to work directly at the Ethernet frame level.
-   **Protocol Decoding**: It decodes various networking protocols suck as Ethernet, IPv4, ICMP, TCP, and UDP, giving you detailed insights into the structure and content of the packets.
-   **Human-Readable Output**: Data is presented in a clean, readable format, which is invaluable for diagnostics and education.

## Key Functions Breakdown

Let's dive into how to the packet sniffer works by breaking down some important functions:

1. **Capturing Network Packets**:

```python
conn = socket.socket(socket.AF_PACKET, socket.SOCK_RAW, socket.ntohs(3))
```

Here, the sniffer sets up a raw socket that can capture all incoming and outgoing packets. This allows for the inspection of Ethernet frames, which is the foundation for understanding network traffic.

2. **Decoding Ethernet Frames**:

```python
def ethernet_frame(data):
    dest_mac, src_mac, proto = struct.unpack("! 6s 6s H", data[:14])
    return get_mac_addr(dest_mac), get_mac_addr(src_mac), socket.htons(proto), data[14:]
```

Ethernet frames contain essential details suck as the source and destination MAC addresses, and the protocol being used. This function extracts and converts the raw bytes into a readable format.

3. **Decoding IPv4 Packets**:

```python
def ipv4_packet(data):
    version_header_length = data[0]
    version = version_header_length >> 4
    header_length = (version_header_length & 15) * 4
    ttl, proto, src, target = struct.unpack ('! 8x B B 2x 4s 4s', data[:20])
    return version, header_length, ttl, proto, ipv4(src), ipv4(target), data[header_length:]
```

If the Ethernet protocol points to IPv4 (protocol number 8), this function decodes the packet's details suck as version, header length, TTL (Time to Live), and protocol.

4. **Handling Transport Layer Protocols**: The script supports decoding for popular transport layer protocols like TCP, UDP, and ICMP. Each protocol has its own method for unpacking relevant fields.

    - **TCP Decoding**:

    ```python
    def tcp_segment(data):
        (src_port, dest_port, sequence, acknowledgements, offset_reverse_flags) = struct.unpack('! H H L L H', data[:14])
        # Extract flags and ports
        return src_port, dest_port, sequence, acknowledgements, flag_urg, flag_ack, flag_psh, flag_rst, flag_syn, flag_fin, data[offset:]
    ```

    - **UDP Decoding**:

    ```python
    def udp_segment(data):
        src_port, dest_port, length = struct.unpack('! H H 2x H', data[:8])
        return src_port, dest_port, length, data[8:]
    ```

    - **ICMP Decoding**:

    ```python
    def icmp_packet(data):
        icmp_type, code, checksum = struct.unpack('! B B H', data[:4])
        return icmp_type, code, checksum
    ```

Each packet's information is printed in a structured format, making it easier to understand what is happening on the network.

## Example Output

Once the script is running, you'll see output like this:

```
Ethernet Frame:
Destination: AA:BB:CC:DD:EE:FF, Source: 11:22:33:44:55:66, Protoco: 8
    IPv4 Packet:
        Version: 4, Header Length: 20, TTL: 64
        Protocol: 6, Source: 192.168.0.1, Target: 192.168.0.2
            TCP Segment:
            Source Port: 443, Destination Port: 55678
            Sequence: 123456789, Acknowledgement: 987654321
            Flags:
                URG: 0, ACK: 1, PSH: 0, RST: 0, Syn: 1, FIN: 0
            Data:
                \x50\x61\x63\x6b\x65\x74\x20\x44\x61\x74\x61\x2e\x2e\x2e
```

## Running the Packet Sniffer

Here's a quick guide on how to run the packet sniffer on your system:

1. **Permissions**: Ensure that you have administrative or root privileges. Packet sniffers require access to raw sockets, which generally need elevated permissions.

2. **Run the Script**:

```bash
sudo python3 packet_analyzer.py
```

3. **Start Capturing Traffic**: The script will immediately start capturing network traffic, decoding each Ethernet frame and its subsequent payloads (IPv4, TCP, UDP, ICMP) as they pass through your network interface.

## Learning Points

-   **Packet Structure**: You'll gain an understanding of the basic structure of network packets from the Ethernet to transport layer protocols.

-   **Python's Socket Library**: This project demonstrates how Python can interact with low-level network interfaces using raw sockets.

-   **Data Decoding**: The script unpacks and intercepts binary data into a readable format, which is an essential skill in network programming.

## Final Thoughs

This packet sniffer project is an excellent introduction to network analysis and Python's capabilities in handling raw network traffic. With this tool, you can explore your network's data flow, understand how different protocols function, and gain hands-on experience with packet-level data.

Remember network sniffing hould always be done in compliance with your local laws and network policies.
