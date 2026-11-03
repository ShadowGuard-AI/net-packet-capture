![Banner](banner.png)

# net-packet-capture
Captures network packets for a specific interface and filters them based on user-defined criteria (e.g., port, protocol, IP address). Outputs the captured packets in PCAP format. Focused on basic network operations.

## Install
`git clone https://github.com/ShadowGuard-AI/net-packet-capture`
`pip install -r requirements.txt`

## Usage
`python3 main.py [options]`

## Parameters
- `-h`: Show help message and exit
- `-i, --interface`: Network interface to capture packets from (default: eth0)
- `-o, --output`: Output PCAP file (default: capture.pcap)
- `-p, --port`: Filter packets by port number
- `-proto, --protocol`: Filter packets by protocol (e.g., tcp, udp, icmp)
- `-src, --source`: Filter packets by source IP address
- `-dst, --destination`: Filter packets by destination IP address
- `-n, --number`: Number of packets to capture (default: 0, capture until interrupted)
- `--promisc`: Enable promiscuous mode
- `--timeout`: Timeout in milliseconds (default: 100)

## Verified behavior
- `python3 -m py_compile main.py` passes, but `python3 main.py --help` fails in this sandbox at import: `pcapy` is not installed, and installs are forbidden in this wave. The parameter list above is taken from the argument parser in `main.py`, and no live capture is claimed here. A live capture also needs capture privileges on the interface.
- Port validation, read from the code: a port outside 0 to 65535 logs "Invalid port number" and exits 1. A nonstandard protocol name only logs a warning and continues.
- Limit, read from the code: the output file is created before the live device is opened, so a run that fails to open the device still leaves behind a valid but empty PCAP file.

## License
See LICENSE.
