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



*******************************************************************



*******************************************************************



*******************************************************************




*******************************************************************




*******************************************************************
