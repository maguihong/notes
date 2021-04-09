# Mixins and Plugins

## A Quick Diversion into Ruby

* Every Class only has **one parent**.
* A class may include **many Modules**.
* Modules can add new **methods**.
* Modules can **overload** old methods.
* Metasploit modules inherit **Msf::Module** and include **mixins** to add **features**.

## Metasploit Mixins

* Mixins include one class into another ****\(**Inclusion**\). This is different to **inheritance**. 
* Mixins can **override** a class’ methods and **change behavior**. 
* Mixins can add **new features** and allows modules to have different ‘flavors’.

```ruby
class MyParent
     def woof
          puts “woof!”
     end
end

class MyClass > MyParent
end

object = MyClass.new
object.woof() => “woof!”

================================================================

module MyMixin
     def woof
          puts “hijacked the woof method!”
     end
end

class MyBetterClass > MyClass
     include MyMixin
end
```

## Metasploit Plugins

* Plugins work directly with the **API**. 
* Plugins hook into the **event subsystem**. 
* They **automate** specific tasks that would be tedious to do manually.
* Plugins **only** work in the **msfconsole**.
* Plugins can add **new console commands** and **extend** the overall Framework functionality.

## References

{% embed url="https://www.offensive-security.com/metasploit-unleashed/mixins-plugins/" %}



