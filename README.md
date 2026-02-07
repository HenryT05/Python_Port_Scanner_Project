# Simple Python Nmap Port Scanner

## Objective
This Project involves creating a network port scanning program using python. This program also includes the Nmap library to perform reconnaissance on a target system.. The main objective was to automate port scanning, service detection, OS system identification. This project helps demonstrate practical application of reconnaissance techniques.

### Skills Learned
- network reconnaissance and port scanning methodologies
- Python scripting for security automation
- Understanding Nmap library 
- Knowledge of network protocols (TCP/UDP)

### Tools Used
- Python 3 for scripting and automation
- Python-nmap library for integrating Nmap functionality
- Nmap scanning engine for port scanning and service detection
- Command-line interface for executing scans
- macOS/Linux terminal for running scripts

## Full Code
```import nmap

nm = nmap.PortScanner()

target = "45.33.32.156"

options = "-sV -sC -O"

nm.scan(target, arguments=options)

for host in nm.all_hosts():
    print(f"Host: {host} ({nm[host].hostname()})")
    print(f"State: {nm[host].state()}")
    
    if 'osmatch' in nm[host]:
        print("OS Detection Results:")
        for osmatch in nm[host]['osmatch']:
            print(f"  OS: {osmatch['name']} (Accuracy: {osmatch['accuracy']}%)")
    
    for protocol in nm[host].all_protocols():
        print(f"Protocol: {protocol}")
        port_info = nm[host][protocol]
        
        for port, state in port_info.items():
            print(f"Port: {port}\tState: {state}")
```
## Steps on Creating the Program
Importing the nmap library to add the nmap function into my program

```import nmap```

Creating an instance of the nmap PortScanner class then assigning to nm variable to use later in the program

``` nm = nmap.PortScanner() ```

Creating a target variable to define what our target is. In this case its going to be the actual nmap website that we can use to practice reconnaissance on.

``` target = "45.33.32.156" ```

Creating another varible called option to set the behaviour and function of the scan i am going to do.
-sV: version information about the services found on the port
-sC: Running nmap's default scripts
-O: Enable OS detection to identify the operating system

``` options = "-sV -sC -O" ```

Calling the scan method on the instance of the nm.PortScanner class. used to perform the network scan. using the target ip and options variables from earlier.

``` nm.scan(target, arguments=options) ``` 

Starting a for loop to iterate through the list of hosts returned by the all_hosts method of the nmap.PortScanner instance.

``` for host in nm.all_hosts(): ```

Prints the ip address and hostname.

``` print(f"Host: {host} ({nm[host].hostname()})") ```

prints if the host is up (online) or down (offline)

``` print(f"State: {nm[host].state()}") ``` 

Check if OS detection results are available and print them

```
if 'osmatch' in nm[host]:
        print("OS Detection Results:")
        for osmatch in nm[host]['osmatch']:
            print(f"  OS: {osmatch['name']} (Accuracy: {osmatch['accuracy']}%)")
```

Inner loop for iterating through each network protocol found on the host. can be tcp or udp.

``` for protocol in nm[host].all_protocols(): ```

Prints what protocol is used

``` print(f"Protocol: {protocol}")```

storing all the port information for this protocol in a variable.

```port_info = nm[host][protocol]```

another inner loop to iterate through the dictionary of ports and their states for the current protocol. using the items method
.items() gives a port number and a dictionary of of details on the given port.

``` for port, state in port_info.items(): ``` 

Prints the port number and its complete state dictionary the \t creates a tab space

``` print(f"Port: {port}\tState: {state}") ```

Now here is a result of running the program using sudo privileges. We can see it returns a list of open ports with services running on those ports. it also shows what OS the host is on. we can use this scan result to perform active reconnaisance.
<img width="3276" height="946" alt="image" src="https://github.com/user-attachments/assets/0ed9242f-02c6-4723-a097-15e8953085f0" />
