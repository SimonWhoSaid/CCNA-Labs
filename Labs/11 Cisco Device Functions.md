# Cisco Device Functions

## In this lab we will be exploring the MAC address table on Cisco switches and routing tables on Cisco routers.

We will be exploring the commands used to view the MAC address table and routing table.

# Lab Topology
<img width="694" height="377" alt="Lab Topology" src="https://github.com/user-attachments/assets/0e823579-4673-4349-b0fe-335179cf8bf0" />


# Verify the Switch MAC Address Tables

1. Log into the routers R1-R4 and verify which interface is configured on teh 10.10.10.0/24 network

2. Note down the MAC addresses of these interfaces

3. Verify connectivity between the routers by pinging R2, R3, and R3 from R1

4. Ping R3 and R4 from R2

5. View the dynamically learned MAC addresses on SW1 and verify that the router's MAC addresses are reachable through the expected ports

6. Repeat on SW2

7. Clear the dynamic MAC address table on SW1

8. Show the Dynamic MAC address table on SW1.

# Examine a Routing Table

1. View the routing table on R1.

2. Configure the IP address of 10.10.20.1/24 on interface G0/1

3. Verify the status of interfaces of G0/0 and G0/1

4. Bring interface G0/1 online

5. Configure a static route to 10.10.30.0/24 with a next hop address of 10.10.10.2

6. Check the routing table and verify that 10.10.30.0 can reach 10.10.10.2
