* [Bash](#bash)
* [VIM-notes](#vim-notes)
* [Short-guides](#short-guides)
  * [Adding app to Applications](#add-app-to)
  * [Add permanent alias](#add-alias)
  * [Encrypt storage in Linux](#encrypt)
  * [Configuring nano](#configure-nano)
* [CURL](#curl)

## Bash <a name="bash"></a>
(WORK IN PROGRESS)!

### Basics

- `cd /usr/test` - change directory
- `mkdir test`   - make directory
- `rmdir dir`    - remove directory
- `rm -rf test`  - remove directory even if its not empty
- `cat file` - Read all file
- `:> file`  - clear file contents
- `sed -e 's/test/quest' < file`  - replace every test with quest
- `mv fromPath/ toPath/`    - self explanatory 
- `bc`       - Calculator
- `top`      - Display processes
- `|`        - 'pipe' ,send output from one command to other
- `>`        - 'stream' , you can also output in other command(like | ) or you can stream in file
- `ps -aux`  - Snapshot of currently running processes
- `kill PID` - Useful with ps -aux 

### ps (Information about running processes)
- `ps aux` - list all running processes
- `ps aux | grep {{string}}` - search for a process that matches string
- `ps -ef | grep python` - list all running python processes ('-ef' is for list all{e} and format it{f})

### cat and tac ( work with text files)
- `cat file.txt`               - display file (read text and sent it your standard output{terminal})
- `cat file1.txt file2.txt`    - display file1 and file2
- `cat file.txt > newfile.txt` - works as cat file.txt but shell redirects output to newfile.txt
- `cat file1.txt file2.txt > newcombined.txt` - combine file1 and file2 text and output it to newcombined.txt
- `cat file1.txt >> file2.txt` - append file1 to file2 ( read file1 and append to end of file2)
- `tac file.txt` -its same like cat but it reads file line by line BACKWARDS!
                  tac is really useful when you want output time logs 

### tail (Display the last part of a file)
- `tail file.txt`       -read last 10 lines of file 'file.txt'
- `tail -n 5 file.txt`  -read last 5 lines of 'file.txt'
- `tail -f myfile.txt`  -output last 10 lines of file and keep updating if it changes
- `tail -f access.log | grep 23.10.160.10`  -useful example of using tail and grep to monitor a log in real life

### cp (Copy files and folders)
- `cp picture.jpg picture-02.jpg` -make copy of picture in working dir and name it picture-02
- `cp /home/chuck/pictures/picture.jpg /home/chuck/backup/picture.jpg`
   
   this makes copy of /home/keljo/pictures/picture.jpg in the directory /home/keljo/backup

### find (Find files under the given directory tree, recursively)
- `find /` -name file.deb -search all disk for file.deb
- `find .` -name file.deb -search in current folder

### grep (Matches patterns in input text. Supports simple patterns and regular expressions)
- `grep --color "finding term" somefile.html`       -this will print 'finding term' if there is and highlight it
- `grep --color -n "finding term" somefile.html`    -it will also prefix each matching line with line number
- `grep --color -n -i "finding term" somefile.html` - use -i for case-insensitive match
- `grep --color -n -i "finding term" *.html`        -use * to expand search to all files that end with .html in cur dir
- `grep --color -n -i -r "finding term" *.html`     - use -r to make search recursively(to subdirectories)


### Date and time
- `date`   –Show the current date and time
- `cal`    –Show this month's calendar
- `uptime` –Show current uptime

### Users,hardware usage
- `w`           –Display who is online
- `whoami`      –Who you are logged in as
- `finger user` –Display information about user (sudo apt-get install finger)
- `uname -a`    –Show kernel information
- `cat /proc/cpuinfo` –CPU information
- `cat /proc/meminfo` –Memory information
- `df -h`       –Show disk usage
- `du – Show`   -Directory space usage
- `free`        –Show memory and swap usage

### SSH,openssl..
* `ssh user@hostname` -use's default ssh port(22)
* `ssh user@hostname -p 1234` -non default port
* Using RSA key in file
```sh
$ nano key  # -paste key,save
$ chmod 600 key
$ ssh -i key user@hostname -p 2220
```
* Sending data to port
```sh
$ openssl s_client -connect localhost:port

# Using file as auth
$ openssl s_client -connect localhost:port -quiet < file_with_key
# -quiet option is for no s_client output
```

### Useful commands
* `sed -e "s/ //g" -i test.txt` - Remove all spaces from file
* `sed -i '$ d' ./* -i test.txt` - Remove last line from all files in current dir
* `sed '/^\s*$/d' -i test.txt` - Remove all empty lines from file
* `rename 's/ /_/g' *` - Replace all spaces from filenames with '_'
* `sudo apt-get --purge autoremove` - remove all duplicate/orphan packetes
* `sudo apt-get clean` - remove all .deb instalation files that were downloaded by apt
* `python -m site --user-site` -points you on location of python site-packages directory 
* read file line by line 
```sh
while read p; do 
  echo "$p" 
done < file.txt`
```
* find substring in string
```sh
string='My long string'
if [[ $string == *"My long"* ]]; then
  echo "It's there!"
fi
```
* `kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')`
Details how it works
* The ps gives you the list of all the processes.
* The grep filters that based on your search string, [p] is a trick to stop you picking up the actual grep process itself.
* The awk just gives you the second field of each line, which is the PID.
* The $(x) construct means to execute x then take its output and put it on the command line. 
  The output of that ps pipeline inside that construct above is the list of process IDs so 
  you end up with a command like kill 1234 1122 7654.

### VIM notes <a name="vim-notes"></a>
```
vim FILENAME -> open file for editing
use 
  k
h   l
  j
to move around in normal mode

-------
|Modes|
-------
[i] insert mode 
[A] append something to end of line
[v] visual mode

-----------------
|Delete commants|
-----------------
[dw] a word, EXCLUDING first char
[d$] to the end of line, INCLUDING the last char
[de] to end of current word, INCLUDING the last char

--------------------------
|Using count for a motion|
--------------------------
[in normal mode]
[2w] move cursor two forst forward
[3e] move cursor to the end of the third word forward
[0] go to start of the line

----------------------------
|Using count to delete more|
----------------------------
[d2w] delete the two UPPER CASE words

--------------------
|Operating on lines|
--------------------
[dd] delete a whole line
[2dd] delete two lines(starting on line where cursor is and going down)

------------------
|The UNDO command|
------------------
[u] undo last command executed
[U] return line to its original state

------
|REDO|
------
[<Ctrl-r>] undo the undo's

-------------
|PUT command|
-------------
[p] puts line below cursor(example dd to delete line  and p to put it back on differend place)

------------------
| Replace command|
------------------
[rx] replace char at cursor with x

-----------------
|Change operator|
-----------------
[ce] deletes the word from cursor till end and enters insert mode
[c$] deletes the line till end and enters insert mode
[c2w] can also be uset with numbers(this deletes 2 words after cursor and enters insert mode)

-----------------------------------
| Cursor location and file status |
-----------------------------------
[<Ctrl-g>] message will appear at the bottom of page with the filename and position in the file
[10G] go to 10nth line

---------------
| Split screen|
---------------
[<Ctrl-w>,h/j/k/l] depending where you want to switch
[<Ctrl-w>,s] split current file horizontal
[<Ctrl-w>,v] split current file vertical
[<Ctrl-w>,Q] close one
[:sp filename] horizontal split
[:vsp filename] or [:vs filename] vertical split

---------------------------
| Copy to system clipboard|
---------------------------
["+y] yankes selected text (in visual mode) to system clipboard

```

## Short guides <a name="short-guides"></a>
### Adding app to Applications <a name="add-app-to"></a>
lets say you want to add tor to applications cause you dont want to type ./start-tor...

first go to folder where tor is
`cd -tor-browser_en-US/`

`ls` -to check if there is start-tor-...

`./start-tor-browset.desktop --register-app`

-congratz tor is under applications/internet

### Add permanent alias <a name="add-alias"></a>
- open terminal
- `nano ~/.bashrc` -open bashrc with your text editor
- add on end  `alias ptpython='python3 -m ptpython'` for example, this is your alias now
- now you need to save it ( ctrl+x->Y->enter in nano)
- Execute `. ~/.bashrc` in your terminal(there is space between `.` and `~/.bashrc`)
- Check your alias with `alias` typed in terminal


### Encrypt storage in Linux <a name="encrypt"></a>
* `sudo apt-get install cryptsetup`
* `lsblk`  -find partition you want to encrypt
* `sudo cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb1`
* `sudo cryptsetup luksOpen /dev/sdb1 sdb1` -use password you wrote in step before
* `sudo fdisk -l` verify that disk is listed
* `sudo mkfs.ext4 /dev/mapper/sdb1` - create new file system(recommend ext4)
* `sudo tune2fs -m 0 /dev/mapper/sdb1` -ext4 reserves some space by default,but you wont need it if you dont run sys on it
* `sudo mkdir /mnt/encrypted` - create folder to mount it on (/mnt is commont place to mount)
* `sudo mount /dev/mapper/sdb1 /mnt/encrypted` - mount it  
* `sudo touch /mnt/encrypted/test.txt` - create test file (you need root permision on encrypted partition)
* ``sudo chown -R `whoami`:users /mnt/encrypted`` -you can change that permision with this command
* `touch /mnt/encrypted/test.txt` - test it to see if you can create file without root

When you are done working on encrypted disk

* `sudo umount /dev/mapper/sdb1` - umount it
* `sudo cryptsetup luksClose sdb1` - and close mapped device

When you want to use it again
* `lsblk` - check its name
* `sudo cryptsetup luksOpen /dev/sdb1 sdb1` - open encrypted partition (enter passphrase)
* `sudo mount /dev/mapper/sdb1 /mnt/encrypted` - and mount it

#### Auto mount encrypted partitions during boot

* `lsblk` - check NAME of encrypted partition (sdb1 etc)
* `sudo cryptsetup luksUUID /dev/NAME` - get UUID
* `sudo nano /etc/crypttab` - and add this line `NAME /dev/disk/by-uuid/UUID_from_step_before none luks`
* `sudo mkdir /mnt/encrypted_disk` - create mount point 
* `sudo nano /etc/fstab` - add this mnt point `/dev/mapper/NAME /mnt/encrypted_disk ext4 defaults 0 2`

#### Forgot password?
* DONT UMOUNT DISC!
* `dmsetup ls --target crypt` - check for open crypt devices -> this is <NAME> lets say name is sdc1
* `(sudo dmsetup table --showkey /dev/mapper/sdc1 | awk '{print$5}' | xxd -r -p)> key.txt` - extract masterkey and convert to binary
* `sudo cryptsetup luksAddKey /dev/sdc1 --master-key-file key.txt` - add new password to keyring
* you have successfuly added new password to your storage

### Configuring nano <a name="configure-nano"></a>

To configure global settings -> `sudo nano /etc/nanorc`

Optionally configure nano on a user by user basis by creating a .nanorc file in their home directory

```
So just uncomment/add this lines to alter its behaviour, il write few of them that i personally 
have but rest is on you..you are the one that will use this so make it for you :)
```
* Enable mouse support -> `set mouse`
* Convert typed tabs to spaces -> `set tabstospaces`
* Set tab size to 4 -> `set tabsize 4`
* Text highlighting -> `include /usr/share/nano/*.nanorc` (if you want specific language here is [list](https://pastebin.com/eNBBkKuZ))
* Binding keys '^'==CTRL and 'M'==ALT below are 2 examples

```
bind M-5 copytext all # alt+5 as copy
bind M-2 uncut all    # alt+2 as paste
```

### CURL<a name="curl"></a>

curl is used in command lines or scripts to transfer data


Make simple request
```
curl http://127.0.0.1:5000/
```

curl can be used to specify the request type (GET,POST,PATCH,PUT,DELETE..) [more info](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
```
curl -X PATCH http://127.0.0.1:5000/echo
```

You can also specify the content type with curl
```
curl -H "Content-type: application/json" \
-X POST http://127.0.0.1:5000/messages -d '{"message":"Hello Data"}'
```

Sending files ?
```
curl -H "Content-type: application/octet-stream" \
-X POST http://127.0.0.1:5000/messages --data-binary @message.bin
```

To view HTTP headers specify the `-i` option
```
curl -i http://127.0.0.1:5000/hello
```

Authenticated request - use `-u`, to look at headers in request add `-v` 
```
curl -v -u "admin:secret" http://127.0.0.1:5000/secrets
```

##### To sum it up
* `-X` 	specify HTTP request method e.g. POST
* `-H` 	specify request headers e.g. "Content-type: application/json"
* `-d` 	specify request data e.g. '{"message":"Hello Data"}'
* `--data-binary` 	specify binary request data e.g. @file.bin
* `-i` 	shows the response headers
* `-u`	specify username and password e.g. "admin:secret"
* `-v` 	enables verbose mode which outputs info such as request and response headers and errors


**If you need more info see [docs/book](https://ec.haxx.se/)**
