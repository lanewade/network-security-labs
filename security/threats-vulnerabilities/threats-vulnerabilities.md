# Threats & Vulnerabilities

This lab documents my study of cybersecurity threats, vulnerabilities, attack surfaces, and risk-reduction concepts from CompTIA Security+ coursework.

The goal is to demonstrate my understanding of how weaknesses can be identified, how common threats affect systems and networks, and how security controls can reduce risk.

## Concepts Practiced

- Threats and vulnerabilities
- Attack vectors
- Attack surfaces
- Vulnerability management
- CVEs
- CVSS
- Zero-day vulnerabilities
- Misconfigurations
- Unpatched systems
- Legacy systems
- Malware
- Ransomware
- Spyware
- Trojans
- Worms
- Rootkits
- Social engineering
- Phishing
- Credential attacks
- Insider threats
- Supply-chain threats
- Denial-of-Service attacks
- Network attacks
- Wireless threats
- Web application vulnerabilities
- Cloud security risks
- Vulnerability scanning
- Patch management
- System hardening
- Security awareness
- Defense in depth

## Threat vs Vulnerability

A **threat** is something that has the potential to cause harm.

A **vulnerability** is a weakness that could be exploited by a threat.

Example:

```text
Threat:
Attacker attempting unauthorized access

Vulnerability:
Unpatched software with a known security flaw

Possible Result:
System compromise
```

A vulnerability does not automatically mean an attack will occur, but it can increase risk when a relevant threat exists.

## Risk

Risk involves the possibility that a threat will exploit a vulnerability and create an unwanted impact.

A simplified way to think about risk is:

```text
Threat + Vulnerability + Impact = Security Risk
```

Risk management focuses on identifying these conditions and reducing their likelihood or impact.

## Attack Vector

An attack vector is the path or method used to reach a target.

Examples may include:

- Email
- Websites
- Remote access services
- Wireless networks
- Compromised credentials
- Removable media
- Cloud services
- Third-party software
- Social engineering

Organizations should consider multiple attack vectors when designing security controls.

## Attack Surface

The attack surface represents the possible points through which a system could be targeted.

Examples include:

- Open network ports
- Internet-facing applications
- User accounts
- Remote access services
- Wireless networks
- APIs
- Cloud resources
- End-user devices
- Unused services

Reducing the attack surface can reduce the number of opportunities available to an attacker.

## Attack Surface Reduction

Common strategies include:

- Disable unused services
- Close unnecessary ports
- Remove unused accounts
- Uninstall unnecessary software
- Restrict administrative access
- Patch systems
- Segment networks
- Use strong authentication
- Apply least privilege
- Limit internet-facing systems

## Vulnerability Management

Vulnerability management is an ongoing process used to identify, evaluate, prioritize, and remediate security weaknesses.

A simplified lifecycle includes:

1. Identify assets.
2. Scan or assess systems.
3. Identify vulnerabilities.
4. Evaluate severity and business impact.
5. Prioritize remediation.
6. Apply patches or other controls.
7. Verify remediation.
8. Continue monitoring.

Vulnerability management is continuous because systems, threats, and software change over time.

## CVE

CVE stands for **Common Vulnerabilities and Exposures**.

A CVE provides a standardized identifier for a publicly known vulnerability.

Example format:

`CVE-YYYY-NNNNN`

CVE identifiers help security teams, vendors, researchers, and administrators refer to the same vulnerability consistently.

## CVSS

CVSS stands for **Common Vulnerability Scoring System**.

CVSS provides a standardized method for describing the severity of vulnerabilities.

Scores generally range from:

`0.0 - 10.0`

A higher score generally represents a more severe vulnerability.

Organizations should not rely only on the numerical score. Business context, system importance, exposure, and available mitigations should also be considered.

## Zero-Day Vulnerability

A zero-day vulnerability is a vulnerability for which an effective vendor fix may not yet be available when exploitation becomes possible or known.

Possible temporary protections may include:

- Disabling an affected feature
- Restricting network access
- Increasing monitoring
- Applying vendor-recommended mitigations
- Segmenting affected systems

Once a security update becomes available, organizations can evaluate and deploy the fix according to their patch-management process.

## Misconfiguration

Security problems can occur even when software has no known vulnerability.

Examples of insecure configuration include:

- Default passwords
- Excessive permissions
- Unnecessary open ports
- Publicly exposed services
- Incorrect firewall rules
- Improper cloud permissions
- Weak wireless security
- Unnecessary administrator accounts

Secure configuration and regular reviews help reduce these risks.

## Unpatched Systems

Security updates often correct known vulnerabilities.

Systems that remain unpatched may continue to expose weaknesses that attackers already understand.

Patch management can include:

1. Identify available updates.
2. Review severity and compatibility.
3. Test updates when appropriate.
4. Schedule deployment.
5. Install the update.
6. Verify successful installation.
7. Document the change.

## Legacy Systems

Legacy systems may create security challenges because they can:

- Run unsupported operating systems
- Depend on outdated software
- Lack modern security controls
- Be difficult to patch
- Support older protocols

When replacement is not immediately possible, compensating controls may include:

- Network segmentation
- Strict firewall rules
- Restricted access
- Increased monitoring
- Application allowlisting

## Malware

Malware is software designed to perform unwanted or harmful actions.

Malware can affect:

- Confidentiality
- Integrity
- Availability
- System performance
- User accounts
- Data
- Network operations

Different forms of malware behave differently.

## Virus

A virus typically attaches itself to another file or program and may spread when that infected content is executed.

Security controls may include:

- Endpoint protection
- Software updates
- Application controls
- User awareness
- Email filtering

## Worm

A worm can spread between systems without requiring the same type of user interaction as a traditional file-infecting virus.

Network segmentation, patching, endpoint protection, and monitoring can help reduce the impact of worm activity.

## Trojan

A Trojan disguises malicious functionality as legitimate or desirable software.

Users may believe they are installing something safe when the application actually performs harmful actions.

Trusted software sources and user awareness help reduce this risk.

## Ransomware

Ransomware attempts to deny access to data or systems, often through encryption, and demands payment.

Possible defenses include:

- Offline or protected backups
- Patch management
- Endpoint security
- Email filtering
- MFA
- Least privilege
- Network segmentation
- Security awareness
- Tested recovery procedures

Backups are especially important because they can support recovery without relying on the attacker.

## Spyware

Spyware attempts to collect information from a system or user without appropriate authorization.

Possible targets may include:

- Browsing activity
- Credentials
- Personal information
- System information

Endpoint security, secure software practices, and user awareness can help reduce spyware risk.

## Rootkit

A rootkit attempts to hide malicious activity or maintain privileged access to a system.

Rootkits can be difficult to detect because they may interfere with normal system visibility.

Strong endpoint protections, integrity monitoring, secure boot technologies, and system reimaging may be relevant depending on the situation.

## Social Engineering

Social engineering targets people rather than relying only on technical vulnerabilities.

The attacker may attempt to manipulate someone into:

- Revealing credentials
- Opening malicious content
- Sending money
- Changing account information
- Providing sensitive data
- Granting access

Security awareness training is an important defense.

## Phishing

Phishing uses fraudulent communications to trick users into revealing information or taking an unsafe action.

Common warning signs include:

- Unexpected login requests
- Urgent language
- Suspicious links
- Unknown attachments
- Requests for sensitive information
- Sender addresses that do not match the expected organization

## Spear Phishing

Spear phishing is more targeted than general phishing.

The message may be customized for:

- A specific user
- Department
- Organization
- Job role

Targeted attacks may appear more convincing because they use information relevant to the recipient.

## Smishing and Vishing

**Smishing** uses text messages or messaging platforms.

**Vishing** uses voice calls.

Both attempt to manipulate users into revealing information or taking an unsafe action.

## Credential Attacks

User credentials are a common target because valid accounts can provide access without exploiting a software vulnerability.

Risks include:

- Weak passwords
- Password reuse
- Stolen credentials
- Credential stuffing
- Password spraying
- Social engineering

Defenses include:

- MFA
- Unique passwords
- Password managers
- Login monitoring
- Account lockout or rate-limiting controls
- Conditional access

## Password Spraying

Password spraying involves attempting a small number of commonly used passwords across multiple accounts.

This differs from repeatedly trying many passwords against one account.

Defensive controls can include:

- MFA
- Strong password policies
- Monitoring authentication failures
- Smart lockout controls

## Credential Stuffing

Credential stuffing uses username and password combinations obtained from previous data breaches against other services.

Password reuse makes this attack more effective.

Using unique passwords for each service greatly reduces the risk.

## Insider Threats

An insider threat involves someone with legitimate access who creates risk.

Insiders may be:

- Malicious
- Negligent
- Compromised

Possible controls include:

- Least privilege
- Logging
- Access reviews
- Data-loss prevention
- Separation of duties
- Security awareness
- Account lifecycle management

## Supply-Chain Threats

Organizations rely on software vendors, hardware manufacturers, cloud services, and other third parties.

A compromise involving a trusted supplier can affect downstream organizations.

Supply-chain risk management may include:

- Vendor assessments
- Software integrity validation
- Contractual security requirements
- Monitoring
- Access restrictions
- Patch management
- Third-party risk reviews

## Denial of Service

A Denial-of-Service attack attempts to make a service unavailable.

Targets may include:

- Websites
- Servers
- Applications
- Network connections

Possible defenses depend on the environment and may include:

- Traffic filtering
- Rate limiting
- Redundant systems
- Content delivery services
- DDoS protection services
- Monitoring and alerting

## Distributed Denial of Service

A Distributed Denial-of-Service, or DDoS, attack uses many systems to generate traffic toward a target.

Because traffic originates from many sources, DDoS attacks can be more difficult to filter than attacks coming from one source.

## On-Path Attack

An on-path attack occurs when an attacker positions themselves between communicating systems and attempts to observe or manipulate traffic.

Protections may include:

- TLS
- VPNs
- Secure wireless networks
- Certificate validation
- Secure authentication

Encryption helps protect the confidentiality and integrity of data in transit.

## ARP Spoofing

ARP spoofing targets the relationship between IPv4 addresses and MAC addresses on a local network.

An attacker may attempt to provide false ARP information so traffic is redirected through another system.

Potential protections include:

- Network segmentation
- Switch security features
- Monitoring
- Encryption
- Dynamic ARP Inspection where supported

## Rogue DHCP

A rogue DHCP server provides unauthorized network configuration information.

A rogue server could provide incorrect settings such as:

- Default gateway
- DNS server
- IP address configuration

Switch security features such as DHCP snooping can help reduce this risk in supported environments.

## DNS Poisoning

DNS poisoning attempts to cause incorrect DNS information to be accepted so users are directed to the wrong destination.

Possible defenses include:

- Secure DNS configuration
- DNSSEC where appropriate
- Trusted DNS servers
- Monitoring
- Patch management

## Rogue Access Point

A rogue access point is an unauthorized wireless access point operating within or connected to an organization's environment.

It can create an unmanaged path into the network.

Wireless monitoring and network access controls can help identify unauthorized access points.

## Evil Twin

An evil twin is a malicious wireless network designed to imitate a legitimate one.

Users may unknowingly connect to the malicious access point.

Strong enterprise authentication, certificate validation, and user awareness help reduce this risk.

## VLAN Hopping

VLAN hopping refers to attempts to cross VLAN boundaries improperly.

Security practices may include:

- Manually configuring access ports
- Restricting trunk ports
- Limiting allowed VLANs
- Proper native VLAN configuration
- Disabling unused switch ports

## Web Application Vulnerabilities

Web applications can contain security weaknesses involving:

- Input validation
- Authentication
- Session management
- Access control
- Data handling
- Software dependencies

Secure development practices, testing, patching, and web application security controls help reduce these risks.

## Injection

Injection vulnerabilities occur when untrusted input is interpreted as part of a command or query.

Defensive development techniques include:

- Input validation
- Parameterized queries
- Least-privileged service accounts
- Secure coding practices

## Cross-Site Scripting

Cross-Site Scripting, or XSS, involves unsafe content being returned to a user's browser.

Defenses can include:

- Output encoding
- Input validation
- Content Security Policy
- Secure development practices

## Broken Access Control

Broken access control occurs when users can access resources or perform actions beyond their intended permissions.

Possible protections include:

- Server-side authorization checks
- Least privilege
- Role-based access controls
- Access testing
- Secure session management

## Cloud Security Risks

Cloud environments introduce security responsibilities involving:

- Identity and access
- Resource permissions
- Public exposure
- Data protection
- Logging
- Network configuration
- Shared responsibility

Misconfigured cloud storage or excessive permissions can expose information even when the underlying cloud platform is secure.

## Mobile and IoT Risks

Mobile and IoT devices may introduce risks involving:

- Weak passwords
- Unpatched firmware
- Insecure wireless communication
- Unsupported software
- Default credentials
- Limited security controls

Network segmentation can help isolate devices with different security requirements.

## Vulnerability Scanning

Vulnerability scanning uses automated tools to identify known weaknesses or configuration problems.

A vulnerability scan may identify:

- Missing patches
- Known CVEs
- Open services
- Insecure configurations
- Unsupported software

Scanning identifies potential weaknesses but does not automatically prove that every finding can be exploited.

## Vulnerability Scan vs Penetration Test

A vulnerability scan primarily identifies potential weaknesses.

A penetration test goes further by attempting to validate selected weaknesses within an explicitly authorized scope.

Both must be performed only with proper authorization.

## False Positives

A vulnerability scanner may report an issue that does not actually exist or apply to the system.

This is called a false positive.

Security teams should verify findings rather than assuming every automated result is correct.

## False Negatives

A false negative occurs when a vulnerability exists but the assessment fails to identify it.

This is why organizations use multiple security controls rather than relying on one tool.

## Patch Management

Patch management reduces exposure to known vulnerabilities.

A structured process may include:

1. Inventory systems.
2. Identify available patches.
3. Determine severity and relevance.
4. Test when appropriate.
5. Schedule deployment.
6. Install updates.
7. Verify successful installation.
8. Document results.

## System Hardening

System hardening reduces unnecessary exposure.

Common hardening practices include:

- Disable unused services
- Remove unnecessary software
- Change default credentials
- Apply security updates
- Restrict administrative privileges
- Configure host firewalls
- Enable logging
- Use secure protocols
- Remove inactive accounts
- Apply security baselines

## Defense in Depth

Defense in depth uses multiple layers of security instead of relying on one control.

Example:

```text
User Awareness
      |
      v
Email Security
      |
      v
MFA
      |
      v
Endpoint Protection
      |
      v
Network Segmentation
      |
      v
Firewalls
      |
      v
Monitoring & Logging
      |
      v
Backups & Recovery
```

If one control fails, another layer may still reduce the impact.

## Example Scenario — Unpatched Server

**Problem:** A vulnerability scan identifies a critical vulnerability on an internet-facing server.

A structured response may include:

1. Confirm the affected software and version.
2. Review the vulnerability information.
3. Determine whether the system is exposed.
4. Evaluate business impact.
5. Review available vendor patches or mitigations.
6. Test the remediation when appropriate.
7. Apply the security update.
8. Verify that the vulnerability is resolved.
9. Increase monitoring if necessary.
10. Document the remediation.

## Example Scenario — Suspicious Email

**Problem:** A user receives an unexpected email requesting an immediate password reset through an external link.

Possible response:

1. Do not open the link.
2. Verify the sender.
3. Report the message through the organization's approved process.
4. Review the message for phishing indicators.
5. Remove similar messages if confirmed malicious.
6. Check whether any user interacted with the message.
7. Reset credentials if compromise is suspected.
8. Review authentication activity.
9. Document the incident.

## Example Scenario — Excessive Permissions

**Problem:** A standard user is discovered to have unnecessary administrator access.

Possible response:

1. Verify whether the access is required.
2. Review the user's job role.
3. Remove unnecessary administrative permissions.
4. Confirm required access still works.
5. Review for similar permission issues.
6. Document the change.

This supports least privilege.

## Vulnerability Prioritization

Not every vulnerability can be treated equally.

Prioritization may consider:

- Severity
- System exposure
- Asset importance
- Exploit availability
- Existing mitigations
- Business impact
- Regulatory requirements

A critical vulnerability on an internet-facing production system may require faster action than the same vulnerability on an isolated lab system.

## Threat Mitigation Process

When evaluating a threat or vulnerability, I use a structured approach:

1. Identify the affected asset.
2. Identify the threat or vulnerability.
3. Determine exposure.
4. Evaluate possible impact.
5. Review existing controls.
6. Prioritize based on risk.
7. Apply an appropriate mitigation.
8. Verify the mitigation.
9. Monitor for additional activity.
10. Document the findings.

## Key Takeaways

Some of the most important concepts I learned include:

- Threats represent potential sources of harm.
- Vulnerabilities are weaknesses that threats may exploit.
- Attack vectors describe how a target can be reached.
- Reducing the attack surface reduces unnecessary exposure.
- CVEs provide standardized vulnerability identifiers.
- CVSS helps communicate vulnerability severity.
- Patching and secure configuration reduce known weaknesses.
- Malware and social engineering target both technology and people.
- MFA and unique passwords reduce credential-related risk.
- Network segmentation helps limit unnecessary communication.
- Vulnerability scanning helps identify potential weaknesses.
- Vulnerability findings should be validated and prioritized based on risk.
- Defense in depth uses multiple security controls together.
- Security is an ongoing process rather than a one-time configuration.

Studying threats and vulnerabilities has helped me connect networking, system administration, identity, access control, patching, monitoring, and security operations into a broader cybersecurity risk-management process.
