# Cisco Device Functions

## In this lab we will be exploring the MAC address table on Cisco switches and routing tables on Cisco routers.

We will be exploring the commands used to view the MAC address table and routing table.

# Lab Topology
<img width="694" height="377" alt="Lab Topology" src="https://github.com/user-attachments/assets/0e823579-4673-4349-b0fe-335179cf8bf0" />


# Verify the Switch MAC Address Tables

1. Log into the routers R1-R4 and verify which interface is configured on teh 10.10.10.0/24 network

To show the configuration of the interfaces on each router you must first
- Enter in _Privileged Exec Mode_ by using the command _Enable_
- Then enter the command _Show IP Interface Brief_ this command allows you to view the IP interface status and configuration with a brief summary of the IP status
- Down below are the interface configurations for each router

R1 Configuration

<img width="641" height="256" alt="R1 config" src="https://github.com/user-attachments/assets/0ed6a75b-6c25-41c5-be50-f7f958388914" />

R2 Configuration

<img width="623" height="195" alt="R2 Config" src="https://github.com/user-attachments/assets/5f625840-7220-489a-8125-6ffd52c8d04c" />

R3 Configuration

<img width="660" height="204" alt="R3 Config" src="https://github.com/user-attachments/assets/1a8543e5-d00c-4a77-8c6e-9696b029ded9" />

R4 Configuration

<img width="632" height="176" alt="R4 config" src="https://github.com/user-attachments/assets/f83899bb-5d43-4220-8e9b-57a57044ba00" />

R1, R2, R4 are using interface G0/0 for the 10.10.10.0/24 network while R3 is using G0/1

2. Note down the MAC addresses of these interfaces

Now we must make note of the individual MAC address of each interface.
- Remember each interface has its own assigned MAC address
- To view the MAC address we must again _Enable_ the router
- Then type in the command _Show Interface_ (Interface). This will show the specific interface and its settings.
- - In R1 example we will be using the command _Show Interface G0/0_. But in R3 we will be using _Show Interface G0/1_

R1 Interface MAC

<img width="572" height="85" alt="R1 MAC" src="https://github.com/user-attachments/assets/411f6ddb-1100-4eb6-9071-9e17942e1efa" />

R2 Interface MAC

<img width="579" height="85" alt="R2 MAC" src="https://github.com/user-attachments/assets/f1a6cc61-2606-49bb-94e3-db6191d9cfd8" />

R3 Interface MAC

<img width="580" height="82" alt="R3 MAC" src="https://github.com/user-attachments/assets/c1a667a3-6183-4685-95da-6c7a134175a7" />

R4 Interface MAC

<img width="577" height="84" alt="R4 MAC" src="https://github.com/user-attachments/assets/4e46ba60-40b2-4ec5-90b5-33fcade3c545" />


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
