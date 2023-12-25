# Santa's PCAP Challenge

## Challenge Overview

Santa had forgotten the password to his SSH server, but he remembered that it consisted of three words separated by hyphens (-). A sample of network traffic (santasdns.pcapng) and a backup of the password hash were provided to assist in recovering the password.

## Tools and Techniques Used

- Tshark: For extracting DNS requests from the PCAP file.
- Bash Scripting: To generate a wordlist from the DNS requests.
- Hashcat: For performing a dictionary attack against the SHA-256 hash.

## Solution Steps

### DNS Requests Extraction

```bash
tshark -nr santasdns.pcapng -Y "dns.flags.response == 0" -T fields -e dns.qry.name | sort | uniq | cut -d "." -f 1 > list.txt
```

This command extracted unique DNS queries and saved them to `list.txt`.

### Wordlist Generation

A bash script was used to create all possible three-word combinations from `list.txt`, formatted as required by the challenge (words separated by hyphens).

The script generated a comprehensive wordlist passwords.txt.

```bash
#!/bin/bash

while read word1; do
    while read word2; do
        while read word3; do
            echo "$word1-$word2-$word3"
        done < list.txt
    done < list.txt
done < list.txt > passwords.txt
```

### Hash Cracking with Hashcat

The SHA-256 hash was cracked using Hashcat with the following command:

```bash
hashcat -m 1400 -a 0 Hash.txt passwords.txt
```

The password `Santa-Love-Rudolph` was successfully recovered.

### Logging in with ssh

```sh
sshpass -p Santa-Love-Rudolph ssh santa@167.172.109.120 -p 50005
```

We are presented with the flag: `CEMA{Santa_Claus_Is_Watching_You}`

## Conclusion

The password `Santa-Love-Rudolph` was recovered by analyzing network traffic, creatively generating a targeted wordlist, and efficiently cracking the hash. This solution demonstrated skills in network analysis, scripting for custom wordlist generation, and proficiency in using Hashcat for password recovery.
