# 5 September

This room as the title is about hashing and how it's used. I have learnt most of these from my Computer Science degree so this is more like a refresh and jotting down anything I find interesting/new.

>Crack the hash "5b31f93c09ad1d065c0491b764d04933" using online tools

I tried using hashcat with '-m 0' but did not work on my Kali VM. Either I used the wrong hash mode which according to the website I used, should be MD5 or hashcat really does not like VMs. I think I really should run Kali on baremetal. Either way, the answer for that can be found [here](https://md5hashing.net/hash/md5/5b31f93c09ad1d065c0491b764d04933). Weirdly enough, using CrackStation does not work.

I tried to recall where Linux stores passwords so I will write it down here.

1. /etc/shadow

>How many rounds does sha512crypt ($6$) use by default?

5000. Reference [here](https://blog.michael.franzl.name/2016/09/09/hashing-passwords-sha512-stronger-than-bcrypt-rounds/). Rounds are the number of times results of the algorithm is fed back into the algorithm creating an 'avalanche' effect. More on that [here](https://www.tutorialspoint.com/cryptography/cryptography_hash_functions.htm)

