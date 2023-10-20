# Attacks

## Phishing

Social engineering with a touch of spoofing. The goal is to get sensitive information or get a person to install a mallware.
Often delivered via email trying to get the victim to click a link.
Some emails look super legit (good design, good grammar, relevant service), but there is always something a little odd.

- Always check Urls for typos and misspellings
- Don't click link but go to the page directly

**Pharming** - attack a whole group of people, attacker took over a website or a DNS server.

**Vishing** - voice phishing, caller ID spoofing, trying to get personal information to gain access to your account

**Spear phishing** - very targeted phishing attack, to make it very believable

**Whaling** - targeted phishing attack for a higher executive in the company (CFO, CEO)

**Smishing** - SMS phishing, contain links

Various scams - https://www.reddit.com/r/Scams/

Background information is easy to gather from public sites like: LinkedIn, Twitter, Facebook, Instagram, company websites, etc.

Scammer builds a profile of you and basically knows everything about you - where you work, bank, you recent purchases, family, friends, events you went to.

## Impersonating

There is an actor and a story. Someone is trying to pretend to be someone else (Microsoft representative, bank, etc.) to gain some information/action/response/personal data from you.

The attacker will use information about you during the conversation to make the attack more tailored for you sepcifically (your bank branch). In order to build trust they might use some information that you might know (your company info, local info, etc). They can pretend to be higher in rank than you or use loads of tech terms, etc.

The attacker extracts data without the victim noticing.

Personal details are very valuable. Identity fraud is a massice problem around the world (credit card, loan, lease, tax, government benefits fraud etc).

Never volunteer information over the phone! Verify who is calling.

## Dumpster Diving

Gathering of personal information from what was thrown out to use those in a different attack.

Legal? Legal in the US.

Lock and secure your garbage to prevent people from accessing it.

## Shoulder surfing

Looking over your shoulder when you are accessing important information on your computer.

Privacy filters, controlling your environment, turn monitor away from window or hallway,

## Hoaxes

A threat that doesnt actually exist. Situation might seem to be real but it is not.

Facebook post, email, tweet, etc.

Viruses or malware that look like you are affected with that type of mallware.

Update your Java/Flash player. A very well done sw update page.

## Watering Hole Attack

Attacker goes to the third party, e.g. third party site, local coffee or sandwich shop.

Attackers focus on infecting the third party site.

Defense in depth - layered defense.
Firewalls and IPS - stop the network traffic before things get bad

E.g. a mallware is installed on deviced of people who belong to a certain group.

## Spam

Unsolicited messages - commercial advertising, malicious phishing.

Issues with spam - security concernts, resource utilization, storage costs, managing it.

SPIM - Spam over instant messaging

Ways to stop spam:

- Have your spam filter - filtering in the cloud or on site in a screened subnet. Mail coming from the internet is filtered in Mail Gateway and spam is thrown out before its transferred to an internal mail server.

Characteristics for filtration:

- Allowed list only (only trusted senders)
- Block anything that doesnt follow RFC standards
- Reverse DNS - block email where the senders domain doesnt math the IP address of the domain.
- Tarpitting - intentionally slowing down the mail server - sending and receiving is slow
- Recipient filtering - block all mail not addressed to a valid recipient email address

## Influence campaign

The goal is to sway public opinion on political and social issues. This is enabled through social media - creating, sharing, liking, etc.

Bad actor creates bad accounts -> create content -> post it on many different platforms -> their messages gets amplified and more people read the content -> real people start sharing it to other people -> mass media picks up the story as it gets popular.

Reasons for these campaigns can even be military aka cyberwarfare. E.g. influencing elections, "fake news".

## Social engineering attacks

Social engineering uses a lot of open source intelligence, using social media and overall information on the internet. E.g. email a funeral notification of a friend or associates.

Main principles:

- Authority - message comes from CEO or help desk
- Intimidation - bad things will happen if you dont react, give them information, perform an action. "If you dont help me than the payroll checks wont be processed"
- Consensus/ Social proof - convince based on whats expected or known, using personal information or mentioning people you know.
- Scarcity - must make the change before time expires, something will go away in a time frame
- Urgency - act quickly, don't think
- Familiarity/Liking - mention someone you know, common friends.
- Trust - the attacker prentends to be someone who is safe, e.g. from IT deparment etc.

### Tailgating

Use an authorized person to gain unauthorized access to a building. Important to prevent as its last line of defence - entrance door.

- People blend in using clothing
- other legitimate 3d party reasons to enter the building
- sit in a smoking section and then follow employees inside the building
- carry food like doughnuts and have their hands full

### Invoice scam

Attacker sends a fake ivoice to the person who takes care of invoicing in the organization. (Attack starts with spear phishing). E.g. invoice for toner cartridges, domain renewal. Invoice if from a spoofed version of the CEO etc.

### Credential Harvesting

Attacker tries to get access to usernames and passwords stored locally on your computer in your browser (Chrome, Firefox, Outlook etc). To extract credentials a script needs to run on your machine.
To prevent - antivirus, antimalware to scan for these types of attacks.
