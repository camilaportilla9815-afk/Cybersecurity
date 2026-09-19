# Linux Server Hardening & UFW Firewall Configuration

1. Implement a strict **Default Deny Incoming** traffic policy.
2. Configure secure access for essential network services (SSH, HTTP, HTTPS).
3. Apply **Rate Limiting** on port 22 to mitigate SSH brute-force attacks.
4. Establish network access controls based on source IP addresses and internal subnets.
5. Explicitly block unauthorized or insecure protocols/services (e.g., SMB/NetBIOS).
6. Enable security event logging (`logging medium`) for SIEM integration and SOC analysis.
7. Audit and verify firewall status using numbered rule indices and log analysis.

---

## Key Commands Summary

| Category | Command | Description |
| :--- | :--- | :--- |
| **Management** | `sudo ufw enable / disable` | Enables or disables the firewall status |
| **Policies** | `sudo ufw default deny incoming` | Blocks all incoming traffic by default |
| **Web Services**| `sudo ufw allow 80/tcp` / `443/tcp` | Allows HTTP and HTTPS web traffic |
| **SSH Hardening**| `sudo ufw limit 22/tcp` | Applies rate limiting against brute-force attempts |
| **Subnet Access**| `sudo ufw allow from 10.0.2.0/24 to any port 8080` | Restricts access to specific subnets |
| **Denylist** | `sudo ufw deny from 203.0.113.0/24` | Explicitly blocks untrusted external networks |
| **Audit** | `sudo ufw status numbered` | Displays active rules with numbered indices |
| **Rule Removal**| `sudo ufw delete [number_or_rule]` | Deletes a rule by index number or definition |
| **Logging** | `sudo ufw logging medium` | Configures verbosity for firewall audit logs |

---
#!/bin/bash
# ==============================================================================
# Script: iptables-basic-firewall
# ==============================================================================

# ------------------------------------------------------------------------------
# 1. Limpieza de reglas previas
# ------------------------------------------------------------------------------
echo "[-] Limpiando reglas anteriores"
iptables -F


# ------------------------------------------------------------------------------
# 2. Políticas por defecto (Denegar todo lo entrante)
# ------------------------------------------------------------------------------
echo "[-] Estableciendo políticas por defecto..."
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -P OUTPUT ACCEPT

# ------------------------------------------------------------------------------
# 3. Permitir tráfico en Loopback (127.0.0.1)
# ------------------------------------------------------------------------------
echo "[-] Configurando interfaz de loopback..."
iptables -A INPUT -i lo -j ACCEPT
iptables -A OUTPUT -o lo -j ACCEPT

# ------------------------------------------------------------------------------
# 4. Permitir tráfico de conexiones ya establecidas y relacionadas
# ------------------------------------------------------------------------------
echo "[-] Permitiendo tráfico de conexiones existentes..."
iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT

# ------------------------------------------------------------------------------
# 5. Permitir servicios entrantes esenciales (SSH, HTTP, HTTPS)
# ------------------------------------------------------------------------------
echo "[-] Abriendo puertos 22 (SSH), 80 (HTTP) y 443 (HTTPS)..."
iptables -A INPUT -p tcp --dport 22 -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT

# ------------------------------------------------------------------------------
# 6. Permitir Pings (ICMP) con control de frecuencia (Rate Limiting)
# ------------------------------------------------------------------------------
echo "[-] Configurando control de peticiones ICMP (Ping)..."
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s --limit-burst 5 -j ACCEPT

echo "[+] Cortafuegos configurado con éxito."
