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


# Router 1
## Router 1 Configuring DNS Server

## Router 1 Verifying Ping to R2 and R3

## Router 1 Examining ARP Cache

# Router 2
## Router 2 Configuring DNS Server

## Router 2 Examining ARP Cache

# Router 3 
## Router 3 Configuring DNS Server

## Router 3 Verifying Ping to R1 aand R2

## Router 3 Examining ARP Cache

