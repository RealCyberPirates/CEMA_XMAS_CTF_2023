# SantaVM Challenge Writeup

## Overview

The "SantaVM" challenge was a complex problem involving code reversal, data manipulation, and decoding techniques. The challenge presented a custom virtual machine environment, where participants were required to modify and upload a script to retrieve a hidden flag.
Challenge Description

- **URL**: <http://67.172.109.120:50004>
- **Task**: To retrieve a hidden flag by modifying and uploading a script in a custom VM environment.

## Steps Taken

1. Exploring the Webpage:
    - The webpage provided an option to upload and process a `.casm` file.
    - A sample file `sample_file.casm` was available for download.

2. Analyzing the Sample File:
    - The file contained several functions, with `main` being the primary function.
    - The `constants` and `operations` within the `main` function were examined.

3. Modifying the Sample File:
    - The goal was to adjust the `sample_file.casm` to manipulate the VM into revealing the flag.
    - The other functions (`c`, `d`, `fn_some_list`) seemed non-essential for flag extraction.

4. Uploading the Modified File:
    - The modified script was uploaded to the VM through the webpage.
    - The VM processed the script and returned an output in decimal format.

    ```sh
    [81, 48, 86, 78, 81, 88, 116, 87, 84, 84, 86, 102, 78, 72, 73, 122, 88, 50, 90, 49, 98, 108, 57, 48, 77, 70, 57, 119, 98, 68, 82, 53, 88, 51, 99, 120, 100, 71, 103, 104, 102, 81, 61, 61]
    ```

5. Decoding the Output:
    - The output was a sequence of decimal numbers.
    - These numbers were first converted to their ASCII equivalents, forming a Base64 encoded string.
    - The ASCII string was Base64 decoded to reveal the flag.

    ```bash
    echo "81 48 86 78 81 88 116 87 84 84 86 102 78 72 73 122 88 50 90 49 98 108 57 48 77 70 57 119 98 68 82 53 88 51 99 120 100 71 103 104 102 81 61 61" | awk '{for(i=1;i<=NF;i++) printf "%c", $i}' | base64 -d
    ```

## Final Flag

`CEMA{VM5_4r3_fun_t0_pl4y_w1th!}`

## Conclusion

This challenge required a blend of reverse engineering, scripting, and data decoding skills. Successfully modifying the .casm file and decoding the output demonstrated not only a technical proficiency but also a methodical approach to problem-solving.
