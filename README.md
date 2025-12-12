# Nmap-Scapy-Lab-Documentation
🛡️ Network Recon & Packet Capture – Lab Summary
1. Purpose of the Lab

This lab session was designed to build practical experience with network discovery, service probing, and traffic analysis. Using Nmap for scanning and Scapy for packet inspection, the goal was to analyze the target system at 10.6.6.23 inside a safe, isolated environment.

These steps simulate actions performed during the reconnaissance phase of a penetration test.

2. Lab Setup & Tools

OS: Kali Linux

Applications Used:

Nmap

Scapy

Wireshark

Test Network: 10.6.6.0/24

Primary Target: 10.6.6.23

The tasks were all carried out on the internal network assigned for hands-on security testing.

🔎 3. Nmap Activities
3.1 Identifying Active Devices

Command used:

nmap -sn 10.6.6.0/24


Why: To perform a quick sweep and determine which systems are reachable.
Outcome: The target responded, confirming its availability.

3.2 Determining the Operating System

Command:

sudo nmap -O 10.6.6.23


Why: To analyze packet patterns and compare them to known OS fingerprints.
Result: Nmap produced its best OS estimate based on response behavior.

3.3 FTP Analysis on Port 21

Command:

nmap -p21 -sV -A -T4 10.6.6.23


Reason: Gather more details about the service version and any extra information.
Findings: The FTP service was detected along with version and configuration details.

3.4 SMB Share Enumeration

Command:

nmap --script smb-enum-shares.nse -p445 10.6.6.23


Goal: List shared folders exposed over SMB.
Result: Returned available shares and highlighted security-relevant information.

3.5 Testing for Guest SMB Login

Command:

smbclient //10.6.6.23/print$ -N


Purpose: Confirm whether anonymous authentication was enabled.
Observation: Guest access succeeded, indicating a potential security concern.

🧪 4. Scapy Exercises
4.1 Entering the Scapy Environment
sudo su
scapy


Completed all Scapy tasks in the interactive shell.

4.2 Capturing General Traffic

Command:

sniff()


Generated packets by running a ping to an external site.
The sniffing session picked up various types of packets including DNS and ICMP.

Saving results:

paro = _
paro.summary()

4.3 Monitoring a Specific Interface

Command:

sniff(iface="br-internal")


Triggered traffic by:

Browsing to 10.6.6.23

Performing pings

Saved output for review:

paro2 = _
paro2.summary()

4.4 Capturing Only ICMP Packets

Command:

sniff(iface="br-internal", filter="icmp", count=5)


Sent test traffic with a ping to the target.
Exactly five ICMP packets were collected.

Stored:

paro3 = _
paro3.summary()
paro3[3]

🧠 5. Main Takeaways

Network scanning revealed how to pinpoint active hosts and identify what services they run.

SMB testing showed that anonymous access can expose unnecessary risks.

Scapy provided a deeper understanding of how packets appear on the wire.

Filtering captures makes it easier to focus on specific protocols like ICMP.

The combined use of Nmap and Scapy mirrors real reconnaissance steps performed during penetration testing engagements.

🏁 6. Wrap-Up

This lab strengthened my ability to gather and interpret network information using industry-standard tools. Working through these exercises helped reinforce how attackers—and defenders—use scanning and packet capture to understand a system's exposure. Overall, it was a valuable hands-on experience in early-stage security assessment techniques.
