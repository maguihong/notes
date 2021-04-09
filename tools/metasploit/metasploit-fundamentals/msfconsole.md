# MSFConsole

## Benefits to Using MSFconsole

* It is the **only** supported way to access **most** of the features within Metasploit.
* Provides a **console-based interface** to the framework.
* Full **readline** support, **tabbing**, and **command completion**.
* Execution of **external commands** in msfconsole is possible: 

```bash
msf > ping -c 1 192.168.1.100
[*] exec: ping -c 1 192.168.1.100

PING 192.168.1.100 (192.168.1.100) 56(84) bytes of data.
64 bytes from 192.168.1.100: icmp_seq=1 ttl=128 time=10.3 ms

--- 192.168.1.100 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 10.308/10.308/10.308/0.000 ms
msf >
```

## How to Use the Command Prompt

### Launching MSFConsole

* MSFconsole is located in the **/usr/share/metasploit-framework/msfconsole** directory.
* The **-q** option removes the launch banner by starting msfconsole in **quiet mode**.

```bash
root@kali:# msfconsole -q
msf >
```

### Help Information

* Pass **-h** to msfconsole to see the other usage options available.

```bash
root@kali:~# msfconsole -h
Usage: msfconsole [options]

Common options
    -E, --environment ENVIRONMENT    The Rails environment. Will use RAIL_ENV environment variable if that is set.  Defaults to production if neither option not RAILS_ENV environment variable is set.

Database options
    -M, --migration-path DIRECTORY   Specify a directory containing additional DB migrations
    -n, --no-database                Disable database support
    -y, --yaml PATH                  Specify a YAML file containing database settings

Framework options
    -c FILE                          Load the specified configuration file
    -v, --version                    Show version

Module options
        --defer-module-loads         Defer module loading unless explicitly asked.
    -m, --module-path DIRECTORY      An additional module path


Console options:
    -a, --ask                        Ask before exiting Metasploit or accept 'exit -y'
    -d, --defanged                   Execute the console as defanged
    -L, --real-readline              Use the system Readline library instead of RbReadline
    -o, --output FILE                Output to the specified file
    -p, --plugin PLUGIN              Load a plugin on startup
    -q, --quiet                      Do not print the banner on startup
    -r, --resource FILE              Execute the specified resource file (- for stdin)
    -x, --execute-command COMMAND    Execute the specified string as console commands (use ; for multiples)
    -h, --help                       Show this message
```

* Entering **help** or a **?** once in the msf command prompt will display a listing of available commands along with a description of what they are used for.

```bash
msf > help

Core Commands
=============

    Command       Description
    -------       -----------
    ?             Help menu
    advanced      Displays advanced options for one or more modules
    back          Move back from the current context
    banner        Display an awesome metasploit banner
    cd            Change the current working directory
    color         Toggle color
    connect       Communicate with a host
    edit          Edit the current module with $VISUAL or $EDITOR
    exit          Exit the console
    get           Gets the value of a context-specific variable
    getg          Gets the value of a global variable
    grep          Grep the output of another command
    help          Help menu
    info          Displays information about one or more modules
    irb           Drop into irb scripting mode
    jobs          Displays and manages jobs
    kill          Kill a job
    load          Load a framework plugin
    loadpath      Searches for and loads modules from a path
    makerc        Save commands entered since start to a file
    options       Displays global options or for one or more modules
    popm          Pops the latest module off the stack and makes it active
    previous      Sets the previously loaded module as the current module
    pushm         Pushes the active or list of modules onto the module stack
    quit          Exit the console
    reload_all    Reloads all modules from all defined module paths
    rename_job    Rename a job
    resource      Run the commands stored in a file
    route         Route traffic through a session
    save          Saves the active datastores
    search        Searches module names and descriptions
    sessions      Dump session listings and display information about sessions
    set           Sets a context-specific variable to a value
    setg          Sets a global variable to a value
    show          Displays modules of a given type, or all modules
    sleep         Do nothing for the specified number of seconds
    spool         Write console output into a file as well the screen
    threads       View and manipulate background threads
    unload        Unload a framework plugin
    unset         Unsets one or more context-specific variables
    unsetg        Unsets one or more global variables
    use           Selects a module by name
    version       Show the framework and console library version numbers


Database Backend Commands
=========================

    Command           Description
    -------           -----------
    creds             List all credentials in the database
    db_connect        Connect to an existing database
    db_disconnect     Disconnect from the current database instance
    db_export         Export a file containing the contents of the database
    db_import         Import a scan result file (filetype will be auto-detected)
    db_nmap           Executes nmap and records the output automatically
    db_rebuild_cache  Rebuilds the database-stored module cache
    db_status         Show the current database status
    hosts             List all hosts in the database
    loot              List all loot in the database
    notes             List all notes in the database
    services          List all services in the database
    vulns             List all vulnerabilities in the database
    workspace         Switch between database workspaces
```

### Tab Completion

* As with most other shells, entering what you know and pressing ‘**Tab**’ will present you with a list of options available to you or auto-complete the string if there is only one option.

```bash
msf > use exploit/windows/smb/ms
use exploit/windows/smb/ms03_049_netapi
use exploit/windows/smb/ms04_007_killbill
use exploit/windows/smb/ms04_011_lsass
use exploit/windows/smb/ms04_031_netdde
use exploit/windows/smb/ms05_039_pnp
use exploit/windows/smb/ms06_025_rasmans_reg
use exploit/windows/smb/ms06_025_rras
use exploit/windows/smb/ms06_040_netapi
use exploit/windows/smb/ms06_066_nwapi
use exploit/windows/smb/ms06_066_nwwks
use exploit/windows/smb/ms06_070_wkssvc
use exploit/windows/smb/ms07_029_msdns_zonename
use exploit/windows/smb/ms08_067_netapi
use exploit/windows/smb/ms09_050_smb2_negotiate_func_index
use exploit/windows/smb/ms10_046_shortcut_icon_dllloader
use exploit/windows/smb/ms10_061_spoolss
use exploit/windows/smb/ms15_020_shortcut_icon_dllloader
msf > use exploit/windows/smb/ms08_067_netapi
```

## MSFConsole Commands

### Back

* Move back from the current context.
* **Variables** will only **carry over** if they are set **globally**.

```bash
msf auxiliary(ms09_001_write) > back
msf >
```

### Banner

* **Display** an awesome metasploit banner.

### Check

* To see if a target is vulnerable to a particular exploit **instead of actually exploiting it**.

```bash
msf exploit(ms08_067_netapi) > show options

Module options (exploit/windows/smb/ms08_067_netapi):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST    172.16.194.134   yes       The target address
   RPORT    445              yes       Set the SMB service port
   SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)

Exploit target:

   Id  Name
   --  ----
   0   Automatic Targeting

msf exploit(ms08_067_netapi) > check

[*] Verifying vulnerable status... (path: 0x0000005a)
[*] System is not vulnerable (status: 0x00000000)
[*] The target is not exploitable.
msf  exploit(ms08_067_netapi) >
```

### Color

* Enable or disable **color output**.

### Connect

* A miniature **Netcat** clone is built into the msfconsole to support SSL, proxies, pivoting, and file transfers.
* Connect to a remote host, by issuing the **connect** command with an **IP address** and **port number**.

```bash
msf > connect 192.168.1.1 23
[*] Connected to 192.168.1.1:23
DD-WRT v24 std (c) 2008 NewMedia-NET GmbH
Release: 07/27/08 (SVN revision: 10011)
DD-WRT login:
```

### Edit

* The edit command will edit the current module with **$VISUAL** or **$EDITOR**.
* By default, this will open the current module in **Vim**.

```bash
msf exploit(ms10_061_spoolss) > edit
[*] Launching /usr/bin/vim /usr/share/metasploit-framework/modules/exploits/windows/smb/ms10_061_spoolss.rb
```

### Exit

* Exit msfconsole.

### Grep

* Grep the output of another command.
* The following is an example of using **grep** to match output containing the string “**http**” from a **search** for modules containing the string “**oracle**”.

```bash
msf > grep http search oracle
   auxiliary/scanner/http/oracle_demantra_database_credentials_leak      2014-02-28       normal     Oracle Demantra Database Credentials Leak
   auxiliary/scanner/http/oracle_demantra_file_retrieval                 2014-02-28       normal     Oracle Demantra Arbitrary File Retrieval with Authentication Bypass
   auxiliary/scanner/http/oracle_ilom_login                                               normal     Oracle ILO Manager Login Brute Force Utility
   exploit/multi/http/glassfish_deployer                                 2011-08-04       excellent  Sun/Oracle GlassFish Server Authenticated Code Execution
   exploit/multi/http/oracle_ats_file_upload                             2016-01-20       excellent  Oracle ATS Arbitrary File Upload
```

### Help

* The help command will give you a **list** and small **description** of all available commands or options.

### Info

* The info command will provide **detailed** information about a particular module including all **options**, **targets**, and **other** information.
* Be sure to always **read the module description prior to using it** as some may have un-desired effects.

```bash
msf  exploit(ms09_050_smb2_negotiate_func_index) > info exploit/windows/smb/ms09_050_smb2_negotiate_func_index 

       Name: Microsoft SRV2.SYS SMB Negotiate ProcessID Function Table Dereference
     Module: exploit/windows/smb/ms09_050_smb2_negotiate_func_index
    Version: 14774
   Platform: Windows
 Privileged: Yes
    License: Metasploit Framework License (BSD)
       Rank: Good
...snip...
```

### IRB

* Running the **irb** command will drop you into a live **Ruby interpreter shell** where you can issue commands and create Metasploit scripts on the fly. \(IRB Scripting Mode\)

```bash
msf > irb
[*] Starting IRB shell...

>> puts "Hello, metasploit!"
Hello, metasploit!
=> nil
>> Framework::Version
=> "4.8.2-2014022601"
```

### Jobs

* **Display** and **terminate** jobs.

### Kill

* The kill command will **kill** any **running** jobs when supplied with the **job id**.

```bash
msf exploit(ms10_002_aurora) > kill 0
Stopping job: 0...

[*] Server stopped.
```

### Load

* The load command loads a **plugin** from Metasploit’s **plugin directory**.
* **Arguments** are passed as **key=val** on the shell.

```bash
msf > load
Usage: load  [var=val var=val ...]

Loads a plugin from the supplied path.  If path is not absolute, first looks
in the user's plugin directory (/root/.msf4/plugins) then
in the framework root plugin directory (/usr/share/metasploit-framework/plugins).
The optional var=val options are custom parameters that can be passed to plugins.

msf > load pcap_log
[*] PcapLog plugin loaded.
[*] Successfully loaded plugin: pcap_log
```

### Loadpath

* The loadpath command will load a **third-part module tree** for the path so you can point Metasploit at your 0-day exploits, encoders, payloads, etc.

```bash
msf > loadpath /home/secret/modules

Loaded 0 modules.
```

### Unload

*  The unload command **unloads** a previously loaded plugin and **removes** any extended commands.

```bash
msf > unload pcap_log
Unloading plugin pcap_log...unloaded.
```

### Resource

* Run the **commands stored in a file**.
* Use **-r** to pass a batch file to msfconsole at startup.

```bash
msf > resource karma.rc
[*] Processing karma.rc for ERB directives.
resource (karma.rc_.txt)> db_connect postgres:toor@127.0.0.1/msfbook
resource (karma.rc_.txt)> use auxiliary/server/browser_autopwn
...snip...


root@kali:~# echo version > version.rc
root@kali:~# msfconsole -r version.rc
```

### Route

* Route traffic destined to a given subnet through a supplied session.
* To add a route, you pass the **target subnet** and **network mask** followed by the **session \(comm\) number**.

```bash
meterpreter > route add 192.168.0.0 255.255.255.0 1
meterpreter > route remove 192.168.0.0/24 1
meterpreter > route get 192.168.0.11
```

### Search

* Searche **module names**, **descriptions**, **references** and etc, based on extensive regular-expression.

```bash
msf > help search
Usage: search [keywords]

Keywords:
  app       :  Modules that are client or server attacks
  author    :  Modules written by this author
  bid       :  Modules with a matching Bugtraq ID
  cve       :  Modules with a matching CVE ID
  edb       :  Modules with a matching Exploit-DB ID
  name      :  Modules with a matching descriptive name
  platform  :  Modules affecting this platform
  ref       :  Modules with a matching ref
  type      :  Modules of a specific type (exploit, auxiliary, or post)

Examples:
  search cve:2009 type:exploit app:client

msf > search usermap_script 

msf > search name:mysql

msf > search platform:aix

msf > search type:post

msf > search author:dookie

msf > search cve:2011 author:jduck platform:linux
```

### Session

* The sessions command allows you to **list**, **interact** with, and **kill** spawned sessions.
* The sessions can be **shells**, **Meterpreter** sessions, **VNC**, etc.
*  To **list** any active sessions, pass the **-l** options to sessions.
* To interact with a given session, use the **-i** **switch** followed by the **id number** of the session.

```bash
msf exploit(3proxy) > sessions -l

Active sessions
===============

  Id  Description    Tunnel
  --  -----------    ------
  1   Command shell  192.168.1.101:33191 -> 192.168.1.104:4444
  

msf exploit(3proxy) > sessions -i 1
[*] Starting interaction with 1...

C:WINDOWSsystem32>
```

### Set

* The set command allows you to **configure Framework options and parameters** for the current module you are working with.
* **Unset** removes a parameter previously configured with set.
* You can remove all assigned variables with **unset all**.

```bash
msf > set RHOSTS 192.168.1.0/24
RHOSTS => 192.168.1.0/24
msf > set THREADS 50
THREADS => 50
msf > set

Global
======

  Name     Value
  ----     -----
  RHOSTS   192.168.1.0/24
  THREADS  50

msf > unset THREADS
Unsetting THREADS...
msf > unset all
Flushing datastore...
msf > set

Global
======

No entries in data store.

msf >
```

### Setg

* Set **global variables** with  the setg command.
* The pitfall is **forgetting** you have saved globals, so always **check** your options **before** you run or exploit.
* Use the **unsetg** command to unset a global variable.

```bash
msf > setg LHOST 192.168.1.101
LHOST => 192.168.1.101
msf > setg RHOSTS 192.168.1.0/24
RHOSTS => 192.168.1.0/24
msf > setg RHOST 192.168.1.136
RHOST => 192.168.1.136
```

### Save

* Run the **save** command to save your current environment and settings, which will be automatically loaded on the **next startup**.

```bash
msf > save
Saved configuration to: /root/.msf4/config
```

### Show

* **Displays modules** of a given type, or all modules.

```bash
msf > show
msf > show auxiliary
msf > show exploits
msf > show payloads
msf > show encoders
msf > show nops
```

* When you are in the context of a particular exploit, you can:
  * run **show payloads** to display the payloads that are compatible with that particular exploit.
  * issue the **show options** command to display which settings are available and/or required for that specific module.
  * run the **show targets** command to see which targets are supported.
  * run **show** **advanced** to see more advanced options.

```bash
msf exploit(ms08_067_netapi) > show payloads
msf exploit(ms08_067_netapi) > show options
msf exploit(ms08_067_netapi) > show targets
msf exploit(ms08_067_netapi) > show advanced
```

### Use

* Selects a module by name.
* The use command changes your **context** to a specific module, exposing **type-specific commands**.

```bash
msf > use dos/windows/smb/ms09_001_write
msf auxiliary(ms09_001_write) >
```

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/msfconsole/" %}

{% embed url="https://www.offensive-security.com/metasploit-unleashed/msfconsole-commands/" %}



