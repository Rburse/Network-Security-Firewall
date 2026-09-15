# Network Security

![GNS3](https://img.shields.io/badge/GNS3-network%20emulation-2E8B57)
![Cisco IOS](https://img.shields.io/badge/Cisco%20IOS-3745%20router-1BA0D7)
![Windows](https://img.shields.io/badge/Windows-PC%20%26%20Server-0078D6)
![Focus](https://img.shields.io/badge/focus-routing%20%26%20connectivity-blue)

Hands-on network security coursework for **CYB 220** at Southern New Hampshire University.
Each module is a self-contained lab: build the environment, configure the devices, and
verify the result at the command line.

**Author:** Robert Burse Jr. · Security+ · U.S. Army veteran

---

## Module 2 — Network Topology & Ping Testing

Design and validate a routed network across three subnets in GNS3, then prove
end-to-end connectivity using a structured, layer-by-layer troubleshooting method.

![Completed GNS3 topology](module-02-network-topology/media/image1.png)

*Two Windows PCs, a Windows server, and a Cisco 3745 router — one host per subnet,
all links active.*

### Addressing scheme

| Host | IP address | Subnet mask | Default gateway | Router interface |
|------|-----------|-------------|-----------------|------------------|
| PC1_TestNetwork | 192.168.1.101 | 255.255.255.0 | 192.168.1.100 | Fa0/0 |
| PC2_TestNetwork | 192.168.2.101 | 255.255.255.0 | 192.168.2.100 | Fa0/1 |
| Server_TestNetwork | 192.168.3.101 | 255.255.255.0 | 192.168.3.100 | Fa1/0 |

Three separate /24 networks, so no two hosts can reach each other without the router
forwarding between subnets — which is exactly what the ping tests confirm.

### What the lab covers

- **Router configuration (Cisco 3745).** Each FastEthernet interface assigned its
  gateway address in privileged EXEC mode, brought up with `no shutdown`, and the
  running config saved with `write memory`.
- **Host configuration.** Static addressing on the PCs and the server (the server via
  `netsh` from an elevated prompt), verified with `ipconfig`.
- **Structured connectivity testing.** Pings run in best-practice troubleshooting order —
  local NIC → local gateway → remote gateway → remote host — from every host in the
  topology.

### Results

All tests returned replies at **0% packet loss**. Cross-subnet pings show **TTL=127**,
confirming the router decremented the TTL and forwarded traffic between subnets rather
than the hosts reaching each other directly. Full command output and screenshots are in
[`module-02-network-topology/`](module-02-network-topology/).

### Skills demonstrated

`IPv4 subnetting` · `Cisco IOS interface configuration` · `static host addressing`
· `default-gateway routing` · `ICMP connectivity testing` · `structured troubleshooting`
· `TTL analysis` · `network documentation`

---

## Repository structure

```
cyb-220-network-security/
├── README.md                       <- this file
├── .gitignore
└── module-02-network-topology/
    ├── README.md                   <- module summary
    ├── CYB_220_Module2_Assignment_Robert_Burse.docx   <- submitted deliverable
    ├── assignment.md               <- text version (diffable in Git)
    └── media/                      <- topology & ping-test screenshots
```

Every module is self-contained — its own `media/` and `README.md` — so modules can be
added, renamed, or removed without touching the others.

## Adding a new module

```bash
mkdir -p module-03-<short-name>/media   # drop in your .docx, notes, and screenshots
git add module-03-<short-name>
git commit -m "Add Module 3: <short name>"
git push
```

## Modules

| Module | Topic | Folder |
|--------|-------|--------|
| 02 | Network topology & ping testing (GNS3) | [`module-02-network-topology/`](module-02-network-topology/) |

---


