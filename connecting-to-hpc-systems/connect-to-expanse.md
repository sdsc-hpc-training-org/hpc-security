# Connecting to your Expanse.sdsc.edu Account
[//]: # " Comment example "

[//]: # ( Comment2 )

<a name="top"></a>Contents:
* [Connecting to HPC Systems](#connecting)    
* [Obtain your Expanse account](#expanse-account)
* [Install/Locate the Terminal App](#term-app)
    - [Linux ](#term-linux)
    - [Mac](#term-mac)
    - [Windows ](#term-windows)
        - [Windows 10](#term-windows10)
        - [Windows (pre-Win10)](#term-windows-older)
* [Install/Locate Secure Shell (SSH) App](#ssh)
* [Terminal Connection Example](#connect-example)
    - [Getting Domain Name & Host Information](#dn-info)
    - [Making the Connction](#connection)
* [Read the Expanse User Guide](#expanse-guide)

Note: if you have any difficulties completing these tasks, please contact Institute staff at <consult@sdsc.edu>.

## Connecting to HPC Systems <a name="connecting"></a>

To connect to an SDSC HPC system, you need the following:
* An *expanse* account.
* A *terminal* client running on your laptop that can be used to connect to Expanse. 
* The *SSH* application running in the terminal to make the connection. 

<img src="./images/ssh_login.png" alt="SSH Connection" width="300px" />

Terminal applications are used to connect clients (you and your laptop) to remote computers (such as Expanse). See https://en.wikipedia.org/wiki/Terminal_emulator for more information. The best known example of using a terminal is for logging in/connecting to a remote computer systems by users. This is called a client-server connection. Terminals are interactive: you type in a command to run, and the outputs are displayed on the terminal. Executing any command is done by typing it and pressing Enter.

SSH provides a secure channel over any network in a client-server architecture (see https://en.wikipedia.org/wiki/Secure_Shell). You will be using your laptop to access SDSC’s HPC systems using the secure shell command `ssh`. It is essential that you be able to run secure shell (or a similar connection tool) with X11 forwarding enabled, which allows you to have data encryption and to launch windows applications (e.g. plotting, or a browser). There are multiple ways to connect via SSH, see [here](https://github.com/sdsc-hpc-training-org/hpc-security/tree/master/ssh_methods) for more information.

This tutorial can be used to verify that your account is working, that your laptop is properly configured, and that your Expanse user environment is correctly setup. If you are new to Unix, please see the [Basic Linux Skills](https://github.com/sdsc-hpc-training-org/basic_skills) tutorial.



## Obtain your Expanse account <a name="expanse-account"></a>

To obtain a trial Expanse account see the Expanse user guide at  http://www.sdsc.edu/support/user_guides/expanse.html#trial_accounts

You will be directed to the *XSEDE portal*, where you will create a *Portal User account*. Information from that account will be used to set up your *trial* Expanse account. Note that the Portal account name and the Expanse account name may be different, so keep track of them both. The Expanse account can then be used for all Expanse allocations.

[Back to Top](#top)
<hr>


## Locate or Install the Terminal App <a name="term-app"></a>

*NOTE: The `hostname` for Expanse is `expanse.sdsc.edu`

<img src="./images/cluster-connection-diagram.png" alt="SSH Connection" width="350px" />

[Back to Top](#top)
<hr>

## <a name="term-linux"></a>Linux 
There are a lot of terminal emulators available for Linux. See http://www.linuxandubuntu.com/home/10-best-linux-terminals-for-ubuntu-and-fedora for a 'Top 10' List. A very popular terminal is the [Gnome]() terminal, which is included in the Linux distribution software. 

<img src="./images/gnome-terminal_lightweight_Desktop.png" alt="SSH Connection" width="350px" />
(Image Source from http://www.necopost.com/2011/11/gnome-terminal-as-lightweight-desktop.html)


## <a name="term-mac"></a>Mac 
For Mac  users, the *Terminal* application is typically used for connections. The application can be found in the */Applications/Utilities* folder:

<img src="./images/mac-term-app-listing.png" alt="Mac terminal listing" width="350px" />

The terminal launches on the Mac Desktop like other applications, and uses an interactive command-line based interface:
<img src="./images/mac-os-terminal.png" alt="Mac terminal desktop" width="350px" />

Note that for macs, if you want to run applications on the remote that involves visualization or user GUIs such as Jupyter Notebooks, R-Studio, or Matlab, you will need to install [XQuartz](https://www.xquartz.org/) which launches an X11-type app. For more info, see 

[Back to Top](#top)
<hr>

### <a name="term-windows"></a>MSFT Windows 
All windows users will need to run a terminal emulation application capable of supporting an X Server and an ssh-like client.

**Windows 10** <a name="term-windows10"></a>
Windows 10 has a new terminal app called *Windows Terminal*, which is a terminal emulator for Windows 10 written by Microsoft. It includes support for the Command Prompt, PowerShell, WSL and SSH and other commands. While not a full Unix OS, it has shown to be very popular and useful within the HPC community. MSFT has created a GitHub repo with source code, installation and documentation here:
   * https://github.com/Microsoft/Terminal

<img src="./images/windows-10-powershell-commands.png" alt="Win10 Powershell" width="350px" />

[Back to Top](#top)
<hr>

**Windows** (pre-Win10) <a name="term-windows-older"></a> 
Older Windows users will need to run an X Server and an ssh-like client. [Cygwin](https://www.cygwin.com) provides a comprehensive Linux-like environment and an X server (Cygwin/X). Putty will also work for direct access to Expanse, it is only used for file transfers. For download and installation instructions, see:

   * http://www.cygwin.com/
   * http://x.cygwin.com/
   * https://www.putty.org/
   
[Back to Top](#top)
<hr>


## InstallLocate Secure Shell (SSH) App <a name="ssh"></a>
For connecting to SDSC systems, we recommend using [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell). 

*NOTE1:* Using Null passphrase SSH public keys is *not* recommended for SDSC HPC systems; to automate your connections use the SSH-Agent command. For more information, see the [SDSC Security Repo](https://github.com/sdsc-hpc-training-org/hpc-security)
 
*NOTE2:*  See [here](https://github.com/sdsc-hpc-training-org/hpc-security/tree/master/ssh_methods) for information on various methods for using SSH to securely connect to HPC systems.
 
[Back to Top](#top)
<hr>

## Terminal Connection Example <a name="connect-example"></a>

### Getting Domain Name & Host Information <a name="dn-info"></a>
Each machine you work with will have a `<domain_name>`,  `<hostname>` or `<ip_address>`. You can learn about IP addresses and domain names here: https://computer.howstuffworks.com/dns.htm.

* NOTE: The *DN* (domain name) for Expanse is    `expanse.sdsc.edu`

You may need to know the physical IP address of the cluster. To do this, run the `nslookup` command from the command line of your local terminal window (or on `expanse` if are logged in)
```
[username@laptop:] nslookup expanse.sdsc.edu
(base) [mthomas@login02 ~]$ nslookup expanse.sdsc.edu
Server:		10.21.0.1
Address:	10.21.0.1#53

Non-authoritative answer:
Name:	expanse.sdsc.edu
Address: 132.249.21.111
```

The public IP address appears under the line labeled "Non-authoritative answer:" and for Expanse there are two. 
* Expanse's DN is. expanse.sdsc.edu
* Expanse's IP address is:  132.249.21.111 

You can log onto Expanse using either the DN or the IP addresses. 

[Back to Top](#top)
<hr>



### Making the Connection <a name="connection"></a>
```
[localuser@localhost]: ssh -X username@expanse.sdsc.edu
Welcome to Bright release         9.0

                                                        Based on CentOS Linux 8
                                                                    ID: #000002

--------------------------------------------------------------------------------

                                 WELCOME TO
                  _______  __ ____  ___    _   _______ ______
                 / ____/ |/ // __ \/   |  / | / / ___// ____/
                / __/  |   // /_/ / /| | /  |/ /\__ \/ __/
               / /___ /   |/ ____/ ___ |/ /|  /___/ / /___
              /_____//_/|_/_/   /_/  |_/_/ |_//____/_____/

--------------------------------------------------------------------------------

Use the following commands to adjust your environment:

'module avail'            - show available modules
'module add <module>'     - adds a module to your environment for this session
'module initadd <module>' - configure module to be loaded at every login

-------------------------------------------------------------------------------
Last login: Mon Nov 11 13:51:39 2020 from 12.34.56.78
[username@login02 ~]$
```


[Back to Top](#top)
<hr>

## Read the Expanse User Guide <a name="expanse-guide"></a>

Please read the Expanse user guide and familiarize yourself with the hardware, file systems, batch job submission, compilers and modules. The guide can be found here:
http://www.sdsc.edu/support/user_guides/expanse.html

Once you are logged onto Expanse, you can begin working with your code. For more help on using Expanse, see the [Expanse 101](https://github.com/sdsc-hpc-training-org/expanse-101) tutorial
 
