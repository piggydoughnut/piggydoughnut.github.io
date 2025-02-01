# Domain enumeration

Kali has a lot of wordlists in `/usr/share/wordlists`

## fuff

Looks for all subdomains of the given domain. It tries all the words in a wordlist to match as subdomains.

`ffuf -w </path/to/wordlist> -u <domain> -H "Host: FUZZ.<domain>"`

ffuf -w /usr/share/wordlists/wfuzz/general/common.txt -u http://thetoppers.htb -H "Host: FUZZ.thetoppers.htb"

Wordlists:
[https://github.com/danielmiessler/SecLists](https://github.com/danielmiessler/SecLists)

## wfuzz

Exclude http responses

`wfuzz -c -w </usr/share/wordlist/path> -u http://FUZZ.example.com -H "Host: FUZZ.example.com" --hc 301,302,400,401,403,404,500`

Filter http responses

`wfuzz -c -w </usr/share/wordlist/path> -u http://FUZZ.example.com -H "Host: FUZZ.example.com" --sc 200`

`1wfuzz -c -w /usr/share/wordlists/amass/subdomains-top1mil-5000.txt -u http://thetoppers.htb -H "Host: FUZZ.thetoppers.htb"`

the domain must be accessible from the browser. if I know the IP and the domain, I can add it as a record to `/etc/hosts`

I do not want only 200 responses, but I want to see other responses, as everything apparently returns 200 not just success.

## gobuster

`gobuster vhost -w /usr/share/wordlists/amass/subdomains-top1mil-5000.txt -u http://thetoppers.htb`
