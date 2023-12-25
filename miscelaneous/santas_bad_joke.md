# Santas Bad Joke

## Introduction

In a recent Capture The Flag (CTF) challenge, I was presented with a seemingly incomplete PNG image. The bottom half of the image was grayed out, indicating potential corruption or intentional manipulation of the image file.
Objective

The goal was to analyze and modify the PNG file to reveal the hidden content, presumably containing a flag for the challenge.
Tools Used

- Bless Hex Editor: A hex editor for Linux, used for viewing and editing the hex representation of the file.

## Analysis and Approach

### Initial Inspection

Upon opening the PNG file, only the upper half of the image was visible, with the lower half appearing completely gray.

### Hex Data Examination

- Using Bless Hex Editor, I inspected the hex data of the PNG file.
- I noticed a premature IEND chunk in the file, indicated by the hex sequence `49 45 4E 44` (the ASCII representation of 'IEND'), followed by its CRC `AE 42 60 82`.
- The IEND chunk signifies the end of a PNG file, so its premature presence suggested it was truncating the image.

### Editing the File:

- To reveal the full image, I removed the premature IEND chunk along with its CRC from the file.
- Carefully, I deleted the bytes `49 45 4E 44 AE 42 60 82` using Bless Hex Editor.

### Revealing the Flag:

- After saving the modified file, I reopened it in an image viewer.
- The full image was now visible, revealing the flag.

- The flag, hidden in the previously obscured part of the image, read: `CEMA{4Cr0p4lyps3}`.

## Conclusion

This challenge demonstrated the importance of understanding file structures and the usefulness of hex editing in digital forensics. By identifying and removing the errant IEND chunk, I was able to restore the image and extract the flag.