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

## Physical secucity

### Bollards/Barricades

- prevent access to certain areas of a physical area
- allow people, prevent vehicles
- high security area - brightly coloured
- another option is water, to make people go over a bridge

### Access control vestibule

- An access control vestibule, or mantrap, is part of a physical access control system that typically provides a space between two sets of interlocking doors.
- Mantraps are designed to prevent unauthorized individuals from following authorized individuals into facilities with controlled access. This activity, also known as piggybacking or tailgating, results in unauthorized access to the facility.

Types:

- all doors are normally unlocked, but opening one door causes other to lock
- all doors are locked, unlocking one door prevents others from being unlocked
- one door is open/ other locked, when one is open the other cannot be unlocked

### Fencing

- prevents acess to an area
- transparent or opaque
- robust structure, high fence, wire across the top

### Video surveillance

- CCTV - closed circuit television
- built in motion detection, object detection, read faces or licence tags
- multiple cameras networked together

### Security guard

- physical protection
- validating visitors
- two person integrity/control - no single person has access to a physical access
- access badge - person details, worn at all times, electronic locks

### Access badge

- access badge - personal details, worn at all times, electronic locks

### Lighting

- illuminate particular area
- non IR cameras can see better
- specialized designed lights to make sure there is not glare, facial recognition is possible

### Sensors

- Infrared - motion detectors, can see in both light and dark
- Pressure - detects a change in force, someone passing through a location
- Microwave - detect movement over large areas
- Ultrasonic - sends ultrasonice signals, receive reflected sound waves, detects motion, collision detection

## Deception and disruption technology

### Honeypot

- Attract attackers in the system and keep them involved in the system, so you can see what type of security techniques they are using against you, what type of automation is used.
- Honeypot is a virtual world, which attracks attackers or automated systems
- Attackers spend all of the time trying to identify and attack systems which are not part of your production systems

### Honeynet

- honeypots connected to a network
- workstations, servers, routers, firewalls
- build a larger deception network with one or more honeypots

### Honeyfile

- files that have fake information, that appear to be important or contain sensitive information
- attacker will spend a long time processing and studying the fake information

### Honeytoken

- track malicious actors
- bit of traceable data that is added to the honey net, if the data is stolen you will know where it came from

E.g.

- API credentials out on a public cloud share, notifications are sent when used
- A file with fake email addresses - constantly monitor to see who posts these addresses on the internet, then you can have an idea who is attacking you
- any type of data that you can falsify and put in an area for an attacker to find - database records, browser cookies, web page pixels

## Change management

How to make a change. Changes in corporations have to follow a formal process in order to make sure the change is performed properly as many people can be affected by it.

Types of changes: upgrade software, patch an application, change firewall configuration, modify switch ports

### Formal change control process

- might include frequency of change, duration, installation process, rollback procedure
- exist so we can avoid downtime, confusion, mistakes

Typical approval process

- complete the request forms
- detemine the purpose of the change
- identify the scope of the change
- schedule a date and time
- detemine affected systems and the impact
- analyze the risk associated with the change
- get approval from the change control board
- get end-user acceptance after the change is complete

### Ownership

- the owner of the application or data do not control the change control process, they just manage the process
- once the change is complete, the owner is responsible for testing the systems and verifying that everything is working properly

E.g. Address label printers need to be upgraded

- Shipping and receiving department owns the process
- IT handles the actual change

### Stakeholders

Individuals or departments that will be impacted by the proposed change

- identifying stakeholders is not as easy as it seems
- IT deparment needs to reasearch and identify who can be affected

E.g. Address label printers need to be upgraded

- shipping and receiving department
- accounting reports
- product delivery timeframes
- revenue recognition - CEO visibility

### Impact analysis

Every change has a different potential impact on the organization

- high, medium, low risks
- the risks can be minor or far-reaching, e.g. the fix breaks something else, data corruption

What is the risk of NOT making the change?

- security vulnerability
- application unvailability

### Test results

- Sandbox testing environment
- test contingency plans

### Backout plan

- a way to revert back to the original configuration
- some changes are difficult to revert
- full backup before making a change

### Maintenance window

- when is the change happening?
- during the workday is not a good time - high potential downtime for active users
- overnight are often a better choice
- time of the year has to be considered

### Standard operating procedure

- change control process has to be well documented and available to everyone in the organization through the intranet

## Technical change management

There is no such thing as a simple upgrade

### Allow lists/deny lists

- allow or prevent application from working in the environment
- vulnerabilities, trojan horses, malware
- Allow list - deny all, only allow specific
- Deny list - nothing bad on the list can be executed, everything else can run

### Restricted activities

- The scope of the change is important
- You cannot do any other changes, but you can do additional changes that will help reach primary goals, extend the scope if necessary, but it has to be related

### Downtime

- services will eventually be unavailable
- there might be some unavailability during a set window
- nights and non production hours are good for changes
- point users to a secondary system while working on the primary system
- everyone should be informed about changes, emails etc

### Service and Application restart

- its common to require a restart after a change - to implement a new configuration
- reboot service or the OS

### Legacy applications

Changes affecting legacy applications are tricky. They are usually not supported anymore. Can be introduced to the support cycle by documenting the application.

### Dependencies

- to complete A you must complete B
- modifying one component may require changing or restarting other components
- dependencies may occur accross systems - update firewalls before firewall management sw

### Documentation

- Documentation has to be updated after every change
- Updating diagrams, charts with network configuration
- Updating policies/procedures (for managing a brand new application in your network)

### Version control

- many popportunities to manage versions: router configurations, windows OS patches, application registry entities

## Public key infrastructure (PKI)

### Public key

### Private key

### Key escrow
