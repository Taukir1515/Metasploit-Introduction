As previously mentioned, the console will be your main interface to the Metasploit Framework. You can launch it using the  <mark style="background: #D2B3FFA6;">msfconsole</mark> command on your AttackBox terminal or any system the Metasploit Framework is installed on.

![[Pasted image 20231123015357.png | 1080]]

## <mark style="background: #FF5582A6;">ls </mark>
Once launched, you will see the command line changes to msf6 (or msf5 depending on the installed version of Metasploit). The Metasploit console (msfconsole) can be used just like a regular command-line shell, as you can see below. The first command is <mark style="background: #D2B3FFA6;">ls</mark> which lists the contents of the folder from which Metasploit was launched using the <mark style="background: #D2B3FFA6;">msfconsole</mark> command.

## <mark style="background: #FF5582A6;">ping</mark>
It is followed by a <mark style="background: #D2B3FFA6;">ping</mark> sent to ==Google's DNS IP address (8.8.8.8)==. As we operate from the AttackBox, which is Linux we had to add the <mark style="background: #D2B3FFA6;">-c 1</mark> option, so only a single ping was sent. Otherwise, the ping process would continue until it is stopped using <mark style="background: #D2B3FFA6;">CTRL+C.</mark>

![[Pasted image 20231123015518.png]]

## <mark style="background: #FF5582A6;">clear</mark> 
It will support most Linux commands, including <mark style="background: #D2B3FFA6;">clear</mark> (to clear the terminal screen), but will not allow you to use some features of a regular command line (e.g. does not support output redirection), as seen below.

![[Pasted image 20231123015538.png]]

## <mark style="background: #FF5582A6;">help</mark>
While on the subject, the help command can be used on its own or for a specific command. Below is the help menu for the set command we will cover soon.

![[Pasted image 20231123015557.png]]

## <mark style="background: #FF5582A6;">history</mark>
You can use the history command to see commands you have typed earlier.

![[Pasted image 20231123015613.png]]

An important feature of msfconsole is the support of tab completion. This will come in handy later when using Metasploit commands or dealing with modules. For example, if you start typing <mark style="background: #D2B3FFA6;">he</mark> and <mark style="background: #D2B3FFA6;">press the tab key</mark>, you will see it auto-completes to <mark style="background: #D2B3FFA6;">help</mark>.

Msfconsole is managed by context; this means that unless set as a global variable, all parameter settings will be lost if you change the module you have decided to use. In the example below, we have used the ms17_010_eternalblue exploit, and we have set parameters such as RHOSTS. If we were to switch to another module (e.g. a port scanner), we would need to set the RHOSTS value again as all changes we have made remained in the context of the ms17_010_eternalblue exploit. 

Let us look at the example below to have a better understanding of this feature. We will use the <mark style="background: #FFB86CA6;">MS17-010 “Eternalblue” exploit</mark> for illustration purposes.

Once you type the use <mark style="background: #D2B3FFA6;">exploit/windows/smb/ms17_010_eternalblue</mark> command, you will see the command line prompt change from msf6 to “<mark style="background: #D2B3FFA6;">msf6 exploit(windows/smb/ms17_010_eternalblue)</mark>”. The "<mark style="background: #FFB86CA6;">EternalBlue</mark>" is an exploit allegedly developed by the U.S. National Security Agency (N.S.A.) for a vulnerability affecting the SMBv1 server on numerous Windows systems. The <mark style="background: #FFB86CA6;">SMB (Server Message Block)</mark> is widely used in Windows networks for file sharing and even for sending files to printers. <mark style="background: #FFB86CA6;">EternalBlue was leaked by the cybercriminal group "Shadow Brokers" in April 2017. In May 2017, this vulnerability was exploited worldwide in the WannaCry ransomware attack. </mark>

![[Pasted image 20231123015716.png]]

The module to be used can also be selected with the use command followed by the number at the beginning of the search result line.

While the prompt has changed, you will notice we can still run the commands previously mentioned. This means we did not "enter" a folder as you would typically expect in an operating system command line.

![[Pasted image 20231123015745.png]]

The prompt tells us we now have a context set in which we will work. You can see this by typing the show options command.

![[Pasted image 20231123015806.png]]

This will print options related to the exploit we have chosen earlier. The show options command will have different outputs depending on the context it is used in. The example above shows that this exploit will require we set variables like RHOSTS and RPORT. On the other hand, a post-exploitation module may only need us to set a SESSION ID (see the screenshot below). A session is an existing connection to the target system that the post-exploitation module will use.

![[Pasted image 20231123015837.png]]

The show command can be used in any context followed by a module type (auxiliary, payload, exploit, etc.) to list available modules. The example below lists payloads that can be used with the ms17-010 Eternalblue exploit.

![[Pasted image 20231123015858.png]]

If used from the msfconsole prompt, the show command will list all modules.

The use and show options commands we have seen so far are identical for all modules in Metasploit.

You can leave the context using the back command.

![[Pasted image 20231123015941.png]]

Further information on any module can be obtained by typing the info command within its context.

![[Pasted image 20231123020001.png]]

Alternatively, you can use the info command followed by the module’s path from the msfconsole prompt (e.g. info exploit/windows/smb/ms17_010_eternalblue). Info is not a help menu; it will display detailed information on the module such as its author, relevant sources, etc.

#Search
One of the most useful commands in msfconsole is search. This command will search the Metasploit Framework database for modules relevant to the given search parameter. You can conduct searches using CVE numbers, exploit names (eternalblue, heartbleed, etc.), or target system.

![[Pasted image 20231123020056.png]]

The output of the search command provides an overview of each returned module. You may notice the “name” column already gives more information than just the module name. You can see the type of module (auxiliary, exploit, etc.) and the category of the module (scanner, admin, windows, Unix, etc.). You can use any module returned in a search result with the command use followed by the number at the beginning of the result line. (e.g. use 0 instead of use auxiliary/admin/smb/ms17_010_command)

Another essential piece of information returned is in the “rank” column. Exploits are rated based on their reliability. The table below provides their respective descriptions.

![[Pasted image 20231123020133.png]]


|[Source: https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking](https://github.com/rapid7/metasploit-framework/wiki/Exploit-Ranking)|

You can direct the search function using keywords such as type and platform. 

For example, if we wanted our search results to only include auxiliary modules, we could set the type to auxiliary. The screenshot below shows the output of the search type:auxiliary telnet command. 

![[Pasted image 20231123020229.png]]


Please remember that exploits take advantage of a vulnerability on the target system and may always show unexpected behavior. A low-ranking exploit may work perfectly, and an excellent ranked exploit may not, or worse, crash the target system.

## Answer the questions below

1. How would you search for a module related to Apache?

2. Who provided the auxiliary/scanner/ssh/ssh_login module?