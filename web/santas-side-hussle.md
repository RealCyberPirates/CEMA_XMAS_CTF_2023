# Santa's Side Hussle

## Description

The challenge required participants to decrypt encrypted credentials found in the source code of a hastily set-up web server by Santa. The encrypted string provided was `cnaKLUNeCeyoGwN8GKOkgQ==`. The hint suggested the encryption was not Base64 but could be decrypted using an online decryptor, implying a combination of encryption and hashing without a secret.

## Tools Used

- Online Decryptor: encode-decode.com for trying various encryption methods.
- Feroxbuster: For initial reconnaissance of the web server.

## Initial Reconnaissance

- Feroxbuster: Used for initial scanning of the web server at <http://167.172.109.120:80>.
- Discovery: Found a Basic Auth protected page at `/files`.

## Decrypting the First String

- Initial String: `cnaKLUNeCeyoGwN8GKOkgQ==`
- Method: Applied various encryption methods using an online decryptor.
- Discovery: Identified that the string was encrypted with `aes-256-CBC`.
- Result: Decryption revealed the credentials `user:PwndMe`.

## Accessing the Web Server

- URL: Accessed <http://167.172.109.120/files> using the decrypted credentials.
- Finding: Located a file named flag.

## Decrypting the Second String

- Encrypted String in Flag File: `6sOm79+TCrRH6wPMAPQ7baxz2J3XK43xTxvIao5IDWqG2Q==`
- Method: Continued using the online decryptor, trying different encryption methods.
- Discovery: The string was encrypted with `aes-256-cfb1`.
- Flag: `{CEMA}You_Have_Defeated_Encryption`
