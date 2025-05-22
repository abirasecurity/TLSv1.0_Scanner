# TLSv1.0_Scanner
A Python tool for scanning multiple hosts to detect TLSv1.0 support and track remediation progress.

# Features
Scan multiple hosts concurrently for TLSv1.0 support
Parse target lists with IP:PORT format
Two operation modes:
	Basic scan mode: Shows which hosts have TLSv1.0 enabled/disabled
        Remediation test mode: Tracks remediation status of hosts

# Requirements
Python 3.6+

sslscan command-line tool installed on your system

# Installation
   Clone this repository:

 ```
git clone https://github.com/yourusername/TLSv1.0_Scanner.git
cd TLSv1.0_Scanner
```
Make sure you have sslscan installed:
```
# On Debian/Ubuntu
sudo apt-get install sslscan

# On CentOS/RHEL
sudo yum install sslscan

# On macOS
brew install sslscan
```
# Usage
## Basic Scanning
To scan hosts and see which ones have TLSv1.0 enabled:	

```python tls10_check.py -i targets.txt```
	
## Remediation Testing
To check remediation status (shows REMEDIATED/NOT REMEDIATED for each host):	

```python tls10_check.py -i targets.txt -r```
	
## Command-line Options

```
-i, --input          Input file with targets (required)
-t, --threads        Number of concurrent threads (default: 10)
-r, --remediation_test  Run in remediation test mode
```

## Input File Format
Input File Format
The input file should contain one target per line in the following format:

```
192.168.1.1:443
example.com:8443
10.0.0.1
```

If no port is specified, the default port (443) will be used.
	
# Output Examples
## Basic Scan Mode

```
# Here's a sample of what the output would look like with the updated script:

[+] Loaded 10 targets from targets.txt
[+] Scanning 192.168.42.15:443
[+] Scanning 203.45.167.89:443
[!] TLSv1.0 ENABLED on 192.168.42.15:443
[+] Scanning 18.204.56.112:443
[+] Scanning 54.231.78.92:443
[+] Scanning 104.18.25.64:443
[!] TLSv1.0 ENABLED on 203.45.167.89:443
[+] Scanning 172.217.164.110:443
[+] Scanning 35.186.224.47:443
[+] Scanning 13.107.42.16:443
[+] Scanning 52.95.116.115:443
[+] Scanning 8.8.8.8:443
[!] TLSv1.0 ENABLED on 104.18.25.64:443
[!] TLSv1.0 ENABLED on 13.107.42.16:443
[!] Error scanning 18.204.56.112:443: Connection refused

[✓] Scan Results:

[!] Hosts with TLSv1.0 ENABLED:

    - 192.168.42.15:443
    - 203.45.167.89:443
    - 104.18.25.64:443
    - 13.107.42.16:443

[+] Hosts with TLSv1.0 DISABLED:

    - 54.231.78.92:443
    - 172.217.164.110:443
    - 35.186.224.47:443
    - 52.95.116.115:443
    - 8.8.8.8:443

# And if you run it with the -r remediation flag:

[+] Loaded 10 targets from targets.txt
[+] Scanning 192.168.42.15:443
[+] Scanning 203.45.167.89:443
[!] TLSv1.0 ENABLED on 192.168.42.15:443
[+] Scanning 18.204.56.112:443
[+] Scanning 54.231.78.92:443
[+] Scanning 104.18.25.64:443
[!] TLSv1.0 ENABLED on 203.45.167.89:443
[+] Scanning 172.217.164.110:443
[+] Scanning 35.186.224.47:443
[+] Scanning 13.107.42.16:443
[+] Scanning 52.95.116.115:443
[+] Scanning 8.8.8.8:443
[!] TLSv1.0 ENABLED on 104.18.25.64:443
[!] TLSv1.0 ENABLED on 13.107.42.16:443
[!] Error scanning 18.204.56.112:443: Connection refused

[✓] Remediation Test Results:

[!] Hosts with TLSv1.0 still ENABLED:

    192.168.42.15:443 - NOT REMEDIATED
    203.45.167.89:443 - NOT REMEDIATED
    104.18.25.64:443 - NOT REMEDIATED
    13.107.42.16:443 - NOT REMEDIATED

[+] Hosts with TLSv1.0 disabled:

    54.231.78.92:443 - REMEDIATED
    172.217.164.110:443 - REMEDIATED
    35.186.224.47:443 - REMEDIATED
    52.95.116.115:443 - REMEDIATED
    8.8.8.8:443 - REMEDIATED

[*] Total hosts scanned: 9
[*] Hosts with TLSv1.0 enabled: 4
[*] Hosts with TLSv1.0 disabled: 5

```
# License
MIT License

# Contributing
Contributions are welcome! Please feel free to submit a Pull Request.
