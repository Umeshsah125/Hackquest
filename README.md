# Hackquest
This repo is created as a proof of concept for the CTF challenges created by TCS Hackquest V

1. DigiMagic
============
Points: 100
- This challenge was created to check the security certificates of the given domain. We were provided a link which gives us certificate error on visiting the link.
- Steps to solve this challenges are given below:

i. Visit the given link which was tcshackquest.com in my case.
ii. Perform whois lookup to the domain and notedown the IP(x.x.x.x) of domain
iii. Well the domain was using HTTP protocol which is Insecure, Thus we will click on the left corner *LOCK Icon* of the url tab and see the certificates.
iv. We got following info:
    O =  TCSL
    L =  Bhubaneswar, Special Economic Zone,
      aHE1e3MwX1kwdV9LTjBXX0hvV18kJDFfd29yS3N9     
    ST = HQState
    C  = IN
    
v. Copy the above encoded value which is ofcourse a base64 encoded value.
vi. Decode it using an online tool(base64decode.org) or we can use our own Linux distro for this one as below:
  root> echo aHE1e3MwX1kwdV9LTjBXX0hvV18kJDFfd29yS3N9 | base64 -d
 
vii. Flag is hq5{s0_Y0u_KN0W_HoW_$$1_worKs}



2. Record
==========
Points: 400
- This challenge was pretty much easy compare to others because it was related to event logs of windows system. I had solved various challenges regarding the logs and events of
the windows and linux which provided me great help into this.
- We were provided with a .rar file where two .evtx file are stored named as: App and System
- Steps to approach this challenge are given below:

i. Uncompress the record.rar file and we will have two file named as App and System
ii. Open the control panel and search event logs
iii. In event viewer panel, Click on open saved logs and open *System* logs because system logs store each and every logs related to the particular system
iv. Scrolling down through the few events we got following data in the *Details* Panel
      
      EventData 
  ServiceName SFE1e01hbHdhcmVfaW1wbGVtZW50X3BlcnNpc3RlbmNlfQ== 
  ImagePath C:\Users\Binary\AppData\Local\Temp\ransomware.exe 
  ServiceType user mode service 
  StartType demand start 
  AccountName LocalSystem 

v. Well, we found an interesting service named encoded with base64 encoding let's decode it.
vi. Online tool or we can use our builtin *nix utilities.

    root> echo SFE1e01hbHdhcmVfaW1wbGVtZW50X3BlcnNpc3RlbmNlfQ== | base64 -d
vii. Flag is HQ5{Malware_implement_persistence}


3.IamNotPermanent
==================
Points: 400
- This was very much interesting challenge related to memory forensics which I was not able to solve at the challenge time but I solved it after an hour of end of the challenge.
- The Question was related to memory forensics using the tools Volatility.
- For solving this challenge, we need a Forensic tool called Volatility
- So the steps involved are:

user> sudo volatility -f IamNotPermanent.mem imageinfo
- It gives us the information about the system profile whether it is windows XP,NT,8,10 etc..

user> sudo volatility -f IamNotPermanent.mem --profile=Win7SP1x64 kdbgscan
- Here, profile is the name we obtained from above scan and kdbgscan gives us  more accurate details about kernel profile

user> sudo volatility -f IamNotPermanent.mem --profile=Win7SP1x64 cmdscan
- It scans all the command line history which gives us an interesting encoded value of ransomeware exe file. Let's copy that value and decode it.

user> echo SFE1e2NtZGxpbmVzX2FyZV9jcnVjaWFsX2R1cmluZ19mb3JlbnNpY3N9 | base64 -d
- We can use online tool or our own linux utilities

FLAG is HQ5{cmdlines_are_crucial_during_forensics}

4. 
