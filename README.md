# write-up-log
For cybersecurity

Level 0 linux/general 
What it asked: Log into the game using SSH. Use this password to log into bandit1 using SSH.
What I tried: Going to the website link itself, which didn't work.
What worked: I was able to successfully connect to Bandit over SSH using the command ssh bandit0@bandit.labs.overthewire.org -p 2220. I also entered level 1.
What I learned: How to enter each level using SSH. 

Level 1 linux/general
What it asked: The password for the next level is stored in a file called - located in the home directory
What I tried: Using the regular cat method to find the file didn't work.
What worked: Used the cat ./- command to find the password for level 2.
What I learned: What command to use when the file has a "-".
Assistant: I asked why the cat command didn't work, and it asked me if I had added ./ for "-" characters. 

Level 2 linux/general
What it asked: The password for the next level is stored in a file called --spaces in this filename-- located in the home directory
What I tried: Used the cat ./ method which didn't work because the file has spaces. 
What worked: Used cat "./--spaces in this filename--" to find the password for level 3.
What I learned: What to do for files that have spaces in them.
Assistant: I asked why the cat ./ method didn't work, and it asked me if I added quotation marks for the spaces. 


Level 3 Linux/General
What it asked: Find a password hidden inside a file within the inhere directory.
What I tried: Entering the inhere directory using cd and trying to look for a file using a normal ls command, which made the directory look empty.
What worked: Changing directories with cd inhere and using the ls -a command to list hidden files starting with a dot, then reading it with cat .hidden.
What I learned: Files starting with a dot are hidden by default in Linux, and you must use the -a flag with ls to see them.
Assistant: I asked why the directory looked empty, and it asked me if I checked for hidden files using flags. No command given.

Level 4 Linux/General
What it asked: Find the password hidden inside one of the many files within the inhere directory, where only one file contains human-readable ASCII text.
What I tried: Manually looking at the file names using ls, which all started with dashes like -file00 or -file01.
What worked: Using the file ./* command to scan all files simultaneously to check their types, finding the single one labeled ASCII text, and reading it using its explicit path cat ./-fileXX.
What I learned: The file command analyzes the content of files to determine their type, which saves time when wading through non-human-readable binary data.
Assistant: I asked how to tell which file was human-readable without opening all of them, and it asked me what command looks at a file's format instead of its contents. No command given.

Level 5 Linux/General
What it asked: Find a password hidden inside a file somewhere within the inhere directory that is human-readable, 1033 bytes in size, and not executable.
What I tried: Looking through the subdirectories manually, which was impossible because there were too many folders and files.
What worked: Using the find command with specific filters: find inhere/ -type f -size 1033c ! -executable to pinpoint the exact file path instantly, then using cat to read it.
What I learned: The find command can powerfully filter large directories based on specific properties like file size (c for bytes) and permissions (! -executable).
Assistant: I asked how to search for a specific file size across multiple folders, and it asked me what tool filters by size and parameters. No command given.


Level 6 Linux/General
What it asked: Find a password stored somewhere on the server that is owned by user bandit7, owned by group bandit6, and is exactly 33 bytes in size.
What I tried: Looking around the local home directory with ls -la, but finding no files there.
What worked: Using the root directory search tool find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null to locate the file, and then reading its path with cat.
Concept I learned: How to use global root searches (/) along with specific ownership attributes (-user, -group), and how to suppress permission errors using 2>/dev/null.
If I used my assistant: I asked why my root search was filling the screen with "Permission denied" errors, and it asked me how to redirect standard error outputs. No command given.


Level 7 Linux/General
What it asked: Find a password stored inside a large text file named data.txt next to the word millionth.
What I tried: Running cat data.txt, which instantly flooded the terminal with millions of lines of text and proved completely unreadable.
What worked: Utilizing pattern matching by running grep millionth data.txt to pull only the single line containing that specific keyword.
Concept I learned: The grep tool is essential for filtering down massive outputs or files to target specific string patterns.
If I used my assistant: I asked how to search for text inside a file without scrolling through thousands of lines, and it asked me what command is used to match strings and print lines. No command given.

Level 8 Linux/General
What it asked: Find a password hidden in data.txt that is unique and is the only line of text that occurs exactly once.
What I tried: Using uniq -u data.txt directly on the file, which returned absolutely nothing.
What worked: Piping the commands together by running sort data.txt | uniq -u to organize the file first before isolating the unique line.
Concept I learned: Small tools chained with pipes beat one clever command [image_A-otKS.png]; the deduplication tool uniq only filters neighboring lines, meaning data must be alphabetical via sort first to make it work [image_A-otKS.png].
If I used my assistant: I asked why my dedupe tool found nothing, and it asked me what order the file was in [image_A-otKS.png]. No command given.

Level 9 Linux/General
What it asked: Find a password stored in data.txt inside one of the few human-readable strings, preceded by several = characters.
What I tried: Trying to open the file with cat or grep, but the terminal output was glitched and unreadable due to massive amounts of raw binary data.
What worked: Extracting the text strings via strings data.txt | grep "==" to pull human-readable sequences containing the marker characters.
Concept I learned: The strings command prints sequences of printable characters from files, allowing you to easily view text embedded inside binary or non-printable outputs.
If I used my assistant: I asked how to clear out binary junk from a file to read hidden strings, and it asked me what utility strips unprintable sequences from code. No command given.

Level 10 Linux/General
What it asked: Find a password stored in data.txt that is encoded as base64 data.
What I tried: Using standard text tools, but the data looked like scrambled characters ending with = padding symbols.
What worked: Running the tool base64 -d data.txt to decode the contents directly back into plaintext data.
Concept I learned: Data encoding is not encryption; built-in command utilities like base64 can instantly decode strings when the pattern format is known.
If I used my assistant: I asked what a long string of letters and numbers ending in equal signs means, and it asked me what common binary-to-text decoding tool handles that syntax. No command given.


Level 11 Linux/General
What it asked: Find a password stored in data.txt where all lowercase and uppercase letters have been rotated by 13 positions (ROT13).
What I tried: Reading the file with cat, but the letters were scrambled into a nonsense cipher text.
What worked: Using the translation command tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt to shift the characters back by 13 places.
Concept I learned: The tr utility translates or deletes characters from standard input, making it easy to decode basic substitution ciphers like ROT13.
If I used my assistant: I asked how to automatically rotate characters in a file by a set offset, and it asked me what text manipulation command maps one set of characters to another. No command given.

Level 12 Linux/General
What it asked: Extract a password from data.txt, which is a text hexdump of a file that has been repeatedly compressed.
What I tried: Trying to decompress data.txt directly, but the file commands failed because it was formatted as text hex data instead of raw binary.
What worked: Reversing the hexdump using xxd -r data.txt > file, then repeatedly using file to check the compression type and running the corresponding tools Concept I learned: Multi-layered archive nesting requires step-by-step decoding, and xxd -r is the tool used to convert structural hex outputs back into a raw binary format.
If I used my assistant: I asked why my decompression tool said the file wasn't an archive, and it asked me how to convert text hexdumps back into binaries first. No command given.

Level 13 Linux/General
What it asked: Log in to the next level using an SSH private key stored in the home directory, since the password itself cannot be read directly.
What I tried: Attempting to cat /etc/bandit_pass/bandit14, but getting a "Permission denied" error because my current user lacked access.
What worked: Using the private key to authenticate an SSH session directly into the local host with ssh -i sshkey.private bandit14@localhost -p 2220.
Concept I learned: The -i flag in SSH tells the system to authenticate using a private key file instead of demanding an interactive text password.
If I used my assistant: I asked how to use a saved cryptographic key file to log in via terminal, and it asked me what parameter specifies an identity file in SSH. No command given.

Level 14 Linux/General
What it asked: Retrieve the password for the next level by submitting the current level's password to port 30000 on localhost.
What I tried: Running ssh or standard terminal commands against that specific port number, which rejected the connection.
What worked: Using a networking utility to establish a raw TCP connection via nc localhost 30000 and pasting the current bandit14 password into the open stream.
Concept I learned: Netcat (nc) is a powerful networking tool used to read from and write to raw network connections across specific TCP or UDP ports.• If I used my assistant: I asked how to send raw text data directly to a local network port, and it asked me what networking tool acts as an arbitrary data pipeline. No command given.

Level 15 Linux/General
What it asked: Retrieve the password for the next level by submitting the current password to port 30001 on localhost using SSL/TLS encryption.
What I tried: Using nc localhost 30001, which connected but immediately dropped the connection without a response when I sent the password because it lacked encryption.
What worked: Opening a secure, encrypted socket connection using openssl s_client -connect localhost:30001 and then pasting the current password.
Concept I learned: Regular netcat cannot handle SSL handshake protocols; you must use dedicated secure client utilities like openssl s_client for encrypted ports.
If I used my assistant: I asked why a network port kept closing immediately after I connected, and it asked me if the port required an encrypted TLS handshake instead of a raw connection. No command given.

PICOCTF CHALLENGES

Obedient Cat (General Skills)
What it asked: Download a file and retrieve the flag directly from its contents.
What I tried: Clicking the link to open the file in the browser, which displayed a raw block of text.
What worked: Downloading the file via the terminal and using the cat flag command to read the plaintext flag stored inside it.
Concept I learned: Basic file retrieval and viewing in a terminal environment using standard output utilities.
If I used my assistant: I asked how to look at the text inside a downloaded file without using a heavy text editor, and it asked me what core command concatenates and prints file contents to the screen. No command given.

Python Wrangling (General Skills)
What it asked: Run a Python script to decrypt a file using a provided password file.
What I tried: Running the Python script directly without any arguments, which just printed a help/usage menu.
What worked: Executing the script with the decryption flag and input arguments (python3 ende.py -d flag.txt.en) and pasting the password found inside pw.txt when prompted.
Concept I learned: How to pass flags and command-line arguments into Python scripts to control execution parameters.
If I used my assistant: I asked why the script didn't automatically find the password file in the folder, and it asked me how to supply arguments to a terminal application based on its help menu. No command given.


Mod 26 (Crypto)
What it asked: Decode a cryptography string formatted with a ROT13 cipher.
What I tried: Reading the string manually, which looked like an alphabet soup variant of the standard flag format.
What worked: Passing the scrambled flag through a ROT13 translation utility to shift every letter forward by 13 positions in the alphabet.
Concept I learned: ROT13 is a simple symmetric substitution cipher that rotates letters by half the alphabet size, meaning repeating the rotation decodes it.
If I used my assistant: I asked what "Mod 26" meant in the context of letter shifts, and it asked me how many letters are in the standard alphabet and what cipher uses a 13-step rotation. No command given.

The Numbers (Crypto)
What it asked: Decrypt a flag hidden behind a sequence of numbers separated by brackets and dashes.
What I tried: Looking for mathematical patterns or equations to solve the numbers sequentially.
What worked: Mapping each individual integer directly to its corresponding position in the alphabet (where 1 = A, 2 = B, 3 = C, etc.) to reveal the flag text.
Concept I learned: An A1Z26 cipher is an elementary substitution method where letters are directly represented by their standard numeric indexes.
If I used my assistant: I asked how to decode numbers that start with patterns matching the standard flag format, and it asked me to look at the first few numbers and see if they match the positions of the letters P-I-C-O. No command given.


Glory of the Garden (Forensics)
What it asked: Find a hidden flag inside an image file named garden.jpg.
What I tried: Opening the picture in a traditional image viewer to look for hidden text written or hidden visually on the screen.
What worked: Running strings garden.jpg to read the underlying text data and finding the plaintext flag hidden at the very end of the file.
Concept I learned: Data can be appended directly to the end of image files without corrupting the rendering headers, concealing plain text from standard image applications.
If I used my assistant: I asked how text can exist inside a picture file, and it asked me what tool reveals printable characters hidden outside an image's pixel matrix. No command given.

information (Forensics)
What it asked: Retrieve a flag hidden inside an image file called cat.jpg.
What I tried: Inspecting the file size or running standard text lookups, which resulted in a massive wall of unhelpful data.
What worked: Running exiftool cat.jpg to check the image's embedded metadata properties, isolating a weird base64 string in the license field, and decoding it.
Concept I learned: Metadata tags (EXIF data) embedded inside media files can be easily manipulated to store covert tracking strings or encoded data payloads.
If I used my assistant: I asked where files keep structural details like camera types and copyright info, and it asked me what tool extracts metadata properties from image files. No command given.

So Meta (Forensics)
What it asked: Find a flag embedded inside the metadata parameters of an image file.
What I tried: Opening the image and looking at its properties via a basic file manager, which showed nothing out of the ordinary.
What worked: Running an metadata analyzer tool (exiftool pico_img.png) to pull the full list of operational tags, revealing the flag string directly embedded inside a custom property tag.
Concept I learned: File headers contain distinct structural entries that can act as key-value text slots for hiding arbitrary strings or identifiers.
If I used my assistant: I asked how this challenge differs from previous image files, and it asked me if I had scanned the descriptive header tags using specialized inspection tools yet. No command given.

Matryoshka doll (Forensics)
What it asked: Extract a flag hidden inside a series of nested image layers.
What I tried: Running basic text extractions, which only showed hints of alternative files buried deeper inside the image architecture.
What worked: Using an automatic file extraction script via binwalk -e repeatedly on each newly uncovered image file until navigating to the final embedded directory containing flag.txt.
Concept I learned: Nested file systems can overlay storage layers inside a single file container by placing distinct archive signatures inside raw data segments.
If I used my assistant: I asked why the extracted folder just contained another picture, and it asked me what happens if you apply an automated carving tool recursively to sub-files. No command given.
