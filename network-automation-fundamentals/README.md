# Fundamentals

## Bad Scripting
Let's look at an example of a bad Python script that returns the result as expected (output is correct):

```
x=input("What is your name:")
print ("how are you"+x)
y="how are you"+x
if ("test1" in y) and ("test2" in y):
print ("cool") x=y.split(" ") x=x[2]+"awesome" if ("are" in x):
     print ("not cool")
```


After the second or third line of code as we read through, we lose the understanding of program flow, and what the expected result was. Eventually, it becomes very difficult to interpret even a simple script such as this.
Imagine how difficult it would be for someone who has not written this code to interpret a bigger script (say, 50 lines).

Now, let's modify this code to make it readable:

```
   #ask for input of user's name and prints it with a message
x=input("What is your name:") print ("how are you"+x) y="how are you"+x
   #validates and prints message if 'test1' AND 'test2' exists in input
   if ("test1" in y) and ("test2" in y):
       print ("cool")
   #splits the sentence stored in variable x with blank spaces
x=y.split(" ")
print (x)
#adds the string "awesome" to the third word in the sentence and stores it in x
x=x[2]+"awesome"
[6 ]
    #validates if word "are" is in x and prints the message accordingly
   if ("are" in x):
       print ("not cool")
```


As we can see, each section (or line) that achieves a specific result is tagged by a remark line (denoted by #). This line is a human-readable line that is ignored by the program (or compiler) and is used to ensure any reader of the program understands what is going on in each section. This ensures that each and every aspect of the script is easily understood by the reader; as the script is enhanced, troubleshooting and modifications in the program become very easy.
Another key aspect in the readability of a program is to ensure we add some key information at the very start of the code.
A generic suggestion would be to include the following:
The author's name
Version of the script (starts with 1.0)
One-liner description of basic usage of the script Any specific installation requirements

As an example, let 's add this to the very top of the preceding script:
#Name: Abhishek Ratan
#Version: 1.0
#Usage: Asks for user input and validates it for some specific keywords #Additional installation required: None

### Basic programs
Taking this forward, let's write some basic scripts or programs using Python that can help us understand how to leverage Python in our daily automation tasks.
Validating an IPv4 address
This example will show us how to validate an IP address format, given as an input:
```
ip_address=input("Enter IP address: ")
   #remove any extra characters
ip_address=ip_address.strip()
   #initialize a flag to point to true for an ip address
 ip_address_flag=True
#validate if there are only 3 dots (.) in ip address
if (not(ip_address.count('.') == 3)): ip_address_flag=False
else:
#Validate if each of the octet is in range 0 - 255
ip_address=ip_address.split(".") for val in ip_address:
val=int(val)
if (not(0 <= val <=255)):
ip_address_flag=False
   #based upon the flag value display the relevant message
   if (ip_address_flag):
       print ("Given IP is correct")
   else:
       print ("Given IP is not correct")
```
The sample output is as follows:
>>
Enter IP address: 100.100.100.100 Given IP is correct
>>>
Enter IP address: 2.2.2.258 Given IP is not correct
>>>
Enter IP address: 4.7.2.1.3 Given IP is not correct
>>>
As we can see, based upon our validations in the script, the output of our program, returns a validation status of True or False for the IP address that was given as input.
As we move forward, it's important to know that Python, or any programming language, has multiple predefined functions/libraries that can be utilized to perform particular functions. As an example, let's see the earlier example of validating the IPv4 address, using a prebuild library (socket) in Python:
import socket
addr=input("Enter IP address: ") try:
socket.inet_aton(addr)
print ("IP address is valid") except socket.error:
       print ("IP address is NOT valid")
[8 ]
  
Fundamental Concepts of Network Automation
The sample output is as follows:
>>
Enter IP address: 100.100.100.100 IP address is valid
>>>
Enter IP address: 2.2.2.258
IP address is NOT valid
>>>
Enter IP address: 4.7.2.1.3
IP address is NOT valid
>>>
In the preceding approach, using a prebuilt library helps us to ensure that we do not have to reinvent the wheel (or create our own logic for something that has already been developed by other developers), and also ensures our script remains lean and thin while achieving the same expected results.
Making the right choice
In this example, we will use a switch case to identify the right set of configurations based upon certain input given by the user.
As a prerequisite understanding, the syntax of the exec-timeout command based upon OS is as follows:
Cisco IOS command: exec-timeout 15 0 Cisco NXOS command: exec-timeout 15
   #create a dictionary:
config={
"IOS":"exec-timeout 15 0", "NXOS":"exec-timeout 15" }
getchoice=input("Enter IOS type (IOS/NXOS) : ") if (getchoice == "IOS"):
print (config.get("IOS")) if (getchoice == "NXOS"):
print (config.get("NXOS"))
The sample output is as follows:
>
Enter IOS type (IOS/NXOS) : IOS exec-timeout 15 0
[9 ]
Chapter 1
   
Fundamental Concepts of Network Automation Chapter 1
 >>>
Enter IOS type (IOS/NXOS) : NXOS exec-timeout 15
>>>
In the preceding example, we have tackled a common challenge of using a switch case in Python. Unlike some other languages, Python does not provide a switch case statement, hence we need to use a dictionary to overcome this. Using this approach, we can remove the usage of multiple if statements and directly call the dictionary values based upon the mappings done in the dictionary.
Hiding credentials
This is another common problem engineers face. There are times when we need to ask for password as input from the user. As the user types in the password, it is clearly visible on the screen, and view able by anyone watching the screen. Additionally, there are times when we need to save the credentials, but need to ensure they are not visible in the script as clear-text passwords (which is a cause of concern as we share the scripts among fellow engineers). In this example, we will see how to overcome this challenge.
The code to perform encryption and decryption on the given credentials is as follows:
import getpass
import base64
#ask for username .. will be displayed when typed uname=input("Enter your username :")
#ask for password ... will not be displayed when typed
#(try in cmd or invoke using python command)
p = getpass.getpass(prompt="Enter your password: ")
#construct credential with *.* as separator between username and password creds=uname+"*.*"+p
   ###Encrypt a given set of credentials
def encryptcredential(pwd): rvalue=base64.b64encode(pwd.encode()) return rvalue
   ###Decrypt a given set of credentials
def decryptcredential(pwd): rvalue=base64.b64decode(pwd) rvalue=rvalue.decode() return rvalue
[ 10 ]
  
Fundamental Concepts of Network Automation
Chapter 1
 encryptedcreds=encryptcredential(creds)
print ("Simple creds: "+creds)
print ("Encrypted creds: "+str(encryptedcreds))
print ("Decrypted creds: "+decryptcredential(encryptedcreds))
The sample output is as follows:
C:\gdrive\book2\github\edition2\chapter1>python credential_hidings.py Enter your username :Myusername
Enter your password:
Simple creds: Myusername*.*mypassword
Encrypted creds: b'TXl1c2VybmFtZSouKm15cGFzc3dvcmQ=' Decrypted creds: Myusername*.*mypassword
As we can see in the preceding example, we have used two libraries: getpass and base64. The getpass library gives us the advantage of not echoing (or displaying) what we type on the screen, and the value gets stored in the variable that we provide.
Once we have the username and password, we can use it to pass it to the relevant places. Another aspect that we see here is that we can hard code our username and password in the script without showing it in clear text, using the base64 library to encode our credentials.
In the preceding example, a combination of the Myusername username and
the mypassword password have been separated by a *.* tag and it is converted to base64 as b'TXl1c2VybmFtZSouKm15cGFzc3dvcmQ='. The b in front denotes the byte format as base64, which works on byte instead of strings. In this way, the same encoded value of bytes can be hardcoded in a script, and the decrypt function can take that as input and provide back the username and password to be used for authentication.
