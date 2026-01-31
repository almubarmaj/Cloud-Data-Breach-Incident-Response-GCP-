The Scenario
I played the role of a junior cloud security analyst at Cymbal Retail, a multinational retailer that just suffered a massive data breach. Sensitive customer data, including credit card details, was exposed.

My task was to:

Identify vulnerabilities in Google Cloud Security Command Center (SCC)

Remediate misconfigurations across VMs, storage buckets, and firewalls

Verify compliance against PCI DSS standards

This was as close as it gets to a real-world incident response.
Step 1: Analyzing Vulnerabilities
The first thing I did was open the Google Cloud Security Command Center to see an overview of active vulnerabilities.

Key issues stood out immediately:

Buckets: Publicly accessible storage (high risk)

VMs: Public IPs, Secure Boot disabled, default service account in use

Firewall: SSH and RDP open to the whole internet, logging disabled

These misconfigurations explained how attackers were able to gain unauthorized access.






















Step 2: Fixing the Compromised VM
One of the virtual machines (cc-app-01) was compromised. To contain the breach, I:

Stopped the VM

Restored a clean VM (cc-app-02) from a snapshot taken before infection

Configured it securely:

Disabled public IP

Enabled Secure Boot

Restricted permissions (removed default service account with full API access)

Deleted the compromised VM (cc-app-01)

























This ensured that the new VM was hardened and free of malware.

Step 3: Securing Cloud Storage Buckets
Next, I turned to the exposed storage bucket that was publicly accessible. I:

Revoked public access

Switched to uniform bucket-level access

Removed overly permissive permissions










This closed the door on one of the biggest risks — unauthorized external access to sensitive files.

Step 4: Restricting Firewall Ports
The firewall was wide open, allowing SSH (22) and RDP (3389) from anywhere. This is like leaving the front door unlocked.

To fix this, I:

Created a new firewall rule that only allowed SSH access from trusted Google IAP ranges (35.235.240.0/20)

Deleted overly broad default rules (default-allow-icmp, default-allow-rdp, default-allow-ssh)

Enabled firewall logging for better visibility













This limited exposure and made future incidents easier to investigate.

Step 5: Verifying Compliance
After remediation, I re-ran the PCI DSS compliance report in SCC.

Result? ✅ All the major vulnerabilities were resolved, leaving only some low-severity findings (like disabled VPC flow logs, which were part of the lab setup).




🎯 Key Lessons Learned
Working through this project taught me a lot:

Misconfigurations are the real threat. Most breaches don’t need fancy exploits — just open ports, public buckets, or over-permissive accounts.

Snapshots are lifesavers. Being able to restore clean VMs quickly is critical in incident response.

Firewalls and access control matter. Restricting entry points and logging activity makes a huge difference.

Compliance frameworks (PCI DSS here) help measure security. They give you a checklist to make sure nothing slips through.

✅ Final Reflection
This project was my first real contact with Cybersecurity — and it gave me confidence. I wasn’t just reading about attacks, I was actively defending against one.

The hands-on experience showed me how cloud security analysts detect, remediate, and verify fixes in real time. It was a great starting point, and it left me eager to dive deeper into incident response, threat detection, and cloud-native defense strategies.
