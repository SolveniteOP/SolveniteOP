---
title: "Matryoshka Doll | PicoCTF WriteUp"
seoTitle: "Matryoshka Doll Writeup - PicoCTF"
datePublished: Tue Jun 25 2024 12:46:25 GMT+0000 (Coordinated Universal Time)
cuid: clxuehmjv000208lab3m21hil
slug: matryoshka-doll-picoctf-writeup
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1719318380459/2478e621-77de-4958-9c39-b643b8a6acb3.png
tags: linux, cli, cybersecurity, ctf, cyber, cybersecurity-1, cybersec, write-up, picoctf, ctf-writeup, binwalk, cyber-2

---

Hey everyone! I’ll be giving you guys a walkthrough of the “Matryoshka Doll” lab in PicoCTF. It is a very fun room to do and requires just a bit of patience to go about it.

### 1\. Download the image

First, we download the image from the question

Question

After downloading, we get this image:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318351398/319a4377-151d-4c78-b080-722d1bb1fd90.png align="left")

Inspecting the image we downloaded

### 2\. Extract Information

I used binwalk to try and extract any files/folders from the image and I got this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318353173/35337b02-3273-4c94-9250-a8c76302a926.png align="left")

Using binwalk to extract information

We get this particular directory by extracting:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318354912/fe535b55-ebc6-496f-8fdd-e6bacb2fa5fb.png align="left")

Let’s move into this directory to see what the contents of it are:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318356207/a1de33cf-52a1-4905-a9e2-aa31bccc7fe5.png align="left")

Contents after extracting the image

Here we have a zip file and another folder called “base\_images”. First, let’s unzip the file to see if we get anything valuable.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318357896/d4180292-b3e3-49f3-b1d2-8843079f6f95.png align="left")

Unzipping the file

Looks like it had some images, and made a directory called “base\_images” which already exists. Let’s move into that directory now.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318359229/f1396ea7-d499-4f2b-ab7b-bb7781beeb29.png align="left")

Here we have another file.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318360833/58b3a92b-49b3-49c9-b086-3c0937916c6c.png align="left")

Looks exactly like the previous one, maybe binwalking this image will give us more details?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318363315/b381d28f-9d42-4b00-a9bc-09c86a5a6197.png align="left")

We seem to have gotten another directory called “\_2\_c.jpg.extracted”. Let’s move into this directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318365529/1891159f-1c6d-4dc2-ba49-9a126f639dbb.png align="left")

The same method we used earlier, would probably help us with enumerating further.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318366881/959e701f-3a36-442c-9767-ae12d9537fe1.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318368111/d940d282-dcca-419a-9efa-4f3fa725542b.png align="left")

And we get this image:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318370035/b77bd8dc-d004-4a4b-ba2e-79b566d6fb03.png align="left")

We use the same steps again, binwalking, unzipping, and changing directories.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318371973/24fb955c-2083-4bee-b041-7a6fb3f2d771.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318373643/fbb2d42d-4908-4787-976a-aaf82c268a7c.png align="left")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318375105/44c57c79-984f-45af-8475-4d12cd43e6ae.png align="left")

And finally, after enumerating further, we get this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318376631/c6347772-b7da-4e1b-a77f-56ca1077caa0.png align="left")

Opening the file, we get the contents of flag.txt

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1719318378748/7187c1d1-9fd0-41aa-9681-b8f708288380.png align="left")

### Conclusion

This is a pretty good room to get familiar with the tool binwalk, which is widely used in forensics to extract information from images. Overall, this is a pretty fun room to do and I had a lot of fun doing it.

Hope this was helpful and if you have any queries/ suggestions, do reach out to me!