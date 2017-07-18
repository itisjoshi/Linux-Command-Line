# Linux-Command-Line

Must know Commands

## File operations

```javascript
cat	Used for viewing files that are not very long; it does not provide any scroll-back.
tac	Used to look at a file backwards, starting with the last line.
less	Used to view larger files because it is a paging program; it pauses at each screen full of text, provides scroll-back capabilities, and lets you search and navigate within the file. Note: Use / to search for a pattern in the forward direction and ? for a pattern in the backward direction. (An older program named more is still used, but has fewer capabilities.)
tail	Used to print the last 10 lines of a file by default. You can change the number of lines by doing -n 15 or just -15 if you wanted to look at the last 15 lines instead of the default.
head	The opposite of tail; by default, it prints the first 10 lines of a file.
```

```javascript
mv	Rename a file 
rm	Remove a file 
rm –f	Forcefully remove a file
rm –i	Interactively remove a file
```

```javascript
pwd	Displays the present working directory
cd ~ or cd	Change to your home directory (short-cut name is ~ (tilde))
cd ..	Change to parent directory (..)
cd -	Change to previous directory (- (minus))
```

```javascript
cd /	Changes your current directory to the root (/) directory (or path you supply)
ls	List the contents of the present working directory
ls –a	List all files including hidden files and directories (those whose name start with . )
tree	Displays a tree view of the filesystem
```

> ls -li file1 file2

Suppose that file1 already exists. A hard link, called file2, is created with the command:

> ln file1 file2

> ln -s file1 file3
> ls -li file1 file3

Notice file3 no longer appears to be a regular file, and it clearly points to file1 and has a different inode number.

```javascript
pushd .
popd 
```
To work with directories parellely

> touch <filename>

This is normally done to create an empty file as a placeholder for a later purpose.

touch provides several options, but here is one of interest:

The -t option allows you to set the date and time stamp of the file.
To set the time stamp to a specific time:

> touch -t 03201600 myfile

```javascript
mv	Rename a directory
rmdir	Remove an empty directory
rm -rf	Forcefully remove a directory recursively
```

> sudo shutdown -h 10:00 "Shutting down for scheduled maintenance."

> sudo shutdown -r 10:00 "Reboot for scheduled maintenance."

> which diff

## I/O Redirection

Through the command shell we can redirect the three standard file streams so that we can get input from either a file or another command instead of from our keyboard, and we can write output and errors to files or send them as input for subsequent commands.

For example, if we have a program called do_something that reads from stdin and writes to stdout and stderr, we can change its input source by using the less-than sign ( < ) followed by the name of the file to be consumed for input data:

> do_something < input-file

If you want to send the output to a file, use the greater-than sign (>) as in:

> do_something > output-file

Because stderr is not the same as stdout, error messages will still be seen on the terminal windows in the above example.

If you want to redirect stderr to a separate file, you use stderr’s file descriptor number (2), the greater-than sign (>), followed by the name of the file you want to hold everything the running command writes to stderr:

> do_something 2> error-file

A special shorthand notation can be used to put anything written to file descriptor 2 (stderr) in the same place as file descriptor 1 (stdout): 2>&1

> do_something > all-output-file 2>&1

bash permits an easier syntax for the above:

> do_something >& all-output-file

## Search

> locate zip | grep bin


```javascript
sudo updatedb
locate test1.txt
```

? 	Matches any single character
*	Matches any string of characters
[set]	Matches any character in the set of characters, for example [adf] will match any occurrence of "a", "d", or "f"
[!set]	Matches any character not in the set of characters

Searching for files and directories named "gcc":

> find /usr -name gcc

Searching only for directories named "gcc":

> find /usr -type d -name gcc

Searching only for regular files named "gcc":

> find /usr -type f -name gcc

To find and remove all files that end with .swp:

> find -name "*.swp" -exec rm {} ’;’

One can also use the -ok option, which behaves the same as -exec, except that find will prompt you for permission before executing the command. 

> find / -ctime 3

Here, -ctime is when the inode metadata (i.e., file ownership, permissions, etc.) last changed; it is often, but not necessarily, when the file was first created. You can also search for accessed/last read (-atime) or modified/last written (-mtime) times. The number is the number of days and can be expressed as either a number (n) that means exactly that value, +n, which means greater than that number, or -n, which means less than that number. There are similar options for times in minutes (as in -cmin, -amin, and -mmin).

To find files based on sizes:

> find / -size 0

Note the size here is in 512-byte blocks, by default; you can also specify bytes (c), kilobytes (k), megabytes (M), gigabytes (G), etc. As with the time numbers above, file sizes can also be exact numbers (n), +n or -n. For details, consult the man page for find.

For example, to find files greater than 10 MB in size and running a command on those files:

> find / -size +10M -exec command {} ’;’


```javascript
 apt-get install
 apt-cache 
 dpkg --install foo.deb
 apt-get upgrade
```

```javascript
 man -f
 man -k
 man --help
```
> kill -SIGKILL <pid> or kill -9 <pid>
 
> info <topic name>

```javascript
  w
  top
  uptime
```

> jobs -l
  
 add & to run process in background
 
 ```javascript
 ps -ef
 ps -eLf
 
 ps aux
 pstree
 
 /etc/crontab 
 crontab -e
 ```
 
> sleep

```javascript
tar xvf mydir.tar	Extract all the files in mydir.tar into the mydir directory
tar zcvf mydir.tar.gz mydir	Create the archive and compress with gzip
tar jcvf mydir.tar.bz2 mydir	Create the archive and compress with bz2
tar Jcvf mydir.tar.xz mydir	Create the archive and compress with xz
tar xvf mydir.tar.gz	Extract all the files in mydir.tar.gz into the mydir directory. Note you do not have to tell tar it is in gzip format.
```

```javascript
echo line one > myfile

cat << EOF > myfile
> line one
> line two
> line three
> EOF
```

## nano

nano  is easy to use, and requires very little effort to learn. To open a file in nano, type nano <filename> and press Enter.  If the file does not exist, it will be created.

nano provides a two line “shortcut bar” at the bottom of the screen that lists the available commands. Some of these commands are:

```javascript
CTRL-G: Display the help screen
CTRL-O: Write to a file
CTRL-X: Exit a file
CTRL-R: Insert contents from another file to the current buffer
CTRL-C: Cancels previous commands.
```

## Modes in vi

Mode	Feature
Command	
By default, vi starts in Command mode.
Each key is an editor command.
Keyboard strokes are interpreted as commands that can modify file contents.
Insert	
Type i to switch to Insert mode from Command mode.
Insert mode is used to enter (insert) text into a file.
Insert mode is indicated by an “? INSERT ?” indicator at the bottom of the screen.
Press Esc to exit Insert mode and return to Command mode.
Line	
Type : to switch to the Line mode from Command mode. Each key is an external command, including operations such as writing the file contents to disk or exiting.
Uses line editing commands inherited from older line editors. Most of these commands are actually no longer used. Some line editing commands are very powerful.
Press Esc to exit Line mode and return to Command mode.

```javascript
vi myfile	Start the vi editor and edit the myfile file
vi -r myfile	Start vi and edit myfile in recovery mode from a system crash
:r file2	Read in file2 and insert at current position
:w	Write to the file
:w myfile	Write out the file to myfile
:w! file2	Overwrite file2
:x or :wq	Exit vi and write out modified file
:q	Quit vi
:q!	Quit vi even though modifications have not been saved
```

```javascript
arrow keys	To move up, down, left and right
j or <ret>	To move one line down
k	To move one line up
h or Backspace	To move one character left
l or Space	To move one character right
0	To move to beginning of line
$	To move to end of line
w	To move to beginning of next word
:0 or 1G	To move to beginning of file
:n or nG	To move to line n
:$ or G	To move to last line in file
CTRL-F or Page Down	To move forward one page
CTRL-B or Page Up	To move backward one page
^l	To refresh and center screen
```

```javascript
/pattern	Search forward for pattern
?pattern	Search backward for pattern
```

```javascript
n	Move to next occurrence of search pattern
N	Move to previous occurrence of search pattern
```

```javascript
a	Append text after cursor; stop upon Escape key
A	Append text at end of current line; stop upon Escape key
i	Insert text before cursor; stop upon Escape key
I	Insert text at beginning of current line; stop upon Escape key
o	Start a new line below current line, insert text there; stop upon Escape key
O	Start a new line above current line, insert text there; stop upon Escape key
r	Replace character at current position
R	Replace text starting with current position; stop upon Escape key
x	Delete character at current position
Nx	Delete N characters, starting at current position
dw	Delete the word at the current position
D	Delete the rest of the current line
dd	Delete the current line
Ndd or dNd	Delete N lines
u	Undo the previous operation
yy	Yank (copy) the current line and put it in buffer
Nyy or yNy	Yank (copy) N lines and put it in buffer
p	Paste at the current position the yanked line or lines from the buffer.
```

```javascript
chown	Used to change user ownership of a file or directory
chgrp	Used to change group ownership
chmod	Used to change the permissions on the file, which can be done separately for owner, group and the rest of the world (often named as other.)
```

```javascript
ethtool	Queries network interfaces and can also set various parameters such as the speed.
netstat	Displays all active connections and routing tables. Useful for monitoring performance and troubleshooting.
nmap	Scans open ports on a network. Important for security analysis
tcpdump	Dumps network traffic for analysis.
iptraf	Monitors network traffic in text mode.
mtr	Combines functionality of ping and traceroute and gives a continuously updated display.
dig	Tests DNS workings. A good replacement for host and nslookup.
```

> scp <localfile> <user@remotesystem>:/home/user/
