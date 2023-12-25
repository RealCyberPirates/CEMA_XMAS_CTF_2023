# QR Application Challenge

## Introduction

In the "QR Application Challenge," the objective was to uncover Santa's secret passphrase encrypted within a series of QR codes. These codes, at first glance, appeared to be mere holiday decorations, but held within them the key to accessing Santa's list.
Steps to Solve the Challenge
Discovering the QR Codes

### Connecting to the Server

- We initiated the challenge by connecting to the provided server at `167.172.109.120:50001` using curl.
- The server response revealed a webpage containing a collection of QR codes, dynamically displayed through JavaScript.

### Downloading and Decoding the QR Codes

Scripting the Download

- A Python script was written to automate the downloading of each QR code image from the server.
- This script used the requests library to fetch the images and stored them locally for decoding.

### Decoding Process

- We employed the pyzbar library to decode the QR codes, which was integrated into our Python script.
- Each QR code was scanned to extract the embedded text.

### Identifying the Flag

Flag Extraction

- The script was designed to search for a specific pattern in the decoded text, matching the format `CEMA{...}`.
- Upon finding a QR code with the matching pattern, the script successfully identified the flag: `CEMA{SAME_SAME_BUT_DIFFERENT}`.

```py
import requests
from PIL import Image
from io import BytesIO
from pyzbar.pyzbar import decode

def download_image(url):
    response = requests.get(url)
    if response.status_code == 200:
        return Image.open(BytesIO(response.content))
    return None

def decode_qr(image):
    decoded_data = decode(image)
    return [data.data.decode('utf-8') for data in decoded_data]

def main():
    base_url = "http://167.172.109.120:50001/static/images/"
    flag_prefix = "CEMA{"  # Adjust this based on expected flag format

    for i in range(1338):  # Adjust the range based on the number of QR codes
        url = f"{base_url}qr_code_{i}.png"
        print(f"Checking {url}...")

        image = download_image(url)
        if image:
            decoded_texts = decode_qr(image)
            for text in decoded_texts:
                if text.startswith(flag_prefix):
                    print(f"Flag found: {text}")
                    return
        else:
            print(f"Failed to download or decode: {url}")

if __name__ == "__main__":
    main()
```

## Conclusion

The challenge was an intriguing blend of network interaction, automated scripting, and QR code decryption. The Python script played a crucial role in efficiently processing a large number of QR codes and extracting the hidden passphrase. This challenge underscored the importance of automation in handling repetitive tasks in CTF competitions.