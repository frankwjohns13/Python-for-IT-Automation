# Python for IT Automation - D522 - Notes

## Key Terms (A running collection of terms I feel are important from each section)
- **Module Docstring:** a documentation string placed at the beginning of a Python file that explains the script's purpose, functionality, and sometimes its inputs or environment requirements. Indicated by triple quotes.
- **Import Statements:** Python statements used to include built-in modules or external libraries so their functions and features can be used within the script
- **Constants:** named variables whose values are intended to remain unchanged during program execution, typically written in uppercase letters to indicate that they represent fixed configuration values
- **Main Execution block:** the section of a Python script that contains the code that should run when the script is executed directly
- **Clean Code:** Clean code is essential in automation because scripts often support operational workflows where reliability, readability, and maintainability are critical.
- **Hard-coded:** Hard-coding occurs when you use values instead of variables. This makes updating difficult as every place that value is used has to be found and corrected if something changes.

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
Notice how much easier it is to read when it has proper spacing. This makes updating, error checking, and troubleshooting easier.



---

## Lesson 1

**Learning Objectives**
- Develop a Python script that demonstrates correct syntax, clean structure, meaningful variable handling, and appropriate inline documentation.

**Hard-coded:** Hard-coding occurs when you use values instead of variables. This makes updating difficult as every place that value is used has to be found and corrected if something changes.

---

### Variable Naming:
A good variable name describes the data it contains. Variable names must follow the following four rules:
- Cannot have spaces
- can use only letters, numbers, and underscores (_)
- Cannot begin with a number
- Cannot be a Python keyword, (if, for, return...)

---

### Effective Documentation
Professional Python code contains documentation within the script. Clear documentation allows other coders to quickly understand what the code block is for. Documentation blocks start and end with triple quote marks. 
```
"""
This code check which servers are up
"""
```

---

### Lesson 1 - Refactoring an Automation Script Practical
**Overview**\
In this task, you will take an existing Python script and refactor it.

**What the Script Does**\
The script simulates a simple monitoring task:
- It contains a list of servers.
- Each server has a hostname and a status ("up" or "down").
- The script does the following:
  - checks each server
  - prints a message for each one
  - displays an alert if a server is down
  - displays a normal message if the server is operational

**Task**\
You will refactor the provided script to improve its structure, readability, and maintainability. You must not change what the script does, only how it is written.

**Requirements**\
Your refactored script must include the following components:

**Clean Structure**
- Use proper indentation.
- Organize code into logical sections.
- Avoid writing multiple statements on one line.

**Meaningful Variable Names**
- Replace unclear names.
- Use descriptive names.

**Constants for Configuration**
- Replace hard-coded values with named constants.

**Module Docstring**
- At the top of your script, include a docstring that explains what the script does and what problem it solves.

**Clear Inline Documentation**
- Add comments to explain intent, not obvious code.

**Proper Formatting and Syntax**
- Follow consistent spacing.
- Use readable formatting.
- Ensure the script runs without syntax errors.

**Use a Main Function**
- Wrap your logic in a function.
- Use the following:

```
if __name__ == "__main__":
check_servers()
```

**What You Should Not Do**
- Do not change the logic or output of the script.
- Do not add new features.

**Code to Refactor**
```
servers=[{"hostname":"web01","status":"up"},{"hostname":"db01","status":"down"},{"hostname":"app01","status":"up"},{"hostname":"dns01","status":"down"}]
def x():
   for s in servers:
      h=s["hostname"];z=s["status"]
      if z=="down":print(h+" is down")
      else:print(h+" is operational")
x()
```

**Solution** (One possible solution)
```
Correct code: 
""" 
Checks the status of servers and prints alerts for any server 
that is down.

This script iterates through a list of servers and reports 
whether each server is operational or requires attention. 
""" 
DOWN_STATUS = "down"   """ Setting a constant variable to 'down' for status check later """

""" Putting each server on its own line makes it clear to see what each one is """
servers = [ 
   {"hostname": "web01", "status": "up"}, 
   {"hostname": "db01", "status": "down"}, 
   {"hostname": "app01", "status": "up"}, 
   {"hostname": "dns01", "status": "down"} 
]

""" This section defines the function we are creating """
def check_servers(): 
"""Check each server and print its status.""" 
   for server in servers: 
      hostname = server["hostname"] 
      status = server["status"] 

      # Determine if the server is down 
      if status == DOWN_STATUS: 
         print(f"ALERT: {hostname} is down") 
      else: 
         print(f"{hostname} is operational")

if __name__ == "__main__": 
   check_servers() """ This calls the previously declared function. """

```


**End Lesson 1**

---



