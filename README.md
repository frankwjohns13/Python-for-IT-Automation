# Python for IT Automation - D522 - Notes

<details><summary><Strong>Key Terms (A running collection of terms I feel are important from each section)</Strong></summary> 

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







</details> <!-- Ends Key Terms -->

---

<details><summary><strong>Code Snippets (I will add example code here)</summary>

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


**Conditional Logic**
```
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
```
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

**Deeply Nested Logic**
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










</details> <!-- Ends Code Snippets -->

---

<!-- THIS BEGINS SECTION 1 -->

<details><summary><strong>Section 1 - Python Principles and Syntax</strong></summary>

---

**Prepare for the Assessment**\
To prepare for the assessment, ask yourself these questions:
- Can I write clean, well-documented code within Python scripts, demonstrating correct syntax and basic variable handling?
- Can I create a README file that clearly documents the purpose, usage, and functionality of Python modules and scripts in a human-readable format, including descriptions of variables, data structures, and operators used?

---


<!-- 
      *******************************
      THIS BEGINS SECTION 1: LESSON 1 
      *******************************
-->



   <details><summary><strong>Lesson 1 - Clean and Well-Documented Scripts</strong></summary>

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

   ---
   
   **Task**\
   You will refactor the provided script to improve its structure, readability, and maintainability. You must not change what the script does, only how it is written.
   
   **Overview**\
   You will refactor the provided script to improve its structure, readability, and maintainability. You must not change what the script does, only how it is written.

   **What the Script Does**\
   The script simulates a simple monitoring task:
   - It contains a list of servers.
   - Each server has a hostname and a status ("up" or "down").
   - The script does the following:
     - checks each server
     - prints a message for each one
     - displays an alert if a server is down
     - displays a normal message if the server is operational
   
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

   
   
   <!--
   **********************
         Solution 
   **********************
   -->

   
   
   <details><summary><strong>Solution (One possible solution)</strong></summary>
   
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
      def Check_servers_status(): 
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
         Check_servers_status() """ This calls the previously declared function. """
   
      ```
      
   </details> <!-- Ends Solution -->
   
   **End Lesson 1**

</details> <!-- Ends Section 1: Lesson 1 -->

---







<!-- 
      *******************************
      THIS BEGINS SECTION 1: LESSON 2 
      *******************************
-->




<details><summary><strong>Lesson 2 - README Files</strong></summary>

   **Learning Objectives**
   - Produce a README file that clearly documents the purpose, usage, functionality, variables, data structures, and control logic of a Python script in a human-readable format.
   
   **README Example:** Server Connectivity Monitor
   
   **Overview**\
   This Python script checks whether specified servers are reachable over the network and logs the results to a file. It is designed to help system administrators quickly verify connectivity to important services.
   
   **Purpose**\
   The script automates network connectivity checks for a list of servers. It attempts to connect to each server on a specified port and records whether the connection was successful.
   
   **Requirements**
   - Python 3.x
   - network access to the target servers
   
   **Usage**\
   Run the script from the command line:\
   `python connectivity_check.py`
   
   The script will attempt to connect to each server listed in the configuration section and display the results in the terminal.
   
   **Configuration**\
   The following variables can be modified inside the script:
   
   | **Variable** | **Description** |
   |--------------|-----------------|
   | SERVERS      | List of server hostnames to check |
   | PORT         | Port number used for the connection test |
   | LOG_FILE     | File where connection results are stored |
   
   
   **Example configuration in the script:**
   
   ```
   SERVERS = ["google.com", "example.com"]
   PORT = 80
   LOG_FILE = "connectivity_log.txt"
   ```
   
   **Output**\
   The script prints the connection status for each server and writes the results to a log file.
   
   **Example output:**
   ```
   google.com: REACHABLE
   example.com: UNREACHABLE
   Example log entry:
   2026-03-06T14:32:10 - google.com - REACHABLE
   ```
   
   **Notes**\
   This script is intended for basic connectivity verification and can be scheduled to run periodically using a task scheduler or cron job.

   ---
   
   **Task**\
   Write a README file for the provided script.

   Your README must do the following:
   - Clearly explain the purpose.
   - Document usage correctly.
   - Describe the configuration variables.
   - Explain the data structures used.
   - Summarize the control logic.
   - Include example execution and output.
   - Use clear formatting.
   - Be understandable without reading the script.
   
   **Overview**\
   You will create a README file for a provided Python automation script. Your README should explain the script clearly enough that another person can understand what the script does and how to use it without opening         the source code.

   **What the Script Does**\
   The provided script checks the status of several servers and prints a message for each one.

   Depending on the server's status, the script will perform the following:
   - Print a normal message if the server is operational.
   - Print a warning if the server needs attention.
   - Print an alert if the server is down.

   Your README should explain this behavior clearly.
   
   **Required Sections**\
   Your README must include these sections:
   - Project Title
   - Purpose/Overview
   - Usage Instructions
   - Configuration Variables
   - Data Structures
   - Logic Overview
   - Example Execution/Output

   ```
   Automation Script
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
   
  <details><summary><strong>Solution</strong></summary>
   
   ## Applied Practice S1L2
   **Server Status Monitor**
  
   **Purpose / Overview**\
   This Python script monitors the status of a small group of servers and prints a message for each one. It is designed to 
   simulate a basic system monitoring task by checking whether a server is operational, in a warning state, or down.\
   The script helps demonstrate how conditional logic can be used to evaluate system conditions and produce appropriate 
   output. 
   
   **Usage Instructions**
   Run the script in Python:
   python server_status_monitor.py
   When the script runs, it checks each server in the list and prints a message based on its status. 
   
   **Configuration Variables**
   
   | **Variable** | **Type** | **Description** |
   |:-------------|:--------:|:----------------|
   | DOWN_STATUS  | string   | The status value that indicates a server is down |
   | WARNING_STATUS | string | The status value that indicates a server needs attention |
   | servers | list | A list of dictionaries containing server names and status values |
   
   **Data Structures**\
   The script uses a list of dictionaries to store server information. 
   - The list stores multiple server records.
   - Each dictionary represents one server.
   - Each server dictionary contains:
     - hostname: the name of the server
     - status: the current status of the server 
   
   **Example:**
   `{"hostname": "web01", "status": "up"} `\
   This structure makes it easy to loop through all servers and evaluate each one individually. 
      
   **Logic Overview**\
   The script uses a for loop to iterate through the list of servers. For each server, it checks the value of the status field. 
   - If the status is equal to DOWN_STATUS, the script prints an alert.
   - If the status is equal to WARNING_STATUS, the script prints a warning.
   - Otherwise, the script prints that the server is operational. 
   This decision-making is controlled with if, elif, and else statements. 
   
   **Example Execution / Output**
   
   **Example command**\
   `python server_status_monitor.py `
   
   **Example output**
   ```
   web01 is operational 
   ALERT: db01 is down 
   WARNING: app01 needs attention 
   dns01 is operational
   ```
   
   </details> <!-- Ends Solution -->

   ---
   
   **End Lesson 2**

   ---

   **End Section 1**
   
   
   </details> <!-- Ends Section 1: Lesson 2 -->
   
   
</details> <!-- Ends Section 1 -->

---









<!-- 
      *******************************
      THIS BEGINS SECTION 2 
      *******************************
-->


<details><summary><strong>Section 2 - Create Python Scripts</strong></summary>

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












</details> <!-- Ends Section 2: Lesson 1 -->

---




<!-- 
      *******************************
      THIS BEGINS SECTION 2: LESSON 2 
      *******************************
-->


<details><summary><strong>Lesson 2 - Reading and Writing Files</strong></summary>








</details> <!-- Ends Section 2: Lesson 2 -->


---





<!-- 
      *******************************
      THIS BEGINS SECTION 2: LESSON 3 
      *******************************
-->


<details><summary><strong>Lesson 3 - Organizing Files and Folders</strong></summary>








</details> <!-- Ends Section 2: Lesson 3 -->







</details> <!-- Ends Section 2 -->

---










<!-- 
      *******************************
      THIS BEGINS SECTION 3 
      *******************************
-->

<details><summary><strong>Section 3 - Integrate Python Modules</strong></summary>


<!-- 
      *******************************
      THIS BEGINS SECTION 3: LESSON 1 
      *******************************
-->


<!-- 
      *******************************
      THIS BEGINS SECTION 3: LESSON 2 
      *******************************
-->




</details> <!-- Ends Section 3 -->

---


<!-- End of File -->


