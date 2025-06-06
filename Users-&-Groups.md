## Notes 
- script to add users to a group, then create a directory if it doesn't exist
- then giving full permissions to the dir for users in the group


#!/usr/bin/python3
import os

userlist = ["matty", "brodie", "the_guy"]

print("adding users to system")
print("#####################################################")

for user in userlist:
    exitcodie = os.system("id {}".format(user))

    if exitcodie != 0:
        print("user {} does not exist".format(user))
        print()
        os.system("useradd {}".format(user))
        print("#######################################################")
    else:
        print("user {} does exist".format(user))
        print("##################################")

exitcode = os.system("grep science /etc/group")

if exitcode != 0:
    print("Adding group science")
    print()
    os.system("groupadd science")
else:
    print("group already exists. skipping it")
    print("##########################################")
print()

# adding users to 'science' group

for user in userlist:
    print("adding user {} to 'science' group".format(user))
    print("##########################################")
    print()
    os.system("usermod -G science {}".format(user))

print("adding directory")
print("###############################")
print()

if os.path.isdir("/opt/science_dir"):
    print("directory already exists")
else:
    os.mkdir("/opt/science_dir")
