# Linux-Command-Line

1. cat: used to type out a file (or combine files)
2. head: used to show the first few lines of a file
3. tail: used to show the last few lines of a file
4. man: used to view documentation.

cat	Used for viewing files that are not very long; it does not provide any scroll-back.
tac	Used to look at a file backwards, starting with the last line.
less	Used to view larger files because it is a paging program; it pauses at each screen full of text, provides scroll-back capabilities, and lets you search and navigate within the file. Note: Use / to search for a pattern in the forward direction and ? for a pattern in the backward direction. (An older program named more is still used, but has fewer capabilities.)
tail	Used to print the last 10 lines of a file by default. You can change the number of lines by doing -n 15 or just -15 if you wanted to look at the last 15 lines instead of the default.
head	The opposite of tail; by default, it prints the first 10 lines of a file.
mv	Rename a file 
rm	Remove a file 
rm –f	Forcefully remove a file
rm –i	Interactively remove a file

sudo shutdown -h 10:00 "Shutting down for scheduled maintenance."

sudo shutdown -r 10:00 "Reboot for scheduled maintenance."

which diff

pwd	Displays the present working directory
cd ~ or cd	Change to your home directory (short-cut name is ~ (tilde))
cd ..	Change to parent directory (..)
cd -	Change to previous directory (- (minus))

cd /	Changes your current directory to the root (/) directory (or path you supply)
ls	List the contents of the present working directory
ls –a	List all files including hidden files and directories (those whose name start with . )
tree	Displays a tree view of the filesystem


ls -li file1 file2

Suppose that file1 already exists. A hard link, called file2, is created with the command:

ln file1 file2

$ ln -s file1 file3
$ ls -li file1 file3

Notice file3 no longer appears to be a regular file, and it clearly points to file1 and has a different inode number.

pushd .
popd 

to work with directories


$ touch <filename>

This is normally done to create an empty file as a placeholder for a later purpose.

touch provides several options, but here is one of interest:

The -t option allows you to set the date and time stamp of the file.
To set the time stamp to a specific time:
$ touch -t 03201600 myfile

mv	Rename a directory
rmdir	Remove an empty directory
rm -rf	Forcefully remove a directory recursively

I/O Redirection

Through the command shell we can redirect the three standard file streams so that we can get input from either a file or another command instead of from our keyboard, and we can write output and errors to files or send them as input for subsequent commands.

For example, if we have a program called do_something that reads from stdin and writes to stdout and stderr, we can change its input source by using the less-than sign ( < ) followed by the name of the file to be consumed for input data:

$ do_something < input-file

If you want to send the output to a file, use the greater-than sign (>) as in:

$ do_something > output-file

Because stderr is not the same as stdout, error messages will still be seen on the terminal windows in the above example.

If you want to redirect stderr to a separate file, you use stderr’s file descriptor number (2), the greater-than sign (>), followed by the name of the file you want to hold everything the running command writes to stderr:

$ do_something 2> error-file

A special shorthand notation can be used to put anything written to file descriptor 2 (stderr) in the same place as file descriptor 1 (stdout): 2>&1

$ do_something > all-output-file 2>&1

bash permits an easier syntax for the above:

$ do_something >& all-output-file

$ locate zip | grep bin

sudo updatedb
locate test1.txt


? 	Matches any single character
*	Matches any string of characters
[set]	Matches any character in the set of characters, for example [adf] will match any occurrence of "a", "d", or "f"
[!set]	Matches any character not in the set of characters

Searching for files and directories named "gcc":

$ find /usr -name gcc

Searching only for directories named "gcc":

$ find /usr -type d -name gcc

Searching only for regular files named "gcc":

$ find /usr -type f -name gcc

To find and remove all files that end with .swp:

$ find -name "*.swp" -exec rm {} ’;’

One can also use the -ok option, which behaves the same as -exec, except that find will prompt you for permission before executing the command. 

$ find / -ctime 3

Here, -ctime is when the inode metadata (i.e., file ownership, permissions, etc.) last changed; it is often, but not necessarily, when the file was first created. You can also search for accessed/last read (-atime) or modified/last written (-mtime) times. The number is the number of days and can be expressed as either a number (n) that means exactly that value, +n, which means greater than that number, or -n, which means less than that number. There are similar options for times in minutes (as in -cmin, -amin, and -mmin).

To find files based on sizes:

$ find / -size 0

Note the size here is in 512-byte blocks, by default; you can also specify bytes (c), kilobytes (k), megabytes (M), gigabytes (G), etc. As with the time numbers above, file sizes can also be exact numbers (n), +n or -n. For details, consult the man page for find.

For example, to find files greater than 10 MB in size and running a command on those files:

$ find / -size +10M -exec command {} ’;’

