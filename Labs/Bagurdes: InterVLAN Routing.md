We will be configuring InterVLAN Routing in this lab.

Here is our lab diagram and we want to have PC1 be able to ping PC2. Because PC1 and PC 2 are on different networks we need to configure everything so that they are able to communicate with each other.

<img width="1263" height="712" alt="image" src="https://github.com/user-attachments/assets/613fd66d-5e30-4c38-966d-98219e58848d" />

In Cisco Packet Tracer I have created the network diagram and the first thing we need to do is configure the IP addresses of the PCs.

<img width="539" height="172" alt="image" src="https://github.com/user-attachments/assets/140c1963-6cfa-4f88-a238-d1c9d016c0c2" />

PC1 IP Address 10.0.0.10/24 with a Default Gateway of 10.0.0.1 and PC2 IP Address 172.16.0.10/24 with a Default Gateway of 172.16.0.1

<img width="448" height="186" alt="image" src="https://github.com/user-attachments/assets/ebd6fc00-7a46-434c-ae3b-9581719aa0ec" />

<img width="436" height="181" alt="image" src="https://github.com/user-attachments/assets/73dd14f3-0022-4a5d-9bc7-bb66bd871f67" />

Next on both switches we want to create VLANs for 10.0.0.0 and 172.16.0.0 networks. 10.0.0.0 will be assigned VLAN 10 and 172.16.0.0 will be assigned VLAN 20. VLAN 10 will be named LEFT and VLAN 20 will be named RIGHT.

<img width="568" height="286" alt="image" src="https://github.com/user-attachments/assets/ed75ba1e-4348-4788-b7e2-0baffc52e70b" />

Now that is done we will need to create Access Ports for the VLANs on the switch. 

<img width="309" height="118" alt="image" src="https://github.com/user-attachments/assets/dd050e63-5ab6-49dd-a3ab-12c7e97a3741" />

Then we can confirm the VLAN that we set up. 

<img width="595" height="224" alt="image" src="https://github.com/user-attachments/assets/b80f170a-5379-4650-85ed-64f622a5b87a" />

Over on interface f0/10 we need to set up the link as a trunk link. This allows this link to have multiple VLANs sent across it.

<img width="623" height="181" alt="image" src="https://github.com/user-attachments/assets/69e2da47-a8f0-44b5-b319-99634dbf61eb" />

Now we confirm if the interface is all set up correctly. With _show interface trunk_

<img width="485" height="155" alt="image" src="https://github.com/user-attachments/assets/632e4bb2-a4b1-402f-8dbc-befa1744c920" />

Time to configure switch 2 with the same steps, except we will not be making access ports. Instead we will make 2 trunk ports for f0/12 and g0/1.

<img width="381" height="172" alt="image" src="https://github.com/user-attachments/assets/2bfd5438-fb99-4634-bc48-b646380c9dd0" />
<img width="562" height="147" alt="image" src="https://github.com/user-attachments/assets/874e2cd8-8fd6-4d4b-824e-c0b4e7dec0d1" />
<img width="472" height="216" alt="image" src="https://github.com/user-attachments/assets/6ee344c1-7c76-46fa-bbae-38d5954e9ff5" />



In Ross Bagurdes' video he works on a layer 3 switch, but in Cisco Packet Tracer it does not allow you to create sub-interfaces on layer 3 switches. So we will be using a router.

On the router we want to enable _IP routing_ then enter the interface of g0/1 and enable the interface with a _no shutdown_

<img width="444" height="123" alt="image" src="https://github.com/user-attachments/assets/53113655-2785-4c6d-b4dd-d0169efbb36c" />

While still in the interface we want to create a sub-interface and specify the type of encapsulation we will be doing. We will use _encapsulation dot1q_

<img width="330" height="157" alt="image" src="https://github.com/user-attachments/assets/1f3c5d6d-0978-4326-9118-98e8e54d29f1" />

Then in the sub-interfaces we want to create an IP address of the default gateway. Remember when configuring a router's interface it is always important to use _no shut_.

<img width="616" height="381" alt="image" src="https://github.com/user-attachments/assets/83fd613f-4d1c-4e56-8dd1-e793d4bc0e5b" />

Then we can double check all of our work is done with _show ip route_

<img width="555" height="232" alt="image" src="https://github.com/user-attachments/assets/89f4fa25-d72d-480f-b189-1cce64bdd99e" />


After all of this has been completed we can go back to our PCs and attempt to ping the other PC. Since we can confirm that PC1 can ping PC2 we know that there is a two connection being established.

<img width="432" height="368" alt="image" src="https://github.com/user-attachments/assets/bf0192db-1826-4c01-b296-6f9271e7d4d6" />


