# Santas Digital Sleigh Ride

In the "Santa's Digital Sleigh Ride" CTF challenge, participants were tasked with reconstructing files from partial downloads and deciphering codes hidden within them. The challenge required skills in digital forensics, file manipulation, and pattern recognition.

## Process and Discovery

### Step 1: Torrent File Reconstruction

Context: Participants were provided with multiple .bin files, seemingly parts of a torrent download.

Action: By examining the `failed.torrent` metadata, it was determined that these .bin files were parts of two larger files: `file1.h3m` and `artraits.txt`.

Method: The first four .bin files (torrent1.bin through torrent4.bin) were concatenated using the command:

```sh
cat torrent1.bin torrent2.bin torrent3.bin torrent4.bin > file1.h3m
```

to reconstruct `file1.h3m`. Similarly, the last four .bin files (torrent5.bin through torrent8.bin) were merged to form artraits.txt using:

```sh
cat torrent5.bin torrent6.bin torrent7.bin torrent8.bin > artraits.txt
```

### Step 2: Extracting Information from file1.h3m

Action: After reconstruction, file1.h3m was found to be a GZIP compressed file, which when examined with tools like strings, revealed multiple flags.

Commands Used:

```sh
file file1.h3m #to identify the file type.
```

```sh
strings file1.h3m #to extract readable strings from the file.
```

Flags Discovered:

- FLAG(Narsil_Reborn)
- FLAG(dwarven_forge_armor)
- FLAG{TheGames_Has_just_started_GOODLUCK}
- FLAG(Heroes_Of_Cyber_and_CEMA_)
- FLAG{Heroes_Might_and_Magic_3}

### Step 3: Deciphering artraits.txt

- Context: The `artraits.txt` file contained a series of emojis.
- Action: A substitution cipher was suspected due to the structured format of the emojis. Through analysis, each emoji was mapped to specific character, resulting in additional flags.

`🌟🌈🎉🌺🌼🎈🎨🌲🌙🍀🌸🎸🎤🎶🌕🎁🎭🚀🌞🌷💫🔮🌌❌✨💤1️⃣2️⃣3️⃣4️⃣5️⃣6️⃣7️⃣8️⃣9️⃣🔟🔵🔴🔄💠❗❤️🔥💰🌐🔼➡️✳️`

Translates to:

`ABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890(){}!@#$%^&*`

The following flags cen be retrieved from the file.

- `FLAG(+nolife)`
- `FLAG(pouch_of_hewhomustnotbenamed)`
- `FLAG(crown_of_the_white_city)`

## Flags

```text
Flag 1: FLAG(Narsil_Reborn)
Flag 2: FLAG(dwarven_forge_armor)
Flag 3: FLAG{TheGames_Has_just_started_GOODLUCK}
Flag 4: FLAG{}
Flag 5: FLAG(+nolife)
Flag 6: FLAG(pouch_of_hewhomustnotbenamed)
Flag 7: FLAG(crown_of_the_white_city)
Flag 8: FLAG(Heroes_Of_Cyber_and_CEMA_)
Flag 9: FLAG{Heroes_Might_and_Magic_3}
```
