# Santa's Lost CEMA Picture (by BP) - CTF Writeup

## Challenge Description

In this challenge, we needed to recover Santa's critical Continuity of Essential Mental Activities (CEMA) picture, which was lost. The task involved navigating through challenges on a specific web server.

## Target URL

<http://167.172.109.120:50003>

## Methodology and Findings

1. Web Server Scanning

    We used feroxbuster to scan the web server:

    ```sh
    feroxbuster -u http://167.172.109.120:50003/ --auto-tune -o feroxbuster_output.txt
    ```

2. Initial Discoveries

    Feroxbuster revealed two interesting directories: `/admin` and `/uploads`. It also found a file `password.txt` under the `/admin` directory and `CEMA.jpeg` under `/uploads`.

3. Decoding the Password

    `/admin/password.txt` contained an encrypted message and a hash:

    ```text
    Khw zdfkwzrrug yrru FHPD lv;
    02e98800f21e0d79b83c2f481614bc96
    ```

    We used a Caesar cipher with ROT-23 to decrypt the message, which translated to:

    ```csharp
    Het wachtwoord voor CEMA is;
    ```

    This means "`The password for CEMA is;`" in Dutch.

    Using <https://crackstation.net/>, we cracked the MD5 hash `02e98800f21e0d79b83c2f481614bc96` to find the password:

    `Welcome01`

4. Recovering the CEMA Picture

    The file `CEMA.jpeg` in the `/uploads` directory contained a secret. Using steghide with the password `Welcome01`, we extracted the hidden content:

    ```sh
    steghide extract -sf CEMA.jpeg
    ```

    This revealed `flag.txt`, which contained the secret flag.

## Flag

The flag for the challenge: `CEMA{Th1s_1s_4_s3cr3t_fl4g}`
