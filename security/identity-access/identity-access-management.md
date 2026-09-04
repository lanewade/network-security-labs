# Identity & Access Management

This lab documents my study and practice with identity, authentication, authorization, account management, and access-control concepts from CompTIA Security+ coursework.

The goal is to demonstrate my understanding of how users and devices prove their identity, how permissions are assigned, and how organizations can control access to systems and resources.

## Concepts Practiced

- Identity and Access Management (IAM)
- Identification
- Authentication
- Authorization
- Accounting
- AAA
- Multi-Factor Authentication (MFA)
- Password authentication
- Biometrics
- Smart cards
- Certificates
- Single Sign-On (SSO)
- Federation
- Kerberos
- RADIUS
- TACACS+
- Role-Based Access Control (RBAC)
- Attribute-Based Access Control (ABAC)
- Least privilege
- Privileged accounts
- Account provisioning
- Account deprovisioning
- Password policies
- Conditional access
- Zero Trust concepts

## Identity and Access Management

Identity and Access Management, or IAM, is the process of managing digital identities and controlling access to systems, applications, and data.

IAM helps answer questions such as:

- Who is the user or device?
- How is the identity verified?
- What resources should they be allowed to access?
- What actions should they be allowed to perform?
- How should that access be monitored and removed when no longer needed?

## Identification

Identification occurs when a user claims an identity.

Examples include:

- Username
- Email address
- Employee ID
- Account name

Identification alone does not prove that the person is actually the owner of the account.

Authentication is required to verify the identity.

## Authentication

Authentication verifies that a user, device, or service is who it claims to be.

Common authentication methods include:

- Passwords
- PINs
- Smart cards
- Security keys
- Certificates
- Biometrics
- One-time passwords
- Authentication applications

## Authorization

Authorization determines what an authenticated identity is allowed to access or perform.

Examples include:

- Accessing a shared folder
- Installing software
- Modifying network settings
- Viewing sensitive files
- Creating user accounts
- Accessing administrative tools

A user may successfully authenticate but still be denied access to a resource because they are not authorized.

## Accounting

Accounting records activity associated with users or systems.

Examples include:

- Login events
- Logout events
- Resource access
- Administrative changes
- Authentication failures
- Network access activity

Accounting supports:

- Auditing
- Troubleshooting
- Security investigations
- Compliance
- Accountability

## AAA

AAA stands for:

1. **Authentication** — Who are you?
2. **Authorization** — What are you allowed to do?
3. **Accounting** — What did you do?

AAA is commonly used when controlling access to network devices, remote-access systems, and enterprise resources.

## Authentication Factors

Authentication factors are commonly divided into categories.

### Something You Know

Examples:

- Password
- PIN
- Passphrase

### Something You Have

Examples:

- Smartphone
- Hardware token
- Smart card
- Security key

### Something You Are

Examples:

- Fingerprint
- Face recognition
- Iris recognition

### Somewhere You Are

Authentication may consider location information such as:

- Geographic location
- Network location
- Trusted office environment

### Something You Do

Behavioral characteristics may include:

- Typing patterns
- Gesture patterns
- Other behavioral characteristics

## Multi-Factor Authentication

Multi-Factor Authentication, or MFA, requires authentication factors from more than one category.

Example:

```text
Password
   +
Authenticator App
```

The password is something the user knows.

The authenticator application is associated with something the user has.

Using two passwords would not normally qualify as MFA because both belong to the same factor category.

## Why MFA Matters

If an attacker obtains a user's password, MFA can provide an additional barrier to account compromise.

MFA is especially important for:

- Administrative accounts
- Remote access
- Email
- Cloud services
- Financial systems
- Sensitive applications

## Password Security

Strong password practices can include:

- Using long passwords or passphrases
- Avoiding password reuse
- Using unique credentials
- Using password managers
- Protecting password reset processes
- Enabling MFA
- Monitoring compromised credentials

Organizations may also enforce password policies according to their security requirements.

## Biometrics

Biometric authentication uses physical or behavioral characteristics.

Examples include:

- Fingerprint
- Facial recognition
- Iris scan
- Voice recognition

Biometrics can provide convenient authentication but should be implemented with appropriate privacy and security controls.

## Smart Cards

A smart card can store authentication information such as digital certificates.

The card is something the user has.

A smart card may also require a PIN, combining:

- Something the user has
- Something the user knows

This can provide multi-factor authentication.

## Digital Certificates

Certificates can be used to authenticate:

- Users
- Devices
- Servers
- Services

A certificate connects an identity with a public key and can be validated through a trusted certificate authority.

Certificates are commonly used in technologies such as:

- TLS
- VPNs
- Smart-card authentication
- Device authentication

## Single Sign-On

Single Sign-On, or SSO, allows a user to authenticate once and access multiple approved resources without repeatedly entering credentials.

Benefits can include:

- Improved user experience
- Fewer password prompts
- Centralized authentication
- Easier access management

SSO also makes protection of the primary account especially important because one identity may provide access to multiple services.

## Federation

Federation allows identity information to be trusted between separate systems or organizations.

Instead of creating a completely separate account for every service, a user may authenticate through a trusted identity provider.

Conceptually:

```text
User
  |
  v
Identity Provider
  |
  v
Trusted Application
```

The application trusts identity information provided by the identity provider.

## Claims

Federated identity systems may use claims.

A claim is information about an identity.

Examples might include:

- Username
- Email
- Group membership
- Role
- Department

Applications can use claims when making access decisions.

## Kerberos

Kerberos is a network authentication protocol commonly associated with Microsoft Active Directory environments.

Kerberos uses tickets rather than repeatedly sending a user's password across the network.

Important Kerberos concepts include:

- Key Distribution Center (KDC)
- Authentication Service (AS)
- Ticket Granting Service (TGS)
- Ticket Granting Ticket (TGT)
- Service tickets

## Simplified Kerberos Process

A simplified process looks like:

1. A user authenticates.
2. The Authentication Service verifies the user.
3. The user receives a Ticket Granting Ticket.
4. The user presents the TGT when requesting access to another service.
5. The Ticket Granting Service provides a service ticket.
6. The service ticket is presented to the destination service.

This allows the user to access approved services without repeatedly transmitting the original password.

## RADIUS

RADIUS can provide centralized AAA services.

It is commonly associated with:

- Remote-access authentication
- VPN access
- Wireless enterprise authentication
- Network access

RADIUS can authenticate users and help determine whether network access should be permitted.

## TACACS+

TACACS+ is commonly used for administrative access to network infrastructure.

Examples include managing access to:

- Routers
- Switches
- Firewalls

TACACS+ separates authentication, authorization, and accounting functions and provides detailed control over administrative activity.

## RADIUS vs TACACS+

A simplified comparison:

| Feature | RADIUS | TACACS+ |
|---|---|---|
| Common Use | Network access | Device administration |
| AAA | Combined more closely | Separates AAA functions |
| Transport | UDP | TCP |
| Typical Examples | VPN, Wi-Fi, remote access | Router and switch administration |

Both can provide centralized access control, but they are often used for different purposes.

## Role-Based Access Control

Role-Based Access Control, or RBAC, assigns permissions according to job roles.

Example:

```text
Help Desk
- Reset passwords
- Unlock accounts

Network Administrator
- Configure switches
- Configure routers

Security Administrator
- Review security events
- Manage security controls
```

Users receive access based on the responsibilities associated with their role.

## Attribute-Based Access Control

Attribute-Based Access Control, or ABAC, can make access decisions using attributes.

Examples may include:

- User role
- Department
- Device status
- Location
- Time
- Resource sensitivity

A policy might allow access only when multiple conditions are satisfied.

Example:

```text
User = Finance Department
Device = Company Managed
Location = Approved
Resource = Financial Application
```

## Least Privilege

Least privilege means users should receive only the permissions required to perform their responsibilities.

For example, a standard employee should not automatically receive administrator privileges.

Benefits include:

- Reduced attack surface
- Reduced accidental changes
- Better protection of sensitive systems
- Limited impact if an account is compromised

## Privileged Accounts

Privileged accounts have elevated permissions.

Examples include:

- Domain administrator
- Local administrator
- Network administrator
- Root account
- Security administrator

Privileged accounts require additional protection because compromise can provide broad access to systems.

Security practices may include:

- MFA
- Separate administrative accounts
- Strong monitoring
- Limited use
- Privileged access management
- Logging administrative activity

## Account Provisioning

Provisioning creates and configures access for a user.

A typical process might include:

1. Create the user account.
2. Assign required groups.
3. Assign appropriate permissions.
4. Configure MFA.
5. Provide access to approved applications.
6. Document the access granted.

Access should reflect the user's job requirements.

## Account Deprovisioning

Deprovisioning removes access when it is no longer required.

Examples include:

- Employee termination
- Role change
- Contractor departure
- Expired temporary access

A deprovisioning process may include:

1. Disable the account.
2. Revoke active sessions.
3. Remove group membership.
4. Revoke tokens or certificates.
5. Remove application access.
6. Recover organization-owned devices.
7. Document completion.

Prompt deprovisioning reduces the risk of unauthorized access through inactive accounts.

## Access Reviews

Organizations may periodically review account permissions.

Questions may include:

- Does the user still need this access?
- Is the account still active?
- Are administrator privileges still required?
- Does the user's access match their current role?

Regular reviews help prevent permission accumulation over time.

## Conditional Access

Conditional access uses additional context when deciding whether access should be allowed.

Conditions may include:

- User identity
- Device health
- Location
- Risk level
- Authentication strength
- Application sensitivity

Example:

```text
User signs in
      |
      v
Check identity
      |
      v
Check device
      |
      v
Check location/risk
      |
      v
Allow, deny, or require MFA
```

## Zero Trust and Identity

Identity is a major part of Zero Trust.

Instead of automatically trusting a user because they are on an internal network, access can be evaluated based on:

- Identity
- Authentication strength
- Device condition
- Resource sensitivity
- Current risk
- Least privilege

The goal is to continuously verify access rather than assuming internal users or devices are automatically trustworthy.

## Example Scenario — Remote VPN Access

A user needs remote access to the corporate network.

A secure access process might include:

1. The user enters their credentials.
2. MFA verifies a second factor.
3. RADIUS validates the network access request.
4. Security policies verify that the account is authorized.
5. The VPN connection is established.
6. Access is limited according to the user's role.
7. Authentication and session activity is logged.

This combines authentication, authorization, accounting, MFA, and network access control.

## Example Scenario — Employee Changes Roles

An employee moves from the Help Desk team to the Networking team.

The access-management process should include:

1. Review current permissions.
2. Remove access that is no longer needed.
3. Assign the appropriate networking role.
4. Grant only required network-management permissions.
5. Review privileged access.
6. Document the change.

This prevents the employee from accumulating unnecessary permissions from both roles.

## Example Scenario — Former Employee Account

An employee leaves the organization.

Security concerns include:

- Active credentials
- VPN access
- Cloud sessions
- Email access
- Administrative privileges
- Certificates or tokens

A proper deprovisioning process should quickly revoke access and disable the account.

## Example Scenario — Authentication vs Authorization

A user successfully logs into a server.

Authentication succeeded.

The user then tries to open an administrative configuration tool and receives an access-denied message.

Authentication:

**Successful**

Authorization:

**Denied**

The system knows who the user is but does not permit the requested administrative action.

## IAM Troubleshooting Process

When troubleshooting identity or access problems, I use a structured process:

1. Confirm the correct user account.
2. Determine whether authentication succeeds.
3. Identify any MFA problems.
4. Check account status.
5. Check for lockout or expiration.
6. Verify group membership.
7. Review assigned roles and permissions.
8. Determine whether access is being denied by policy.
9. Check device or network requirements.
10. Review authentication logs when available.
11. Test the expected access.
12. Document the findings.

## Security Considerations

Good identity and access practices include:

- Require MFA for sensitive access
- Follow least privilege
- Protect privileged accounts
- Use separate administrative accounts when appropriate
- Disable inactive accounts
- Remove access promptly when users leave
- Review permissions periodically
- Centralize identity management where appropriate
- Log authentication and administrative events
- Avoid shared administrator credentials
- Use strong authentication methods
- Apply access policies consistently

## Key Takeaways

Some of the most important concepts I learned include:

- Identification claims an identity.
- Authentication verifies an identity.
- Authorization determines permitted actions.
- Accounting records activity.
- MFA uses factors from multiple authentication categories.
- SSO allows one authentication process to provide access to multiple approved services.
- Federation allows separate systems to trust identity information.
- Kerberos uses tickets for authentication in many enterprise environments.
- RADIUS is commonly used for centralized network-access authentication.
- TACACS+ is commonly used for network-device administration.
- RBAC assigns permissions based on job roles.
- ABAC can make decisions using multiple attributes.
- Least privilege limits unnecessary access.
- Provisioning and deprovisioning are important parts of the account lifecycle.
- Zero Trust relies heavily on identity, verification, and least-privilege access.

Identity and access management helped me connect authentication technologies with broader cybersecurity concepts such as least privilege, account lifecycle management, secure remote access, and Zero Trust.
