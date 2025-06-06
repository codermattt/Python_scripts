## Notes
- I setup a website using the python fabric library, to execute python functions on command line
- I installed fabric library using pip on command line
- The "fabfile.py" has all the functions declared in it to execute on command line
- "fab function_name:argument"  is the format used to execute functions on command line of current vm 
- everything before the webSetup function were practice functions



#!/usr/bin/python3
from fabric.api import *
127.0.0.1       localhost
from fabric.api import *
from fabric.api import *

def greetings(msg):
    print("good {}".format(msg))

def count_n10():
    count = 1
    while count <=10:
        print("{} ".format(count))
        count = count + 1

def remote_exec():
    run("hostname")
    run("uptime")
    run("df -h")
    run("free -m")

def webSetup(WEBURL, DIRNAME):
    print("install depencies")
    print("###############################")
    sudo("yum install httpd wget unzip -y")

    print("start & enable service")
    print("#######################################")
    sudo("systemctl start httpd")
    sudo("systemctl enable httpd")

    local("apt install zip unzip -y")

    print("Download and push website to webservers")
    print("###########################################")
    local(("wget -O website.zip %s") %WEBURL)
    local("unzip -o website.zip")

    with lcd(DIRNAME):
        local("zip -r tooplate.zip *")
        put("tooplate.zip", "/var/www/html/", use_sudo=True)

    with cd("/var/www/html"):
        sudo("unzip -o tooplate.zip")

    sudo("systemctl restart httpd")
    print("website setup is done")

## Remote connection: 
- we will then use python fabric to remotely setup website on a different machine in the Vagrantfile.
- to do it, we need to set up users on the other machines, then add those users to those machines' sudo's file (visudo)
- enable "Password Auth" in /etc/ssh/sshd_config file, then restart sshd
- now we are able to ssh into the other vms from one machine with the format -> ssh devver@web01 for e.g.
- to setup website remotely on a different vm do -> fab -H web01 -u devver webSetup: WEBURL, DIRNAME
