-----
Vanitygen PLUS!  
-----

** This is released only as source code. You need to compile it yourself. I will release compiled versions soon!**  

**WARNING!** While this program has been thoroughly tested, issues could occur in rare cases. Please, first attempt importing an address into a running node. Then, send a tiny amount of your coin that you do not mind losing to the address, and perform a test spend. I will not be held liable for lost funds as a result of the use of this program. You are responsible for your own use of this open source software, on which many crypto community members have labored to make a reality.

Please be sure to report any issues or bugs and fixes, I am happy to accept pull requests! If you have an altcoin you would like to add please let me know immediately!  

-----
Getting Started  
-----  
**Download the code and build with make**

After compiling, run it like:

Running On Linux: `./vanitygen -ARGS`, or `./oclvanitygen -ARGS`, `./keyconv -ARGS`, etc  
Running On Windows: `vanitygen.exe -ARGS`, `oclvanitygen.exe -ARGS`, `keyconv.exe -ARGS`, etc  

**For generating addresses using the CPU(slower) use: vanitygen **  
**For generating addresses using the GPU(faster) use: oclvanitygen **  

**NOTES:**	All arguments are case sensitive!  
	Address prefix must be at the end of the command.  
	oclvanitygen requires OpenCL and correct drivers. This software works well on mining rigs.

**Get a list of the supported Coins with:**  
Linux CPU: `./vanitygen -C LIST`  
Linux GPU: `./oclvanitygen -C LIST`  
Windows CPU: `vanitygen.exe -C LIST`  
Windows GPU: `oclvanitygen.exe -C LIST`  

A list of all the supported crypto coins will be output.  

Choose your coin from the list noting the ARGUMENT needed for the coin located in the left hand column.  
For Meowcoin it is MEOW. For Bitcoin it is BTC.  Etc...  

**Now lets generate a RITO address with the prefix "BFoo":**  
Linux CPU: `./vanitygen -C RITO -o results.txt -i -k BFoo`  
Linux GPU: `./oclvanitygen -C RITO -o results.txt -i -k BFoo`  
Windows CPU: `vanitygen.exe -C RITO -o results.txt -i -k BFoo`  
Windows GPU: `oclvanitygen.exe -C RITO -o results.txt -i -k BFoo`  

 * `-C MEWC` : Chooses the MEWC coin  
 * `-o results.txt` : saves the matches to results.txt  
 * `-i` : case-Insensitive(do not add this flag to match exact case)  
 * `-k` : keep going even after match is found(do not add this flag to stop after the first match)  
 * `MFoo` : the address you are searching for (MEWC addresses start with "M")  

Example output of above command:  

>Generating MEWC Address  

>Difficulty: 4553521  

>MEWC Address: MFoo4XJNzKk2CZW2cJZ6nP9ncVNvdQrp8V

>MEWC Privkey: 5gKsgY4Bf7cbqZtW2CX1Lxy5j99oRa6YBT7TQDj7AuJCPAAb9FW

**If you have dependency errors on Linux or need instructions for compiling from source(Kaling Rolling/Linux) see link below:**  
https://legacysecuritygroup.com/index.php/projects/recent/12-software/35-oclvanitygen-compiling-and-use  

------  
Fix libcrypto.so.1.0.2 error(Debian, Ubuntu)  
------  
Error:
>./vanitygen: error while loading shared libraries: libcrypto.so.1.0.2: cannot open shared object file: No such file or directory  

Fix it by issuing the below commands, in turn either installing or downgrading libcrypto.  The error comes from an incompatibility with the newer version of libcrypto.  Most older projects have this same bug.  
```
wget http://ftp.us.debian.org/debian/pool/main/g/glibc/libc6-udeb_2.24-11+deb9u3_amd64.udeb
dpkg -i libc6-udeb_2.24-11+deb9u3_amd64.udeb
wget http://ftp.us.debian.org/debian/pool/main/o/openssl1.0/libcrypto1.0.2-udeb_1.0.2l-2+deb9u3_amd64.udeb
dpkg -i libcrypto1.0.2-udeb_1.0.2l-2+deb9u3_amd64.udeb
rm libc6-udeb_2.24-11+deb9u3_amd64.udeb && rm libcrypto1.0.2-udeb_1.0.2l-2+deb9u3_amd64.udeb 
```
-----
Encrypting and Decrypting a vanitygen or oclvanitygen private key  
-----  
**Encrypting generated private key:**  
Linux: `./vanitygen -E password -C MEWC MFoo`  
Windows: `./vanitygen -E password -C MEWC MFoo`  
*For GPU use "oclvanitygen" in place of "vanitygen"*  

 * `-C MEWC MFoo` Choose Mewocoin and address prefix "MFoo"  
 * `-E password` Encrypt key with password as "password",  
**NOTE:** It is more secure to use option `-e` with no trailing password,  
then vanitygen prompts for a password so theres no command history.  
Also please choose a stronger password than "password".  

>Generating MEWC Address  
>Difficulty: 4553521   
>AC Pattern: MFoo                                                                      
>AC Address: MFoo853vQs6QGrTuTHb7Q45tbeB8n4EL47vd  
>AC Protkey: yTYFUWAsgFmMxCbKtu3RdrrJXosZrjxiQFA2o43neB4jPpfLe5owNNrteTs8mpvua8Ge  

**Decrypting generated ProtKey with Keyconv:**  
Linux: `./keyconv -C MEWC -d yTYFUWAsgFmMxCbKtu3RdrrJXosZrjxiQFA2o43neB4jPpfLe5owNNrteTs8mpvua8Ge`  
Windows: `keyconv.exe -C MEWC -d yTYFUWAsgFmMxCbKtu3RdrrJXosZrjxiQFA2o43neB4jPpfLe5owNNrteTs8mpvua8Ge`  

 * `-C MEWC` Specifies Meowcoin  
 * `-d` means decrypt the protected key of "yTYFUWAsgFmMxCbKtu3RdrrJXosZrjxiQFA2o43neB4jPpfLe5owNNrteTs8mpvua8Ge"  

>Enter import password:  --- Enter "password" or whatever you specified as password and press enter  
>Address: MFoo853vQs6QGrTuTHb7Q45tbeB8n4EL47vd  
>Privkey: 66GRP2W5H4sWbgrBRAuPc3qZxUtP5boubJ9N2M5wZio6fhWjzbr  

