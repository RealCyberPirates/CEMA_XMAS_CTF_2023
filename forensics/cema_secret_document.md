# CEMA Secret Document Challenge Write-up

## Challenge Overview

In the "CEMA Secret Document" challenge, participants were tasked with uncovering a hidden flag within a seemingly normal Word document named "CEMA_SECRET_DOCUMENT.docx". The challenge was crafted to test the participants' ability to scrutinize embedded objects within the document.
Challenge Description

Emily, a young and curious girl, embarks on an adventure to unravel the mystery of Santa's secret hidden deep within CEMA documents. The key to solving this challenge lies in the exploration of embedded objects within the document's header and footer, specifically the CEMA logos.

## Solution

Upon downloading and opening the "CEMA_SECRET_DOCUMENT.docx", the document appeared to contain standard text. However, the intriguing part of the document was the CEMA logos embedded in the header and footer.
Steps to Uncover the Flag:

- Inspecting the Document: Initially, the document appeared to be a typical Word file with text and CEMA logos in the header and footer.
- Exploring Embedded Objects: The CEMA logos were not mere images; they were embedded documents.
- Accessing the Embedded Documents: Double-clicking on the right image in the footer of the document opened another document.
- Revealing the Flag: This action revealed the hidden flag: `CEMA{!!!_SUPER_SECRET_FLAG_HERE_!!!}`.
