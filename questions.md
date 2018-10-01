Sun-Jung Yum
04 October 2018
Problem Set 3

# Questions

## What's `stdint.h`?

'stdint.h' is a header file that is used in 'bmp.h' which declares new types of integers with specified widths. In other words, it allows a programmer to declare integer types with certain numbers of bits allocated as memory for the storage of values. It defines the limits of these integer types.

## What's the point of using `uint8_t`, `uint32_t`, `int32_t`, and `uint16_t` in a program?

By using 'uint8_t', 'uint32_t', 'int32_t', and 'uint16_t', a certain number of bits are already set aside for memory when declaring the variables. A 'uint8_t' will only use 8 bits, which ranges from 0 to 255 in decimal. If the value assigned to the variable is 200, it is more beneficial to use a 'uint8_t' or a 'int8_t' as opposed to a 'uint32_t' or a 'int32_t', which ranges from 0 to 4294967295 in decimal. These width-specified integer types allows one to allocate only the amount of memory needed for each variable, which will ultimately use up RAM space more wisely and sparingly.

## How many bytes is a `BYTE`, a `DWORD`, a `LONG`, and a `WORD`, respectively?

A 'BYTE' is made up of 8 bits, which is equivalent to 1 byte. A 'DWORD' and a 'LONG' are made up of 32 bits each, or 4 bytes. A 'WORD' is made up of 16 bits, which is 2 bytes.

## What (in ASCII, decimal, or hexadecimal) must the first two bytes of any BMP file be? Leading bytes used to identify file formats (with high probability) are generally called "magic numbers."

The first two bytes, or the "magic numbers", of any BMP file is 0x42 and 0x4D in hexadecimal.

## What's the difference between `bfSize` and `biSize`?

'bfsize' is metadata stored in the BITMAPFILEHEADER, which is a data structure that stores information about the file containing a BMP. It is the size of the full file holding the BMP, including the image and the headers. 'bisize' is, on the other hand, metadata stored in the BITMAPINFOHEADER. It is the number of bytes which the BITMAPINFOHEADER header file takes up, which is 40 bytes. Therefore, 'bfsize' is the size of the entire bitmap file, whereas 'bisize' is the size of the BITMAPINFOHEADER.

## What does it mean if `biHeight` is negative?

'biHeight' is the height of the BMP in pixels. If it is negative, the BMP is top-down, meaning that the image's top row is at the beginning of the file. Specifically, the first byte of memory used (or the origin) is the upper-left pixel of the image. Top-down BMPs cannot be compressed, and biCompression for these files must be BI_RGB or BI_BITFIELDS.

## What field in `BITMAPINFOHEADER` specifies the BMP's color depth (i.e., bits per pixel)?

The 'biBitCount' field in the 'BITMAPINFOHEADER' structure is the one which specifies the BMP's color depth. The BMP's color depth is the number of bits which are defined in each pixel. This field also specifies the maximum number of colors in the BMP. The value of this field can be 0, 1, 4, 8, 16, 24, or 32.

## Why might `fopen` return `NULL` in lines 24 and 32 of `copy.c`?

In line 24 of 'copy.c', 'fopen' is used in read mode to open the file that will be copied, whose pathname is the string inputted by the user, accessed by argv[1]. It attempts to return the FILE pointer using this pathname. However, if there is no existing file with the inputted pathname, there is no file to input and cannot return a pointer. Therefore, it will return 'NULL'. 'fopen' can similarly return 'NULL' in line 32, but for a slightly different reason. In line 32, 'fopen' is in write mode rather than read mode. Therefore, if there is no existing file with the given pathname, it will simply create one. It will not return 'NULL' for this reason. Instead, it will return 'NULL' if the named file is a read-only file, is a directory, or is any other type of file where permissions to write are denied.

## Why is the third argument to `fread` always `1` in our code? (For example, see lines 40, 44, and 75.)

'fread' is a function which reads elements from a file. The third argument of this function is the number of blocks/elements in the file being read. Whenever 'fread' is called in 'copy.c', it is reading only one block in a file. For example, it is reading only the 'BITMAPFILEHEADER', the 'BITMAPINFOHEADER' or the 'RGBTRIPLE'.

## What value does line 63 of `copy.c` assign to `padding` if `bi.biWidth` is `3`?

If 'bi.biWidth' is '3', 'copy.c' assigns 'padding' to '3'. The 'sizeof(RGBTRIPLE)' is '3', (3 * 3) is '9', (9 % 4) is '1', (4 - 1) is '3', and (3 % 4) is '3'.

## What does `fseek` do?

'fseek' changes the location of a file pointer associated with the given file, moving it forward or background by a certain number of bytes. 

## What is `SEEK_CUR`?

'SEEK_CUR' is a constant defined in the function 'fseek'. It denotes the file pointer's current position, which will likely be changed in the processing of completing 'fseek'.
