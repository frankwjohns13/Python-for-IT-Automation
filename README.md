# Python for IT Automation - D522 - Textbook Notes

<details>
<summary><Strong>Key Terms (A running collection of terms I feel are important from each section)</Strong></summary> 

   - **Module Docstring:** a documentation string placed at the beginning of a Python file that explains the script's purpose, functionality, and sometimes its inputs or environment requirements. Indicated by triple quotes.
   - **Import Statements:** Python statements used to include built-in modules or external libraries so their functions and features can be used within the script
   - **Constants:** named variables whose values are intended to remain unchanged during program execution, typically written in uppercase letters to indicate that they represent fixed configuration values
   - **Main Execution block:** the section of a Python script that contains the code that should run when the script is executed directly
   - **Clean Code:** Clean code is essential in automation because scripts often support operational workflows where reliability, readability, and maintainability are critical.
   - **Hard-coded:** Hard-coding occurs when you use values instead of variables. This makes updating difficult as every place that value is used has to be found and corrected if something changes.
   - **README:** Is a document that explains how a piece of software or script works.
   - **cron:** Unix or Linux scheduling tool that automates recurring commands or scripts at specified times
   - **Conditional Logic:** Allows a program to make decisions and execute different code based on whether a condition is true or false.
   - **Monitoring:** Collecting information about the system.
   - **Evaluating:** Compare data against a predefined set of rules.
   - **Acting:** Performing a task.
   - **Triggers:** Condition or event that causes a specific block of code to execute.
   - **Magic Numbers:** Numeric values written directly into code without explanation or context.
   - **Measurable Condition:** Defines a clear rule that a script can evaluate to determine whether an action should occur.
   - **Threshold:** Predefined value that determines when a condition triggers a specific action.
   - **Nested Logic:** Multiple conditional statements are placed inside one another repeatedly, creating several layers of indentation.
   - **Alert:** Notification that indicates a condition has occurred
   - **Action:** Automated response that attempts to resolve or manage a condition
   - **import:** Reuse existing code from modules and libraries instead of writing everything from scratch
   - **current working directory:** the folder where the Python script reads and writes files by default
   - **home directory:** default personal folder where a user's files and settings are stored
   - **absolute path:** the full path to a file or directory, starting from the root directory
   - **relative path:** specifies a file or directory location based on the current working directory
   - **anchor:** root folder of the filesystem
   - **plaintext files:** files that contain only basic text characters and do not include font, size, or color information
   - **csv files:** these store tabular data using commas to separate values


---

**End Key Terms**




</details> <!-- Ends Key Terms -->

---

<details>
<summary><strong>Code Snippets (I will add example code here)</summary>

**Module Docstring** 
```python
"""
Network connectivity monitor.

This script checks whether specified servers are reachable
and logs the results to a file.
"""
```

**Import Statements** 
```python
import socket
from datetime import datetime
```

**Constants**
```python
SERVERS = ["google.com", "example.com", "github.com"]
PORT = 80
TIMEOUT = 5
LOG_FILE = "connectivity_log.txt"
```

**Main Execution Block**
```python
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
```python
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
```python
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


**Conditional Logic**
```python
MAX_CPU_USAGE = 85

cpu_usage = 92 # Simulated CPU usage value, in a real time environment you would have a function to get the actual CPU usage at the time.

if cpu_usage > MAX_CPU_USAGE:
   print("ALERT: CPU usage is too high.")
   print(f"Current CPU usage: {cpu_usage}%")
else:
   print("CPU usage is within acceptable limits.")
   print(f"Current CPU usage: {cpu_usage}%")
```

**Match/Case**
```python
command = "start" # This would come from an input statement asking what you want to do. 

match command:
   case "start":
      print("Starting system")
   case "stop":
      print("Stopping system")
   case _:
      print("Unknown command")
```

**Monitoring, Evaluating, Acting
```python
MAX_FAILED_LOGINS = 5

failed_login_attempts = 7 # Simulated monitoring value

# Monitoring
print("Checking failed login attempts...")

# Evaluating
if failed_login_attempts > MAX_FAILED_LOGINS:
   # Acting
   print("ALERT: Too many failed login attempts detected.")
else:
   # Acting
   print("Login activity is within acceptable limits.")
```

**Deeply Nested Logic**
```python
CRITICAL_THRESHOLD = 90
server_reachable = True
disk_usage = 92
service_running = False

if server_reachable:
   if disk_usage > CRITICAL_THRESHOLD:
      if not service_running:
        print("Alert: Server reachable, disk usage high, and service is down.")
```

**Clearer Alternative**
```python
CRITICAL_THRESHOLD = 90
server_reachable = True
disk_usage = 92
service_running = False

if server_reachable and disk_usage > CRITICAL_THRESHOLD and not service_running:
   print("Alert: Server reachable, disk usage high, and service is down.")
```

---

**End Code Snippets**


</details> <!-- Ends Code Snippets -->

---

<!-- THIS BEGINS SECTION 1 -->

<details>
<summary><strong>Section 1 - Python Principles and Syntax</strong></summary>

---







<!-- 
      *******************************
      THIS BEGINS SECTION 1: LESSON 1 
      *******************************
-->








   <details>
   <summary><strong>Lesson 1 - Clean and Well-Documented Scripts</strong></summary>

   **Learning Objectives**
   - Develop a Python script that demonstrates correct syntax, clean structure, meaningful variable handling, and appropriate inline documentation.

   ---
   
   ### Hard-Coded Values
   
   Hard-coding occurs when you use fixed values directly in the code instead of variables.\
   This makes the script harder to update because every occurrence of that value must be found and changed manually.
   
   ---
   
   ### Variable Naming Rules
   
   A good variable name clearly describes the data it holds.
   
   Rules for naming variables:
   - Cannot contain spaces
   - Can only use letters, numbers, and underscores (`_`)
   - Cannot begin with a number
   - Cannot be a Python keyword (`if`, `for`, `return`, etc.)
   
   ---
   
   ### Effective Documentation
   
   Professional Python scripts include documentation that explains what the code does.
   
   Documentation blocks start and end with triple quotes:
   
   ```python
   """
   This script checks which servers are currently up.
   """
   ```
  
   ---
   
  ### Lesson 1 - Refactoring an Automation Script Practical
  
  **Overview**\
  In this task, you will take an existing Python script and refactor it to improve readability and maintainability without changing what it does.
   
  **What the Script Does**\
  - Contains a list of servers.
  - Each server has a hostname and a status ("up" or "down").
  - Checks each server and prints:
    - An alert if the server is down
    - A normal message if the server is operational

   ---
     
   **Requirements**\
   Your refactored script must include:
   
   **Clean Structure**
   - Proper indentation.
   - Logical organization
   - One statement per line
   
   **Meaningful Variable Names**
   - Replace unclear names with descriptive ones.
   
   **Constants for Configuration**
   - Replace hard-coded values with named constants.
   
   **Module Docstring**
   - Include a docstring at the top explaining the purpose of the script
   
   **Clear Inline Documentation**
   - Add comments that explain intent (not obvious code)
   
   **Proper Formatting**
   - Consistent spacing
   - Readable layout
   - No syntax errors
   
   **Use a Main Function**
   - Wrap your logic in a function.
   - Use the following:
   
   ```Python
   if __name__ == "__main__":
      check_servers()
   ```
   
   **Code to Refactor**
   ```Python
   servers=[{"hostname":"web01","status":"up"},{"hostname":"db01","status":"down"},{"hostname":"app01","status":"up"},{"hostname":"dns01","status":"down"}]
   def x():
      for s in servers:
         h=s["hostname"];z=s["status"]
         if z=="down":print(h+" is down")
         else:print(h+" is operational")
   x()
   ```

   
   
   <!--
   **********************
         Solution 
   **********************
   -->

   
   
   <details>
   <summary><strong>Solution (One possible solution)</strong></summary>

   ```Python
   """
   Checks the status of servers and prints alerts for any server that is down.

   This script iterates through a list of servers and reports whether each server is operational or requires attention.
   """

   DOWN_STATUS = "down"

   servers = [
    {"hostname": "web01", "status": "up"},
    {"hostname": "db01", "status": "down"},
    {"hostname": "app01", "status": "up"},
    {"hostname": "dns01", "status": "down"}
   ]

   def check_servers_status():
    """Check each server and print its status."""
    for server in servers:
        hostname = server["hostname"]
        status = server["status"]

        if status == DOWN_STATUS:
            print(f"ALERT: {hostname} is down")
        else:
            print(f"{hostname} is operational")

   if __name__ == "__main__":
      check_servers_status()
   ```
     
   </details> <!-- Ends Solution -->
   
   **End Section 1: Lesson 1**

</details> <!-- Ends Section 1: Lesson 1 -->

---





<!-- 
      *******************************
      THIS BEGINS SECTION 1: LESSON 2 
      *******************************
-->






<details>
<summary><strong>Lesson 2 - README Files</strong></summary>
   **Learning Objectives**
   - Produce a README file that clearly documents the purpose, usage, functionality, variables, data structures, and control logic of a Python script in a human-readable format.
   
   ---
   
   ### What is a README?
   
   A **README** is a document that explains how a script or piece of software works.\
   It should allow another person to understand the purpose and usage of the script **without reading the source code**.
   
   ---

   ### README Example Structure

   A good README usually includes:
   - Project Title
   - Purpose / Overview
   - Usage Instructions
   - Configuration Variables
   - Data Structures
   - Logic Overview
   - Example Execution / Output
   
   ---

   ### Practical Task

   **Overview**  
   You will create a README file for a provided Python automation script.  
   Your README should clearly explain what the script does and how to use it.
   
   **What the Script Does**
   - Checks the status of several servers
   - Prints a normal message if the server is operational
   - Prints a warning if the server needs attention
   - Prints an alert if the server is down
   
   ---
   
   ### Required Sections
   
   Your README must include the following:
   
   - **Project Title**
   - **Purpose / Overview**
   - **Usage Instructions**
   - **Configuration Variables**
   - **Data Structures**
   - **Logic Overview**
   - **Example Execution / Output**
   
   ---

   ### Script to Document
   
   ```python
   """
   Monitors server status values and reports whether each server is operational.
   
   This script checks a list of servers and prints either an alert message
   or a normal status message based on each server's current condition.
   """
   
   DOWN_STATUS = "down"
   WARNING_STATUS = "warning"
   
   servers = [
       {"hostname": "web01", "status": "up"},
       {"hostname": "db01", "status": "down"},
       {"hostname": "app01", "status": "warning"},
       {"hostname": "dns01", "status": "up"}
   ]
   
   def check_servers():
       """Check each server and print a message based on its status."""
       for server in servers:
           hostname = server["hostname"]
           status = server["status"]
   
           if status == DOWN_STATUS:
               print(f"ALERT: {hostname} is down")
           elif status == WARNING_STATUS:
               print(f"WARNING: {hostname} needs attention")
           else:
               print(f"{hostname} is operational")
   
   if __name__ == "__main__":
       check_servers()
   ```

   ---

   <!--
   **********************
         Solution 
   **********************
   -->
   
   <details>
   <summary><strong>Solution</strong></summary>
   
  **Server Status Monitor**

  **Purpose / Overview**\
  This Python script monitors the status of a small group of servers and prints a message for each one.\
  It simulates a basic system monitoring task by checking whether a server is operational, in a warning state, or down.

  ---
  
  **Usage Instructions**
  Run the script bash:
  ```Bash
  python server_status_monitor.py
  ```
  When the script runs, it checks each server in the list and prints a message based on its status.

  ---
  
  **Configuration Variables**
   
   | **Variable** | **Type** | **Description** |
   |:-------------|:--------:|:----------------|
   | DOWN_STATUS  | string   | The status value that indicates a server is down |
   | WARNING_STATUS | string | The status value that indicates a server needs attention |
   | servers | list | A list of dictionaries containing server names and status values |

   ---
   
   **Data Structures**\
   The script uses a list of dictionaries to store server information. 
   - The list stores multiple server records.
   - Each dictionary represents one server.
   - Each server dictionary contains:
     - `hostname` → the name of the server
     - `status` → the current status of the server 
   
   **Example:**
   `{"hostname": "web01", "status": "up"}`

   ---
         
   **Logic Overview**\
   The script uses a `for` loop to iterate through the list of servers.\
   For each server, it evaluates the `status` value: 
   - If the status equals `DOWN_STATUS` → print an alert
   - If the status equals `WARNING_STATUS` → print a warning
   - Otherwise → print that the server is operational
   This decision-making is controlled with `if`, `elif`, and `else` statements. 
   
   **Example Execution / Output**
   
   **Command:**
   ```Bash
   python server_status_monitor.py
   ```
   
   **Example output**
   ```
   web01 is operational 
   ALERT: db01 is down 
   WARNING: app01 needs attention 
   dns01 is operational
   ```
   
   </details> <!-- Ends Solution -->

   ---
   
   **End Section 1: Lesson 2**

   </details> <!-- Ends Section 1: Lesson 2 -->
   
   
---

**End Section 1**

</details> <!-- Ends Section 1 -->

---














<!-- 
      *******************************
      THIS BEGINS SECTION 2 
      *******************************
-->










<details>
<summary><strong>Section 2 - Create Python Scripts</strong></summary>

---

**Prepare for the Assessment**\
To prepare for the assessment ask yourself these questions:
- Can I develop a Python script that uses if-else statements to monitor system conditions and automatically triggers an alert or action based on specified criteria?
- Can I create a Python script utilizing for and while loops to iterate through directories and files, performing automated backups and logging the results for each file processed?
- Can I create a Python script that processes data extracted from a file, applies control structures to organize the information, and stores the results for reporting purposes?

---


<!-- 
      *******************************
      THIS BEGINS SECTION 2: LESSON 1 
      *******************************
-->




<details><summary><strong>Lesson 1 - Using Conditional Logic to Automate System Monitoring</strong></summary>

**Learning Objectives**\
This lesson addresses the following learning objective:
- Write a Python script that uses conditional logic to monitor defined system conditions and trigger automated alerts or actions based on specified criteria.

**Conditional Statements**

Conditional statements allow automated systems to perform different actions based on system conditions.

There are three key steps in the workflow process:
- Monitoring
- Evaluating
- Acting

**Monitoring** involves constantly checking the various system conditions and reading their current values.

**Evaluating** takes those values and compares them to expected results. 

**Acting** allows the script to make decisions based on how the current values compare to the expected value. 

```
MAX_FAILED_LOGINS = 5

failed_login_attempts = 7 # Simulated monitoring value

# Monitoring
print("Checking failed login attempts...")

# Evaluating
if failed_login_attempts > MAX_FAILED_LOGINS:
   # Acting
   print("ALERT: Too many failed login attempts detected.")
else:
   # Acting
   print("Login activity is within acceptable limits.")
```

**Triggers**

  | **IT Trigger** | **Condition Being Checked** | **Example Automated Action** |
  |----------------|-----------------------------|------------------------------|
  | Disk usage threshold exceeded | Disk usage percentage is greater than a defined limit (e.g., >85% | Attempt to restart the service or notify an administrator |
  | Service down | A required system service is not running. | Attempt to restart the service or notify an administrator. |
  | File exceeds size limit | A file grows larger than a configured maximum size. | Archive the file, compress it, or delete old logs. |
  | Failed log-in count exceeds threshold | The number of failed log-in attempts exceeds a defined limit. | Log the event, send a security alert, or temporarily lock the account. |
  | High CPU usage | CPU utilization exceeds a defined threshold. | Log the event or trigger a scaling or restart action. |
  | Network connectivity failure | A server or device cannot be reached over the network. | Generate an alert or retry the connection. |


**Magic Numbers**\
Numeric values written directly into code without explanation or context.

**For Example:**
```
if disk_usage > 85:
   print("ALERT: Disk usage too high")
```
**Cleaner Approach**
```
MAX_DISK_USAGE_PERCENT = 85

if disk_usage > MAX_DISK_USAGE_PERCENT:
   print("ALERT: Disk usage too high")
```

**Measurable Conditions**\
A clear rule that a script can evaluate to determine whether an action should occur.

**Steps in designing measurable conditions:**
1) Identifying a quantifiable system metric.
2) Define a threshold value.


**Thresholds**\
Define the point at which a system condition becomes significant enough to requie action.

**Comparison Operators**

  | **Operator** | **Purpose** | **Example** | **Meaning** |
  |--------------|-------------|-------------|-------------|
  | == | Equal to | if status == "running": | Checks if two values are the same |
  | != | Not equal to | if service_status != "running": | Checks if two values are different |
  | >	| Greater than | if disk_usage > MAX_DISK_USAGE: | True if the left value is larger than the right |
  | < | Less than | if cpu_usage < MAX_CPU_USAGE: | True if the left value is smaller than the right |
  | >= | Greater than or equal to | if retry_count >= MAX_RETRIES: | True if the value is greater than or equal to the limit |
  | <= | Less than or equal to | if temperature <= SAFE_LIMIT: | True if the value is less than or equal to the threshold |


**Logical Operators**\
Python uses three main logical operator: and, or, not

| **Logical Operator** | **Purpose** | **Example** | **Meaning** |
|----------------------|-------------|-------------|-------------|
| and	| Returns True only if both conditions are true | if cpu_usage > CRITICAL_THRESHOLD and memory_usage > CRITICAL_THRESHOLD: | The condition is true only when both CPU and memory usage exceed CRITICAL_THRESHOLD, which may indicate heavy system load. |
| or | Returns True if at least one condition is true | if service_down or network_unreachable: | The condition is true if either the service is down or the network cannot be reached, triggering an alert. |
| not | Reverses the result of a condition | if not service_running: | The condition is true when the service is not running, meaning the system may need to restart the service or notify an administrator. |


**Deeply Nested Logic**\
Occurs when multiple conditional statements are placed inside one another repeatedly, creating several layers of indentation. 

**Example:**
```
CRITICAL_THRESHOLD = 90
server_reachable = True
disk_usage = 92
service_running = False

if server_reachable:
   if disk_usage > CRITICAL_THRESHOLD:
      if not service_running:
        print("Alert: Server reachable, disk usage high, and service is down.")
```

**Clearer Alternative**
```
CRITICAL_THRESHOLD = 90
server_reachable = True
disk_usage = 92
service_running = False

if server_reachable and disk_usage > CRITICAL_THRESHOLD and not service_running:
   print("Alert: Server reachable, disk usage high, and service is down.")
```

**Alerts and Actions**

An **alert** is a notification that indicates a condition has occurred.\
Example of an alert:
```
if disk_usage > MAX_DISK_USAGE:
   print("Alert: Disk usage exceeds safe threshold.")
```

An **action**, on the other hand, is an automated response that attempts to resolve or manage the condition.\
Example of an action:
```
if log_file_size > MAX_LOG_SIZE:
   archive_log_file()
```

**Functions as Responses**\
Calling functions as responses is important in automation scripts because it helps organize actions in a clear, reusable, and maintainable way.\
Example:
```
"""Defines what to do when an alert occurs"""
def send_alert():
   print("Alert: Disk usage exceeded safe threshold.")

"""Checks to see if a condition is met that requires action/alert"""
if disk_usage > MAX_DISK_USAGE:
   send_alert()
```

**Separating Condition Checks from Action Logic**\
A condition check determines whether a specific situation has occurred, while action logic performs the task that responds to that situation.

Example with mixed logic (less clear):
```
CRITICAL_THRESHOLD = 90
disk_usage = 92

if disk_usage > CRITICAL_THRESHOLD:
   print("Alert: Disk usage too high")
   with open("alert_log.txt", "a") as file:
      file.write("Disk usage exceeded threshold\n")
```
Example with separated logic:
```
CRITICAL_THRESHOLD = 90

def send_alert():
   print("Alert: Disk usage too high")

disk_usage = 92

if disk_usage > CRITICAL_THRESHOLD:
   send_alert()
```

The following is a table of common automated actions that may be triggered by automation scripts when certain monitoring conditions are met.

| **Trigger Condition** | **Automated Action** | **Purpose of the Action** |
|-----------------------|----------------------|---------------------------|
| Disk usage exceeds threshold | Send alert notification | Warn administrators before storage becomes critically full |
| Service stops running | Restart the service | Restore system functionality automatically |
| Failed login attempts exceed limit | Lock user account or trigger security alert | Prevent potential unauthorized access |
| Log file exceeds size limit | Archive or compress log file | Prevent storage issues and maintain log history |
| Network device unreachable | Retry connection or log failure | Detect connectivity issues and record them for troubleshooting |
| CPU usage exceeds threshold | Log the event or scale system resources | Identify system overload and maintain performance |
| Backup job fails | Retry backup process | Ensure critical data is successfully backed up |
| Configuration drift detected | Reapply correct configuration | Maintain consistent system configuration |

---

**End Section 2: Lesson 1**




</details> <!-- Ends Section 2: Lesson 1 -->

---






<!-- 
      *******************************
      THIS BEGINS SECTION 2: LESSON 2 
      *******************************
-->








<details>
<summary><strong>Lesson 2 - Reading and Writing Files</strong></summary>

**Learning Objectives**
- Develop a Python script that uses `for` and `while` loops to iterate through directories and files
- Perform automated backups
- Log the results for each file processed

---

### Python Imports

Importing allows you to reuse code from other modules or libraries.

**Basic syntax:**\
from module import item


**Example:**
```
Python

from netmiko import ConnectHandler

device = {
    "device_type": "cisco_ios",
    "host": "192.168.1.1",
    "username": "admin",
    "password": "password",
}

connection = ConnectHandler(**device)
output = connection.send_command("show ip interface brief")
print(output)
connection.disconnect()
```

---

### Files and Folders

Every file has two key components:
- **Filename** — the name of the file
- **Path** — the location of the file

| **Path Type** | **Description** | **Example** |
|---------------|-----------------|-------------|
| Absolute Path | Full path starting from root | `C:/Users/Frank/Documents/file.txt` |
| Relative Path | Path relative to the current working directory | `Documents/file.txt` |

---

### Working with Paths (pathlib)

Python’s Path class (from the pathlib module) makes working with file paths easier and more consistent across operating systems.

```
Python

from pathlib import Path

current_directory = Path.cwd()   # Current working directory
home_directory = Path.home()     # User’s home directory
```

**Joining paths:**
```
Python

file_path = Path.cwd() / "logs" / "report.txt"
```

**Creating folders:**
```
Python

folder_path = Path("processed")
folder_path.mkdir(exist_ok=True)
```

---

### Reading and Writing Files

There are three basic steps when working with files:
1. Open the file
2. Read from or write to the file
3. Close the file

Recommended method (using with):
```
Python

from pathlib import Path

file_path = Path("example.txt")

# Write to a file
with open(file_path, "w") as file:
    file.write("This is a sample line of text.\n")
    file.write("Python file handling with Path objects.")

# Read from a file
with open(file_path, "r") as file:
    content = file.read()

print(content)
```

Using `with` automatically closes the file when the code block completes.

---

### Working with CSV Files

CSV files store tabular data using commas to separate values.

```
Python

import csv

with open("devices.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

---

### Applied Practice: Process and Save a Network Device List

**Task**
1. Read the device list from devices.txt
2. Add the label - READY FOR AUTOMATION to each device
3. Overwrite the original file with the updated content
4. Create a directory named processed
5. Save a copy of the updated list as devices_processed.txt inside the processed folder

**Expected Output:**
```
text

router1 - READY FOR AUTOMATION
switch1 - READY FOR AUTOMATION
firewall1 - READY FOR AUTOMATION
```

---

<details>
<summary><strong>Solution</strong></summary>

```
Python

from pathlib import Path

# Set up file paths
project_dir = Path(__file__).parent
devices_file = project_dir / "devices.txt"
processed_dir = project_dir / "processed"
processed_file = processed_dir / "devices_processed.txt"

# Part 1: Read the file
with open(devices_file, "r") as file:
    lines = file.readlines()

# Part 2: Modify the data
updated_lines = []
for line in lines:
    device = line.strip()
    if device:
        updated_line = f"{device} - READY FOR AUTOMATION\n"
        updated_lines.append(updated_line)

# Part 3: Write back to the original file
with open(devices_file, "w") as file:
    file.writelines(updated_lines)

# Part 4: Create the directory
processed_dir.mkdir(exist_ok=True)

# Part 5: Save a copy in the new directory
with open(processed_file, "w") as file:
    file.writelines(updated_lines)

print("Device list updated and saved to processed directory.")

```
</details> <!-- Ends Solution -->

---

**End Section 2: Lesson 2**


</details> <!-- Ends Section 2: Lesson 2 -->

---






<!-- 
      *******************************
      THIS BEGINS SECTION 2: LESSON 3 
      *******************************
-->









<details>
<summary><strong>Lesson 3 - Organizing Files and Folders</strong></summary>

**Learning Objectives**
- Develop a Python script that processes data from a file
- Apply control structures to organize information
- Store results for reporting purposes

---

### The `shutil` Module

The `shutil` module provides functions for copying, moving, renaming, and deleting files and folders.

### Copying Files
```python
import shutil

shutil.copy("source.txt", "destination.txt")
```

**Copying Entire Folders**
```python
shutil.copytree("source_folder", "destination_folder")
```

**Moving Files or Folders**
```Python
shutil.move("source.txt", "destination.txt")
shutil.move("source_folder", "new_location/source_folder")
```

---

#### Deleting Files and Folders

| **Function** | **Purpose** |
|--------------|-------------|
| `os.unlink(path)` | Delete a single file |
| `os.rmdir(path)`  | Delete an empty folder |
| `shutil.rmtree(path)` | Delete a folder and all of its contents |

**Examples:**
```Python
import os
import shutil

os.unlink("example.txt")              # Delete a file
shutil.rmtree("example_folder")       # Delete a folder and everything inside it
```

---

### Listing Files and Folders

Using `os.listdir()`:
```python
import os

items = os.listdir("example_folder")
for item in items:
    print(item)
```

**Using `pathlib`:**
```python
from pathlib import Path

folder = Path("example_folder")
for item in folder.iterdir():
    print(item)
```

---

### Walking a Directory Tree (`os.walk`)

`os.walk()` lets you visit every folder and file in a directory tree.\
It returns three values on each loop:
1. Current folder name
2. List of subfolders
3. List of files

```python
import os
from pathlib import Path

for folder_name, subfolders, filenames in os.walk(Path.home() / "spam"):
    print("Current folder:", folder_name)
    
    for subfolder in subfolders:
        print("  Subfolder:", subfolder)
    
    for filename in filenames:
        print("  File:", filename)
```

---

### Storing Results for Reporting

**Summary Directories**
```python
summary = {
    "processed": 0,
    "skipped": 0,
    "failed": 0
}

files = ["data.txt", "image.png", "report.txt"]

for file in files:
    if not file.endswith(".txt"):
        summary["skipped"] += 1
    else:
        summary["processed"] += 1

print(summary)
```

**Writing a Simple Report**
```python
summary = {
    "processed": 10,
    "skipped": 2,
    "failed": 1
}

with open("report.txt", "w") as report:
    report.write("Processing Summary\n")
    report.write("------------------\n")
    report.write(f"Processed: {summary['processed']}\n")
    report.write(f"Skipped: {summary['skipped']}\n")
    report.write(f"Failed: {summary['failed']}\n")
```

**Writing CSV Output**
```python
import csv

data = [
    ["hostname", "status"],
    ["server01", "active"],
    ["server02", "inactive"]
]

with open("report.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(data)
```

---

### Best Practice: Separate Processing from Reporting

**Less clear (mixed logic):**
```python
error_count = 0
with open("system.log", "r") as file:
    for line in file:
        if "ERROR" in line:
            error_count += 1
            print("Error found:", line.strip())
```

**Cleaner approach:**
```python
def count_errors(file_path):
    count = 0
    with open(file_path, "r") as file:
        for line in file:
            if "ERROR" in line:
                count += 1
    return count

def report_results(error_count):
    print(f"Total errors: {error_count}")
```

---

### Applied Practice: Organizing Network Configuration Files

**Goal**
- Create a backup of the configuration files
- Rename files to a standard naming convention
- Move outdated files into an archive folder
- Remove temporary files

**Starting Structure:**
```text
network_cleanup_lab/
├── configs/
│   ├── router1.cfg
│   ├── switch1.cfg
│   ├── old_firewall.cfg
│   └── temp/
│       └── test.cfg
```

**Desired Final Structure:**
```text
network_cleanup_lab/
├── configs/
│   ├── router1_config.txt
│   └── switch1_config.txt
├── configs_backup/
│   ├── router1.cfg
│   ├── switch1.cfg
│   └── old_firewall.cfg
└── archived/
    └── old_firewall.cfg
```

---

<details>
<summary><strong>Solution</strong></summary>

```python
from pathlib import Path
import shutil

# Set up paths
project_dir = Path(__file__).parent
configs_dir = project_dir / "configs"
backup_dir = project_dir / "configs_backup"
archived_dir = project_dir / "archived"

# Part 1: Backup the configs directory
if not backup_dir.exists():
    shutil.copytree(configs_dir, backup_dir)
    print("Configs directory backed up.")

# Part 2: Rename files
router_file = configs_dir / "router1.cfg"
switch_file = configs_dir / "switch1.cfg"

if router_file.exists():
    router_file.rename(configs_dir / "router1_config.txt")

if switch_file.exists():
    switch_file.rename(configs_dir / "switch1_config.txt")

print("Files renamed.")

# Part 3: Archive old file
archived_dir.mkdir(exist_ok=True)
old_firewall = configs_dir / "old_firewall.cfg"

if old_firewall.exists():
    shutil.move(str(old_firewall), archived_dir / old_firewall.name)

print("Old firewall config archived.")

# Part 4: Delete temporary directory
temp_dir = configs_dir / "temp"
if temp_dir.exists():
    shutil.rmtree(temp_dir)

print("Temporary files removed.")
print("Cleanup complete.")
```

</details> <!-- End Solution -->

---

**End Section 2: Lesson 3**

</details> <!-- Ends Section 2: Lesson 3 -->

---

**End Section 2**





</details> <!-- Ends Section 2 -->

---













<!-- 
      *******************************
      THIS BEGINS SECTION 3 
      *******************************
-->













<details><summary><strong>Section 3 - Integrate Python Modules</strong></summary>

---

**Prepare for the Assessment**  
To prepare for the assessment, ask yourself these questions:
- Can I develop a Python script that uses if-else statements to monitor system conditions and automatically triggers an alert or action based on specified criteria?
- Can I create a Python script utilizing for and while loops to iterate through directories and files, performing automated backups and logging the results for each file processed?
- Can I create a Python script that processes data extracted from a file, applies control structures to organize the information, and stores the results for reporting purposes?

---












<!-- 
      *******************************
      THIS BEGINS SECTION 3: LESSON 1 
      *******************************
-->












<details>
<summary><strong>Lesson 1 - Automating Network Connectivity Checks</strong></summary>

**Learning Objectives**
- Develop a Python script that uses standard library modules to automate network connectivity checks and log the results to a file

---

### Connectivity Checks

Connectivity checks verify whether systems, services, and network resources are reachable.

**Common uses:**
- Service availability monitoring
- Server health validation
- Pre-deployment checks
- Scheduled uptime monitoring

**Manual vs Automated Testing**

| Type | Description | Example |
|------|-------------|---------|
| **Manual** | Person runs the check and interprets results | `ping example.com` |
| **Automated** | Script performs the check and evaluates the result | `if check_connection("example.com"):` |

---

### Useful Standard Library Modules

| Module | Purpose |
|--------|---------|
| `socket` | Test if a host/port is reachable |
| `subprocess` | Run system commands (like `ping`) |
| `datetime` | Add timestamps to logs |
| `os` / `pathlib` | Work with files and directories |

**Socket example:**
```python
import socket

try:
    socket.create_connection(("example.com", 80), timeout=5)
    print("Connection successful")
except OSError:
    print("Connection failed")
```

**Subprocess (ping) example:**

```python
import subprocess

HOST = "192.168.1.1"

result = subprocess.run(
    ["ping", "-c", "1", HOST],
    capture_output=True,
    text=True
)

if result.returncode == 0:
    print(f"SUCCESS: {HOST} is reachable")
else:
    print(f"ERROR: {HOST} is not reachable")
```

---

### Control Structures for Connectivity Logic

**Basic pattern:**
1. Perform a connection check
2. Store the result (True / False)
3. Use if-else to respond

```python
is_connected = check_connection()

if is_connected:
    print("Connection successful")
else:
    print("Connection failed")
```

---

### Exeception Handling

Use `try-except` to prevent scripts from crashing.

**Bad (silent failure):**

```python
try:
    connect_to_server()
except Exception:
    pass
```

 **Better:**

 ```python
try:
    connect_to_server()
except Exception as error:
    print(f"ERROR: Connection failed - {error}")
```

---

### Meaningful Status Messages

Avoid vague messages like "Done".

**Better:**

```python
print("Backup completed successfully for report.txt")
print(f"ERROR: Unable to reach {host}")
```

---

### Logging Results

```python
from datetime import datetime
from pathlib import Path

log_file = Path("network_log.txt")
timestamp = datetime.now()

with open(log_file, "a") as log:
    log.write(f"{timestamp} - Connection check completed\n")
```

---

### Applied Practice: Network Automation Report with Email and Logging

**Overview**

You are building a simple network automation script that does the following:
- processes a list of devices
- logs whether each device succeeded or failed
- sends a summary email with the results

**Project Setup**

Create this structure:
- network_reporting_lab\
   - devices.txt
   - automation.log

devices.txt contains the following:

router1  
switch1  
firewall1  
bad_device  

**Instructions**

Step 1: Configure logging.
- log messages to automation.log
- use
  - INFO for successful processing
  - ERROR for failures

Step 2: Process devices.
- Read devices from devices.txt.
- For each device
  - if the device is "bad_device" → log an error
  - otherwise → log success 
- Keep track of the following:
  - number of successes
  - number of failures

Step 3: Send an email.
- Create an email message using email.message.EmailMessage.
- Include the following:
  - total successes
  - total failures 
- Send the email using a local SMTP debug server.

**Expected Output**  
2026-04-29 10:00:00 - INFO - router1 processed successfully  
2026-04-29 10:00:00 - INFO - switch1 processed successfully  
2026-04-29 10:00:00 - INFO - firewall1 processed successfully  
2026-04-29 10:00:00 - ERROR - bad_device failed to process  
2026-04-29 10:00:01 - INFO - Email sent successfully  

---

<details>
<summary><strong>SOLUTION</strong></summary>

```python
import logging
from pathlib import Path
import smtplib
from email.message import EmailMessage

# Setup paths
project_dir = Path(__file__).parent
devices_file = project_dir / "devices.txt"
log_file = project_dir / "automation.log"

# Step 1: Configure logging
logging.basicConfig(
   filename=log_file,
   level=logging.INFO,
   format="%(asctime)s - %(levelname)s - %(message)s"
)

# Step 2: Process devices
success_count = 0
failure_count = 0

with open(devices_file, "r") as file:
   devices = [line.strip() for line in file if line.strip()]

for device in devices:
   if device == "bad_device":
      logging.error(f"{device} failed to process")
      failure_count += 1
   else:
      logging.info(f"{device} processed successfully")
      success_count += 1

# Step 3: Create and send email
msg = EmailMessage()
msg["Subject"] = "Network Automation Report"
msg["From"] = "sender@example.com"
msg["To"] = "recipient@example.com"

msg.set_content(f"""
Automation Summary:

Successful devices: {success_count}
Failed devices: {failure_count}
""")

# Send email (assumes local SMTP debug server is running)
with smtplib.SMTP("localhost", 1025) as server:
   server.send_message(msg)

logging.info("Email sent successfully")

print("Automation complete. Check the log file and SMTP output.")
```
   
</details> <!-- End Solution -->

---


















**End Section 3: Lesson 1**

</details> <!-- This ends Section 3: Lesson 1 -->

---












<!-- 
      *******************************
      THIS BEGINS SECTION 3: LESSON 2 
      *******************************
-->












<details>
<summary><strong>Lesson 2 - Automating Network Device Configuration</strong></summary>

**Learning Objectives**
- Use third-party libraries to connect to and configure network devices
- Understand the role of external packages in automation scripts

---

### Why Use Third-Party Libraries?

The standard library is powerful, but some tasks (like managing network devices) are much easier with specialized libraries.

Common example: `netmiko` for SSH connections to network devices.

```python
from netmiko import ConnectHandler

device = {
    "device_type": "cisco_ios",
    "host": "192.168.1.1",
    "username": "admin",
    "password": "password",
}

connection = ConnectHandler(**device)
output = connection.send_command("show ip interface brief")
print(output)
connection.disconnect()
```

---

### Best Practices with External Packages

- Install only what you need
- Prefer standard library when possible
- Keep imports organized at the top of the script
- Avoid hard-coding credentials

---

### Applied Practice: Reviewing VyOS Router Information with NAPALM

**Overview**  You are working in a lab environment with a VyOS router. Your task is to use Python and NAPALM to connect to the router and collect basic device information.

The router has the following details:

IP address: 10.10.10.1  
Username: vyos  
Password: vyos  

Make sure NAPALM is installed.

**Instructions**

Step 1: Import NAPALM.
- Import get_network_driver from the napalm library 

Step 2: Define the VyOS connection.
- Create variables for the following:
  - IP Address
  - username
  - password 

Step 3: Connect to the router.
- Use the NAPALM vyos driver to open a connection to the router.

Step 4: Retrieve device facts. 
- Use get_facts() to collect information:
  - hostname
  - vendor
  - model
  - operating system version
  - uptime
  - interfaces 

Step 5: Retrieve interface information.
- Use get_interfaces() to collect interface status details.

Step 6: Print the results. 
- Display the router facts and interface information in the terminal.

---

<details>
<summary><strong>SOLUTION</strong></summary>

```python
from napalm import get_network_driver

# Device connection information
ip_address = "10.10.10.1"          # Best to not hard code things that may change
username = "vyos"                  # NEVER hard code usernames
password = "vyos"                  # NEVER EVER hard code passwords

# Select the VyOS NAPALM driver
driver = get_network_driver("vyos")

# Create the device connection object
router = driver(
   hostname=ip_address,
   username=username,
   password=password
)

# Open the connection
router.open()

print("Connected to VyOS router")

# Retrieve device facts
facts = router.get_facts()

print("\nDevice Facts")
print("------------")
print(f"Hostname: {facts['hostname']}")
print(f"Vendor: {facts['vendor']}")
print(f"Model: {facts['model']}")
print(f"OS Version: {facts['os_version']}")
print(f"Uptime: {facts['uptime']} seconds")

print("\nInterfaces")
print("----------")

for interface in facts["interface_list"]:
   print(interface)

# Retrieve interface details
interfaces = router.get_interfaces()

print("\nInterface Details")
print("-----------------")

for interface_name, details in interfaces.items():
   print(f"\nInterface: {interface_name}")
   print(f"Enabled: {details['is_enabled']}")
   print(f"Up: {details['is_up']}")
   print(f"Description: {details['description']}")
   print(f"MAC Address: {details['mac_address']}")
   print(f"Speed: {details['speed']} Mbps")

# Close the connection
router.close()

print("\nConnection closed")
```
   
</details> <!-- End Solution -->















---

**End Section 3: Lesson 2**
   
</details> <!-- Ends Section 3: Lesson 2 -->




</details> <!-- Ends Section 3 -->

---


<!-- End of File -->


