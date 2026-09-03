## Exercise 1: Linux Network Diagnostics & Troubleshooting

* **Configuration & Gateway Discovery:** Utilized `ip a` to verify the local interface configuration (`192.168.8.113/24` on `eth0`) and `ip route` to identify the default gateway (`192.168.8.1`).
* **Socket & Port Auditing:** Executed `ss -tuln` and `netstat -tuln` to list active listening TCP/UDP ports and system services.
* **Connectivity & TCP Verification:** Tested ICMP reachability via `ping`, validated open remote ports using `nc -zv <IP> <PORT>`, and inspected active TCP sessions with `ss -t`.

---

## Exercise 2: Automated Backup Script (`backup.sh`)

* **Script Purpose:** Automates directory backups by generating date-stamped archive folders.
* **Logic & Variables:** Defined target source (`/home/camila/Fundamental-of-Cybersecurity`) and destination paths, incorporating dynamic date tagging (`backup-$(date +%F)`).
* **Execution & Verification:** Applied executable permissions via `chmod +x backup.sh`, executed `./backup.sh`, and validated structural output using `ls`.

```bash
#!/bin/bash
ORIGEN="/home/camila/Fundamental-of-Cybersecurity"
DESTINO="/home/camila/backup"

mkdir -p "$DESTINO"
cp -r "$ORIGEN" "$DESTINO/backup-$(date +%F)" ```

---



## Exercise 3: Automated File Search Script (`search.sh`)

* **Script Purpose:** Automates recursive pattern matching across directory structures using Bash and `grep`.
* **Core Logic:** Configured `grep -rnw` to execute full-word, recursive searches with line number reporting across targeted paths.
* **Execution & Permissions:** Granted execution privileges via `chmod +x search.sh` and verified output via `./search.sh`.

```bash
#!/bin/bash
CARPETA="/home/camila/Fundamental-of-Cybersecurity"
PALABRA="Network"

grep -rnw "$CARPETA" -e "$PALABRA"
```

---

## Exercise 4: System Resource Monitoring Script (`monitoring.sh`)

* **Script Creation & Logic:** Utilized the `nano` text editor to construct `monitoring.sh`. Integrated `top -b -n 1 | head -n 10` to capture non-interactive CPU metrics and top resource-consuming processes, followed by `free -h` to display memory/swap utilization in human-readable format.
* **Permissions Management:** Granted execution rights using `chmod +x monitoring.sh`.
* **Verification:** Executed the script via `./monitoring.sh` to confirm rapid, clear diagnostic terminal output for real-time monitoring.

```bash
#!/bin/bash
echo "=== CPU & Top Processes ==="
top -b -n 1 | head -n 10

echo -e "\n=== Memory Usage ==="
free -h
```

---

## Exercise 5: Isolated Internal Virtual Network Setup

* **VM Provisioning:** Cloned an existing virtual machine to establish a secondary node for network testing.
* **Adapter Configuration:** Reconfigured the virtual network adapters on both VMs to **Internal Network** mode to isolate traffic from external networks.
* **Interface & IP Configuration:** Modified `/etc/network/interfaces` via `nano` and manually assigned static IP addresses within the same subnet using `sudo ip link set eth0 up` and `sudo ip addr add 192.168.x.x dev eth0`.
* **Connectivity Verification:** Executed bidirectional `ping` requests between both nodes to confirm successful L3 reachability within the isolated segment.

```bash
# Enable the eth0 interface
sudo ip link set eth0 up

# Assign static IP address to internal interface
sudo ip addr add 192.168.10.5/24 dev eth0

# Verify isolated network connectivity
ping -c 4 192.168.10.6
```
