---
title: "Essential Linux Commands"
published: 2025-09-01
draft: false
toc: true
description: "A compilation of essential Linux commands to get you started"
series: 'Linux'
tags: ['cli', 'bash']
---

All these commands works in bash and should cover the majority of your needs. This tools are installed by default in most Linux distributions.

## Documentation
Get the knowledge directly from the command line.

### man
The only command needed to understand all of them. Shows options, usage patterns and examples.

```bash

man mv

man ls

man -k search_term  # search for commands containing keyword

```

## Move around
Find your way in the filesystem.

### pwd
Prints current working directory path. Essential for knowing your location in the filesystem.

```bash
pwd                  # Output : /home/username/documents
```

### cd
Move around directories. Navigate through the filesystem by changing your current location. In recent version of bash you don't even have to use CD, you can just type the directory name.

```bash
cd /home/user        # go to specific path
cd ..                # go up one level
cd ~                 # go to home directory
cd -                 # go back to previous directory
cd                   # go to home directory (shortcut)

my_folder            # go to my_folder
```

### ls
List files and folders inside the current directory. Shows what's available in your current location.

```bash
ls                     # basic listing
ls -l                  # detailed list with permissions, size, date
ls -la                 # include hidden files (starting with .)
ls -lh                 # human readable file sizes
ls *.txt               # list all files with .txt extension
```

## Manipulate files and folder

### touch
Create an empty file or update timestamp of existing file. Quick way to create new files.

```bash
touch newfile.txt
touch file1.txt file2.txt file3.txt
```

### mkdir
Create new directories. Build folder structure for organizing files.

```bash
mkdir newfolder
mkdir folder1 folder2 folder3
mkdir -p path/to/deep/folder       # use -p also to avoid errors if folder exists
mkdir -p project/{src,docs,tests}
```

### mv
Move files/folders to new location or rename them.

```bash
mv oldname.txt newname.txt           # rename file
mv file.txt /path/to/destination/    # move file to another directory
mv folder/ /new/location/            # move entire folder
mv *.txt documents/                  # move all .txt files to documents folder
```

### rm
Delete files and directories permanently. Be careful - there's no trash/recycle bin in terminal.

```bash
rm file.txt                          # delete single file
rm file1.txt file2.txt               # delete multiple files
rm -r folder/                        # delete folder and all contents recursively
rm -rf dangerous_folder/             # force delete without confirmation
rm *.tmp                             # delete all .tmp files
```

## Manipulate text

### echo
Print text to terminal output. Display messages, variables, or create simple text content.

```bash
echo "Hi mom !"                      # print simple text
echo "Hello $USER"                   # print with variable
echo -n "No newline"                 # print without newline at end
echo "Line 1\nLine 2"                # print with newline characters

```

### cat
Print entire content of file(s) to terminal. View file contents or combine multiple files.

```bash
cat file.txt                         # display file content
cat file1.txt file2.txt              # display multiple files
cat -n file.txt                      # display with line numbers
cat > newfile.txt                    # create file and type content (Ctrl+D to save)
```

### cut
Extract specific columns or fields from text. Useful for processing structured data like CSV files.

```bash
cut -d',' -f2 data.csv               # extract 2nd column from CSV
cut -d':' -f1,3 /etc/passwd          # extract 1st and 3rd fields
cut -c1-5 file.txt                   # extract characters 1-5 from each line
echo "a,b,c,d" | cut -d',' -f2-4     # extract columns 2 to 4
```

### sort
Sort lines of text alphabetically or numerically. Organize data in readable order.

```bash
sort file.txt                        # alphabetical sort
sort -n numbers.txt                  # numerical sort
sort -r file.txt                     # reverse sort
sort -u file.txt                     # sort and remove duplicates
sort -k2 data.txt                    # sort by 2nd column
```

### tr
Replace or transform characters in text stream. Modify text by substituting characters.

```bash
echo "hello" | tr 'l' 'x'            # replace 'l' with 'x'
echo "HELLO" | tr 'A-Z' 'a-z'        # convert to lowercase
echo "hello world" | tr ' ' '_'      # replace spaces with underscores
echo "abc123" | tr -d '0-9'          # delete all numbers
```

### wc
Count lines, words and characters in files. Get statistics about text content.

```bash
wc file.txt                          # show lines, words, characters
wc -l file.txt                       # count only lines
wc -w file.txt                       # count only words
wc -c file.txt                       # count only characters
echo "hello world" | wc -w           # count words in string
```

### awk
Perform text manipulation and data extraction. Nice when the text looks like a table.

```bash
awk '{print $1}' file.txt                   # print first column
awk '{print $NF}' file.txt                  # print last column
awk '{sum += $3} END {print sum}' file.txt  # sum all values in column 3

# Calculate average of numbers in second column
awk '{sum += $2; count++} END {print sum/count}' numbers.txt

# Print lines longer than 80 characters
awk 'length > 80' file.txt
```

### sed
Similar to awk, more suitable for complex replacements based on regex.

```bash
sed 's/old/new/g' file.txt   # replace all occurrences of "old" with "new"
sed '/pattern/d' file.txt    # delete lines matching pattern
sed 's/^#.*$//' file.txt     # remove comments from shell scripts
sed '1,3d' file.txt          # delete lines 1 to 3
sed 's/ /\n/g' file.txt      # replace spaces with newlines
```

## System commands

### whoami
Print name of the current user. Identify which user account you're currently using.

```bash
whoami                               # shows current username
```

### ps aux
Print currently running processes with detailed information. Monitor what's running on your system.


```bash
ps aux                              # show all processes
ps aux | grep firefox               # find specific process
ps -ef                              # alternative format
ps -u username                      # show processes for specific user
```

### kill

Stop a running process by sending termination signals. End unresponsive or unwanted programs.

```bash
kill 1234                           # terminate process with ID 1234
kill -9 1234                        # force kill (SIGKILL)
kill -15 1234                       # graceful termination (SIGTERM)
killall firefox                     # kill all firefox processes
```

### df
Show disk space usage for mounted filesystems. Monitor available storage space.

```bash
df                                   # show disk usage
df -h                                # human readable sizes (GB, MB)
df -h /home                          # check specific directory
df -i                                # show inode usage
```

### printenv
Print one or all environment variables. Useful for debugging and checking configuration.

```bash
printenv HOME
printenv
```

### history
Check previously executed commands. Review and reuse your command history.

```bash
history                              # show all command history
history | tail -10                   # show last 10 commands
history | grep "git"                 # search for git commands in history
!123                                 # re-run command number 123
!!                                   # re-run last command
```

### ip a
Find network interface information including IP addresses. Check your network configuration.

```bash
ip a                                 # show all network interfaces
ip addr show                         # alternative syntax
ip a show eth0                       # show specific interface
ip route                             # show routing table
```


### curl
Make HTTP requests to web servers. Download content, test APIs, or check website status.

```bash
curl www.google.com                            # get webpage content
curl -I www.google.com                         # get only headers
curl -o page.html www.example.com              # save response to file
curl -X POST -d "data=value" api.com           # send POST request with data
curl -s https://api.github.com/users/octocat   # silent mode (no progress)

```

## Redirections

### >
Send command output to file, replacing existing content. Redirect output to create or overwrite files.

```bash
echo "Hello" > file.txt              # create file with content
ls > filelist.txt                    # save directory listing to file
cat file1.txt > copy.txt             # copy file content to new file
date > timestamp.txt                 # save current date to file
```

### >>
Send command output to file, appending to existing content. Add output to end of existing files.

```bash
echo "New line" >> file.txt          # add line to existing file
ls >> filelist.txt                   # append directory listing
cat file2.txt >> combined.txt        # append file content
date >> log.txt                      # append timestamp to log
```

### |
Send output from one command as input to the next command. Chain commands together for complex operations.

```bash
cat logs.txt | wc -l                 # count lines in file
ls -la | grep "txt"                  # list only .txt files
ps aux | grep firefox                # find firefox processes
cat data.csv | cut -d',' -f2 | sort  # extract column, then sort
```

### xargs
Pass output as arguments to another command. Convert input into command arguments.

```bash
find . -name "*.txt" | xargs rm         # find and delete all .txt files
echo "file1 file2 file3" | xargs touch  # create multiple files
ls *.txt | xargs -I {} cp {} backup/    # copy each file to backup folder
cat filelist.txt | xargs grep "error"   # search for "error" in listed files
```

## Wildcards
### *
Match zero or more characters. Select multiple files with pattern matching.

```bash
ls *.txt                             # list all .txt files
rm temp*                             # delete files starting with "temp"
cp /path/*.jpg images/               # copy all jpg files
echo file*.log                       # expand to matching filenames
```

### ?
Match exactly one character. Precise single-character pattern matching.
```bash
ls file?.txt                         # match file1.txt, fileA.txt, etc.
rm temp?.log                         # delete temp1.log, tempX.log, etc.
cp image?.png backup/                # copy image1.png, imageA.png, etc.
```

### [1-2]
Match any character within the specified range or set. Define specific character alternatives.

```bash
ls file[1-5].txt                     # match file1.txt through file5.txt
rm log[ABC].txt                      # delete logA.txt, logB.txt, logC.txt
cp data[0-9][0-9].csv archive/       # match data01.csv, data99.csv, etc.
ls [a-z]*.txt                        # files starting with lowercase letter
```

## Utils

### apt
To install packages on Debian-based systems.

```bash
sudo apt update                # update package list
sudo apt install package_name  # install a package
sudo apt remove package_name   # remove a package
```

### crontab
Schedule recurring tasks with cron.

```bash
crontab -e                            # edit crontab
crontab -l                            # list current cron jobs
crontab -r                            # remove all cron jobs
```

### date
Print the current date and time.

```bash
date               # mar. 02 sept. 2025 15:44:52 CEST
date -u            # mar. 02 sept. 2025 13:44:52 UTC
date +"%Y-%m-%d"   # 2025-09-02
```

### free
Display information about system memory usage.

```bash
free               # display memory usage
free -h            # display memory usage in human-readable format
```

### du
Check size of a folder

```bash
du -sh /folder
```

## Path manipulation

### basename
Get the filename from a full path.

```bash
basename /path/to/file.txt         # Output: file.txt
basename /path/to/file.txt .txt    # Output: file
```

### realpath
Get the absolute path of a file or directory.

```bash
realpath file.txt                   # Output: /full/path/to/file.txt
realpath ../relative/path           # Output: /full/path/to/relative/path
```