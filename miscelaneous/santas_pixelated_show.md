# Santa's Pixelated Show

Description: The challenge involved analyzing a WAV audio file named Flag.wav. The initial hypothesis was that the file contained hidden data or a message pertinent to the challenge, possibly using an audio steganography technique.

## Tools Used

- QSSTV: Software for decoding Slow Scan Television (SSTV) signals.
- Audacity: Audio editing software used for file conversion and analysis.

## Initial Examination

### File Analysis

Using file and exiftool, the Flag.wav file was identified as a RIFF (little-endian) data, WAVE audio, Microsoft PCM, 16 bit, mono `11025` Hz.

No immediately visible anomalies or hidden files were detected.

## Hypothesis Formation

Suspected that the file might contain a PAL test card encoded within its frequency spectrum, typically a technique known as `SSTV`.

## Adjusting Audio File

- Sample Rate Issue:

    The original sample rate of 11025 Hz was too low for effective SSTV decoding.

- Conversion:

    Used Audacity to export the file with a higher sample rate of `48000`, resulting in Flag2.wav.

## Decoding SSTV Signal

- QSSTV Configuration:

    Adjusted QSSTV settings under `Options -> Configuration -> Sound` to select the "`From File`" radio button.

- Decoding Process:

    On playing Flag2.wav in QSSTV, the software decoded the SSTV signal.
    The signal resolved into a PAL test card image.

![flag](flag.png)

## Result

- Flag Extraction:

    The decoded PAL test card image contained the flag `CEMA{0nly_F4ns}`.
