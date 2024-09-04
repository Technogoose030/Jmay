---
layout: default
---

# YOU HAVE REACHED THE END OF THE CTF YOU ARE AWESOME 
## Halo 3 Never Forget <a href="https://www.youtube.com/watch?v=JX5O3n9K_d0">Song</a>
### If you want the code for hiding your own text in files using stegonography then use this script with proper dependancies , This is a combined script so it encodes and decodes, never save your passwords in plaintext again instead encrypt it or better yet hide it in an image file 
<img src="docs/assets/42-1183456338.png" style="display: block; margin: auto;" />




```
from PIL import Image
from bitarray import bitarray

def text_to_bits(text):
    """Convert text to a bitarray."""
    bits = bitarray()
    bits.frombytes(text.encode('utf-8'))
    return bits

def bits_to_text(bits):
    """Convert bitarray to text, handling potential decoding issues."""
    try:
        return bits.tobytes().decode('utf-8')
    except UnicodeDecodeError as e:
        print(f"Error decoding bytes: {e}")
        return bits.tobytes()  # Return raw bytes if decoding fails

def encode_message(image_path, message, output_path):
    """Hide the message in the image and save it."""
    img = Image.open(image_path)
    pixels = img.load()

    # Convert message to bits
    message_bits = text_to_bits(message) + bitarray('00000000')  # Append a null byte as a delimiter

    # Check if the image is large enough
    width, height = img.size
    if len(message_bits) > width * height * 3:
        raise ValueError("Image is too small to hold the message.")

    # Embed message into image
    bit_index = 0
    for y in range(height):
        for x in range(width):
            if bit_index >= len(message_bits):
                img.save(output_path)
                return

            r, g, b = pixels[x, y]

            # Modify each color component to hide a bit of the message
            r = (r & ~1) | message_bits[bit_index]
            bit_index += 1
            if bit_index >= len(message_bits):
                pixels[x, y] = (r, g, b)
                img.save(output_path)
                return

            g = (g & ~1) | message_bits[bit_index]
            bit_index += 1
            if bit_index >= len(message_bits):
                pixels[x, y] = (r, g, b)
                img.save(output_path)
                return

            b = (b & ~1) | message_bits[bit_index]
            bit_index += 1
            pixels[x, y] = (r, g, b)

    img.save(output_path)

def decode_message(image_path):
    """Extract the hidden message from the image."""
    img = Image.open(image_path)
    pixels = img.load()
    
    bits = bitarray()
    width, height = img.size

    for y in range(height):
        for x in range(width):
            r, g, b = pixels[x, y]
            bits.append(r & 1)
            bits.append(g & 1)
            bits.append(b & 1)

            # Check for the null byte (end of message delimiter)
            if bits[-8:] == bitarray('00000000'):
                return bits_to_text(bits[:-8])

    # If we reach here, no null byte was found; return whatever we could extract
    raw_bytes = bits_to_text(bits)
    print("No delimiter found. Raw bytes extracted:")
    print(raw_bytes)
    return raw_bytes

# Example usage
if __name__ == "__main__":
    # Set your image paths and messages here
    input_image = "input_image.png"  # Replace with your input image file
    output_image = "output_image.png"  # Replace with your output image file
    secret_message = "Hello, this is a secret message congrats.. REACH the right sub domain now !"

    # Encode the message
    encode_message(input_image, secret_message, output_image)
    print(f"Message encoded into {output_image}")

    # Decode the message
    decoded_message = decode_message(output_image)
    print("Decoded message:", decoded_message)


```




[back](./)
