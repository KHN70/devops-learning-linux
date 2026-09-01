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

# Create a temporary workspace
mkdir /tmp/bandit12_work && cd /tmp/bandit12_work
cp ~/data.txt .

# Convert hexdump back to binary
xxd -r data.txt > data.bin

# Inspect file type and decompress iteratively based on file format
file data.bin
# (Repeat checking with 'file' and decompressing with gzip -d, bzip2 -d, or tar -xf)

Explanation:

    xxd -r data.txt > data.bin reverses the original hexdump back into its underlying binary format

    file <name> identifies the exact compression algorithm at each stage

    Renaming the files to appropriate extensions (.gz, .bz2, .tar) allows tools like gzip, bzip2, and tar to decompress each layer until reaching plaintext

Password: [password here]

What I learned: Reversing hexdumps using xxd -r and peeling back nested compression formats iteratively with file, gzip, bzip2, and tar.

*******************************************************************
