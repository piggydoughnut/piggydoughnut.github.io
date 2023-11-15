# General Security Concepts

## [Security controls](https://youtu.be/STM3EUvL7wg?feature=shared)

Technical - operating system controls, firewalls, anti-virus, etc. Block access to a resource. You shall not pass. E.g. a firewall rule

Managerial - security policies for people, standard operating procedures

Operational controls - people instead of systems, security guards, guard schack, monthly lunch and learn, awareness program

Physical controls - limit physical access, fence, locks, badge readers, posters etc.

**Categories**

Preventive - prevents someone's access

Deterrent - discourage intrusion attempt, does not directly prevent access.

Detective - identify and log an intrusion attempt

Corrective - apply a control after an event has been detected, can reverse the impact of an event, can potentially continue operating with minimal downtime.

Compensating - control using other means, existing controls arent sufficient. This could be something temporary until you can put together a plan to resolve security incident. Precent the exploitation of weakness.

- Firewall blocks a specific application instead of patching the app
- Implement separation of duties
- Require simultaneous guard duties
- Generator used after power outage

Directive - directing someone to do something more secure than less secure

| -           | Preventive         | Deterrent      | Detective            | Corrective                    | Compensating                    | Directive                        |
| ----------- | ------------------ | -------------- | -------------------- | ----------------------------- | ------------------------------- | -------------------------------- |
| Technical   | Firewall           | Splash screen  | System logs          | Backup recovery               | Block instead of a patch        | File storage policies            |
| Managerial  | On-boarding policy | Demotion       | Review login reports | Policied for reporting issues | Separation of duties            | Compliance policies              |
| Operational | Guard shack        | Reception desk | Propety patrols      | Contact authorities           | Require multiple security staff | Secuiryt policy training         |
| Physical    | Door lock          | Warning signs  | Motion detectors     | Fire extinguisher             | Power generator                 | sign "Authorized Personnel Only" |

## [The CIA Triad](https://youtu.be/SBcDGb9l6yo?feature=shared)

**Confidentiality**

- Prevent disclosure of information to unauthorized inividuals or systems
- Encryption
- Access controls - selecitvely restrict access to a resource
- 2FA - additional confirmation before information is disclosed

**Integrity**

- Messages can't be modified without detection
- Hashing - map data of an arbitrary length to data of a fixed length
- Digital signatures - mathematical scheme to verify the integrity of data
- Certificates = combine with a digital signature to verify an individual
- Non-repudiation - provides proof of integrity, can be asserted to be genuine

**Availability**

- Sytems and networks must be up and running
- Redundancy - build services that will always be available
- Fault tolerance - system will continue to run, even when a failure occurs
- Patching - stability, close security holes

## [Non-repudiation](https://youtu.be/XxnCxPEllMg?feature=shared)

You can't deny what you ve said. There is not taking back. E.g. sign a contract

Cryptography - proof of integrity, proof of origin with high assurance of authenticity

### Proof of integrity

Verify that data doe snot change, the data remains accurate and consistent.

Hash - represents data as a short string of text, fingerprint of data.

### Proof of origin

Digital signature - public/private key cryptography.

1. Hash of the content is created
2. Hash is encrypted with Alice's Private Key
3. Hash is sent together with the content - Digital signature
4. Bob will receive a message.
5. Bob uses Alice's public key to decrypt the Hash (Digital signature) he received. He obtains the hash of the content in the process.
6. Bob checks if the received hash matches the hash of the content he received.

## AAA - Auhtorization Authentication Accounting

Authentication - who are you? Password and authentication factors.

Authorization - what access do you have? Decided based on your identification and authentication.

Accounting - login time, data sent and received, logout time

How can you verify if the computer on your network is authorized to be on your network? How can you truly authenticated a device?

- Digitally signed certificate on a device
- Other business processes rely on that certificate - e.g. Access to the VPN from authorized devices

Certificate Authority (CA)

- The organization creates a certificate for a device and digitally signs the cerificate with the organization's CA. The CA's digital signature is used to validate the certificate.

### Authorization models

- Define roles, organizations, attributes to decide who and when can access data
- Abstraction - clear relationship between the user and the resource

## Gap Analysis

- A study of where we are and where we would like to be
- Work towards a known baseline
  - NIST Special Publication 800-171 Revision 2
  - ISO/IEC 270001
- Baselines involve analysis of the people and processes used for security
- Examine the current IT systems
- Comparison of the existing systems of the current systems - find weakensess
- End result is a document (gap analysis report) with clear view of the current state and the security goals, recommendation for meeting the baseline

## [Zero Trust](https://www.youtube.com/watch?v=zC_Pndpg8-c)

- Many networks are relatively open on the inside, once you are through the firewall, there are a few security controls
- Everything is subject to a security check

### Planes of the operation

- Split netwrok into functional planes - applies to physical, virtual, and cloud components.

Data plane - processing frames, packets, network data
Control plane - manage the actions of the data plane, define policies and rules, determine how packets should be forwarded

Adaptive identity - examining identity of an individual applying security controls based on information that we are gathering about this authentication process. E.g. source of the requested resources - where is the IP address located. Limit entry points to access the network.

Policy drive access control - combine adaptive identity with a predefined set of rules.

### Security zones

Where are you coming from and where are you going. Internal, external network, VPN, Marketing, IT, Accounting, etc.

Implicitly trusted zomes - trusted to internal zone traffic

**Policy enforcement point** - subjects and systems communicating through this point are subject to evaluation by the policy enforcement point. Gatekeeper. All of the traffic passing through network passes through PEP. Allow, monitor and terminate connections. Gathers all of the information and provides it to Policy Decision Poiunt

**Policy Decision Point** - examines requests, compares to a predefined security policy, then makes a decision if it is allowed or denined.
