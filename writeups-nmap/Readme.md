A service and version detection scan was conducted specifically for ports 22 and 80 on the Nmap public test server


Apache HTTP Server software version 2.4.7 was detected on port 80, and OpenSSH software version 6.6.1p1 on port 22


According to the CVE results, the Apache version contains a vulnerability: Possible NULL dereference or SSRF in forward proxy configurations in Apache HTTP Server 2.4.51 and earlier.



It was detected that for the OpenSSH version, the verify_host_key function in sshconnect.c in the client in OpenSSH 6.6 and earlier allows remote servers to trigger the skipping of SSHFP DNS RR checking by presenting an unacceptable HostCertificate. Additionally, in OpenSSH, sshd prior to version 6.6 does not properly support wildcards in AcceptEnv lines in sshd_config, which allows remote attackers to bypass intended environment restrictions by using a substring located before a wildcard character.
