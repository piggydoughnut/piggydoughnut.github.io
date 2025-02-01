**Name-Based Virtual hosting** is a method for hosting multiple domain names (with separate handling of
each name) on a single server. This allows one server to share its resources, such as memory and processor
cycles, without requiring all the services to be used by the same hostname.

The web server checks the domain name provided in the Host header field of the HTTP request and sends
a response according to that.
The /etc/hosts file is used to resolve a hostname into an IP address & thus we will need to add an entry in
the /etc/hosts file for this domain to enable the browser to resolve the address for unika.htb.

Adding an entry in the /etc/hosts file will enable the browser to resolve the hostname `unika.htb` to
the corresponding IP address & thus make the browser include the HTTP header Host: unika.htb in
every HTTP request that the browser sends to this IP address, which will make the server respond with the
webpage for unika.htb.

**LFI or Local File Inclusion** occurs when an attacker is able to get a website to include a file that was not
intended to be an option for this application. A common example is when an application uses the path to a
file as input. If the application treats this input as trusted, and the required sanitary checks are not
performed on this input, then the attacker can exploit it by using the ../ string in the inputted file name
and eventually view sensitive files in the local file system. In some limited cases, an LFI can lead to code
execution as well.

**RFI or Remote File Inclusion** is similar to LFI but in this case it is possible for an attacker to load a remote
file on the host using protocols like HTTP, FTP etc.

**include() method in PHP**
The include statement takes all the text/code/markup that exists in the specified file and loads it into the
memory, making it available for use.
For example:

[A more detailed explanation about the include() method of PHP can be found here](https://www.php.net/manual/en/function.include.php).

```
File 1 --> vars.php

<?php
$color = 'green';
$fruit = 'apple';
?>

#############################################
File 2 --> test.php

<?php
echo "A $color $fruit"; // output = "A"
include 'vars.php';
echo "A $color $fruit"; // output = "A green apple"
?>
```

[Windows New Technology LAN Manager (NTLM)](https://www.crowdstrike.com/cybersecurity-101/ntlm-windows-new-technology-lan-manager/) is a suite of security protocols offered by Microsoft to authenticate users’ identity and protect the integrity and confidentiality of their activity. At its core, NTLM is a single sign on (SSO) tool that relies on a challenge-response protocol to confirm the user without requiring them to submit a password.
