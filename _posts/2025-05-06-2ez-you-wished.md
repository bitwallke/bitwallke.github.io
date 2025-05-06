---
title: 2ez You Wished
date: 2025-05-06 22:40:00 +0300
categories: [writeups, ctf, bitsiegectf2025]
tags: [steganography]
render_with_liquid: true

---
![kiwi khaos](/assets/img/blogs/kiwi.png)

---

> In this walkthrough, we are going to solve a steganography challenge called `2ez_you_wished`. As the name suggests, it is not your typical challenge and required keen observation.

---

> **Steganography** is the practice of concealing a message within another message or object, making the hidden information undetectable without specific knowledge or tools.

---

## Solving 2ez_you_wished

1. We are first provided with a zip file named `2ez.zip`. Download it and unzip it in your CTF/Steganography folder. its always nice to have clean working directories.   
![alt text](/assets/img/blogs/2ez-you-wished/image.png)
2. We get an image `2ez_y0u_wish.bmp`.
3. Running `file 2ez_y0u_wish.bmp` reveals it is a `bitmap` image.   
![alt text](/assets/img/blogs/2ez-you-wished/image-1.png)
4. We then proceed to run tools like `zsteg` to see whether we can find any hidden data.   
![alt text](/assets/img/blogs/2ez-you-wished/image-2.png)
5. Players were lost here, thinking the string was a hidden flag or hidden secret.   
6. One way of knowing that a file has been embedded in another is usually detected by checking the file size. First open the image as shown below.  
![alt text](/assets/img/blogs/2ez-you-wished/image-3.png)
7. The image is very light from the looks of it, but running `exiftool 2ez_y0u_wish.bmp` reveals that it's file size is `6.5 MB`. Pretty sus, right?  
![alt text](/assets/img/blogs/2ez-you-wished/image-4.png)
8. Now, let's use stegseek to find hidden data within the image. Run `stegseek 2ez_y0u_wish.bmp`.  
![alt text](/assets/img/blogs/2ez-you-wished/image-5.png)
9. Immedietely, we recover a passphrase `liverpool25` which is then used to recover a file `notyet.txt` that is saved under `2ez_y0u_wish.bmp.out`.  
10. Lets see the contents of the file by running `cat 2ez_y0u_wish.bmp.out`.  
![alt text](/assets/img/blogs/2ez-you-wished/image-6.png)
11. Is that chinese, Korean or even Japanese?? Lets ask google translate.   
![alt text](/assets/img/blogs/2ez-you-wished/image-7.png)
12. What does `The 1980s was a very happy time for the 1980s` that even mean??  
13. That is where almost every player was lost. Is this an `OSINT` challenge or a `Steganography` challenge.   
14. Well, it was in the steganography challenge, and the author intended you to decode critical information from that text.   
15. Googling around you will find that there exists `base65536` and using online decoders like [Better Converter](https://www.better-converter.com/Encoders-Decoders/Base65536-Decode), you can decode the string.    
![alt text](/assets/img/blogs/2ez-you-wished/image-8.png)
16. And there we get a key `B1tw4ll#b4db0y4l1f3` to the second part of the challenge...we are almost there.   
17. After trying multiple tools, you should end up using `openstego`. Either the GUI version or the CLI version should work just fine.     
![alt text](/assets/img/blogs/2ez-you-wished/image-9.png)
18. Finally, we can read our flag!!.     
![alt text](/assets/img/blogs/2ez-you-wished/image-10.png)

---

## Takeaways
This challenge demanded a great deal of critical thinking due to its numerous rabbit holes. All in all, `steganography` continues to play a crucial role in our everyday digital landscape.

