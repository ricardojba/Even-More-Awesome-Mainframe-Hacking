# Even More Awesome Mainframe Hacking 
![Even More Awesome Mainframe Hacking](https://img.shields.io/badge/mainframe-hacking-lightgrey.svg) ![Awesome Hacking](https://img.shields.io/badge/awesome-hacking-red.svg) ![Awesome community](https://img.shields.io/badge/awesome-community-green.svg) <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/80x15.png" /></a>

All creds to [@samanL33T](https://twitter.com/samanL33T) for starting the list [here](https://github.com/samanL33T/Awesome-Mainframe-Hacking).

List of Mainframe Hacking/Pentesting Resources.
This list is a collection of resources available online to learn Mainframe Penetration Testing & Security.

Special thanks to [@samanL33T](https://twitter.com/samanL33T), [@hacksomeheavymetal](https://github.com/hacksomeheavymetal), [@mainframed767](https://twitter.com/mainframed767), [@bigendiansmalls](https://twitter.com/bigendiansmalls), [@ayoul3__](https://twitter.com/ayoul3__) and many other researchers for all their work in this field. 

[Contributions](contributing.md) are welcome !

Table of Contents
=================

* [IBM zSeries](#-IBM-zSeries)
 	* [Books](#-Books)
 	* [Tutorials](#-Tutorials)
	* [Concepts and Terms](#-Acronyms-and-Concepts)
	* [Typical TCP Ports](#-Typical-TCP-Ports)
	* [Web based Thin Clients Terminal Emulators](#-Web-based-Thin-Clients-Terminal-Emulators)
	* [Emulate zOS](#-Emulate-zOS)
	* [zOS booting, logging and working environments](#-zOS-booting,-logging-and-working-environments)
	* [Top Ten Security Vulnerabilities in z/OS Security](#-Top-Ten-Security-Vulnerabilities-in-zOS-Security)
 	* [Scripts & Tools](#-Scripts-and-Tools)
 	* [Default Accounts and Transactions](#-Default-Accounts-and-Transactions)
 	* [Pentesting](#-Pentesting)
 	* [Presentations & Talks](#-Presentations-and-Talks)
 	* [ACF2 Specific references](#-ACF2-Specific-references)
	* [Security Technical Implementation Guides (STIGs)](#-STIGs)
 	* [Miscellaneous](#-Miscellaneous)
* [IBM iSeries](#-IBM-iSeries)
 	* [iSeries Books](#-iSeries-Books)
 	* [Tutorials & Checklists](#-Tutorials-and-Checklists)
 	* [Tools](#-Tools)
 	* [iSeries Presentations & Talks](#-iSeries-Presentations-and-Talks)
 	* [Miscellaneous](#-miscellaneous)


 
# [↑](#table-of-contents) IBM zSeries

## [↑](#table-of-contents) Books
* Amazon - [Mainframe Basics for Security Professionals_ Getting Started with RACF - Ori Pomerantz, Barbara Vander Weele, Mark E. Nelson, Tim Hahn (2008, IBM Press)](https://www.amazon.com/Mainframe-Basics-Security-Professionals-paperback/dp/0133763048)
* Amazon - [IBM Redbooks - Introduction to the New Mainframe: z/OS Basics](https://www.amazon.com/Introduction-New-Mainframe-OS-Basics/dp/0738435341)
* PDF - [PoCorGTFO#12 - Page 32 - A JCL Adventure with Network Job Entry](https://www.exploit-db.com/download/40624)


## [↑](#table-of-contents) Tutorials
* [bigiron - Wiki/Collection of materials related to IBM z/OS security](https://github.com/v-p-b/bigiron)
* [TSO Tutorial](http://www.jaymoseley.com/hercules/tso_tutor/tsotutor.htm)
* [Z/OS Introduction- An IBM Redbooks video course](https://www.redbooks.ibm.com/redbooks.nsf/redbookabstracts/crse0304.html?Open)
* [Multiple Mainframe Security guides from Chicago Classic Computing](http://chiclassiccomp.org/docs/content/computing/IBM/Mainframe/MainframeSecurity/)
* [Using UNIX System Services to escalate your privileges on z/OS](https://www.bigendiansmalls.com/all-aboard-the-uss-exploits/)
* [The crash course to z/OS pentesting](https://github.com/hacksomeheavymetal/zOS/blob/master/pentesting.md) by [@hacksomeheavymetal](https://github.com/hacksomeheavymetal)


## [↑](#table-of-contents) Acronyms and Concepts

**[The complete list of z/OS acronyms](https://github.com/hacksomeheavymetal/zOS/blob/master/vocabulary.md)**

* **Username limited to 7 char length**
* **Legacy password policy but YMMV**
  * 8 char length restrictions
  * No special chars
* **Master Console**
  * [A "system" level console](https://youtu.be/kjEEFSr-ncE?t=1356)
  * If you get access then its game over
* **External Security Managers (ESMs) - ACL, RBAC, etc**
  * TOP-SECRET
  * ACF-2
  * RACF
    * The "racf.db" file stores all password hashes, provides access control and more
    * There are three main security attributes on RACF:
      * **Special** : can alter RACF rules and access any resource
      * **Operations** : access all files unless being forbidden from doing so
      * **Auditor** : access audit trails and manage logging classes
* **REXX files**
  * The equivalent of scripting language like Python/Ruby
  * REXX Sockets have ASCII translation built in
* **JCL files**
  * The equivalent of shell scripts (sort of)
  * You can submit JOBs in JCL over FTP
  * Has a "JOB card" or header and a "PMG" or program to exec
* **Everything on a Mainframe is a JOB managed by JES (Job Entry Sub-system)**
* **CLIST** - The equivalent of scripting language like Python
* **TSO** - z/OS cli (Linux bash equivalent)
  * Login has a user enumeration flaw via on-screen error messages
  * "Traditional" process accounting
  * CLIST/REXX/JCL scripting
  * OMVS / USS – Unix
  * ISPF - Menu Screens (GUI)
* **LPAR or Logical partition** - Allocation of cpu, disk and mem resources (z/OS VMs equivalent) - Each LPAR can run different stuff e.g. IBM z/OS (mainframe) or with z/VM Linux (RedHat)
* **SYSPLEX** - Multiple LPARS (across hardware too)
* **CICS / IMS**
  * Transaction Managers
  * CICS is a middleware of sorts
  * If we manage to "exit" the application running on CICS, we can instruct CICS to execute default admin programs (CECI, CEMT, etc.) => rarely secured
* **Applications** - Run COBOL, Fortran or Java
* **TN3270/E** - 3270 terminal emulation over Telnet
  * Telnet-like protocol introduced in 1971
  * Allowed "green screen" terminals to go over network TCP/IP rather than hardwire
  * Transmits "screens" made up of fields
  * Response submits modified screen & fields
  * Synchronous & Stateful
  * All apps presented in same way – i.e. TSO, CICS, IMS, REXX etc. all use it
  * Emulator client can be modified to reveal HIDDEN/non-display fields and edit PROTECTED fields
* **SNA** - Systems Network Architecture
* **VTAM**
  * Virtual Telecommunications Access Method Subsystem that implements SNA
  * Multiplexer of sorts
  * Often the first thing you connect to on a mainframe
  * Lets you connect to different application – Can connect you to other LPARs & sysplex’s
  * Uses APPLIDs or "macros"
* **LU / PU** - Logical/Physical Unit – Connections to VTAM (wired vs multiplexed) – TN3270 to mainframe usually gives you a LU
* **DATASETS** - The "file" z/OS concept
* **PDS or PARTITIONED DATASETS** - The "folder" z/OS concept
* **OMVS**
  * TSO command that gives you a /bin/sh shell 
  * Its a Unix subsystem for network, FTP, webservices support
  * You can "su" to root (and run other Unix commands) without a password, if the account is in 'BPX.SUPERUSER'
* **ISPF** 
  * TSO command that gives you the Menu screens (GUI)
  * What everyone uses to interact with TSO
  * Includes file browser & editor
* **APF** - Programs that are setuid 0
* **TPX** - Similar to the gnu-screen
* **App Creds**
  * User enumeration flaws are common
  * Sometimes weaker password policies
* **Other stuff**
  * Databases: DB2 & IMS
  * Unix: FTP, HTTP, WebSphere
  * MQ
  * Etc

[Reference 1](https://www.slideshare.net/sensepost/vulnerabilities-in-tn3270-based-application)

[Reference 2](https://cansecwest.com/slides/2018/Post%20exploit%20goodness%20on%20a%20Mainframe%20SPECIAL%20is%20the%20new%20root%20-%20Ayoub%20Elaassal,%20PwC%20France.pdf)


## [↑](#table-of-contents) Typical TCP Ports
* **TN3270**
  * 23 - default, often VTAM
  * 992 - default, SSL enabled
  * 1023-x0xx - application environments (direct to CICS/IMS regions)
  * 2323, x023, x992 - other ports to check
* **FTP**
  * Provides access to both worlds (TSO & OMVS)
  * Respects wildcards (*.RACF*.*)
  * Awesome brute forcing point
C
  * DB2 (5023) & MQ (1415)
  * HP/BMC/Tivoli monitoring
  * WebSphere
* **Note: One host can have lots of IPs (Order of 10-20)**

[Reference (slide 12)](https://www.slideshare.net/sensepost/vulnerabilities-in-tn3270-based-application)


## [↑](#table-of-contents) Web based Thin Clients Terminal Emulators
* **[Virtel Web Access](https://virtelweb.com)**


## [↑](#table-of-contents) Emulate zOS
* [Hercules Opensource zARCH Emulator](http://www.hercules-390.org) (Free)
* [Emulating a MVS/zOS with Hercules](https://famicoman.com/2018/06/28/emulating-a-z-os-mainframe-with-hercules/)
* [YARGHHH! Avast! :) ](https://pastebin.com/PHiT8jm)


## [↑](#table-of-contents) zOS booting, logging and working environments
**Logging in:**
- On the login screen enter credentials, e.g.:

  `login: ibmuser`

  `pass: sys1 or <empty>`

  `proc: ISPFPROC|OMVSPROC|IKJACCNT`

- On the welcome screen enter userid and see 2.1., e.g.:

  `logon ibmuser`

- In some cases you may need to confirm that you are in VTAM or CICS - run this:

  `ibmtest`

- VTAM returns the following alphanumeric sequence:

  `IBMECHO ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789`

**Working environments:**
Depending on the chosen procedure you will end up in on of the working environments.
- ISPF:
  Courses-like environment with various panels. Allows to perform various tasks on its own, execute commands in TSO, run installed utilities in the z/OS etc.
- OMVS:
  Also known as Unix System Services is a POSIX compliant unix that runs within the z/OS itself. Similar to other unices. Execute "omvs" in TSO  (may not work if you don't have a pseudo terminal allocated, e.g. via SSH. In such case remove and create symlink in / to dev).
- TSO:
  Time Sharing Option is like a login session on linux. Very basic. You can run various commands and applications including "omvs" and "ispf". By typing "ishell" you can run ISPF shell that allows you to run commands in the OMVS.

**Basic navigation:**
In the ISPF-like programs:
  - PF10/PF11 shifts screen view right/left to see all displayed info
  - PF7/PF8 scrolls screen view up/down to see all displayed info
  - PA1 attention key on the virtual keyboard that terminates the execution of the current command in TSO (e.g. when in the '***' prompt).
  - use "File -> Save screen contents" in x3270 (or similar) to save output from the terminal to a local file
  - you can abbreviate some of the commands, e.g. setropts -> setr, listcat -> listc etc.

[Reference](https://github.com/hacksomeheavymetal/zOS/blob/master/firststeps.md)


## [↑](#table-of-contents) Top Ten Security Vulnerabilities in zOS Security
* Excessive Number of User ID’s w/No Password Interval
* Inappropriate Usage of z/OS UNIX Superuser Privilege, UID = 0
* Data Set Profiles with UACC Greater than READ
* RACF Database is not Adequately Protected
* Excessive Access to APF Libraries
* General Resource Profiles in WARN Mode
* Production Batch Jobs have Excessive Resource Access
* Data Set Profiles with UACC of READ
* Improper Use or Lack of UNIXPRIV Profiles
* Started Task IDs are not Defined as PROTECTED IDs


[Reference](https://chapters.theiia.org/fort-worth/ChapterDocuments/zOS%20Security%20Audit%20Top%20Ten%20-%20ISACA.pdf)


## [↑](#table-of-contents) Scripts and Tools
* [TN3270 Clients - X3270](http://x3270.bgp.nu)
* [Multipurpose Nmap Scripts](https://github.com/nmap/nmap/tree/master/scripts)
	* [tn3270-screen.nse](https://nmap.org/nsedoc/scripts/tn3270-screen.html)
	* [tso-enum.nse](https://nmap.org/nsedoc/scripts/tso-enum.html)
	* [tso-brute.nse](https://nmap.org/nsedoc/scripts/tso-brute.html)
	* [vtam-enum.nse](https://nmap.org/nsedoc/scripts/vtam-enum.html)
	* [lu-enum.nse](https://nmap.org/nsedoc/scripts/lu-enum.html)
	* [cics-enum.nse](https://nmap.org/nsedoc/scripts/cics-enum.html) - needs valid account and applid
	* [cics-info.nse](https://nmap.org/nsedoc/scripts/cics-info.html) - needs valid account and applid
	* [cics-user-brute.nse](https://nmap.org/nsedoc/scripts/cics-user-brute.html) - needs valid applid
	* [cics-user-enum.nse](https://nmap.org/nsedoc/scripts/cics-user-enum.html) - needs valid applid
	* [nje-node-brute.nse](https://nmap.org/nsedoc/scripts/nje-node-brute.html)
	* [nje-pass-brute.nse](https://nmap.org/nsedoc/scripts/nje-pass-brute.html)
* [TSO-Brute](https://github.com/mainframed/TSO-Brute)
* [TPX Brute - The z/OS TPX logon panel brute forcer](https://github.com/quentinhardy/TPX-Brute)
* [RACF Database Parser](https://github.com/bigendiansmalls/racfdbparse)
* [OMVSenum.sh](https://gist.github.com/mainframed/c52a4dc93d2ab16d39a4da9b3f38bbe0)
* [lu_brute.py](https://gist.github.com/mainframed/381724f4537b1e893d66a206e4ab1d9b)
* Mainframe Application pentesting (CICS etc.)
	* [CICSPwn](https://github.com/ayoul3/cicspwn) - If your account has access to the CICS trans. "CECI" you can upload JCL and get a shell
	* [BIRP](https://github.com/sensepost/birp)
	* [CICSshot - Take screenshots of CICS](https://github.com/ayoul3/cicsshot)
	* [Hacked wc3270 emulator](https://github.com/ayoul3/wc3270_hacked)	
* zOS Enumeration Scripts
	* [All in one Enumeration of information like VERSION, APF Libraries, SVCs, USERS etc. on Z/OS ](https://github.com/mainframed/Enumeration)
	* [Collection of REXX Scripts by @ayoul3__](https://github.com/ayoul3/Rexx_scripts)
	* [SETRRCVT by @jaytay79](https://github.com/jaytay79/zos/blob/master/SETRRCVT.rexx)
* [FTP - JCL commmand execution - Metasploit Modules by @bigendiansmalls](https://github.com/rapid7/metasploit-framework/blob/master/documentation/modules/exploit/mainframe/ftp/ftp_jcl_creds.md)
* [Metasploit Payloads for z/OS](https://github.com/rapid7/metasploit-framework/tree/12198a088132f047e0a86724bc5ebba92a73ac66/modules/payloads/singles/cmd/mainframe)
* [NC110-OMVS Netcat for z/OS OMVS](https://github.com/mainframed/NC110-OMVS)
* [TShOcker - Mini command interpreter for TSO & UNIX accessible by NetCat](https://github.com/mainframed/TShOcker)
* [MainTP](https://github.com/mainframed/MainTP)
* [zOS Privilege Escalation scripts by ayoul3__](https://github.com/ayoul3/Privesc)
* [Note on TESTAUTH command for running a program in elevated state](https://github.com/zBit31/testauth)
* [zOSFTPlib - python ftplib-like library specifically for Z/OS](https://pypi.org/project/zosftplib/)


## [↑](#table-of-contents) Default Accounts and Transactions
* [Default Accounts](https://github.com/hacksomeheavymetal/zOS/blob/master/default_accounts.txt)
* [Default CICS Transactions](https://github.com/hacksomeheavymetal/zOS/blob/master/default_cics_transactions.txt)


## [↑](#table-of-contents) Pentesting


This is a small pentest guide based on several Talks and Presentations available on the Internet, namely tasks and tools to run for each steps listed bellow and some advice.

Mainframes are just computers... costing ungodly prices with also ungodly high specs and availability capacity. That said unless theres something very wrong, it will hold high loads.

As with every typical security assessment there is always lots of reservations by the teams or person managing the systems. This is especially true since these are very expensive systems handling probably the most mission critical operations in the company. Remember to tell them that you are there to help them secure their systems and not to make their lives harder. Respect them and win them over, because they probably are the same age as your father or mother (or even older) ;)

Before starting, ask the Team or Person that manages the Mainframe if there is a TEST or QA LPAR(s) or Sysplex(s) that mirror PROD. Its preferable to test those. 


**Initial Recon**

First off... without valid credentials not much can be done, so it is important to find valid creds and enumeration is very important in obtaining them.

Start with a full TCP port Portscan and enable Service discovery e.g.:

`nmap -sTV --allports --version-all --version-intensity 9 -p- -v --open -Pn -n mainframe.com -oA mainframe.com`

The mainframe can be running webservers (e.g. web based 3270 clients), so do try all the usual web attacks and reverse engineer (java applets) shenanigans.


**Gaining Access**

Get creds:
* Test for [Default accounts](https://github.com/hacksomeheavymetal/zOS/blob/master/default_accounts.txt)
* Reuse them - If you have creds from, for example, Windows try them - they could be synced with with Active Directory
* Steal them - Phishing, Social Engineer, Check Config Files, Keepass Confluence, Sharepoint, SMB Shares, Wikis, etc - search for terms associated with Mainframes (TSO, LPAR, CICS, etc)
* Sniff them - MITM TN3270 on port TCP/23 is plain text... yes in 2021.
* Brute-Force them - Be careful doing this because you can lock accounts, depending on the password policy.

So you got some valid creds, but remember when trying to login, that some users might only have access to TSO or Unix, but not both.


**Local Recon**

[todo]


**Privilege Escalation**

[todo]


## [↑](#table-of-contents) Presentations and Talks

* [Playlist - All the videos of Security Talks by Soldier of FORTRAN (@mainframed767)](https://www.youtube.com/playlist?list=PLBVy6TfEpKmEL56fb5AnZCM8pXXFfJS0n)
* [Playlist - All the videos of Tools by Soldier of FORTRAN (@mainframed767)](https://www.youtube.com/playlist?list=PLBVy6TfEpKmF_CB9VYbcAhiyg1i1IYaWP)
* [Playlist - All the videos of Mainframe Hacking by Soldier of FORTRAN (@mainframed767)](https://www.youtube.com/playlist?list=PLBVy6TfEpKmGdX1OE_xjK0GKGjSLwxVn_)


**2011**
* [Prezo - How to Break Into z/OS Systems Through USS, TCP/IP, and the Internet](http://www.stuhenderson.com/STUuss01.pdf)
* [Video - DEFCON 14: IBM Networking Attacks-Or The Easiest Way To Own A Mainframe by Martyn Ruks](https://youtu.be/r9hOiXtrumM)


**2012**



**2013**
* [Prezo - How to Break into z/OS Systems - Staurt Henderson](http://www.stuhenderson.com/XBRKZTXT.PDF)
* [Prezo - BSidesLV 2013 - Legacy 0-Day How hackers breached the Logica Mainframe - Soldier of FORTRAN (@mainframed767)](https://www.dropbox.com/s/w8c9e4yfsmx56tw/BSidesLV%202013%20-%20Logica%20Breach%20.pdf)
* [Prezo - Mainframes: What the F$#K is That About? - Soldier of FORTRAN (@mainframed767)](https://www.dropbox.com/s/zl7suai6g1558yl/April%202013%20-%20ThotCon%202013%20-%20Mainframes-%20What%20the%20fuck%20is%20that%20about-.pdf)
* [Prezo - BSidesAustin Mainframes: Everybody has one but nobody knows how to hack them - Soldier of FORTRAN (@mainframed767)](https://www.dropbox.com/s/8vdrhepojde9wah/March%202013%20-%20BSidesAustin%20-%20Mainframes-%20Everyones%20got%20one%2C%20no%20one%20knows%20how%20to%20hack%20them.pdf)


**2014**
* [Video - Hacking Mainframes; Vulnerabilities in applications exposed over TN3270 by Dominic White (Sensepost)](http://www.irongeek.com/i.php?page=videos/derbycon4/t217-hacking-mainframes-vulnerabilities-in-applications-exposed-over-tn3270-dominic-white)
* [Prezo - Hacking Mainframes; Vulnerabilities in applications exposed over TN3270 by Dominic White (Sensepost)](https://www.slideshare.net/sensepost/vulnerabilities-in-tn3270-based-application)


**2015**
* [Prezo - Top 10 Security Vulnerabilities in z/OS by John Hillman (Vanguard)](https://chapters.theiia.org/fort-worth/ChapterDocuments/zOS%20Security%20Audit%20Top%20Ten%20-%20ISACA.pdf)
* [Video - Defcon 22 From ROOT to SPECIAL - Soldier of FORTRAN (@mainframed767)](https://youtu.be/Xfl4spvM5DI)
* [Prezo - Defcon 22 From ROOT to SPECIAL - Soldier of FORTRAN (@mainframed767)](https://media.defcon.org/DEF%20CON%2022/DEF%20CON%2022%20presentations/DEF%20CON%2022%20-%20Philip-Young-From-root-to-SPECIAL-Hacking-IBM-Mainframes.pdf)
* [Video - Learning Mainframe Hacking: Where the hell did all my free time go? by @bigendiansmalls](http://www.irongeek.com/i.php?page=videos/derbycon5/stable31-learning-mainframe-hacking-where-the-hell-did-all-my-free-time-go-chad-rikansrud)
* [Video - DEF CON 23 - Young and Rikansrud - Security Necromancy : Further Adventures in Mainframe Hacking (@mainframed767) & @bigendiansmalls](https://youtu.be/LgmqiugpVyU)


**2016**
* [Video - Gaps in your Defense: Hacking the Mainframe by Soldier of FORTRAN (@mainframed767)](https://youtu.be/1G5Q2sduexs)
* [Prezo - Gaps in your Defense: Hacking the Mainframe by Soldier of FORTRAN (@mainframed767)](https://www.slideshare.net/PhilipYoung14/ca-world-mft1755-gaps-in-your-defense-hacking-the-mainframe-philip-young)
* [Prezo - The current state of Mainframe Hacking by Phil Young - Soldier of FORTRAN (@mainframed767)](https://www.slideshare.net/PhilipYoung14/philip-young-current-state-of-mainframe-hacking-vanguard-101016)
* [Prezo - Advanced Mainframe Hacking by Phil Young - Soldier of FORTRAN (@mainframed767)](https://www.slideshare.net/PhilipYoung14/advanced-mainframe-hacking)

**2017**
* [Video - #HITB2017AMS​ D1T1 - Hacking Customer Information Control System (CICS) by Ayoub Elaassal (@ayoul3__)](https://youtu.be/KnY0Gg_WSLU)
* [Video - Ransomware on the Mainframe: Checkmate by @bigendiansmalls](https://youtu.be/i-DbTy3bEj8)


**2018**
* [Prezo - Post exploit goodness on a Mainframe SPECIAL is the new root by (@ayoul3__)](https://cansecwest.com/slides/2018/Post%20exploit%20goodness%20on%20a%20Mainframe%20SPECIAL%20is%20the%20new%20root%20-%20Ayoub%20Elaassal,%20PwC%20France.pdf)
* [Video - Exploiting the Mainframe - Z/OS integrity 101 by Mark Wilson & Ray Overby](https://youtu.be/7UVrF8skbHU)
* [Video - BSides Glasgow 2018 - Nigel Pentland - Cracking Mainframe Passwords](https://youtu.be/scVojIRxv-M)
* [Video - Mainframe [z/OS] Reverse Engineering & Exploit Development by @bigendiansmalls](https://www.bigendiansmalls.com/files/us-18-Rikansrud-Mainframe-[zOS]-Reverse-Engineering-and-Exploit-Development_Publish.mp4)


**2019**
* [Video - NorthSec 2019 – Philip Young – Mainframe Hacking in 2019](https://youtu.be/KXlmru_B-Uk)
* [Video - CackalackyCon1 - Dan Helton - A Gentle Introduction to Hacking Mainframes by Dan Helton](https://youtu.be/ZfUBv2Ac29Q)


**2020**
* [Prezo - Gibson 101 - Quick Introduction to Hacking Mainframes in 2020](https://null.co.in/event_sessions/2993-gibson-101-quick-introduction-to-hacking-mainframes-in-2020)

   
## [↑](#table-of-contents) ACF2 Specific references
* [CA ACF2 for z/OS - 16.0 Documentation](https://docops.ca.com/ca-acf2-for-z-os/16-0/en)
* [GIAC - ACF2 Mainframe Security](https://www.giac.org/paper/gsec/2812/acf2-mainframe-security/104768)


## [↑](#table-of-contents) STIGs
* [z/OS TSS STIG](https://www.stigviewer.com/stig/zos_tss/)
* [z/OS RACF STIG](https://www.stigviewer.com/stig/zos_racf/)
* [z/OS ACF2 STIG](https://www.stigviewer.com/stig/zos_acf2/)
* [DoD Security Technical implementation Guides(STIGS) - Search for ACF2, Z/OS, RACF etc.](https://public.cyber.mil/stigs/downloads/)


## [↑](#table-of-contents) Miscellaneous
* [Mainframe Hacking - Choose Your own Adventure Game](https://archive.org/details/MainframeHackingCYOA)
* [Evil Mainframe Hacking Training/Course](https://evilmainframe.com/)
* [CBT Tape - Collection of Freeware & Open Source distribution of IBM mainframe MVS & OS/360 Environments](http://www.cbttape.org/)
* [z/OS Internet Library by IBM - Collection of manuals,guides & books about z/OS ](https://www-01.ibm.com/servers/resourcelink/svc00100.nsf/pages/zosInternetLibrary)
* [z/OS - all things security](https://github.com/hacksomeheavymetal/zOS)
* [IBM z/OS Management Facility web application arbitrary file read](https://www.whiteoaksecurity.com/2019-12-30-0-day-in-a-multi-million-dollar-machine/)



# [↑](#table-of-contents) IBM iSeries

## [↑](#table-of-contents) iSeries Books
* Amazon - [Hacking iSeries by Shalom Carmel](https://www.amazon.com/Hacking-iSeries-Shalom-Carmel/dp/1419625012)
* Amazon - [Mastering IBM i: The Complete Resource for Today's IBM i System by Jim Buck & Jerry Fottral](https://www.amazon.com/Mastering-IBM-Complete-Resource-Todays/dp/1583473564)
* Amazon - [Experts' Guide to OS/400 & i5/OS Security by Carol Woodbury & Patrick Botz](https://www.amazon.com/gp/offer-listing/158304096X)
* PDF - [The IBM AS400 A technical introduction](https://www.ibm.com/developerworks/community/files/basic/anonymous/api/library/7cd1e29f-0699-4929-a741-516ce47295a8/document/745425bf-c00a-4a8d-bd8f-1f8e14ef9e65/media)


## [↑](#table-of-contents) Tutorials and Checklists
* [AS/400 Security Assessment Mindmap](http://www.toolswatch.org/wp-content/uploads/2013/02/AS400.jpg)
* [iSeries Penetration Testing](https://www.helpsystems.com/resources/articles/iseries-penetration-testing)
* [Security Audit of IBM AS/400 and System i : Part 1](https://blog.securitybrigade.com/security-audit-of-ibm-as-400-system-i-part-1/)
* [Security Audit of IBM AS/400 and System i : Part 2](https://blog.securitybrigade.com/security-audit-ibm-as-400-system-i-2/)
* [Security Assessment of the IBM i (AS 400) System : Part 1](https://iisecurity.in/blog/security-assessment-ibm-400-system-part-1/)
* [Seclists Mailing list thread on Pentesting AS/400](https://seclists.org/pen-test/2000/Dec/205)
* [Resources from Shalom Carmel's talk at BH Europe - 2006](http://www.blackhat.com/presentations/bh-europe-06/bh-eu-06-Carmel/bh-eu-06-carmel-resources.zip)


## [↑](#table-of-contents) Tools
* [hack400tool - security handling tools for IBM Power Systems (formerly known as AS/400)](https://github.com/hackthelegacy/hack400tool)
* [Hash generator for IBM System i hashes (DES, SHA-1)](http://hackthelegacy.org/index.php?p=/discussion/10/hash-generator-for-ibm-system-i-hashes-des-sha-1-updated)
* [AS/400 SHA-1 hash format plugin for John the Ripper](http://hackthelegacy.org/index.php?p=/discussion/9/our-as-400-sha-1-hash-format-plugin-for-john-the-ripper-now-included-in-the-bleeding-jumbo-build)


## [↑](#table-of-contents) iSeries Presentations and Talks
* [Hack the Legacy: IBM I aka AS400 Revealed by Bart Kulach ](https://www.youtube.com/watch?v=JsqUZ3xGdLc)
* [AS/400 for pentesters by Shalom Carmel](https://www.blackhat.com/presentations/bh-europe-06/bh-eu-06-Carmel/bh-eu-06-Carmel.pdf)
* [AS/400: Lifting the Veil of Obscurity](https://www.youtube.com/watch?v=MWcifBsA8BI)


## [↑](#table-of-contents) Miscellaneous
* [AS400i.com](http://as400i.com/)
* [Hack The Legacy Website](http://hackthelegacy.org/)

