# Cowrie Honeypot Project

Simple SSH honeypot using Cowrie to capture and analyze attacker behavior

## Overview
This project simulates a honeypot environment to observe and analyse unauthorized SSH access attempts. Using the Cowrie honeypot on Ubuntu and an attacking Kali machine, the setup allows safe study of brute-force behaviour, command patterns, and attacker interaction in a controlled environment.

## Objectives
- Understand common brute-force and unauthorized access techniques  
- Capture and analyse attacker behaviour and commands  
- Gain hands-on experience with defensive security tools like Cowrie  

## Scope

### In Scope
- Setting up a honeypot environment using Cowrie on Ubuntu  
- Simulating SSH brute-force attacks from a Kali Linux machine  
- Capturing and logging attacker login attempts and commands  
- Basic analysis of attacker behaviour based on collected logs  
  
### Out of Scope
- Development of custom scripts for automated attacks or log analysis  
- Advanced malware analysis or payload execution  
- Integration with SIEM or large-scale monitoring systems  
- Deployment in a real-world production environment  
- Active defense mechanisms (e.g., automated blocking or response)

## Features
- Simulates an SSH/Telnet service using the Cowrie honeypot  
- Captures SSH brute-force attempts (usernames and passwords)  
- Logs all commands executed by attackers during sessions  
- Generates structured log files for analyzing attacker behavior

## Implementation Notes

### Environment
- Two virtual machines running in Oracle VirtualBox:
  - **Ubuntu VM (Honeypot):** Hosts Cowrie to capture and log attacker activity  
  - **Kali Linux VM (Attacker):** Performs SSH brute-force attempts  
- Both VMs were configured using a **Host-Only Adapter**

### Setup
- Ubuntu 22.04 used to meet Cowrie’s requirement for Python 3.10+  
- Kali Linux cloned from an existing setup  
- Cowrie installed from its official GitHub repository  
- Required dependencies installed (e.g., Git, Python, libraries)  

### Attack Simulation
- SSH brute-force attacks conducted from Kali Linux  
- Tools such as **Hydra** were used to simulate login attempts  

### Why Cowrie
- Provides an emulated SSH/Telnet environment  
- Captures login attempts, commands, and session activity  
- Generates detailed logs for analyzing attacker behavior

## Methodology

### Virtual Machine Setup
- Ubuntu 22.04 VM used to host the Cowrie honeypot  
- Kali Linux VM used as the attacker (cloned from existing setup)  
- Both VMs configured with a **Host-Only Adapter** for isolated communication  
- Ubuntu temporarily switched to NAT to download dependencies  

### Cowrie Installation
- Installed required dependencies:
```bash
sudo apt install python3-pip python3-dev libssl-dev libffi-dev build-essential
```

- Cloned Cowrie repository:
```bash
git clone https://github.com/cowrie/cowrie.git
```

### Environment Setup
```bash
python3 -m venv env
source env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
cp etc/cowrie.cfg.dist etc/cowrie.cfg
```

### Configuration
```text
listen_endpoints = tcp:2222:interface=0.0.0.0
```

### Execution and Testing
```bash
cowrie start
tail -f var/log/cowrie/cowrie.log
ssh root@<HONEYPOT_IP> -p 2222
```

## Documentation
Full report is available in `honeypot-proj-report.pdf`
