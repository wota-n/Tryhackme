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


# THM 12 September

## Cracking /etc/shadow hashes

This task is quite interesting and took some time for me to fully get. 

Essentially, given a /etc/shadow file, it needs to be combined with a /etc/passwd file first so that John the Ripper can correctly crack the file.

The 'unshadow' command is used for this. This command essentially combines the /etc/shadow file - which may contain a password hash and a local /etc/passwd file. The end result is a file that looks like it natively belongs in an /etc/shadow file.

Difference between shadow and passwd are as follow: passwd no longer contains user passwords as it is moved to shadow due to security concerns. Only root users can access /etc/shadow which makes it harder for attacker to crack it due to needing access.

Source I used [here](https://unix.stackexchange.com/questions/461022/what-is-the-difference-between-etc-shadow-and-etc-passwd).

>unshadow /etc/passwd etchashes.txt > unshadowed.txt

Above is command I used to unshadow the given task file and a /etc/passwd from the Kali Linux container I am using.

>john --wordlist=rockyou.txt  --format=sha512crypt unshadowed.txt

Above is the command for John to crack the unshadowed.txt file generated.

>What is the root password?
*****

I also began using a Kali docker container for this task to see how well and easy using docker is compared to running a VM. I like that since everything is isolated, I do not need to install my host machine with packages I rarely use. John seems to run well, should try hashcat at some point.