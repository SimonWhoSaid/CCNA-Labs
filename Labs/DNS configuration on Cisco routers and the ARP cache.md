# DNS Configuration on Cisco Routers and The ARP Cache

## Configure the Routers as DNS Clients
The DNS server in this example has been assigned the IP Address on 10.10.10.10/24. The DNS server is able to resolve DNS request for the clients 'R1', 'R2', and 'R3'. There is no domain name in use.
Our first objectives are:
- To configure 'R1', 'R2', and 'R3' to use 10.10.10.10/24 as their DNS server
-  Verify that you can ping R2 and R3 from R1 using their hostnames 'R2' and 'R3'
-  Verify that you can ping R1 and R2 from R3 using their hostnames 'R1' and 'R2'

## Examine the ARP Cache on the Routers
Then our second objective is to examine the ARP cache on the routers.
- Do you expect to see an entry for R3 in the ARP cache of R1? Explain why or why not.
- Verify the ARP cache on R1, R2, and R3. What do you see?

# Network Topology

<img width="667" height="463" alt="Lab Topology" src="https://github.com/user-attachments/assets/7733dbcd-e64b-45d8-a4eb-0b8a6a5aefb9" />


# Router 1
## Configuring as a DNS Client
- Before configuring the router as a DNS client we must enable the router in global configuration. We first do this by entering '_Enable_' which puts the router in Privleged Exec mode, then we input '_Config T_' to get into the global configuration
>R1>enable
>
>R1#config t
>
>Enter configuration commands, one per line.  End with CNTL/Z.

Then we must set up the router to become a DNS client with the following: 
>R1(config)#ip domain-lookup
- This enables DNS hostname translation
>R1(config)#ip name-server 10.10.10.10
- This points the router to the DNS server that is assigned the IP address of 10.10.10.10

## Router 1 Verifying Ping to R2 and R3
Next we will exit out of global configuartion mode by typing 'exit' then we will type enable again to enter Privleged Exec mode.

Afterwards we are going to test to see if R1 can ping R2 by it's hostname and get back the IP address
>R1#Ping R2
>
>Translating "R2"...domain server (10.10.10.10)
>
>Type escape sequence to abort.
>
>Sending 5, 100-byte ICMP Echos to 10.10.10.2, timeout is 2 seconds:
>
>.!!!!
>
>Success rate is 80 percent (4/5), round-trip min/avg/max = 0/1/4 ms

We will also test with R3
>R1#Ping R3
>
>Translating "R3"...domain server (10.10.10.10)
>
>Type escape sequence to abort.
>
>Sending 5, 100-byte ICMP Echos to 10.10.20.1, timeout is 2 seconds:
>
>.!!!!
>
>?Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms

## Router 1 Examining ARP Cache
To show the ARP cache of a router you must enter the command ***show arp*** in *privleged exec mode*.

When viewing the ARP table for R1 it only shows the IP and MAC addresses of

R1 10.10.10.1

R2 10.10.10.2

DNS Server 10.10.10.10

When viewing the ARP table for R1 we only see the R1, R2, and the DNS Server's IP address displayed. This is because they are all within the same subnet. Because a ARP request is broadcast traffic, this means that from R1 it will not reach R3. Instead R1 will know to reach R3 by going through R2 and vice versa.

# Router 2
## Router 2 Configuring DNS Server
We will repeat the process of of what we did with Router 1 on Router 2
>Enable
>
>Config T
>
>ip domain-lookup
>
>ip name-server 10.10.10.10
>
>end
>
>Ping R1
>
>Ping R3

## Router 2 Examining ARP Cache
When viewing the ARP table for R2 it shows

R1 10.10.10.1

R2 F0/0 10.10.10.2

DNS Server 10.10.10.10

R2 F1/0 10.10.20.1

R3 10.10.20.2

Because R2 sits in the middle of everything it will receive ALL ARP request from each device on the network. It will receive request from both the DNS Server and R1 out of interface F0/0 which has the IP address on the 10.10.10.2/24 network. It will also receive
an ARP request from R3 from interface F1/0 on the 10.10.20.0/24 network.

# Router 3 
## Router 3 Configuring DNS Server
Once again we repeat the process of what we did with the other two routers
>Enable
>
>Config T
>
>ip domain-lookup
>
>ip name-server 10.10.10.10
>
>end
>
>Ping R1
>
>Ping R2

## Router 3 Examining ARP Cache
When viewing the ARP table for R3 it shows

R2 10.10.20.1

R3 10.10.20.2

Once again because R3 and R2 are within the same network they can only see each other. So if R3 wanted to send a packet to R1, it knows to go through R2 in order to send the traffic.

