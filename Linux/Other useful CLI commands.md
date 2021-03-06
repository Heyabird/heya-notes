#### `whoami` - Show My Username

#### `echo`
- `echo $USER`
- `echo $HOME`
- `echo $PATH`

####  **superuser** = machine's administrator
- `su` - superuser or switch user (*dont use*)
	- with no argument, switch to the root user
	- with argument, switch to a specific user
	- `logout` (or ctrl+D) to return to user-level account
- `sudo` - "**s**witch **u**ser and **do** this command" (*use with caution*)
	- user is prompoted for their own pw, which is then cached for some time (default 15 min
	- on Ubuntu the first user created when the system is installed is considered to be the superuser)
- `sudo apt-get ...` (for Ubuntu)
	- apt = advanced packaging tool 
	
<hr>

#### Hidden Files / Folders
- usually used to store settings and config data
- start the name with a `.` to make it disappear
	`mv combined.txt .combined.txt`
- to view, you can `ls -a` to view everything including hidden things
	- notice that `.` and `..` also appear as though they're real directories

<hr>

#### Permissions
Hit `ls -l`. See the phrase on the leftmost side.
Example: `-rwxrwxrwx`
- if the first character is `-` then it is file, and if the first character is `d` it is a directory
- The rest are three sets of three characters
	- The first three letters represent the file permissions of the *owner*
	- The second three letters represent the file permissions of the *group*
	- The last three letters represent the file permissions for *others*
	- If `r`,`w`, or `x`, the file permission is granted; if not, (and instead `-`), the file permission is denied
		- `r`: read
		- `w`: write
		- `x`: execute
#### `chmod` = change mode
- One way to use `chmod` is to provide the permissions you wish to give to the owner, group, and others as a 3 digit number.
- ex: `chmod -R 765 example.txt`
	-   **0:** No permission
	-   **1:** Execute permission
	-   **2:** Write permission
	-   **3:** Write and execute permissions
	-   **4:** Read permission
	-   **5:** Read and execute permissions
	-   **6:** Read and write permissions
	-   **7:** Read, write and execute permissions

#### `curl`
-  retrieve info/files from URLs or internet addresses

#### `grep`
- `grep train *.txt` searches for the word 'train' in all text files in current directory 

#### `ps`
- lists running processes

#### Killing Ports
- `ps aux | grep playground`
- `kill -9 <PID>`

####
