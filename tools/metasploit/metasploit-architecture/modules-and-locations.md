# Modules and Locations

* Primary Modules: **/usr/share/metasploit-framework/modules/**
* Custom Modules: **~/.msf4/modules/**

```bash
root@kali:~# ls /usr/share/metasploit-framework/modules/
auxiliary  encoders  exploits  nops  payloads  post
```

### Exploits

* Exploit modules are defined as modules that **use payloads**.

```bash
root@kali:~# ls /usr/share/metasploit-framework/modules/exploits/
aix        bsdi        firefox  irix       multi    solaris
android    dialup      freebsd  linux      netware  unix
apple_ios  example.rb  hpux     mainframe  osx      windows
```

### Auxiliary

* Auxiliary modules include **port scanners**, **fuzzers**, **sniffers**, and more.

```bash
root@kali:~# ls /usr/share/metasploit-framework/modules/auxiliary/
admin    client   dos         gather  scanner  spoof  vsploit
analyze  crawler  example.rb  parser  server   sqli
bnat     docx     fuzzers     pdf     sniffer  voip
```

### Payloads, Encoders, Nops

* Payloads consist of **code that runs remotely**.
* Encoders ensure that payloads make it to their destination **intact**.
* Nops keep the **payload sizes consistent** across exploit attempts.

```bash
root@kali:~# ls /usr/share/metasploit-framework/modules/payloads/
singles  stagers  stages
root@kali:~# ls /usr/share/metasploit-framework/modules/encoders/
cmd  generic  mipsbe  mipsle  php  ppc  ruby  sparc  x64  x86
root@kali:~# ls /usr/share/metasploit-framework/modules/nops/
aarch64  armle  mipsbe  php  ppc  sparc  tty  x64  x86
```

### Loading Additional Module Trees

* Pass the **-m** option when running msfconsole to load additional modules **at runtime**.

```bash
root@kali:~# msfconsole -m ~/secret-modules/
```

* Use the **loadpath** command, If you need to load additional modules **after msfconsole being started**.

```bash
msf > loadpath
Usage: loadpath </path/to/modules>

Loads modules from the given directory which should contain subdirectories for
module types, e.g. /path/to/modules/exploits

msf > loadpath /usr/share/metasploit-framework/modules/
Loaded 399 modules:
    399 payloads
```

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/modules-and-locations/" %}



