# NT Privilege Escalation

## Overview

C++ program designed to escalate privileges from an Administrator account to the NT AUTHORITY\SYSTEM account. NT AUTHORITY\SYSTEM is the account with the highest level of permissions in the Windows OS. This tool is intended for educational and research purposes only, to demonstrate potential security vulnerabilities in systems.

## Code Explanation

The code is a C++ program that attempts to run a specified application with SYSTEM-level privileges on a Windows system by finding a process running with SYSTEM-level privileges and then duplicating its access token to create a new process with the same privileges.

### Function Details

- **getToken:** 
  - Takes a process ID (`pid`) and returns a handle to the process's access token (`cToken`).
  - Uses the `OpenProcess` function to open a handle to the process.
  - Uses the `OpenProcessToken` function to get the process's access token.

- **createProcess:** 
  - Takes a handle to an access token (`token`) and the path of an executable file (`app`).
  - Creates a new process with the same privileges as the process associated with the access token.
  - Uses the `DuplicateTokenEx` function to create a duplicate of the access token.
  - Uses the `CreateProcessWithTokenW` function to create the new process.

- **GetProcessUserName:** 
  - Takes a process ID (`pid`) and returns the username associated with the process's access token.
  - Uses the `OpenProcess` function to open a handle to the process.
  - Uses the `OpenProcessToken` function to get the process's access token.
  - Uses the `GetTokenInformation` function to get the user SID associated with the access token.
  - Uses the `LookupAccountSid` function to convert the SID to a username.

- **main:** 
  - Entry point of the program.
  - Prompts the user to enter the path of the application they want to run as SYSTEM.
  - Loops through all the running processes on the system using the `CreateToolhelp32Snapshot` function and the `Process32First` and `Process32Next` functions.
  - Checks the username associated with the process's access token using the `GetProcessUserName` function.
  - If the username is blank or "NT AUTHORITY\SYSTEM", it tries to create a new process with the same privileges as the current process using the `getToken` and `createProcess` functions.
  - Exits the loop and terminates the program if successful in creating the new process.

## Contributing

Feel free to submit issues or pull requests if you have suggestions or improvements.
