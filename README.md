# write-up-log
For cybersecurity

Level 0 linux/general- 
What it asked: Log into the game using SSH. Use this password to log into bandit1 using SSH.
What I tried: Going to the website link itself, which didn't work.
What worked: I was able to successfully connect to Bandit over SSH using the command ssh bandit0@bandit.labs.overthewire.org -p 2220. I also entered level 1.
What I learned: How to enter each level using SSH. 

Level 1 linux/general-
What it asked: The password for the next level is stored in a file called - located in the home directory
What I tried: Using the regular cat method to find the file didn't work.
What worked: Used the cat ./- command to find the password for level 2.
What I learned: What command to use when the file has a "-".
Assistant: I asked why the cat command didn't work, and it asked me if I had added ./ for "-" characters. 

Level 2 linux/general-
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
