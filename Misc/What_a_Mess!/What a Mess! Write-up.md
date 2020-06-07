## What a Mess! Write-up


-----

### Category: Miscellaneous 

### Challenge Brief:

The flag is in the given file but the file is filled with gibberish!
Can you help make sense of this mess?
There's a flag in it for you if you do!


-----

### Solution:

- The user is given a .txt file.

- The user has to make the file readable to retrieve the flag.

-----

Viewing the text file using a text editor you see unreadable gibberish.

- Verify the file by using the `file` command on it.

```
file flag.txt
```
Turns out the file is a .tiff file and not a .txt file.
```
flag.txt: TIFF image data, little-endian, direntries=20, height=564, bps=9570, compression=LZW, PhotometricIntepretation=RGB, width=1304
```
- Since the file is an image file you can use the `Eye of Gnome` image viewer using the `eog` command on the file to view it.
```
eog flag.txt
```
This opens up an image with the flag in it.

The flag is `HilltopCTF{N0t_a_txt_file}`