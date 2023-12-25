# Once Upon a Time

## Challenge Overview

In the "Once Upon a Time" challenge, participants were presented with a story set in Utrecht, Netherlands, during the Christmas season. The task was to find a hidden object's name within the story and provide its MD5 hash as the flag.

## Tools and Techniques Used

- Bash scripting: For generating MD5 hashes.
- what3words: A geocoding service used to interpret the clues from the story.

## Solution Steps

### Identifying Key Clues

- The story contained a few words in quotation marks: "zondags", "hitlijst", and "boteren".
- These words hinted at the use of the `what3words` service, which maps every 3-meter square in the world to a unique 3-word address.

### Using what3words

- The three words were used as a what3words address: <https://what3words.com/zondags.hitlijst.boteren>.
- This address pointed to `Legerplaats Stroe`, also known as `Generaal-Majoor Kootkazerne`, an army base and home of CEMA.

### Generating the MD5 Hash

The final step involved calculating the MD5 hash of "Generaal-majoor Kootkazerne" using a Bash command:

```bash
echo -n "Generaal-majoor Kootkazerne" | md5sum | awk '{print "CEMA{"$1"}"}'
```

### Submitting the Flag

The MD5 hash was submitted as the flag in the format required by the challenge:

`CEMA{ac2b2f7cd62a59579d85c4f9fa5e0274}`

## Conclusion

This challenge required a blend of creative thinking and technical skills. By interpreting the story clues and utilizing the what3words service, the correct location was identified. The Bash command was then used to generate the required MD5 hash, successfully solving the challenge.
