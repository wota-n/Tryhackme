#THM 8th September

This room is about learning how to use John the Ripper, a password cracking tool like hashcat except its suppsed to be CPU friendly from what I understand.

Documenting this as this would be my first time actually trying to use it since I tend to rely on hashcat. Considering how badly it runs on VMs, this should be a good learning opportunity.

>What type of hash is hash1.txt?

MD5. Found this by using the hash-identifier Python program that was provided [here](https://gitlab.com/kalilinux/packages/hash-identifier/-/raw/kali/master/hash-id.py). Tried using John to identify the hash but as mentioned by the author of this room, it is not very reliable. 

>What is the cracked value of hash1.txt?

b*****

This took some effort to figure out. Firstly, I used John to crack the hash with 

* john --format=raw-md5 --wordlist=Downloads/rockyou.txt Desktop/hash1.txt

This does not immediately show the password in my experience. Not sure how other people do it. Which is why I had to run the following command to get the actual password.

Interesting to note is that in the 'format' flag, 'raw' needs to be provided since there are many sub-types for each hash algorithm. Did not read through the author's explanation thoroughly so found that out after spending some time playing around with John.

* john Desktop/hash1.txt  --show --format=raw-md5

>What type of hash is hash2.txt?

sha1. Obtained this through the Python program as linked previously.

> What is the cracked value of hash2.txt

k*******

>What type of hash is hash3.txt?

sha256

>What is the cracked value of hash3.txt

m*********

>What type of hash is hash4.txt?

Whirlpool. Never encountered this hash before. 

*john --list=formats | grep -F 'whirlpool' 

Above is the command used to check how to use it with john

>What is the cracked value of hash4.txt

* john --format=whirlpool Desktop/hash4.txt Downloads/rockyou.txt

c*******. This format does not need raw.
