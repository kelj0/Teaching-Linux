# Linux
My personal reference for using linux
(WORK IN PROGRESS)!

## Basics
cd -change directory
mkdir -make directory
rmdir -remove directory
cat file -Read all file
:> file -clear file contents
cat file | grep -c "if" -count ifs
sed -e 's/test/quest' < file  -replace every test with quest

## tail
tail file.txt       -read last 10 lines of file 'file.txt'
tail -n 5 file.txt  -read last 5 lines of 'file.txt'
tail -f myfile.txt  -output last 10 lines of file and keep updating if it changes
tail -f access.log | grep 23.10.160.10  -useful example of using tail and grep to monitor a log in real life

## cp
cp picture.jpg picture-02.jpg -make copy of picture in working dir and name it picture-02
cp /home/chuck/pictures/picture.jpg /home/chuck/backup/picture.jpg
-this makes copy of /home/keljo/pictures/picture.jpg in the directory /home/keljo/backup

## find
find / -name file.deb -search all disk for file.deb
find . -name file.deb -search in current folder

## Date and time
date – Show the current date and time
cal – Show this month's calendar
uptime – Show current uptime

## Users,hardware usage
w – Display who is online
whoami – Who you are logged in as
finger user – Display information about user
uname -a – Show kernel information
cat /proc/cpuinfo – CPU information
cat /proc/meminfo – Memory information
df -h – Show disk usage
du – Show directory space usage
free – Show memory and swap usage


