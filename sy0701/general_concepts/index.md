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
