## My personal reference for bash
(WORK IN PROGRESS)!

Very nice page that explains almost every command

https://tldr.ostera.io/

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

### Useful commands
* `sed -e "s/ //g" -i test.txt` - Remove all spaces from file
* `sed -i '$ d' ./* -i test.txt` - Remove last line from all files in current dir
* `sed '/^\s*$/d' -i test.txt` - Remove all empty lines from file
* `rename 's/ /_/g' *` - Replace all spaces from filenames with '_'
* `sudo apt-get --purge autoremove` - remove all duplicate/orphan packetes
* `sudo apt-get clean` - remove all .deb instalation files that were downloaded by apt
* `python -m site --user-site` -points you on location of python site-packages directory 
* `kill $(ps aux | grep '[p]ython csp_build.py' | awk '{print $2}')`
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

Details how it works
* The ps gives you the list of all the processes.
* The grep filters that based on your search string, [p] is a trick to stop you picking up the actual grep process itself.
* The awk just gives you the second field of each line, which is the PID.
* The $(x) construct means to execute x then take its output and put it on the command line. 
  The output of that ps pipeline inside that construct above is the list of process IDs so 
  you end up with a command like kill 1234 1122 7654.


## Short guides
### Adding app to Applications
lets say you want to add tor to applications cause you dont want to type ./start-tor...

first go to folder where tor is
`cd -tor-browser_en-US/`

`ls` -to check if there is start-tor-...

`./start-tor-browset.desktop --register-app`

-congratz tor is under applications/internet

### Add permanent alias
- open terminal
- `nano ~/.bashrc` -open bashrc with your text editor
- add on end  `alias ptpython='python3 -m ptpython'` for example, this is your alias now
- now you need to save it ( ctrl+x->Y->enter in nano)
- Execute `. ~/.bashrc` in your terminal(there is space between `.` and `~/.bashrc`)
- Check your alias with `alias` typed in terminal


### CURL

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
