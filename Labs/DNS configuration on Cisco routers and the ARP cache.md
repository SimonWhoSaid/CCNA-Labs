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
<img width="760" height="482" alt="Cisco Packet Tracer Topology" src="https://github.com/user-attachments/assets/b67f581b-8bb0-44e3-be14-41b61827f611" />


# Router 1
## Configuring as a DNS Client
- Before configuring the router as a DNS client we must enable the router in global configuration. We first do this by entering 'Enable' which puts the router in Privleged Exec mode, then we input 'Config T' to get into the global configuration
- R1>enable
R1#config t
Enter configuration commands, one per line.  End with CNTL/Z.

Then we must set up the router to become a DNS client with the following: 
- R1(config)#ip domain-lookup
- - This enables DNS hostname translation
- R1(config)#ip name-server 10.10.10.10
-  - This points the router to the DNS server that is assigned the IP address of 10.10.10.10

## Router 1 Verifying Ping to R2 and R3
Next we will exit out of global configuartion mode by typing 'exit' then we will type enable again to enter Privleged Exec mode.

Afterwards we are going to test to see if R1 can ping R2 by it's hostname and get back the IP address
- R1#Ping R2
Translating "R2"...domain server (10.10.10.10)
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 10.10.10.2, timeout is 2 seconds:
.!!!!
Success rate is 80 percent (4/5), round-trip min/avg/max = 0/1/4 ms

We will also test with R3
- R1#Ping R3
  Translating "R3"...domain server (10.10.10.10)
  Type escape sequence to abort.
  Sending 5, 100-byte ICMP Echos to 10.10.20.1, timeout is 2 seconds:
  .!!!!
  Success rate is 80 percent (4/5), round-trip min/avg/max = 0/0/0 ms

## Router 1 Examining ARP Cache

# Router 2
## Router 2 Configuring DNS Server

## Router 2 Examining ARP Cache

# Router 3 
## Router 3 Configuring DNS Server

## Router 3 Verifying Ping to R1 aand R2

## Router 3 Examining ARP Cache

