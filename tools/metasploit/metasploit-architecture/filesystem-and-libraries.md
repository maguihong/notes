# Filesystem and Libraries

## Metasploit Filesystem

* **/usr/share/metasploit-framework**

```bash
root@kali:~# ls /usr/share/metasploit-framework/

... 

...

```

### Data

* The data directory contains **editable files** used by Metasploit to store **binaries** required for certain exploits, wordlists, images, and more.

```bash
root@kali:~# ls /usr/share/metasploit-framework/data/
cpuinfo              ipwn           meterpreter  snmp            webcam
eicar.com            isight.bundle  mime.yml     sounds          wmap
eicar.txt            john.conf      msfcrawler   SqlClrPayload   wordlists
emailer_config.yaml  lab            passivex     templates
exploits             logos          php          vncdll.x64.dll
flash_detector       markdown_doc   post         vncdll.x86.dll
```

### Documentation

* The documentation directory contains the available **documentation** for the framework.

```bash
root@kali:~# ls /usr/share/metasploit-framework/documentation/
changelog.Debian.gz  CONTRIBUTING.md.gz  developers_guide.pdf.gz  README.md
CODE_OF_CONDUCT.md   copyright           modules
```

### Lib

* The lib directory contains the ‘meat’ of the **framework code base**.

```bash
root@kali:~# ls /usr/share/metasploit-framework/lib/
anemone        msfenv.rb        rbmysql.rb  sqlmap
anemone.rb     net              rex         tasks
enumerable.rb  postgres         rex.rb      telephony
metasm         postgres_msf.rb  robots.rb   telephony.rb
metasploit     rabal            snmp        windows_console_color_support.rb
msf            rbmysql          snmp.rb
```

### Modules

* The modules directory is where you will find the actual MSF modules for **exploits**, **auxiliary** and **post modules**, **payloads**, **encoders**, and **nop generators**.

```bash
root@kali:~# ls /usr/share/metasploit-framework/modules/
auxiliary  encoders  exploits  nops  payloads  post
```

### Plugins

```bash
root@kali:~# ls /usr/share/metasploit-framework/plugins/
aggregator.rb      ips_filter.rb  openvas.rb           sounds.rb
alias.rb           komand.rb      pcap_log.rb          sqlmap.rb
auto_add_route.rb  lab.rb         request.rb           thread.rb
beholder.rb        libnotify.rb   rssfeed.rb           token_adduser.rb
db_credcollect.rb  msfd.rb        sample.rb            token_hunter.rb
db_tracker.rb      msgrpc.rb      session_notifier.rb  wiki.rb
event_tester.rb    nessus.rb      session_tagger.rb    wmap.rb
ffautoregen.rb     nexpose.rb     socket_logger.rb
```

### Scripts

* The scripts directory contains **Meterpreter** and other **scripts**.

```bash
root@kali:~# ls /usr/share/metasploit-framework/scripts/
meterpreter  ps  resource  shell
```

### Tools

* The tools directory has various useful **command-line utilities**.

```bash
root@kali:~# ls /usr/share/metasploit-framework/tools/
context  dev  exploit  hardware  memdump  modules  password  recon
```

## Metasploit Libraries

### REX

* The basic library for most tasks
* Handles sockets, protocols, text transformations, and others
* SSL, SMB, HTTP, XOR, Base64, Unicode

### MSF::CORE

* Provides the ‘**basic**’ API
* **Defines** the Metasploit Framework

### MSF::BASE

* Provides the ‘**friendly**’ API
* Provides **simplified** APIs for use in the Framework

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/filesystem-and-libraries/" %}



