# Where Is Santa? - CTF Challenge Writeup

## Challenge Overview

The challenge required participants to decipher the last known location of Santa Claus, with the answer to be formatted as `CEMA{State_of_a_Country}`.
Approach and Solution

## Decoding the Text File ("to the world.txt")

### Initial Discovery

The challenge began with a file named "to the world.txt" that contained a series of unprintable characters. These characters were not immediately visible or interpretable in a standard text editor.
Use of xxd for Hexadecimal Analysis

To investigate these unprintable characters, the xxd command-line tool was employed. xxd creates a hex dump of a given file, which is a representation of the file in hexadecimal format. This method is particularly useful for uncovering hidden data within files that may not be visible in conventional file viewers.
Extracting the Binary Pattern

Upon analyzing the hex dump provided by xxd, a repeating pattern was observed in the hexadecimal representation of the file's content. This pattern was as follows:

```php
cefbbbfe2808
befbbbfe2808
befbbbfe2808
cefbbbfe2808
befbbbfe2808
cefbbbfe2808
cefbbbfe2808
cefbbbfe2808
defbbbfe2808
<SNIP>
```

### Translating Hex to Binary

This hexadecimal pattern was then translated into binary. The crucial part of this step was the interpretation of the hex values into binary digits. The pattern within the hex string was decoded based on specific criteria:

Strings starting with `be` and `ce` were translated to binary digits 0 and 1, respectively.
The string starting with `de` was interpreted as a newline indicator.

### Decoding to a URL

After translating the hex string to binary and converting the binary values to ASCII characters, it resulted in a readable URL. The binary sequence formed the following URL:

<https://pastebin.com/UwwUB4NM>

This URL was the next crucial clue in the challenge, leading to the "To the Elves.txt" file on Pastebin.

## Exploring Pastebin Links

The Pastebin link revealed a file titled "To the Elves.txt," ending with "Reindeer Beard You Xmas Beers Quality for Santa." Using the first letters of each word (excluding 'for' as it's in lowercase), a new Pastebin URL was constructed: <https://pastebin.com/RBYXBQfS>.

This URL contained a text file titled "To Mrs Claus.txt," which suggested using the temporary email service at <https://tempr.email> with the username "mrsclaus."

## Accessing the Tempr Email Service

Upon accessing the temporary email service and logging in as "mrsclaus," the inbox revealed encrypted Tutanota emails. The password "Rudolph," derived from "To Mrs Claus.txt," was used to decrypt the emails.

## Deciphering Email Communications

The decrypted emails between Santa and Mrs. Claus hinted at Santa's plan to go off the radar. The key clue was "I'll wait for you at the reindeer recharging station," suggesting a reference to what3words.

## What3Words Geolocation

Using what3words with the clue "reindeer.recharging.station" led to a specific location in India. Upon further investigation, it was determined that this location is in the state of Madhya Pradesh.

## Solution

The flag for the challenge, based on Santa's last known location, was determined to be:

`CEMA{Madhya_Pradesh}`
