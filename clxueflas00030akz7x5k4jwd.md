---
title: "Information | PicoCTF WriteUP"
seoTitle: "Information - PicoCTF Writeup"
datePublished: Tue Jun 25 2024 12:44:50 GMT+0000 (Coordinated Universal Time)
cuid: clxueflas00030akz7x5k4jwd
slug: information-picoctf-writeup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719318392165/a54e1d99-8338-4326-866c-2092298c1e88.png
tags: cybersecurity, cyber, cybersecurity-1, cybersec, write-up, picoctf, exiftool, ctf-writeup, binwalk, cyber-2

---

Hey! I’ll give you guys a guide on how to go about the “Information” lab in PicoCTF. It is quite easy, honestly and just requires a bit of Linux knowledge.

### 1\. Download the Image

First, we download the cat.jpg image from the question

This is the image we get after the file has been downloaded:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318384444/56bd8cb2-5650-4633-a1cb-c2f62d83c180.png align="left")

### 2\. Extract Information

First, I tried using binwalk to try and extract files from the picture, but I couldn’t find anything.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318386727/55804afc-29b3-418a-abab-a8aedb1fdc4f.png align="left")

Next, I decided to use Exiftool to check the metadata of the image.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318389004/839e5225-693c-4ec1-bb20-ab3d37cff410.png align="left")

Over here, I noticed that the “License” section seemed to have a weird value, so I decided to base64 and decode it using cyberchef and viola! I got the flag for the string.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318390714/cea04092-ef9e-426e-a33a-90b19b30a1cf.png align="left")

### Conclusion

This is a very beginner-friendly lab in PicoCTF that aims at strengthening your steganography knowledge. Using a little bit of common sense helps solve this room effortlessly.

If you have any queries/ suggestions, feel free to reach out to me!