# EXPLOIT FTP
1.Set up the two os in a a virtual environment.
 - Kali
 - Metasploitable2
2.Make sure they are host-only. \
3.on kali machine
 - know the ip address route via " ip addr"
 - now nmap the ip address. via " nmap -sV <ip addr>
 - <img width="1365" height="810" alt="image" src="https://github.com/user-attachments/assets/551dce35-9651-4ff2-9a94-0972b08a4e35" />
 - thats what i got.now my target is ftp which is version vsftpd 2.3.4
4.search for common vulnerabilities related with vsftpd 2.3.4
 - command: searchslpoit "vsftpd 2.3.4"
 - <img width="1366" height="238" alt="image" src="https://github.com/user-attachments/assets/857d831f-0bea-42b6-af85-59d6f0a98773" />
 - confirms there is an active exploit.how about we shift to metasploit
5.Exploit
 - msfconsole
 - search an exploit
 - <img width="1362" height="379" alt="image" src="https://github.com/user-attachments/assets/11f27124-4546-49cc-9b13-18ace7671a77" />
 - found it.
 - use it
 - <img width="898" height="303" alt="image" src="https://github.com/user-attachments/assets/037e14ac-b0c3-423c-b71c-b6d718307484" />
 - set RHOSTS and LHOST
 - <img width="840" height="58" alt="image" src="https://github.com/user-attachments/assets/00c02f07-b687-4210-9111-7294047c0a41" />
 - <img width="1342" height="226" alt="image" src="https://github.com/user-attachments/assets/bf13adea-0437-42c8-a798-3aa814061ec4" />
 - EXPLOIT.You will get a meterpreter meaning you have gotten a shell
6.Access an asset.
 - I choose a .deb file since its used by software developers and may contain intellectual rights
 - <img width="1171" height="754" alt="image" src="https://github.com/user-attachments/assets/0086fd76-d948-464c-8ac0-e64798097209" />






