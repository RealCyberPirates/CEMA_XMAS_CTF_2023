# Santa's Christmas Card (by Hermann) - CTF Writeup

## Challenge Description

Santa sent a Christmas card to all his friends, but the message was cryptic. The challenge involved deciphering Santa's message hidden in a series of black and white Christmas trees.

## Challenge Solution

1. Initial Decoding

The PDF contained black and white Christmas trees, which we translated to '**B**' and '**W**'. The trees also included braces { } and dashes -.

The initial decoded string was:

```css
BWBW W BB WB { WWW WB BW B WB
WWWW BBB WBBW W WWW
BWBB BBB WWB
WBB WW WBWW WBWW
WB WBWW WBWW
WWWW WB WWWB W
WB
BB W WBW WBW BWBB
BWBW WWWW WBW WW WWW B BB WB WWW
WWWW BBB - WWWW BBB - WWWW BBB
```

2. Deciphering the Key

Given the CTF flag format `CEMA{}`, the following translations were made:

    "BWBW": "C"
    "W": "E"
    "BB": "M"
    "WB": "A"

The initial part of the message deciphered to `CEMA{`.

3. Further Analysis

We assumed the last part of the message might be `HO - HO - HO`. This led to the following partial decoding:

```css
CEMA{WWW A BW B A 
HO WBBW E WWW 
BWBB BBB WWB 
WBB WW WBWW WBWW 
A WBWW WBWW 
HO A WWWB E 
A 
M E WBW WBW BWBB 
CEMA HO WBW WW WWW B M A WWW 
HO - HO - HO}
```

4. Decoding Christmas Keywords

    - The second last part seemed to spell CHRISTMAS, leading to further decoding.
    - The first word after { was assumed to be SANTA.
    - The part before CHRISTMAS was assumed to be MERRY.

5. Final Decoding

With these assumptions, the final message was decoded as:

```css
CEMA{SANTA 
HOPES 
YOU 
WILL 
ALL 
HAVE 
A 
MERRY 
CHRISTMAS 
HO-HO-HO}
```

## Flag

The final flag for the challenge: `CEMA{SANTA_HOPES_YOU_WILL_ALL_HAVE_A_MERRY_CHRISTMAS_HO-HO-HO}`
