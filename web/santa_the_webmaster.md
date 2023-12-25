# Santa The Webmaster - CTF Challenge Writeup

## Challenge Overview

The challenge involved discovering a hidden gift on Santa's festive website.

## Approach and Solution

### DNS Reconnaissance

The initial step involved conducting DNS reconnaissance on the domain xmas.cema.company. This was achieved using a DNS enumeration tool (possibly dnsrecon), which was used to extract various DNS records associated with the domain.

```sh
┌──(kali㉿kali)-[~/…/cema/xmas-2023/web/santa_the_webmaster]
└─$ dnsrecon -d xmas.cema.company      
[*] std: Performing General Enumeration against: xmas.cema.company...
[-] DNSSEC is not configured for xmas.cema.company
[*]      A xmas.cema.company 146.190.242.34
[*]      TXT xmas.cema.company Q0VNQXtIMWRkM25fMW5fUGw0MW5fUzFnaHR9
[*] Enumerating SRV Records
[-] No SRV Records Found for xmas.cema.company
```

### Decoding the Hidden Message

The key to solving the challenge was in the 'TXT' record. The encoded string was recognized as a Base64 encoded message. Using the Base64 decoding command:

```bash
echo -n "Q0VNQXtIMWRkM25fMW5fUGw0MW5fUzFnaHR9" | base64 -d

CEMA{H1dd3n_1n_Pl41n_S1ght}
```
