---
layout: essay
type: essay
title: Notes on bash and Command Line 
date: 2019-09-21
labels:
  - bash
  - guide
  - notes
---

<em>Notes on bash commands...</em>

## Bash Commands
#### find count number of files in each dir from present dir
```bash
find ./ -mindepth 2 -type f | cut -d/ -f2 | sort | uniq -c | sort -nr
```

#### cp all files and preserve attributes
```bash
cp -a /source/* /destination/
```

#### bc calculator float division
```bash
echo "2/3" | bc -l
```

#### sed edit a file with sed replace underscores with space
```bash
sed 's/_/ /g' <file.txt>
```

#### sed remove string of x # of digits from file
```bash
sed 's/_[0-9]{3}_/_/g' <file.txt>
```

#### sed edit file in place; add prefix to beginning of each line
```bash
sed -i -e 's/^/prefix2add/' <file.txt>
```

#### tr translate/replace newline characters in file with space
```bash
tr '\n' ' ' < <file.txt>
```

#### tr translate/replace lowercase to uppercase characters 
```bash
tr "[:lower:]" "[:upper:]" < <file.txt>
```

#### awk read nth column of file (e.g. 2nd & 3rd cols)
```bash
awk '{ print $2,$3 }' <file.txt>
```

#### wc count number of lines in file
```bash
wc -l <file.txt>
```

#### sed create new file
```bash
sed -i -e 's/^/prefix2add/' oldfile > newfile
```

#### sed delete lines in a file which contain a certain string
```bash
sed -i.bak '/string2snipe/d' ./file2clean
```

#### logical OR
```bash
if [ $a == 0 ] || [ $a == 1 ]; then echo $a; fi
```

#### symlink file with a whitespace (treat as string)
```bash
ln -s "/path/White Space.ext" .
```

#### find files from a given date
```bash
date=1999-12-31
for f in *ext; do if stat -c %y $f | grep $date; then echo $f; fi; done
```

#### count # of ocurrences of a string in a file
```bash
grep 'string' <file.txt> | wc -l
```

#### watch output of command change over time (-n1 => every second)
```bash
watch -n1 "date"
```

#### watch/follow the tail of a log file
```bash
tail -f -n40 <log>
```

#### rename files with index in name (e.g. abc_000005_doremi)
```bash
rename s/_00000[0-9]_/_/g $f
```

#### get unique values in 3rd field
```bash
for f in *ext; do cat $f | awk '{print $3}'; done | sort -u
```

#### ls list all files without an extension
```bash
ls --ignore='*.*'
```

#### get destination path of symbolic link
```bash
readlink $symlink
```

#### kill all threads running 'badprocess'
```bash
ps -ef | grep badprocess | awk '{print $2}' | for f in `xargs $1`; do kill $f; done
```
#### ...or...
```bash
for pid in $(ps -ef | awk '/badprocess/ {print $2}'); do kill -9 $pid; done
```

#### find all unique filetypes in a directory
```bash
for f in *; do echo $f | rev | cut -d'.' -f1 | rev; done | sort -u
```

#### replace space with underscore in filenames
```bash
find -name "* *" -type f | rename 's/ /_/g'
```

#### search for a string in files of a certain format (e.g. .py)
```bash
grep -rn "string" --include \*.py
```

#### diff contents of dirs
```bash
diff -qr dir1 dir2 | sort
```

#### search command history
```bash
Ctrl+R
```

#### Directory structure
```bash
tree
```
#### ...limited to N levels
```bash
tree -L N
```
#### ...w file size
```bash
tree -hs
```

#### human-readable filesize (MB)
```bash
ls -l --block-size=MB <file>
```

#### install .deb package
```bash
sudo dpkg -i <.deb>
```

#### find packages associated with apt-get installation (and their locations)
```bash
dpkg -L <package>
```

#### search for Ubuntu package
```bash
apt-cache search <keyword>
```

#### uncompress a gzipped tarball
```bash
tar xvzf <file>.tar.gz
# x = extract
# v = verbose, list all files
# z = uncompress
# f = file
# c = compress
```

#### compress a directory to .tar.gz
```bash
tar -zcvf archive.tar.gz directory/
```

#### unique entries in a CSV column
```bash
cut -d',' -f$X <file>.csv | sort -u
# (where $X=column index)
```

#### Read file line-by-line
```bash
i=1
while read line; do
      echo $line
        ((i++))
        done < $file
```

#### append to same line of file (-n excludes newline)
```bash
echo -n "text" >> $file
```

#### find files created/edited in the last 24 hours
```bash
find . -maxdepth 3 -mtime -1 -type f
```

#### time a function
```bash
echo "Starting @" `date`;
tic=$SECONDS;
sleep 1;
toc=$SECONDS;
echo "Ending @ " `date`;
echo "Time elapsed:" $((toc-tic)) "secs"
```

#### write stdout and stderr to log file (and print to std out)
```bash
script.sh 2>&1 | tee -a log.txt
```

#### print file ignoring header (start reading from line 2)
```bash
tail -n +2 $file
```

#### delete lines from a text file
```bash
sed -i.bak '/pattern to match/d' $f
```

#### add a header to a file
```bash
sed -i i1'Header,Text' $f
```

#### remove header from file
```bash
sed -i 1d $f
```

#### remove carriage return (^M)
```bash
sed -i 's/\r//g' $f
```

#### view a CSV file in tab-separated table format
```bash
column -s, -t < file.csv | less -#2 -N -S
```

#### JSON inspection with colouring
```bash
cat file.json | jq ''
```

#### see hostname (aka name of machine)
```bash
uname -n` or `hostname
```

#### change hostname
```bash
hostnamectl set-hostname <new_hostname>
```

#### change directory ownership
```bash
sudo chown -R username:group directory
```

#### list all users
```bash
getent passwd | cut -d':' -f1` or `cat /etc/passwd | cut -d: -f1
```

#### get user's id and groups
```bash
id <user>
```

#### groups
```bash
id -G <user>
```

#### list all system groups
```bash
groups
```

#### list all system groups that <user> belongs to
```bash
groups <user>
```

#### List all users in <group>
```bash
getent group <group>
```

#### add <user> to <group>
```bash
usermod -G <group> <user>
sudo su
setfacl -m u:<user>:rwx <file/dir>
```
#### exit code of last executed command (e.g. to check fsck error code)
```bash
echo $?
```

#### list system hardware devices
```bash
lshw
```

#### list files by timestamp (reverse)
```bash
ls -ltr
```

#### change string to lowercase
```bash
echo $string | tr '[A-Z]' '[a-z]'
```

#### check a volume's, and keep the df header
```bash
df -h | grep 'Use\|/mnt/data'
```
