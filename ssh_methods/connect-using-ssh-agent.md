(base) quantum:tools mthomas$ cat howto.setup.ssh-agent.locally.txt 
# ssh-agent is a program to hold private keys used for public key authentication (RSA, DSA, ECDSA, Ed25519).
  

######
# verify that the ssh-agent is running
######
(base) quantum:~ mthomas$ ssh-add -l
The agent has no identities.

# cd into your .ssh directory:
(base) quantum:~ mthomas$ cd ~/.ssh

# generate a new key:
(base) quantum:~ mthomas$ ssh-keygen -t rsa -b 2048 -f sdsc_id_rsa
Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in sdsc_id_rsa.
Your public key has been saved in sdsc_id_rsa.pub.
The key fingerprint is:
SHA256:Y2pBZAvYkn2q5BWrbF2nh2kxas8KdxM0IPWMjIGPlaI mthomas@quantum
The key's randomart image is:
+---[RSA 2048]----+
| .oB+ o          |
|o *=+O..         |
|.=..o=B          |
|E o +o+..        |
| + = ooBS        |
|  * + ==..       |
| ....+=.         |
|   o oo.         |
|    ..           |
+----[SHA256]-----+
(base) quantum:~ mthomas$ ll
total 32480
drwx------  14 mthomas  staff   448 May 20 15:08 .
drwxr-xr-x+ 98 mthomas  staff  3136 May 29 11:31 ..
-rw-------   1 mthomas  staff  1203 Apr 25 11:17 authorized_keys
-rw-------   1 mthomas  staff   324 Apr 25 14:03 config
-rw-------   1 mthomas  staff  1876 May 29 11:31 sdsc_id_rsa
-rw-r--r--   1 mthomas  staff   397 May 29 11:31 sdsc_id_rsa.pub

######
# add the new key to the ssh-agent:
######
(base) quantum:.ssh mthomas$ ssh-add sdsc_id_rsa 
Enter passphrase for sdsc_id_rsa: 
Identity added: sdsc_id_rsa (mthomas@quantum)

######
# check that the new key was added
######
(base) quantum:.ssh mthomas$ ssh-add -l
2048 SHA256:Y2pBZAvYkn2q5BWrbF2nh2kxas8KdxM0IPWMjIGPlaI mthomas@quantum (RSA)

######
# copy the public key information to your remote account
# this will be added to your authorized_keys file
######
(base) quantum:.ssh mthomas$ ssh-copy-id mthomas@comet.sdsc.edu
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'mthomas@comet.sdsc.edu'"
and check to make sure that only the key(s) you wanted were added.

######
# try to logon
######
(base) quantum:.ssh mthomas$ ssh mthomas@comet.sdsc.edu
Last login: Fri May 29 10:10:09 2020 from 76.176.117.51
Rocks 7.0 (Manzanita)
Profile built 12:32 03-Dec-2019

Kickstarted 13:47 03-Dec-2019
                                                                       
                      WELCOME TO 
      __________________  __  _______________
        -----/ ____/ __ \/  |/  / ____/_  __/
          --/ /   / / / / /|_/ / __/   / /
           / /___/ /_/ / /  / / /___  / /
           \____/\____/_/  /_/_____/ /_/
###############################################################################
NOTICE:
The Comet login nodes are not to be used for running processing tasks.
This includes running Jupyter notebooks and the like.  All processing
jobs should be submitted as jobs to the batch scheduler.  If you don’t
know how to do that see the Comet user guide
https://www.sdsc.edu/support/user_guides/comet.html#running.
Any tasks found running on the login nodes in violation of this policy
 may be terminated immediately and the responsible user locked out of
the system until they contact user services.
###############################################################################
(base) [mthomas@comet-ln2:~] 

######
# cleanup copies of the old pub key from remote systems
####
