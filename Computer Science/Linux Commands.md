# Terminal
## pwd
Prints the [[Current Working Directory]].
## cd
Changes the [[Current Working Directory]].
## ls
**Lists** files in a given location.
### Options
- `-a` / `--all` : Show files starting with `.` (hidden files).
- `-A` / `--almost-all` : Same as `-a`, without `.` and `..` directories.
- `-h` / `--human-readable` : Print file sizes in kilobytes, mega, giga etc...
- `-l` : Table (long) listing format.
- `-r`  / `--reverse` : Reverse order while sorting.
- `-t` : Sort by time, newest first.
- `-X` : Sort by file extension. Alphabetical.
# File Handling
## cp
**Copies** files.
## mv
**Move (rename)** files.
### Usage
`mv <source file> <new path>`
This "new path" can either be the same name at a different location in the file system, or just a new name to rename the file and keep it in the [[Current Working Directory]].
You can also combine both to rename something AND move it to a different location.
### Option
- `-f` / `--force` : Doesn't prompt when overwriting a file at the destination.
- `-i` / `--interactive` : Prompt when overwriting a file at the destination.
- `-v` / `--verbose` : Print information on what's happening.
## rm
**Removes** given files.
### Options
- `-i` : Prompts before deleting each file.
- `-v` : Prints what's happening and which files are being deleted.
## find
As the name suggests, **this command can be used to easily find files on a linux filesystem**.
### Usage
```sh
find [-H] [-L] [-P] [-D debugopts] [-0level] [starting-point...] [expression]

$> find -name file_to_search  # Search for a file_to_search file
$> find -name *.txt  # Search all files ending with .txt
```
## chown
Changes the **owner of a file**.
### Usage
```sh
chown user[:group] [files]

chown user:group file1 file2 file3
chown -R user:group file1 file2 file3  # Change owners/groups recursively
```
## mkdir
Creates a directory.
### Usage
```sh
mkdir directory...

mkdir -p path/to/directory  # Create all layers of directories as needed
```
# Process Management
## ps
Allows to **see running processes in the current user session**.
### Usage
```sh
ps  # See current session's processes
ps aux  # See running system processes
```
## jobs
**Lists currently running jobs**.
## fg
Allows you to **resume a stopped [[Process]]** and bring it back to the **foreground**.
Can take multiple job numbers to resume multiple jobs.
### Usage
```sh
fg [PROCESS...]

$> fg 1  # Puts background job 1 to foreground
```
# Other
## grep
**Search the content** of files or other inputs for specific values.
### Usage
```sh
grep [OPTION...] PATTERNS [FILE...]

grep "pattern" file_to_search.txt  # Search the pattern "pattern" in file_to_search.txt
cat file.txt | grep "pattern"  # You can also pipe stuff
```
## [[systemctl]]
Allows to **interact with the [[systemd]] process/daemon**.
### Usage
```sh
systemctl [OPTION] [SERVICE]

systemctl start apache2  # Starts the apache2 service
systemctl stop apache2  # Stops the apache2 service
```