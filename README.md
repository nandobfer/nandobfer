# Code tips
## Python
replace character inside a string
```python
string = string.replace("old_char", "new_char")
```
'concatenate' dictionary
```python
d3 = dict(d1)
d3.update(d2)
```
evaluate list/dict from string
```python
import ast
ast.literal_eval(string)
```

## Git
remember the next git credentials for further logins
```git
git config credential.helper store
```

## Bash
ssh connection to ufpr server
```bash
ssh -i .ssh/burgos root@psa.c3sl.ufpr.br
```
enabling proxy http requests, suited to git pull from ufpr vm
```bash
source /root/proxy
```
show list of process listening to port 5000, can kill it with pid
```bash
lsof -i:5000
```
show list of active process with file's name, to kill it
```bash
ps -x | grep ./file
```

list directories with readable size
```bash
du -sh *
```

disk usage info (/ at end for actual disk only)
```bash
df -h
```

add source of exports (add this to /etc/profile.d/burgos_variables.sh)
```bash
source /home/fernando/burgos_variables/*
```

find files with given text inside
```bash
find path -type f -exec grep -l 'text-to-find-here' {} \;
```

find and replace text inside every file recursively from execution folder
```bash
sudo find ./ -type f -readable -writable -exec sed -i "s/text_to_find/new_text/g" {} \;
```

add free ssl certificate for a domain on nginx (requires apt install certbot and apt install python3-certbot-nginx)
```bash
sudo certbot --nginx -d example.com -d www.example.com
```

reissue certificate with new domains
```bash
sudo certbot --nginx certonly -d alefritzen.com.br,www.alefritzen.com.br -d alefritzen.com.br,www.alefritzen.com.br
```

add user
```bash
sudo adduser fernando
```

append user to sudo group (or any)
```bash
sudo usermod sudo fernando
```

create whm user (create regular user with adduser and passwd)
```bash
echo "username:all" >> /var/cpanel/resellers
cp /var/cpanel/users/system /var/cpanel/users/username
sed -i "s/DNS=//g" /var/cpanel/users/username
```

shell color codes
```bash
# Reset
Color_Off='\033[0m'       # Text Reset

# Regular Colors
Black='\033[0;30m'        # Black
Red='\033[0;31m'          # Red
Green='\033[0;32m'        # Green
Yellow='\033[0;33m'       # Yellow
Blue='\033[0;34m'         # Blue
Purple='\033[0;35m'       # Purple
Cyan='\033[0;36m'         # Cyan
White='\033[0;37m'        # White

# Bold
BBlack='\033[1;30m'       # Black
BRed='\033[1;31m'         # Red
BGreen='\033[1;32m'       # Green
BYellow='\033[1;33m'      # Yellow
BBlue='\033[1;34m'        # Blue
BPurple='\033[1;35m'      # Purple
BCyan='\033[1;36m'        # Cyan
BWhite='\033[1;37m'       # White

# Underline
UBlack='\033[4;30m'       # Black
URed='\033[4;31m'         # Red
UGreen='\033[4;32m'       # Green
UYellow='\033[4;33m'      # Yellow
UBlue='\033[4;34m'        # Blue
UPurple='\033[4;35m'      # Purple
UCyan='\033[4;36m'        # Cyan
UWhite='\033[4;37m'       # White

# Background
On_Black='\033[40m'       # Black
On_Red='\033[41m'         # Red
On_Green='\033[42m'       # Green
On_Yellow='\033[43m'      # Yellow
On_Blue='\033[44m'        # Blue
On_Purple='\033[45m'      # Purple
On_Cyan='\033[46m'        # Cyan
On_White='\033[47m'       # White

# High Intensity
IBlack='\033[0;90m'       # Black
IRed='\033[0;91m'         # Red
IGreen='\033[0;92m'       # Green
IYellow='\033[0;93m'      # Yellow
IBlue='\033[0;94m'        # Blue
IPurple='\033[0;95m'      # Purple
ICyan='\033[0;96m'        # Cyan
IWhite='\033[0;97m'       # White

# Bold High Intensity
BIBlack='\033[1;90m'      # Black
BIRed='\033[1;91m'        # Red
BIGreen='\033[1;92m'      # Green
BIYellow='\033[1;93m'     # Yellow
BIBlue='\033[1;94m'       # Blue
BIPurple='\033[1;95m'     # Purple
BICyan='\033[1;96m'       # Cyan
BIWhite='\033[1;97m'      # White

# High Intensity backgrounds
On_IBlack='\033[0;100m'   # Black
On_IRed='\033[0;101m'     # Red
On_IGreen='\033[0;102m'   # Green
On_IYellow='\033[0;103m'  # Yellow
On_IBlue='\033[0;104m'    # Blue
On_IPurple='\033[0;105m'  # Purple
On_ICyan='\033[0;106m'    # Cyan
On_IWhite='\033[0;107m'   # White
```

## PowerSHell
alert message
```powershell
msg user
mensagem
ctrl+Z
```

tasklist
```powershell
tasklist
```

kill
```powershell
taskkill/im chrome.exe /F
```

restart powershell as admin
```powershell
Start-Process powershell -Verb runAs
```

install ssh server (requires elevated powershell)
```powershell
Add-WindowsCapability -Online -Name OpenSSH.Server*
```

start ssh
```powershell
Start-Service sshd
Start-Service ‘ssh-agent’
```

automatic startup ssh
```powershell
Set-Service -Name sshd -StartupType 'Automatic'
Set-Service -Name ‘ssh-agent’ -StartupType 'Automatic'
```

open ssh port
```powershell
netsh advfirewall firewall add rule name=”SSHD service” dir=in action=allow protocol=TCP localport=22
```

make powershell default shell for ssh
```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

dir size
```powershell
Get-ChildItem CAMINHO -Recurse | Measure-Object -Property Length -Sum
```

## MYSQL
create user and give privileges (replace * . * with database.table for specifics)
```mysql
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON * . * TO 'username'@'localhost';
FLUSH PRIVILEGES;
```

create table
```mysql
CREATE DATABASE db_name;
```

import sql
```mysql
mysql -u username -p database_name < file.sql
```

export sql
```mysql
mysqldump -u username -p database_name > file.sql
```

list databases
```mysql
SHOW DATABASES;
```

select database to work into
```mysql
use database_name;
```

insert data into selected database table
```mysql
insert into table_name (column1, column2, column3) values ("value1", "value2", "value3");
```

## Install LEMP
https://www.cloudsigma.com/how-to-install-the-lemp-stack-linux-nginx-mysql-php-on-ubuntu-20-04/

<img height="180em" src="https://github-readme-stats.vercel.app/api?username=nandobfer&show_icons=true&hide_border=true&&count_private=true&include_all_commits=true" />

<!--
Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
