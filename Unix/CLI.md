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


 `whoami` - Show My Username