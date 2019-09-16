# Shell commands

## Basic commands with examples

### basics

```bash
# this is comment
ls
ls -al
touch hello.txt
touch --help
man touch
echo hello world
echo "hello world"
MY_TEXT="ABC"
echo $MY_TEXT
cat hello.txt
cp hello.txt hello2.txt
mv hello.txt hello1.txt
rm hello*.txt
mkdir abc
cd abc
cd /
cd ~
cd
cd ..
cd .
cd -
rmdir abc
clear
history
exit
```

### redirection

```bash
echo "hello world" > hello.txt
echo "hi world" >> hello.txt
echo "hello world" > /dev/null
ls 1> out.txt 2> error.txt
ls -z 1> out.txt 2> error.txt
```

### pipe

```bash
cat hello.txt|head
```

### search

```bash
whereis python3
which python3
grep search_text -rniH .
find . |grep hello
find . |less
```

### read file

```bash
less hello.txt
head hello.txt
tail hello.txt
tail -f log.txt
```

### process and job management

```bash
ps aux
ps aux |grep python
top
htop
pstree
tail -f log.txt &
jobs
fg
bg
kill -9 12345
nohup a_long_remote_script.sh &
```

### network

```bash
ping google.com
wget http://google.com
wget https://raw.githubusercontent.com/uiuc-cse/data-fa14/gh-pages/data/iris.csv
ifconfig
ssh example_account@example.com
scp hello.txt example_account@example.com:/home/example_account/
scp demo@test.rebex.net:/readme.txt ./
```

### environment variables

```bash
env
FOO=BAR a_script.sh
source venv/bin/activate
. venv/bin/activate

# etc
ln -s target_file link_file_to_create
nano hello.txt
```

### Example bash script

```bash
#!/bin/bash
TALKING_TO=WORLD

echo "Hello $TALKING_TO! ($FOO, $1, $2)"
```

Run with a environment variable

```bash
chmod +x hello.sh
FOO=BAR ./hello.sh
```

- `#!/bin/bash` is called a shebang line. By that the operating system decide the interpreter to run.
- For a python script it can be like `#!/usr/bin/env python3` to be more portable across different systems.

### python development

```bash
python3 -m venv venv
. venv/bin/activate
pip install numpy
pip install -U pip
pip freeze
pip freeze > requirements.txt
pip install -r requirements.txt
python hello.py
deactivate
code .
```

## additional topics

- soft link
  - ln -s target_file link_file_name
- return code or error code
  - `$?`
  - 0: success
  - non-zero: fail
- &&
- ||
- watch
  - `watch ps aux`
- find and execute
- awk
- nano or vim
- apt or brew
- arguments for bash script
- if statement
- for statement
- telnet to check if a port is open
- ssh-add
- ssl 🔑 gen for git configuration

## Remarks

IO devices

- 0: /dev/stdin
- 1: /dev/stdout
- 2: /dev/stderr
- /dev/null
