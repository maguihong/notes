# Metasploit Object Model

![MSF architecture](../../../.gitbook/assets/metasploit-unleashed_metasploit-architecture_msf-architecture.png)

* In the Metasploit Framework, all modules are **Ruby** classes.
* Modules inherit from the **type-specific class**.
* The type-specific class inherits from the **Msf::Module class**.
* There is a **shared common API** between modules.
* Payloads are slightly different.
  * Payloads are **created at runtime** from various components.
  * Glue together **stagers** with **stages**.

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/metasploit-object-model/" %}



