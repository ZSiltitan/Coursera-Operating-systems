
Hardware in each layer

|Hardware|Layer|Protocol|Protocol Data Unit|Addressing
|--|--| --|--|--|
|Hub|Physical|10 Base T protocol||
|Switch|Data Link|Ethernet|IP address
|Router|Network|


## Network Layer
#### 1.1
MAC address is so unique that there is no way of knowing where can find the location of the MAC address in time
**ARP** Address Resolution Protocol
Solution: Network Layer - IP

#### 1.2 IP Addresses
**32 bit (4 octets) address, ofter decribed in decimal numbers
Dotted Decimal Notation 点分十进制**
*1 octet can represent 2^8 (0-255) decimal number*
> decimal sample: 202.123.45.1
> same as: 10101100.11000011.01010011.10100001

IP address are distributed in large sections like company and organisations and belong to network (not like MAC belong to different devices)

Dynamic Host Configuration Protocol
- Static IP addresses for server and devices
- Dynamtic IP addresses for clients

#### 1.3 IP Datagrams

**IP Datagrams are the payload after encapsulation from Ethernet headers.** 
IP datagram also has a payload for upper layer.

IP datagram:  
|0|4|8|16|19|31|
|-|-|-|-|-|-|-|
|version|header length|service type(QoS)|total length|
|identification|||flag|fragment offset||
|TTL||Protocol|Header Checksum|
|source IP addr|
|dest IP addr|
|options||||padding










Version, Header Length, Service Type(QoS), Total Length,  
Identification, Flag, Fragment Offset,  
TTL, Protocol, Header Checksum,  
Source IP Address,  
Destination IP Address,  
Options, Padding

#### IP Address Classes
IP Address => Network  + Host Addresses

|Class|Range(DEC.)(BIN.)|Max Hosts|Rules|
|----|----|----|----|
|Class A|0-127 (0)|16 Million (2^24-n)|1st octet is used as Network ID|
|Class B|128-191(10)|64000(2^16-n)|1st and 2nd octets NetworkID|
|Class C|192-223(110)|254(2^8-2)|1st to 3rd octets NetworkID|
|*Class E*|224-239(1110)|N/A|For broadcasting|
|*Class F*|240-255(11110)|N/A|For testing|

In practical, the class system has been replace by CIDR (无类别域间路由) , but still very important.

#### 1.4 ARP
*Address Resolution Protocol*
**ARP table:** records MAC addresses and IP addresses associated
*ARP Process*
![](https://raw.githubusercontent.com/ZSiltitan/Coursera-Operating-systems/master/Pictures/The%20Bits%20and%20Bytes%20of%20Computer%20Networking/ARP.png)

#### 2.1 subnetting
Split a large network into a few individual subnetworks
 ``` mermaid
 graph LR
	A[Core router]--route-->B(Gateway router)
	A---C(Core routers)
	B---D(Gateway routers)
 ```

#### 2.2 Subnet Mask
```mermaid
graph LR
A[IP Address]-->B[Network ID]
A[IP Address]-->C[Host ID]
C--partially uses for---D[Subset ID]
```
**Subnet Masks**
32 bits

|IP |9.|100.|100.|100|
|:--|--|--|--|--|--|
|IP(bin)|00001001|01100100|01100100|01100100|
|Subnet Mask(bin)|11111111|1111111|11111111|00000000|
|Subnet (dec)|255.|255.|255.|0|
|Part Explanation|Network ID|with 1: Subnet ID||with 0: Host ID|

*Note: This sample has 254 host ID available because 0 is generally not used and 255 reserves a broadcast address*    
Another example:
|IP |9.|100.|100.|100|
|:-|-|-|-|-|
|Subnet|255.|255.|255.|224|
|dec|11111111|11111111|11111111|11100000|
Means only last 5 bits is host ID
The IP address can be represented as 9.100.100.100/27 (because of 27 0s)


#### 2.3 Subnet mask in binary math
Subnet mask calculation is using **AND** calculation to determine if the IP address is on the same network.
|IP Address|9|100|100|100|
|:-|-|-|-|-|
|AND|AND|AND|AND|AND|
|Subnet Mask|11111111|11111111|11111111|00000000|
|Subnet ID|9|100|100||

The subnet ID is 9.100.100, will use it to determine to check.

