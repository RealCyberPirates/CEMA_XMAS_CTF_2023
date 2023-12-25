# Santa's Signal Regiment History Lesson

Description: The challenge presented an encrypted message related to the history of Christmas lore and significant dates. Participants were provided with two files: decipher.py, a Python script for decryption, and `encrypted.txt`, containing the encrypted data.
Tools Used

- Python: For running the decryption script.
- Historical Research: To identify the significant date for the decryption key.

## Understanding the Script

- Analyzed the `decipher.py` script, which uses a date-based shift cipher for decryption.

## Identifying the Key Date

- Initially suspected a significant date related to Christmas history.
- Discovered that `February 18, 2024`, marked the 150th anniversary of the "verbindingsdienst" (communications service).
- Updated the script with the correct date (`1874-02-18`) as the key for decryption.

## Decoding the Encrypted Text

- Modified the Python script to read the `encrypted.txt` file in binary mode due to encoding issues.
- Successfully decrypted the text, revealing a detailed historical account of the "verbindingsdienst".

## Result and Flag

`CEMA{wat_is_de_oprichtingsdatum_van_de_verbindingsdienst_?}`
