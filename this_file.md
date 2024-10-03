```import base64

# Input dari base64
encoded_data = "Eg8Idnc6KSY2IC8dHDMuNik0LzIqNSgzLjYpHDEtNDtiOQ=="
decoded_data = base64.b64decode(encoded_data)

# Key untuk XOR
key = b"key"  # Sesuaikan panjang kunci XOR dengan data

# Lakukan XOR
xor_result = bytes([a ^ b for a, b in zip(decoded_data, key * len(decoded_data))])

# Format hasil dengan smk22{}
result_string = f"smk22{{{xor_result.hex()}}}"
print(result_string)
