* [Bash](#bash)
* [VIM-notes](#vim-notes)
* [Short-guides](#short-guides)
  * [Adding app to Applications](#add-app-to)
  * [Add permanent alias](#add-alias)
  * [Encrypt storage in Linux](#encrypt)
  * [Configuring nano](#configure-nano)
  * [Installing virtualbox6.0 on Debian 10](#installvbox)
* [cURL](#curl)

## Bash <a name="bash"></a>
(WORK IN PROGRESS)!

* [Basics](#basics)
* [Processes](#processes)
* [File system](#file-system)
* [Sorting](#sorting)
* [GREP](#grep-matches-patterns-in-input-text-supports-simple-patterns-and-regular-expressions)
* [Date and time](#date-and-time)
* [Users and permisions](#users-and-permisions)
* [Hardware usage](#hardware-usage)
* [SSH](#ssh)
* [Loops](#loops)
* [Using args in scripts](#using-args-in-scripts)
* [Useful crafted command](#useful-crafted-commands)

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
- `kill PID` - Useful with ps -aux 
- `pwd`      - Print Working Directory  
- `man something` - opens manual for something if exists
- `wc file.txt`    - word count, counts number of lines,words and chars in files(from left to right)  
- `wc -l file.txt` - output only number of lines in file.txt



### Processes 
- `ps aux` - list all running processes
- `ps aux | grep {{string}}` - search for a process that matches string
- `ps -ef | grep python` - list all running python processes ('-ef' is for list all{e} and format it{f})
- `./analyze results.dat &` - run that task in background
- `jobs` - list all background running processes
- `fg %1`   - bring process [1](listed with `jobs`) to foreground
- `kill %1` - kill process [1](listed with `jobs`) to foreground
- `bg %1`   - start process [1](listed with `jobs`) again, but in the background

### File system 
- `cat file.txt`               - display file (read text and sent it your standard output{terminal})
- `cat file1.txt file2.txt`    - display file1 and file2
- `cat file.txt > newfile.txt` - works as cat file.txt but shell redirects output to newfile.txt
- `cat file1.txt file2.txt > newcombined.txt` - combine file1 and file2 text and output it to newcombined.txt
- `cat file1.txt >> file2.txt` - append file1 to file2 ( read file1 and append to end of file2)
- `ls`       - list files in current directory
- `ls -l`    - list files but use long listing format
- `ls -lh`   - list files but use long listing format and make sizes human readable (5369>5.3K)
- `ls -R -t` - list contents of directories recursivly, and sort by last time of change
- `ls -a`    - list ALL files in current directory
- `tac file.txt` -its same like cat but it reads file line by line BACKWARDS!
                  tac is really useful when you want output time logs 
- `tail file.txt`       -read last 10 lines of file 'file.txt'
- `tail -n 5 file.txt`  -read last 5 lines of 'file.txt'
- `tail -f myfile.txt`  -output last 10 lines of file and keep updating if it changes
- `tail -f access.log | grep 23.10.160.10`  -useful example of using tail and grep to monitor a log in real life
- `cp picture.jpg picture-02.jpg` -make copy of picture in working dir and name it picture-02
- `cp /picture.jpg /backup/picture.jpg` - this makes copy of /picture.jpg in the directory /backup
- `cp -r thesis thesis_backup` - copy directory and all its contents recursive  
- `mv file.txt place/` - move file.txt to place
- `rm file.txt`       - remove file.txt
- `rm -r directory/` - remove directory recursively
- `find / - name file.deb`        - search all disk for file.deb
- `find . - name file.deb`        - search in current folder
- `find . -type f`                - get listing of all the files
- `find . -type d`                - get listing of all the directories   
- `find . -type f -perm -u=x`     - get files that users can execute
- `wc -l $(find . -name '*.txt')` - get line count of all files that end on .txt
- `touch myfile.txt` - create new file

### Sorting
```
cat lenghts.txt
1
3
2
```
- `sort -n lenghts.txt` - outputs numerically sorted lenghts in this case (1 2 3) [consider space as newline]
- `sort -n lenghts.txt > sorted.txt` - we can send output of sort to some file
```
cat fil.txt
coho
steelhead
coho
steelhead
steelhead
```
- `uniq fil.txt` - outputs coho steelhead coho steelhead (uniq removes adjecent duplicated lines from its input
- `sort fil.txt | uniq` - now we sorted fil.txt and we removed all duplicates

### grep (Matches patterns in input text. Supports simple patterns and regular expressions)
```
file.txt:
The test is test
This is very nice "They are"
nice
```
- `grep The file.txt`
```
The test is test
This is very nice "The test"
```
- `grep nice file.txt`   - nice
- `grep -w The file.txt` - outputs only first line 'w' flag restricts matches to lines containing words on its own
- `grep --color "finding term" somefile.html`       -this will print 'finding term' if there is and highlight it
- `grep --color -n "finding term" somefile.html`    -it will also prefix each matching line with line number
- `grep --color -n -i "finding term" somefile.html` - use -i for case-insensitive match
- `grep --color -n -i "finding term" *.html`        -use * to expand search to all files that end with .html in cur dir
- `grep --color -n -i -r "finding term" *.html`     - use -r to make search recursively(to subdirectories)



### Date and time
- `date`   –Show the current date and time
- `cal`    –Show this month's calendar
- `uptime` –Show current uptime

### Users and permisions
- `w`           –Display who is online
- `whoami`      –Who you are logged in as
- `finger user` –Display information about user (sudo apt-get install finger)
- `chmod u=rw file.sh` - give user(file owner) read and write permision on file.txt
- `chmod g=x file.sh`  - give group execute permision on file.sh
- `chmod a= file.sh`   - give "all" (everyone on the system who isn't file's ownewe or in its group) no permisions


### Hardware usage
- `cat /proc/cpuinfo` –CPU information
- `cat /proc/meminfo` –Memory information
- `uname -a`    -Show kernel information
- `df -h`       -Show disk usage
- `free`        -Show memory and swap usage

### SSH
* `ssh user@hostname` -use's default ssh port(22)
* `ssh user@hostname -p 1234` -non default port
* Using RSA key in file
```sh
$ nvim key  # -paste key,save
$ chmod 600 key
$ ssh -i key user@hostname -p 2220
```
* `ssh test@backupserver "ls results"` - running commands on a remote machine
```sh
# dont want to type password over and over again when ssh-ing to machine?
# you can use ssh key, firstly check if you already have key pair on your machine
$ cd ~/.ssh
$ ls
# if you see id_rsa.pub, you already have a key pair and don't need to create a new one
# if you don't see id_rsa.pub, use following commant to generate a new key pair
ssh-keygen -r rsa -C "your@email.com"
# use default location
# optional passphrase, used to encrypt key locally with 128bit AES
# now you need to copy yout public key on any machines you would like to ssh wihout passphrase
$ cat ~/.ssh/id_rsa.pub
# good you see your key, now ssh machine
$ ssh test@backupserver
Password: *******
# paste the content of cat ~/.ssh/id_rsa.pub to end of ~/.ssh/authorized_keys on other machine
test> vim ~/.ssh/authorized_keys
# after append the content, logout and try loging again
test> exit
$ ssh test@backupserver
# thats it
```
```
(s)ecure cp
```
* `scp results.dat test@backupserver:backups/results.dat` - copy results from our pc to backupserver 
* `scp -r test@backupserver:backups/all ./backups` - copy "all" folder to our pc recursively


* Sending data to port
```sh
$ openssl s_client -connect localhost:port

# Using file as auth
$ openssl s_client -connect localhost:port -quiet < file_with_key
# -quiet option is for no s_client output
```

### Loops
```sh
for thing in list_of_things
do
    operation_using $thing
done

$ for filename in file1.txt file2.txt
> do    
>     cat $filename
> done
# cats file1 and file2
# we can also use oneliners (to separate two commands use ;)
for filename in file1.txt file2.txt;do cat $filename; done

for datafile in *.txt
do
    cat $datafile >> all.txt
done

# all text from files that end on .txt would be concatenated and saved to file all.txt

# spaces in names
for filename in "red dragon.dat" "purple unicorn.dat"
do
    cat "$filename"
done
```

### Using args in scripts
```sh
#script1
for filename in $1 $2 $3
do
    cat $filename
fone

$ bash script1.sh *.txt
# this would cat first 3 files that end on .txt

#script2
echo $@

$ bash script2.sh *.pdf
#  this would echo all files in current directory that end on .pdf
```


### Useful crafted commands
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

----------
| Search |
----------
In command mode press [/] and start typing
press enter to stay on that line(if you got match), if you escape you will
return back on line when you pressed [/]
To jump to next match press [n], [N] for previous

--------------------------------------------------
|Insert text at beginning of multi-line selection|
--------------------------------------------------
* Press Esc to enter 'command mode'
* Use Ctrl+V to enter visual block mode
* Move Up/Downto select the columns of text in the lines you want to comment.
* Then hit Shift+i and type the text you want to insert.
* Then hit Esc, wait 1 second and the inserted text will appear on every line.
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

### Installing virtualbox6.0 on Debian 10<a name="installvbox"><a/>
```
sudo apt update
sudo apt upgrade
```
Import the Oracle public key
```
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
```
```
Add "deb http://download.virtualbox.org/virtualbox/debian bionic contrib" to /etc/apt/sources.list
(The VirtualBox packages for Debian 10 Buster and Ubuntu 18.04 bionic are same. 
That’s why the repository is pointed to bionic.)

sudo apt update
sudo apt install virtualbox-6.0
```

### cURL<a name="curl"></a>

curl is used in command lines or scripts to transfer data


Download file from internet
```
curl -o filename_for_local_machine target_url
```

Make simple request
```
curl http://127.0.0.1:5000/
```

We could make the output cleaner by limiting the output of curl to just the file contents
```sh
curl -s url

# we can pipe it nice to html2text to parse html and only get clean text from html
# (you need to apt-get html2text)
curl -s url | html2text
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
