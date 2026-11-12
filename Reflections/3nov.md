# Lecture Reflection – Image Representation and Pixel Storage

## 1. Pixel Representation
- A pixel is the smallest unit of a digital image.
- Each pixel is represented using colour values.
- RGB stands for Red, Green and Blue.
- Each RGB channel typically uses 8 bits (1 byte).
- Each channel has values ranging from 0 to 255.

## 2. RGB vs RGBA
- RGB uses 3 bytes (24 bits) per pixel.
- RGBA uses 4 bytes (32 bits) per pixel.
- A stands for Alpha, which represents transparency/opacity.
- Alpha values:
    - 0 = Completely transparent
    - 128 = Approximately 50% opacity
    - 255 = Completely opaque

## 3. Image Storage in Memory
- An image of size m × n contains m × n pixels.
- Each pixel stores its RGB or RGBA values.
- Image data can be stored as a continuous 1D array of bytes.
- For row-major RGB storage, the starting byte index of pixel (i, j) is:

  `Index = (i × n + j) × 3`

- RGB image storage = m × n × 3 bytes.
- RGBA image storage = m × n × 4 bytes.

## 4. Byte Ordering
- Byte ordering determines the order in which bytes are arranged in memory.
- Common colour channel arrangements include:
    - RGBA: Red, Green, Blue, Alpha
    - BGRA: Blue, Green, Red, Alpha
    - ARGB: Alpha, Red, Green, Blue

## 5. Endianness
Endianness determines the order in which bytes of a multi-byte value are stored in memory.

- **Little-endian:** Least Significant Byte (LSB) is stored first.
- **Big-endian:** Most Significant Byte (MSB) is stored first.

Example: `0x12345678`

- Little-endian: `78 56 34 12`
- Big-endian: `12 34 56 78`

## Key Takeaway
Understanding pixel representation, memory storage, byte ordering and endianness is important when working with digital images and image-processing libraries such as ImageJ.


## 6. Network Byte Order and Image Representation
- Network protocols commonly use Big-endian (MSB first), known as Network Byte Order.
- Image data also requires a defined byte/channel arrangement.
- Image channel ordering can be RGBA, BGRA or ARGB.
- Endianness and channel ordering are different concepts, but both determine how data is interpreted.
- Incorrect interpretation can lead to incorrect values or colours.