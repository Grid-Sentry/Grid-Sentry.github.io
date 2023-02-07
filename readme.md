<!-- ---
layout: default
--- -->
# API reference  |  [User Guide](user_guide.md)
# Grid-Sentry.github.io
This is the documentation page for Grid sentry
# API reference- gspentest.iec61850.goose

For importing to python code: **Import gspentest.iec61850**

# Class: gspentest.iec61850.goose

## Nested classes:

## Private method:

| **Function name** | **Details** |
| --- | --- |
| mac\_to\_hex(mac\_id) | Convert mac id it to standard format 0xffffffffffff |

#### mac\_to\_hex()
| **Field** | **Details** |
| --- | --- |
|**Description** | The function is a private function, which can convert different types of mac address into the standard format of 0xffffffffffff.
| **Parameters:** | mac\_id : string Specifies the the mac id in formats such as ff-ff-ff-ff-ff-ff, ff:ff:ff:ff:ff:ff, ff-ff-ff-ff-ff-ff/ ff-ff-ff-ff-ff-ff or ff:ff:ff:ff:ff:ff/ ff:ff:ff:ff:ff:ff |
| **Returns** : | Mac\_id: hexReturns a hexadecimal number with the format 0xffffffffffff |
| **Usage:** | out =mac\_to\_hex("ff:ff:ff:ff:ff:ff")print(out)\>\> 0xffffffffffff |

## Functions:

| **Function name** | **Details** |
| --- | --- |
| goose.snoop(interface) | Capture goose packets |
| goose.filter(packet) | Filter goose packets based on specified filters |
| goose.modify() | Modify different aspects of the packet |
| goose.push() | Push the packet on the specified networking interface with time delay between packets |
| goose.report() | Generate report for the goose packets received |

<br>
<br>


#### goose.snoop(interface, t=1000) 
|Field        |   Information                          |
|-----------------	|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|
|**Description**    |   The module when ran captures the GOOSE messages flowing in the network for the time specified by the user. Since the GOOSE messages are multicast, the attacker system being on the same network can capture the packets sent by any device.  <br> The time in seconds is to be specified by the user manually. The code identifies all the messages flowing in the network and only selects the GOOSE packets. <br> The function returns a dictionary type object with all the goose packets. <br> These snooped packets can then be saved to a file as a PCAP or text file. Which can be accessed by the user. |
| **Parameters:** 	| **interface: string**<br>Specifies the network interface to start capturing messages on.<br>**t: int, default=100**<br>Time for which the packet are to be captured. Default 1 second 	|
| **Returns**     	| **packet: dict**<br>Returns a dictionary containing all the GOOSE packets                                                                                                             	|
| **Usage:**      	| out =goose.snoop(“eth0”, t=15000) <br>print(out) <br>>> {timestamp:[1.1, 1.2], length:[167,167], }                                                                                    	|

<br>
<br>

#### goose.filter(packet, src\_mac=0x000000000000/0x000000000000, dst\_mac=0x000000000000/0x000000000000, length=-1, capture\_time=[0, -1])
|Field              |   Information                          |
|-----------------	|---------------------------------------	|
|**Description**    | The module picks up a dictionary and filters messages based on the Source MAC ID, Destination MAC ID, and length of the packet. The type of filter is to be specified by the user.<br>The function returns a dictionary type object with all the goose packets filtered based on the type of filter.<br>The packets can be saved as a PCAP file where the user can do further forensics on the packets. |
| **Parameters:** 	| **packet : dict** <br>The dictionary containg all goose packets on which the filter is to be applied<br>**src\_mac : {"hex", "hex/hex\_mask", [hex, hex, hex,..]}, default=0x000000000000/0x000000000000**<br>Filter based on source mac id. Input can be single mac id(string), mac id with mask(string) and an array of mac ids(array of strings). Default value is all possible mac ids<br>**dst\_mac : {"hex", "hex/hex\_mask", [hex, hex, hex,..]}, default=0x000000000000/0x000000000000** <br>Filter based on destination mac id. Input can be single mac id (string), mac id with mask(string) and an array of mac ids(array of strings). Default value is all possible mac ids<br>**length : {int, [int, int]}, default=-1** <br>Filter based on length of packet. Input can be integer, array of 2 integers. If an array is given, the first element corresponds to lower limit of length and the second corresponds to upper limit of length. Default value is -1 which specifies that all packets need to be selected.<br> **capture\_time : {"float", ["float", "float"]}, default = [0,-1]**<br>Filter base on capture time. Input can be float where one time is specified or array of 2 floats.<br>If an array is given, the first element corresponds to lower limit of captured time and the second corresponds to upper limit of captured time. |
| **Returns**     	|**packet : dict**    |
| **Usage:**      	| Source mac formats: 11:ff:06:30:01:01/11-ff-06-30-01-01/0x11ff06300101<br>**goose.filter** (packet, src\_mac=0x11ff06300101/0xffff000000000, length=167, capture\_time=[0, -1])	|

<br>
<br>

#### **goose.modify** (packet, gocb=None, payload=None, stnum=None, sqnum=None,capture\_time=None, src\_mac=None, dst\_mac=None, appid=None, length=none)
|Field              |   Information                          |
|-----------------	|---------------------------------------	|
| **Deascription**      | Given a certain GOOSE packet, the submodules can create a replica of the packet and modify the contents based on the user's requirements.. The function allows the user to manually change the parameters of the packet.|
| **Parameters** : | **packet : dict** <br> Input is a dict type variable which containing one or multiple rows. <br> **gocb : {str, ["str", …]}, default = None** <br> Modify the gocb value in the packet. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **Payload : array, default= None** <br> The originally Payload is removed and this payload is attached. The size of old and new payload need not be same. If a single packet is to be modified then 1-d array is the input. If multiple packets need to be modified, then 2-D array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **stnum : {int, [int, …]}, default= None**<br>Modify the stnum parameter. If a single packet is to be modified then int is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **sqnum : {int, [int, …]}, default= None**<br>Modify the sqnum parameter. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **time : {float, [float, …]}, default = None**<br>Modify the timestamp in the packet. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **src\_mac= {hex, [hex, …]}, default= None**<br>Modify the source mac id. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **dst\_mac= {hex, [hex, …]}, default= None**<br>Modify the destination mac id. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **appid: {int, [int, …]} default= None**<br>Modify the appid of the packet. If a single packet is to be modified then string is the input. If multiple packets need to be modified, then array is the input where number of elements matching the number of rows in dict. No change if not specified <br> **length: {int, "nochange", [int, …]}, default = None**<br>Custom change the length of the packet by specifying the integer length or enter string "no change" tokeep the original length. If not specified, the code automatically calculates the correct length of the packet and modifies it. If input packet has multiple rows, then array input is given.|
| **Returns** : | **Packet:dict** |
| **Usage:** | **goose.modify** (packet, gocb=IED3simpleIO$meas$GGIO.3, payload=[[True, True]], stnum=8, sqnum=150) <br> or <br> **goose.modify** (packet, gocb=IED3simpleIO$meas$GGIO.3, payload=[[True, True],[False, True],[False False]], stnum=[7,8,9] sqnum=[150,1,1]) |

<br>
<br>

#### **goose.push** (packet, interface, delay = 100)
|Field              |   Information                          |
|-----------------	|---------------------------------------	|
| **Deascription**      | Given a packet, the submodule can be used to push it into the network without changing the source mac ID in the frame. Thus, the sending device’s MAC ID won’t be reflected on the frame. The function also allows the user to push the packet repeatedly into the network, to do so the user needs to provide the module with a time interval between two consecutive packets. The code doesn’t return any output, but the effect of the packet can be seen on the devices accepting the original messages. The network can also be scanned to see the packets sent by this module.|
| **Parameters** : | **packet: dict** <br>The dictionary of packet needed to be pushed in the network. <br> **Interface: str**<br>Networking interface to be used for pushing the packets <br> **Delay: {int, array}, default = 100ms**<br>Delay between the consecutive packets. The integer value in milliseconds is to be specified for constant time between the packets. An array of any size can be specified. The function will create a repeated array of size same as packet dict based on the delay array.|
| **Returns** : | **None** |
| **Usage:** | **goose.push**(packet, "eth1", delay = 10)<br>**goose.push**(packet, "eth1", delay = [10, 15, 20]) |

