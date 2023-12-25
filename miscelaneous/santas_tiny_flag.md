# Santa's Tiny Flag

Description: The challenge involved finding a hidden flag in a Christmas edition of the CEMA logo. The flag was concealed within a broken JPEG file.

Steps to Solution

## File Download

- Downloaded the file from the provided link: Santa's Tiny Flag File.

## Analyzing the Broken JPEG

- Upon inspection, the JPEG file appeared to be corrupted or broken.

## Using Exiftool

- To extract any hidden data or metadata, the Exiftool was used. This tool is capable of reading, writing, and editing metainformation in a wide variety of files.

## Command Execution

- Ran the command exiftool find_Santa_flag.jpeg in the terminal to inspect the file's metadata.
- Searched specifically for hidden text using grep -i, focusing on any lines that could potentially contain the flag.

## Finding the Flag

- The Exiftool output revealed the following line under 'Text Layer Text':

```sh
exiftool find_Santa_flag.jpeg | grep -i {
```

```sh
Text Layer Text: YOU F0und{$Anta_Tr3e}, , , Merry Christmas, , Merry Christmas
```

Another interesting line under 'Layer Unicode Names' was:

```css
Layer Unicode Names: ... CEMA{NOTTHEFLAGYETSOLVETHEPUZZLEFIRST}, ...
```

The correct flag was identified as `YOU F0und{$Anta_Tr3e}`.
