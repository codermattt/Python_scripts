## Note: the os module is important
        - uses python3 interpreter(installed on vm) to execute 
--------------------------------------------------------------
#!/usr/bin/python3

import os

path = "tmp/pysy"

if os.path.isdir(path):
    print("{} is a directory".format(path))
elif os.path.isfile(path):
    print("{} is a file".format(path))
else:
    print("that does not exit")


--------------------------------------------------------------
