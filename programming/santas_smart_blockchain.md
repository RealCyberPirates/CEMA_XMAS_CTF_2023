# Santas Smart Blockchain

## Part 1

### Challenge Overview

### Objective: Decode and reconstruct Santa's smart blockchain

### Detailed Solution Process

1. Packet Analysis: Began by examining a pcap file, specifically focusing on blockchain-related traffic.
2. Port Filtering: Noted that the relevant blockchain traffic was directed to port `12345`. This observation was key in isolating the specific data needed for the challenge.

    ```sh
    tcpdump -r Santas_traffic.pcapng -w smart_blockchain.pcapng 'port 12345'
    ```

3. Extracting Blockchain Data: In the Genesis Block of the blockchain data, found a Base64 encoded string `RkxBR3tUaDEyX1c0c18yXzM0c3l9`.

    **Block 2810**

    ```hex
    0000   44 61 74 61 3a 20 47 65 6e 65 73 69 73 20 42 6c   Data: Genesis Bl
    0010   6f 63 6b 3a 20 52 6b 78 42 52 33 74 55 61 44 45   ock: RkxBR3tUaDE
    0020   79 58 31 63 30 63 31 38 79 58 7a 4d 30 63 33 6c   yX1c0c18yXzM0c3l
    0030   39 0a 48 61 73 68 3a 20 39 38 30 64 35 66 38 32   9.Hash: 980d5f82
    0040   62 39 63 62 37 35 37 65 63 32 31 33 63 30 61 66   b9cb757ec213c0af
    0050   34 66 36 35 30 37 33 32 63 63 37 65 36 61 64 39   4f650732cc7e6ad9
    0060   33 31 62 36 36 61 36 61 30 63 65 63 31 31 62 32   31b66a6a0cec11b2
    0070   32 62 64 65 64 30 61 65 0a 2d 2d 2d 2d 2d 2d 2d   2bded0ae.-------
    0080   2d 2d 2d 2d 2d 2d 2d 2d 2d 2d 2d 2d 2d 0a         -------------.
    ```

4. Decoding Process: Utilized a Base64 decoder to translate the encoded string, revealing the flag.
5. Flag Discovery: Decoded string yielded `FLAG{Th12_W4s_2_34sy}`, marking the successful completion of the challenge.

### Conclusion

Successfully decoded the Base64 string from the Genesis Block after filtering the traffic by port 12345, demonstrating skills in network traffic analysis and data decoding.

## Part 2

**Objective**: Reassemble and reconstruct a file from disordered blockchain data extracted from a pcap file.

1. Initial Packet Analysis

    The challenge began with analyzing the pcap file `smart_blockchain.pcapng`. I used tools like Wireshark to inspect the structure and content of the packets. This step was crucial to understand how the blockchain data (specifically the Data and Hash values) were encapsulated within the packets.

2. Data Extraction with Scapy

    After understanding the packet structure, I utilized Python's `Scapy` library to process the pcap file. The `process_packets` function was implemented to extract the payload from each packet with a Raw layer, decode the payload, and parse out the Data and Hash values. These values were collected in a list for subsequent processing.

3. Sorting the Blockchain

    Given the blockchain data was out of order, the `sort_blockchain` function was created to sort the blocks based on a hash calculation method. Each block's hash was generated using its data concatenated with the hash of the previous block, with the Genesis block using "0" as its previous hash. This step reestablished the correct order of the blocks.

4. Reconstructing the File

    The next phase involved the reconstruct_file function, which reconstructed the file by concatenating the Data values of the sorted blocks (excluding the Genesis block) and converting this hexadecimal data into binary. The binary data was then written to the output file `reconstructed_image.jpeg`.

5. Script Execution and Debugging

    The final Python script was executed against the `smart_blockchain.pcapng` file. Several iterations were needed to adjust the data extraction and processing logic, as initial runs of the script resulted in errors or an empty output file. Debugging involved refining the packet processing and ensuring the correct extraction and conversion of the blockchain data.

```python
from scapy.all import * 
import hashlib
import binascii

def calculate_hash(data, previous_hash):
    """Calculate SHA256 hash of the given data and previous hash."""
    combined_data = (data + previous_hash).encode()
    return hashlib.sha256(combined_data).hexdigest()

def process_packets(filename):
    packets = rdpcap(filename)
    blocks = []

    for packet in packets:
        if packet.haslayer(Raw):  # Check if packet has Raw layer
            payload = packet[Raw].load
            try:
                payload_str = payload.decode('utf-8', errors='ignore')  # Decode the payload
                # Extract data and hash from payload_str
                if 'Data:' in payload_str and 'Hash:' in payload_str:
                    data_index = payload_str.find('Data:') + len('Data: ')
                    hash_index = payload_str.find('Hash:') + len('Hash: ')
                    data = payload_str[data_index:payload_str.find('\n', data_index)].strip()
                    hash_value = payload_str[hash_index:payload_str.find('\n', hash_index)].strip()
                    blocks.append({'data': data, 'hash': hash_value})
            except Exception as e:
                print(f"Error processing packet: {e}")

    return blocks


def sort_blockchain(blocks):
    """Sort the blockchain based on the hash mechanism."""
    sorted_chain = []
    last_hash = "0"  # Genesis block starts with no previous hash

    while blocks:
        for block in blocks:
            if 'Genesis Block' in block['data'] or calculate_hash(block['data'], last_hash) == block['hash']:
                sorted_chain.append(block)
                last_hash = block['hash']
                blocks.remove(block)
                break

    return sorted_chain


def reconstruct_file(sorted_data, output_filename):
    """Reconstruct the file from sorted blockchain data, excluding the Genesis block."""
    reconstructed_data = b""

    for block in sorted_data:
        if 'Genesis Block' not in block['data']:
            block_data_binary = binascii.unhexlify(block['data'])
            reconstructed_data += block_data_binary
            # print(f"Processed block with data: {block['data']}")  # Debugging

    if not reconstructed_data:
        print("No data to write to the file. Check block processing.")
    else:
        with open(output_filename, 'wb') as output_file:
            output_file.write(reconstructed_data)
        print(f"Data written to {output_filename}")

blockchain_data = process_packets('smart_blockchain.pcapng')
sorted_blockchain = sort_blockchain(blockchain_data)
reconstruct_file(sorted_blockchain, 'reconstructed_image.jpeg')
```

### Final Flag

`FLAG{N0t_S0_Sm4rt_Ch41n?}`
