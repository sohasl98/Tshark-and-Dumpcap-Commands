# Tshark-and-Dumpcap-Commands 🔎

## Tshark Commands 🔎
Tshark is the terminal-based network protocol analyzer that captures and interprets network traffic.

1. Capture Packets:

✔️ Capture traffic on an interface:
tshark -i eth0

This command captures all packets on the eth0 interface.

✔️ Capture with a display filter:
tshark -i eth0 -Y "http"

Filters the output so only packets related to HTTP are displayed.

✔️ Capture to a file:
tshark -i eth0 -w capture.pcap

Captures packets and writes them to a file in .pcap format.

✔️ Capture specific number of packets:
tshark -i eth0 -c 100

Captures only 100 packets.

✔️ Capture with a time limit:
tshark -i eth0 -a duration:60

Stops the capture after 60 seconds.

2. Filtering:

✔️ Capture with a capture filter:
tshark -i eth0 -f "port 80"

Captures only traffic to/from port 80 (HTTP).

✔️ Capture DNS traffic:
tshark -i eth0 -f "udp port 53"

Filters to capture DNS queries and responses.

✔️ Capture and apply display filter:
tshark -r capture.pcap -Y "ip.src == 192.168.1.1"

Reads from a capture file and only displays packets where the source IP is 192.168.1.1.

3. Inspecting Packets:

✔️ Display only packet summary:
tshark -r capture.pcap -q -z io,stat,0

Provides a summary of captured traffic, useful for statistical analysis.

✔️ Output specific fields:
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e frame.len

Displays only the source IP, destination IP, and frame length.

4. Protocols and Layers:

✔️ Display available protocols:
tshark -G protocols

Lists all supported protocols.

✔️ Decode as specific protocol:
tshark -r capture.pcap -d tcp.port==443,ssl

Decodes traffic on port 443 as SSL.

5. Other Useful Options:

✔️ Save in human-readable format:
tshark -r capture.pcap -V > capture.txt

Outputs the entire capture in human-readable format.

✔️ Show packet statistics:
tshark -q -z io,stat,10

Shows I/O statistics for the captured packets every 10 seconds.

## Dumpcap Commands 🔎
Dumpcap is more focused on efficient capturing of traffic to files and is used in scenarios where performance is key.

1. Basic Packet Capture:

✔️ Capture on an interface:
dumpcap -i eth0

Captures all traffic on eth0.

✔️ Capture to a file:
dumpcap -i eth0 -w capture.pcap

Writes the capture to a file capture.pcap.

✔️ Set a capture buffer size:
dumpcap -B 50

Increases the buffer size to 50 MB to avoid packet loss in high-volume captures.

2. Limiting Capture Size:

✔️ Limit capture file size:
dumpcap -i eth0 -a filesize:100000

Captures until the file reaches 100 MB, then stops.

✔️ Capture with a time limit:
dumpcap -i eth0 -a duration:3600

Captures for one hour (3600 seconds).

✔️ Capture with file rotation:
dumpcap -i eth0 -b files:5 -b filesize:100000 -w capture

Creates up to 5 files, each up to 100 MB in size, with automatic file rotation.

3. Capturing Specific Traffic:

✔️ Capture with a capture filter:
dumpcap -i eth0 -f "port 80"

Filters traffic for a specific port.

4. Additional Capture Options:

✔️ Capture in background (daemon mode):
dumpcap -D

Listens for traffic without displaying output, useful for background monitoring.

✔️ Capture with root privileges:
sudo dumpcap -i eth0 -w capture.pcap

Run as root to capture on interfaces requiring elevated permissions.

✔️ Show available interfaces:
dumpcap -D

Lists all available interfaces for capture.

Performance Considerations:

Dumpcap is often used when high performance or low system resource usage is required, while Tshark offers more detailed packet analysis and filtering options during capture or post-processing.

Both tools are valuable for packet analysis in different scenarios, and knowing which tool to use depends on the complexity of the task or the performance required.
