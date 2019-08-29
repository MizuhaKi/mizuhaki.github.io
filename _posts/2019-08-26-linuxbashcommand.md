---
layout: post
title: linux bash command
author: Mizuha Ki
date: 2019-08-26
categories:
- linux
- bash
- command
tags:
- linux
- bash
- command
- blog
---

## Bash Shell Reference

command | description | example
:--: | :---: | :---: 
ls | list files in a directory | ls
cd | changes the shell's working directory to the given directory | cd ..
mkdir | creates a new directory with the given name | mkdir test
cp | copies a file/directory | cp -r test1 test2
mv | moves (or renames) a file/directoy | mv test1 test2
rm | deletes file/directory | rm -rf test
touch | update the last-modified time of a file (or create an empty file) | touch test.py
cat | output the contents of a file | cat test.py
du | report disk space used by a file/directory | du -ah ./  
diff | output differences between two files | diff test1.py test2.py
chmod | change the permissions on a file or group of files | chmod u+x test.py
chown | change the owner of a file | chown -R usr:build test
find | search for files by name within a given directory | find /home -size +128k/test.py
zip, unzip | create a .zip archive or extract its contents | zip -q -r test.zip test
tar | unix archiving/de-archiving program | tar -cvf/-czf test.tar (.gz) test  tar -xvf/-xzvf test.tar (.gz)
date | outputs the current date/time | date +"%Y-%m-%d"
uname | print information about the system  | uname -a
time | measure how long a program takes to run | time -p date
kill | terminate a process | kill -9 pid
wget | download from a URL and save it to a file on the local hard drive | wget URL
curl | download from a URL and output its contents to the console | curl -O URL
vim, emacs | a complicated text editer (recommended) | vim test.py
echo | like println for the shell | echo "Hello"
awk | a full-featured text processing language | awk '{print $0}' /etc/passwd


