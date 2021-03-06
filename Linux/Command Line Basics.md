Brief history
> During the formative years of the computer industry, one of the early operating systems was called Unix. It was designed to run as a multi-user system on mainframe computers, with users connecting to it remotely via individual _**terminals**_.
> ... Linux is a sort-of-descendent of Unix.
<hr>

#### `pwd` - Print Working Directory
#### `cd` - Change Directory

- relative paths
	- `cd ..` - move up to the parent directory 
	- `cd ../..` - move up through multiple levels of parent directory
	- `cd ../../etc` - move up and go straight to the etc directory
- absolute paths
	- `cd` - go to home directory
	- `cd /` - go to the root directory
	-  `cd /etc` ... - switch to the root directory, then follow the route from there 
	-  `cd ~/Desktop` ... - switch to the home directory, then follow the route from there 
#### `mkdir` - Make Directory
- `mkdir dir1 dir2 dir3`
	- dir1, dir2, dir3 are parameters/arguments
	- note: unix-systems are case-sensitive
- `mkdir -p dir4 dir5 dir6`
	- dir4 is made with dir5 in it that has dir6 in it
	- `-p` is an option/switch that, in this case, says to create **p**arent directories too
- `mkdir dir 7` - use escaping to create directory with space inside its name
#### Create files using redirection
- `ls > output.txt` - capture output of `ls` as a text file
- `cat ouput.txt` - look at the file's contents
- `echo "this is a test"` - prints the argument
- `echo "this is a test" > test_1.txt` - adds the argument inside a new text file
- to `cat` multiple text files, you can `cat test_?.txt` or `cat test_*`
- `cat t* > combined.txt` puts all the test files (or files that start with t) into one file
	- if you run that again, it will have same output, since shell clears out the file and restarts the process
- `cat t* >> combined.txt` will append to, rather than replace, the file content
	- `echo "i've appended a line!" >> combined.txt`
 
 #### `mv` - Move 
 - Into a directory:
 	`mv combined.txt dir1`
 - Out of a directory (back to parent directory):
 	`mv combined.txt ..` or `mv dir1/* .` (move all files in dir1 to current directory `.`)
 - Using more than one arguments (last argument is the destination directory and the rest are files being moved):
	`mv combined.txt test_* dir3 dir2`

#### Renaming 
`mv 1_combined.txt combined_1.txt` 

#### `cp` - Copy
`cp dir4/dir5/dir6/combined.txt .`
`cp combined.txt backup_combined.txt` (copy with a new name)

#### `rm`, `rmdir` - Remove/Delete
- Removing files:
	`rm dir4/dir5/dir6/combined.txt combined_backup.txt`
- Removing directories:
	`rmdir folder_*` - will only delete 1 empty directory
	`rmdir -p dir1/dir2/dir3` - will delete all empty directories including its parents
	`rmdir -r folder_6` - (recursive) will delete directory *and* all files in it (use with caution)
	
<hr>

#### `|` - Piping
- STDIN/STDOUT (standard input, standard output)

`ls ~ | wc -l`
- pipes out the output of first command into second; a temporary file is created
- the above command is the shortened version of this:
	```
	ls ~ > file_list.txt
	wc -l file_list.txt
	rm file_list.txt
	```
- to count the number lines in a file (while removing adjacent matching lines), you can:
	`cat combined.txt | uniq | wc -l`
`man uniq` - see instruction manual of the command; press `q` to quit
- `sort combined.text | less` to reorder lines (use `less` to view the file)

<hr>

