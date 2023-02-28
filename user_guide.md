# Product guide- Penetration Testing (GOOSE module) | [API Guide](readme.md)

### 1.	Application
The VAPT GOOSE module provides a technique to snoop, filter, modify and inject GOOSE messages into the network.  The GOOSE module is designed for testing the network for protocol inconsistencies and cyber security.
The GOOSE module is supposed to be run on a system connected to the testing network. The system on which the GOOSE module is installed (host system) is supposed to be connected to the network with IEDs which are using the IEC 61850 GOOSE protocol. 

### 2.	GOOSE snooping
The module when ran captures the GOOSE messages flowing in the network for the time specified by the user. Since the GOOSE messages are multicast, the attacker system being on the same network can capture the packets sent by any device. 
The time in seconds is to be specified by the user manually. The code identifies all the messages flowing in the network and only selects the GOOSE packets. 
The function returns a dictionary type object with all the goose packets.
These snooped packets can then be saved to a file as a PCAP or text file. Which can be accessed by the user.

### 3.	GOOSE Filtering
The module picks up a dictionary and filters messages based on the Source MAC ID, Destination MAC ID, and length of the packet. The type of filter is to be specified by the user. 
The function returns a dictionary type object with all the goose packets filtered based on the type of filter.
The packets can be saved as a PCAP file where the user can do further forensics on the packets.

### 4.	Modifying packet
Given a certain GOOSE packet, the submodules can create a replica of the packet and modify the contents based on the user's requirements. The function allows the user to manually change the parameters of the packet. The parameters which can be modified by the user are as follows:
1.	GOOSE PDU Payload
2.	StNum
3.	SqNum
4.	Timestamp
The values associated with the above values which are present in a standard GOOSE message can be modified using this submodule.
The specially crafted packet’s hex code can be saved as a text file by the user.

### 5.	Pushing into the network (time delays)
Given a packet, the submodule can be used to push it into the network without changing the source mac ID in the frame. Thus, the sending device’s MAC ID won’t be reflected on the frame. The function also allows the user to push the packet repeatedly into the network, to do so the user needs to provide the module with a time interval between two consecutive packets. The code doesn’t return any output, but the effect of the packet can be seen on the devices accepting the original messages. The network can also be scanned to see the packets sent by this module.


### 6.	Report generation
The report generation submodule uses the output from GOOSE snooping and GOOSE filtering submodules to generate a JSON file which can list down the following items:
1.	Names of all the IEDs using GOOSE communication in the network.
2.	Source mac IDs of all the devices communicating through GOOSE.
3.	Name of the company supplying the IED (approximate)
4.	Logical device and logical node names of the devices present in the network.
5.	Application ID associated with each IED.
