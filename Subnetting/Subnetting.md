# Subnetting
-  CIDR - stands for classless inter-domain routing and was introduced in 1993 to alleviate the scarcity of IPv4 IP's. 
    
    Remember to use /30 as a subnet if you only need two hosts. /31 works but unless the exam asks me to use /31, use /30, that's the standard that complies with all the internet standards.
    
    ### Split a network depending on how many subnets you want.
    
    ### C Subnet
    
    ![Untitled](CCNA/Untitled.png)
    
    Let’s say you had the network 192.168.3.0 and you want **five** subnets.
    
    To calculate how many subnets you get with subnetting. You take the bits you borrowed and calculate each bit * 2. If I borrowed 4 bits from the default of /24 from a C network then the available subnets would be 2^4 = 16. 2**2**2*2 = 16. 
    
    If the subnet mask is /30. We borrow six bits from the network address. This gives us 64 subnets (2^6). Which accommodate 2 hosts each.
    
    Think about the power of two when calculating how many subnets are needed.
    
    Take the last octet and put it into binary. 00000011. (2+1 = 3) That takes up two bits, we count from right to left, those two bits we have to subtract from the network bits, that makes the subnet mask /26. That subnet mask in dotted decimal is 255.255.255.192. That only give us 4 subnets not five because we have 64 addresses, or 62 hosts per subnet. That’s why we need to go to /27 subnet mask. That gives us 32 addresses or 30 hosts per subnet, that would give us 8 subnets.
    
    ### B Subnet
    
    172.16.0.0/255.255.0.0 and we want 60 subnets.
    
    Count up by the power of two until you reach 60. 2, 4, 8, 16, 32, 64. That’s six bits taken from the network portion. See pic below, (128 64 | **32 16 8 4 2 1**) The bold represents the six bits. Then we put the the mask into decimal by adding up the six bits we used. 128 + 64 + 32 + 16 + 8 + 4. A easier option is just to add the value together of the remaining bits, 2 and 1, then we figure out the complete number by subtracting 3 from 255 = 252.
    
    This subnet mask would give us a network range of 172.16.4.0, 172.16.8.0, etc.
    
    We find the network range by finding the block size, convert the smallest network bit converted back to a decimal number.
    
    The mask is 255.255.252.0, the smallest network bit in 252 is 4. In binary it’s 11111**1**00. Which would be 1024 hosts per network.
    
    It’s two by the power of how many network bits you have. In this case we have 10 network bits, 10 to the power of 2 is 1024.
    
    Remember, that network just needs one network address and one broadcast address. Which means we could give a computer the ip address 172.16.2.255, or 172.16.0.255, or 172.16.8.0.
    
    ![Untitled](CCNA/Untitled%201.png)
    
    ### Block Size
    
    It’s lowest network bit that you have.  Let’s say the subnet mask was 11111111 11111111 11111111 11000000, the 64 is the last bit, which means the block size is 64 and the subnet size goes up in increments of 64. 255.255.255.192, which would give us 4 subnets for that network.
    
    ### How to find the subnet mask.
    
    For 198.22.45.173/26 the subnet mask would be 255.255.255.192 because it borrows two from the network address, the first bit is 128, the second is 64 which adds up to 192.
    
    ### How many subnets
    
    To calculate how many subnets you get with subnetting. You take the bits you borrowed and calculate each bit * 2. If I borrowed 4 bits from the default of /24 from a C network then the available subnets would be 2^4 = 16. 2**2**2*2 = 16. 
    
    If the subnet mask is /30. We borrow six bits from the network address. This gives us 64 subnets (2^6). Which accommodate 2 hosts each.
    
    ### How many available hosts
    
    198.22.45.173/26
    
    If a c network uses /28 subnet mask then we have 4 bits left for hosts 2**2**2*2 = 16 - 2 for broadcast address and network address.
    
    If we have a subnet mask of /30 or 255.255.255.252. This leaves two bits for the host address since we removed two, we calculate 2**²** to figure out how many hosts we can have on that subnet. 2*2 = 4 hosts.
    
    For this example the line is after 4 which means the network goes up in increments of 4.
    
    ![Untitled](CCNA/Untitled%202.png)
    
     Muna að telja subnet bits frá vinstri til hægri. Myndinni hér fyrir neðan þá notum við 5 bits frá network address sem gefur okkur 32 subnets (2^5), hvert subnet getur haft 6 hosts. Tæknilega séð 8 en við þurfum að mínusa 2 frá vegna broadast address og network address.
    
    ![Untitled](CCNA/Untitled%203.png)
    
    ### The magic number method to figure out the number of hosts.
    
    ![Untitled](CCNA/Untitled%204.png)

	### Subnet Zero ###
![[Screenshot from 2022-02-03 09-44-25.png]]
- **For the CCNA, do not take away two subnets!**


198.22.45.173/26

What is the subnet mask in dotted decimal notation?
What is the network address, broadcast address, and valid host addresses for the IP address?


62 hosts.
4 Subnets.
198.22.45.1 - 198.22.45.62
198.22.45.65 - 198.22.45.126
198.22.45.129 - 198.22.45.190
198.22.45.193 - 198.22.45.253

Subnet mask = 255.255.255.192

-----------------------------------
200.15.10.0/24

New York Sales: 14 hosts.
New York Engineers: 28 hosts.
New York Router, needs an ip.

Boston Sales: 7 hosts.
Boston Engineers: 28 hosts.
Boston Router, needs an ip.

Point to point link between the routers.

----------------------------------------

255.255.255.224 /27
200.15.10.0 Network address
200.15.10.1 - 200.15.10.1.30
200.15.10.31 Broadcast address

200.15.10.32 Network address
200.15.10.33 - 200.15.10.1.62
200.15.10.63 Broadcast address


---------------------------------------------
New York Sales

200.15.10.0/24

255.255.255.240 /28

200.15.10.64 network address
200.15.10.79 broadcast address
200.15.10.65 - 78 hosts.

Boston sales

255.255.255.248 /29
200.15.10.80 network address
200.15.10.87 broadcast address
200.15.10.81-86 hosts

---------------
Routers.

255.255.255.252 /30



-------------------

135.15.0.0 /29
29 network bits

255.255.248.0
8 hosts per subnet


135.15.10.138
136 network address
143 broadcast


------------------------

60.0.0.0/8

255.255.255.240 how many subnets?

20 bits borrowed from the host portion and added to the network portion


-------------------------

60.15.10.75/28
what is the network address
broadcast address
range of valid ips

60.15.10.64 network address
60.15.10.79 broadcast address
60.15.10.65 - 78
how many subnets?

-----------------------------------

60.15.10.75/19
how many subnets?
Network and broadcast address
How many hosts per subnet?

11 borrowed from the network bits
the network portion has 13 bits. 13 bits = 8192. Countdown from 32. 24 bits = 254 hosts. 23 bits 512, etc.
2048 subnets
8192 hosts
60.15.0.0 network address
60.15.31.255 broadcast address
block size is 32

-----------------------------

134.65.0.0
Subnet into six different networks.
What subnet mask do you use?

It's a B network.

A simple way to figure this out is by counting
the bits. B network has 16 bits in the network portion (subnet mask)
We need six different networks, we then borrow three bits from the host portion.
Three bits is 2 - 4 - 8, which give us 8 different networks.

The network would be /19. Add the three bits to the /16 network bits.

Network addresses would be 134.65.0.0, 134.65.32.0, 134.65.64.0 etc.
8190 hosts in each subnet, 13 bits by the power of 2. Remember to -2 for network and broadcast addresses.

