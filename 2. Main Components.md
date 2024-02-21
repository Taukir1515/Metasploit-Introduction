While using the Metasploit Framework, you will primarily interact with the Metasploit console. You can launch it from the AttackBox terminal using  the msfconsole command. The console will be your main interface to interact with the different modules of the Metasploit Framework. Modules are small components within the Metasploit framework that are built to perform a specific task, such as exploiting a vulnerability, scanning a target, or performing a brute-force attack. 

**<mark style="background: #D2B3FFA6;">Exploit</mark>:** A piece of code that uses a vulnerability present on the target system.

Vulnerability: A design, coding, or logic flaw affecting the target system. The exploitation of a vulnerability can result in disclosing confidential information or allowing the attacker to execute code on the target system.

<mark style="background: #D2B3FFA6;">Payload:</mark> An exploit will take advantage of a vulnerability. However, if we want the exploit to have the result we want (gaining access to the target system, read confidential information, etc.), we need to use a payload. Payloads are the code that will run on the target system.

Modules and categories under each one are listed below. These are given for reference purposes, but you will interact with them through the Metasploit console (msfconsole).

## <mark style="background: #FF5582A6;">Auxiliary</mark>
Any supporting module, such as scanners, crawlers and fuzzers, can be found here. 

![[Pasted image 20231123001536.png]]


## <mark style="background: #FF5582A6;">Encoders</mark>
Encoders will allow you to encode the exploit and payload in the hope that a signature-based antivirus solution may miss them.

Signature-based antivirus and security solutions have a database of known threats. They detect threats by comparing suspicious files to this database and raise an alert if there is a match. Thus encoders can have a limited success rate as antivirus solutions can perform additional checks.

![[Pasted image 20231123003504.png]]


## <mark style="background: #FF5582A6;">Evasion</mark>
While encoders will encode the payload, they should not be considered a direct attempt to evade antivirus software. On the other hand, “evasion” modules will try that, with more or less success.

![[Pasted image 20231123003615.png]]


## <mark style="background: #FF5582A6;">Exploits</mark>
Exploits, neatly organized by target system.

![[Pasted image 20231123004343.png]]


## <mark style="background: #FF5582A6;">NOPs</mark>
NOPs (No OPeration) do nothing, literally. They are represented in the Intel x86 CPU family they are represented with 0x90, following which the CPU will do nothing for one cycle. They are often used as a buffer to achieve consistent payload sizes.

![[Pasted image 20231123005505.png]]


## <mark style="background: #FF5582A6;">Payloads</mark>
Payloads are codes that will run on the target system.

Exploits will leverage a vulnerability on the target system, but to achieve the desired result, we will need a payload. Examples could be; getting a shell, loading a malware or backdoor to the target system, running a command, or launching calc.exe as a proof of concept to add to the penetration test report. Starting the calculator on the target system remotely by launching the calc.exe application is a benign way to show that we can run commands on the target system.

Running command on the target system is already an important step but having an interactive connection that allows you to type commands that will be executed on the target system is better. Such an interactive command line is called a "shell". Metasploit offers the ability to send different payloads that can open shells on the target system. 

![[Pasted image 20231123011435.png]]

You will see four different directories under payloads: <mark style="background: #BBFABBA6;">adapters, singles, stagers and stages.</mark>

<mark style="background: #D2B3FFA6;">Adapters</mark>: An adapter wraps single payloads to convert them into different formats. For example, a normal single payload can be wrapped inside a Powershell adapter, which will make a single powershell command that will execute the payload.

<mark style="background: #D2B3FFA6;">Singles</mark>: Self-contained payloads (add user, launch notepad.exe, etc.) that do not need to download an additional component to run.

<mark style="background: #D2B3FFA6;">Stagers</mark>: Responsible for setting up a connection channel between Metasploit and the target system. Useful when working with staged payloads. “Staged payloads” will first upload a stager on the target system then download the rest of the payload (stage). This provides some advantages as the initial size of the payload will be relatively small compared to the full payload sent at once.

<mark style="background: #D2B3FFA6;">Stages</mark>: Downloaded by the stager. This will allow you to use larger sized payloads.

Metasploit has a subtle way to help you identify single (also called “inline”) payloads and staged payloads.

<mark style="background: #FFB86CA6;">generic/shell_reverse_tcp</mark> -- inline (or single) payload

<mark style="background: #FFB86CA6;">windows/x64/shell/reverse_tcp</mark> -- staged payload

Both are reverse Windows shells. The former is an inline (or single) payload, as indicated by the “_” between “shell” and “reverse”. While the latter is a staged payload, as indicated by the “/” between “shell” and “reverse”.


## <mark style="background: #FF5582A6;">Post </mark>
Post modules will be useful on the final stage of the penetration testing process listed above, post-exploitation.

![[Pasted image 20231123011706.png]]

If you wish to familiarize yourself further with these modules, you can find them under the modules folder of your Metasploit installation. For the AttackBox these are under /opt/metasploit-framework/embedded/framework/modules

# <mark style="background: #BBFABBA6;">Answer the questions below:</mark>

1. What is the name of the code taking advantage of a flaw on the target system?

2. What is the name of the code that runs on the target system to achieve the attacker's goal?

3. What are self-contained payloads called?

4. Is "windows/x64/pingback_reverse_tcp" among singles or staged payload?
