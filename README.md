# Python for IT Automation - D522 - Notes

## Key Terms (A running collection of terms I feel are important from each section)
- **Module Docstring:** a documentation string placed at the beginning of a Python file that explains the script's purpose, functionality, and sometimes its inputs or environment requirements. Indicated by triple quotes.
- **Import Statements:** Python statements used to include built-in modules or external libraries so their functions and features can be used within the script
- **Constants:** named variables whose values are intended to remain unchanged during program execution, typically written in uppercase letters to indicate that they represent fixed configuration values
- **Main Execution block:** the section of a Python script that contains the code that should run when the script is executed directly
- **Clean Code:** Clean code is essential in automation because scripts often support operational workflows where reliability, readability, and maintainability are critical.

---

## Code Snippets (I will add example code here)

**Module Docstring** 
```
"""
Network connectivity monitor.

This script checks whether specified servers are reachable
and logs the results to a file.
"""
```

**Import Statements** 
```
import socket
from datetime import datetime
```


**Constants**
```
SERVERS = ["google.com", "example.com", "github.com"]
PORT = 80
TIMEOUT = 5
LOG_FILE = "connectivity_log.txt"
```

**Main Execution Block**
```
def main():
   """Main workflow for checking servers."""
   for server in SERVERS:
      if check_connection(server, PORT):
         status = "REACHABLE"
      else:
         status = "UNREACHABLE"
      print(f"{server}: {status}")
      log_result(server, status)
```

**Messy Code**
```
import os,sys
servers=["server1","server2","server3"]
for s in servers:
   if s=="server1":print("Checking server1");status=True
   elif s=="server2":print("Checking server2");status=True
   else:print("Checking server3");status=False
   if status==True:print(s+" is online")
   else:print(s+" is offline")
```

**Clean Code**
```
import os
import sys

servers = ["server1", "server2", "server3"]

for server in servers:
   print(f"Checking {server}")

   if server == "server1" or server == "server2":
      status = True
   else:
      status = False

   if status:
      print(f"{server} is online")
   else:
      print(f"{server} is offline")
```
Notice how much easier it is to read when it has proper spacing.


---

## Lesson 1

**Learning Objectives**
- Develop a Python script that demonstrates correct syntax, clean structure, meaningful variable handling, and appropriate inline documentation.



