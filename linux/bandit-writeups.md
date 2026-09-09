Bandit Level 0 → Level 1

Challenge:

    The password for the next level is stored in a file called readme located in the home directory.

    Use this password to log into bandit1 using SSH on port 2220.

Solution:
Bash

ls
cat readme
ssh bandit1@bandit.labs.overthewire.org -p 2220

Explanation:

    ls lists files in the current directory to locate readme

    cat readme outputs the contents of the file to standard output

    ssh connects to the remote host on port 2220 using the -p flag

Password: 6y2kwnwK6grgvwvpvLaa2T1cpFEKOhNR

What I learned: Basic shell navigation, displaying file contents with cat, and connecting to SSH servers on non-standard ports.

*******************************************************************

Bandit Level 1 → Level 2

Challenge:

    The password for the next level is stored in a file called - located in the home directory.

Solution:
Bash

cat ./-

Explanation:

    A single hyphen - is interpreted by Linux commands as standard input (stdin)

    Using ./- specifies the relative file path, forcing cat to read the file directly

Password: PK8fYLZg2hnHSz83plBL1iEPKdD3QToB

What I learned: How command-line utilities parse options versus positional arguments, and how prepending ./ resolves special character file paths.

*******************************************************************

Bandit Level 2 → Level 3

Challenge:

    The password for the next level is stored in a file called --spaces in this filename-- located in the home directory.

Solution:
Bash

cat "./--spaces in this filename--"

Explanation:

    Enclosing the filename in double quotes preserves the spaces as a single argument

    The ./ prefix prevents the shell from misinterpreting the leading -- as a command flag

Password: 7ZZ2LFrykP2zEyvBl4m3clcL7tGYJPME

What I learned: Handling filenames that contain spaces and leading hyphens using quotation marks and path prefixes.

*******************************************************************

Bandit Level 3 → Level 4

Challenge:

    The password for the next level is stored in a hidden file in the inhere directory.

Solution:
Bash

cd inhere
ls -la
cat ...Hiding-From-You

Explanation:

    cd inhere changes the working directory to inhere

    ls -la lists all directory contents, including hidden files (prefixed with .)

    cat ...Hiding-From-You reads the revealed hidden file

Password: xzTXq1rDJQVVAzdv5cHq1TQytTWufAMq

What I learned: Hidden files in Linux begin with a dot (.) and require the -a flag in ls to be viewed.

*******************************************************************

Bandit Level 4 → Level 5

Challenge:

    The password for the next level is stored in the only human-readable file in the inhere directory.

Solution:
Bash

cd inhere
file ./*
cat ./-file07

Explanation:

    cd inhere enters the target directory

    file ./* inspects all files and outputs their data format/encoding

    cat ./-file07 opens the specific file identified as ASCII text

Password: 6C7h9GD8M6ai5nr7wo1RonrzFjj9yIrG

What I learned: Using the file command to determine the actual type and encoding of files instead of relying on file extensions.

*******************************************************

Bandit Level 5 → Level 6

Challenge: Find a file with these properties:

    Human-readable

    1033 bytes in size

    Not executable

Solution:
Bash

find . -type f -size 1033c ! -executable -exec file {} \; | grep text
cat ./maybehere07/.file2

Explanation:

    find . -type f -size 1033c searches for files exactly 1033 bytes

    ! -executable excludes executable files

    -exec file {} \; runs file command on each result

    grep text filters for human-readable files

Password: pXa26xhMWaC2SvDotA4r9EgZkulOeSBW

What I learned: The find command is incredibly powerful for filtering files by multiple properties.

*******************************************************

Bandit Level 6 → Level 7

Challenge: Find a file stored somewhere on the server with these properties:

    Owned by user bandit7

    Owned by group bandit6

    33 bytes in size

Solution:
Bash

find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password

Explanation:

    find / initiates a system-wide search from the root directory

    -user bandit7 and -group bandit6 match the exact ownership parameters

    -size 33c limits results to files that are exactly 33 bytes

    2>/dev/null redirects error messages (e.g., Permission Denied) to suppress noise

Password: Bmnnvf82KzQlfxgAI2d1zYbr1u9pr3E3

What I learned: How to search the entire filesystem using ownership flags and redirect standard error streams (2>/dev/null) for clean output.

***************************************************

Bandit Level 7 → Level 8

Challenge:

    The password for the next level is stored in the file data.txt next to the word millionth.

Solution:
Bash

grep "millionth" data.txt

Explanation:

    grep "millionth" data.txt scans the file and returns only the line containing the string millionth

Password: VR1ljMayciFxbnUokuQmJFw6QC9VKtub

What I learned: Using grep to quickly search and extract specific strings or patterns from large text files.

*******************************************************

Bandit Level 8 → Level 9

Challenge:

    The password for the next level is stored in the file data.txt

    It is the only line of text that occurs only once

Solution:
Bash

sort data.txt | uniq -u

Explanation:

    sort data.txt sorts all lines alphabetically so duplicates become adjacent

    | pipes the sorted text stream into the next command

    uniq -u filters the stream and prints only the unique lines that have no duplicates

Password: EjmOSvuAu7sGAHqHVcBDPirRe9T03kxl

What I learned: Chaining sort and uniq -u using pipelines to filter out duplicate data and isolate unique entries.

*******************************************************************

Bandit Level 9 → Level 10

Challenge:

    The password for the next level is stored in the file data.txt in one of the few human-readable strings

    It is preceded by several = characters

Solution:
Bash

strings data.txt | grep "==="

Explanation:

    strings data.txt extracts printable, human-readable character sequences from binary or data files

    | pipes the extracted strings directly to grep

    grep "===" filters the output for lines containing consecutive equal signs where the password is located

Password: B0s2khmbT9u0geKuOoVGW3JZKhndE3BG

What I learned: Using the strings command to extract human-readable text from non-plain-text binary or mixed-data files.

*******************************************************************

Bandit Level 10 → Level 11

Challenge:

    The password for the next level is stored in the file data.txt

    The file contains base64 encoded data

Solution:
Bash

base64 -d data.txt

Explanation:

    base64 is the standard Linux utility for encoding and decoding base64 data

    -d specifies the decode mode, reading the encoded string from data.txt and printing the plaintext output

Password: pYfOY6HwUsDj5rL9UvyhU7MCmv8vN5Ro

What I learned: How to decode Base64-encoded strings directly in the terminal using the base64 -d utility.

*******************************************************************

Bandit Level 11 → Level 12

Challenge:

    The password for the next level is stored in the file data.txt

    All lowercase and uppercase letters have been rotated by 13 positions (ROT13)

Solution:
Bash

cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

Explanation:

    cat data.txt outputs the obfuscated string

    tr (translate) performs character-by-character replacement

    'A-Za-z' 'N-ZA-Mn-za-m' shifts every letter 13 places forward in the alphabet to reverse the ROT13 cipher

Password: GROozWPO8QyN0mGrjUkID0WCYkZiQxrN

What I learned: Using the tr command for character substitution and reversing basic substitution ciphers like ROT13.

*******************************************************************

Bandit Level 12 → Level 13

Challenge:

    The password for the next level is stored in the file data.txt

    The file is a hexdump of a file that has been repeatedly compressed with multiple formats (gzip, bzip2, tar)

Solution:
Bash

 Create a temporary workspace
mkdir /tmp/bandit12_work && cd /tmp/bandit12_work
cp ~/data.txt .

 Convert hexdump back to binary
xxd -r data.txt > data.bin

 Inspect file type and decompress iteratively based on file format
file data.bin
 (Repeat checking with 'file' and decompressing with gzip -d, bzip2 -d, or tar -xf)

Explanation:

    xxd -r data.txt > data.bin reverses the original hexdump back into its underlying binary format

    file <name> identifies the exact compression algorithm at each stage

    Renaming the files to appropriate extensions (.gz, .bz2, .tar) allows tools like gzip, bzip2, and tar to decompress each layer until reaching plaintext

Password: qQYQiHOBPR8zR61qxYqX45quvihF2uzk

What I learned: Reversing hexdumps using xxd -r and peeling back nested compression formats iteratively with file, gzip, bzip2, and tar.

*******************************************************************

Bandit Level 13 → Level 14

Challenge:

    The password for the next level is stored in /etc/bandit_pass/bandit14

    Only user bandit14 can read it, but a private SSH key is provided in sshkey.private

Solution:

You must copy the private key from bandit13 and log out then create a file with the private key inside and then use the commands below
Bash

ssh -i key bandit14@localhost -p 2220
cat /etc/bandit_pass/bandit14

Explanation:

    ssh -i sshkey.private uses the provided private key to authenticate instead of a password

    localhost connects to the same server locally on port 2220

    cat /etc/bandit_pass/bandit14 retrieves the stored password once logged in as user bandit14

Password: aaWecNkG4FhxJQxz07uiwzVP6bJiYS65

What I learned: Using private SSH keys (ssh -i) for key-based authentication without relying on password logins.

*******************************************************************

Bandit Level 14 → Level 15

Challenge:

    The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost

Solution:
Bash

Using Netcat
nc localhost 30000
# (Paste the Bandit 14 password and press Enter)

Explanation:

    nc localhost 30000 opens a raw TCP network socket connection to port 30000 on the local machine

    Sending the Bandit 14 password over the established network socket returns the next password from the listening service

Password: pbLYuZtTg4MgaqfJx8jbA9gKKGqM68A7

What I learned: Interacting directly with network services and sending raw TCP payloads using nc (Netcat).

********************************************************************

Bandit Level 15 → Level 16

Challenge:

    The password for the next level can be retrieved by submitting the current level's password to port 30001 on localhost using SSL/TLS encryption

Solution:
Bash

openssl s_client -connect localhost:30001
(Paste the Bandit 15 password and press Enter)

Explanation:

    openssl s_client establishes an encrypted SSL/TLS connection to the target server

    -connect localhost:30001 specifies the encrypted port to connect to, handling the SSL handshake before transmitting the password

Password: kS0Hf0u5HiXFwKMKFqXvPdOTNGGa0X8V

What I learned: Connecting and communicating securely over SSL/TLS-encrypted ports using openssl s_client.

**********************************************************************

Bandit Level 16 → Level 17

Challenge:

    The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000.

    Find which port has a server listening on it and speaks SSL/TLS.

    Only one of them will respond with credentials (which will be an SSH private key).

Solution:
Bash

 1. Scan the port range to find open SSL services
nmap -p 31000-32000 --open -sV localhost

 2. Connect to the correct SSL port (e.g. port 31790) and send credentials
openssl s_client -quiet -connect localhost:31790
 (Paste Bandit 16 password and press Enter to receive the private RSA key)

3. Save the private key to a temporary directory and secure its permissions
mkdir -p /tmp/bandit17_key && cd /tmp/bandit17_key
nano key.private
chmod 600 key.private

 4. Connect to bandit17 using the key
ssh -i key.private bandit17@localhost -p 2220

Explanation:

    nmap -p 31000-32000 --open -sV localhost scans the port range to identify active listening services and detects which service speaks SSL.

    openssl s_client -quiet -connect localhost:<port> establishes an encrypted SSL handshake and sends the password.

    The server responds with an RSA private key instead of a password string.

    chmod 600 key.private sets read/write permissions for the current user only; SSH will reject private keys that are too permissive.

Password: pWXMAZoxGC8JmDMfmT5MGEsobMM3vnj2

What I learned: Port scanning with nmap, interacting with SSL/TLS services, and setting correct file permissions (chmod 600) to authenticate using an SSH private key.

**********************************************************************

Bandit Level 17 → Level 18

Challenge:

    There are two files in the home directory: passwords.old and passwords.new.

    The password for the next level is in passwords.new and is the only line that has been changed between the two files.

Solution:
Bash

diff passwords.old passwords.new --suppress-common-lines

Explanation:

    diff compares two files line by line and highlights the differences between them.

    Lines prefixed with < are unique to passwords.old, while lines prefixed with > show the changed/new entry in passwords.new.

    --suppress-common-lines only outputs the lines that are different between the two files

Password: OQxXZjELndr90zuhOTDYBEomI0SZITXI

What I learned: Comparing file modifications and tracking version changes using the diff utility.

**********************************************************************

Bandit Level 18 → Level 19

Challenge:

    The password for the next level is stored in a file named readme in the home directory.

    The .bashrc file has been modified to log you out immediately upon connecting via SSH.

Solution:
Bash

# Execute the command directly through SSH without spawning an interactive login shell
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

Explanation:

    Specifying a command (cat readme) at the end of the ssh command instructs the SSH daemon to run that single non-interactive command directly instead of launching an interactive login shell.

    Because an interactive shell is not initialized, the modified .bashrc script is bypassed, allowing standard output to return the file contents directly before the connection closes.

Password: KpsOfPkcP7i1FlIExk2QEjyt6dw8dxZI

What I learned: Bypassing restrictive login startup scripts by executing remote non-interactive commands directly via SSH.

**********************************************************************

Bandit Level 19 → Level 20

Challenge:

    To gain access to the next level, inspect the SetUID binary named bandit20-do located in the home directory.

    Find out how to use it to execute commands as user bandit20.

Solution:
Bash

ls -la
./bandit20-do cat /etc/bandit_pass/bandit20

Explanation:

    ls -la reveals that bandit20-do has the SetUID (SUID) bit set (-rwsr-x---), meaning the executable runs with the effective privileges of its owner (bandit20).

    Running ./bandit20-do <command> executes any provided command with the elevated permissions of bandit20, allowing direct read access to /etc/bandit_pass/bandit20.

Password: 4pIjcunZ0fK2vmp3IwfG8Vf7VhxD6pOA

What I learned: Understanding SUID (Set Owner User ID) binary permissions and how privilege elevation works in Unix systems.

**********************************************************************
