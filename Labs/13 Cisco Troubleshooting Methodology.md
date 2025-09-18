# Troubleshoot Connectivity to DNS Server

1. The host with IP address 10.10.10.10 has been configured as a DNS server and should be able to resolve requests for ‘R1’, ‘R2’ and ‘R3’. Members of staff have complained that DNS is not working.

2. From R3, use Telnet to check if the DNS service appears operational on the DNS server at 10.10.10.10.

3. When you have verified that DNS is not working, troubleshoot and fix the problem. You have fixed the problem when R3 can ping R1 by hostname. Note that there may be more than one issue causing the problem.

# Lab Topology

<img width="726" height="471" alt="Lab Topology" src="https://github.com/user-attachments/assets/86afb4a5-1c74-4c6c-8b1c-bd07bfc19ec1" />


# Objective 1

We first need to check if a DNS request can be made from the routers
We will ping a router by their hostname. In this example our router's hostnames are 'R1', 'R2', amd 'R3'.

From R1 we will enter _Privileged Exec Mode_ and try to ping a router by it's hostname.

<img width="400" height="73" alt="image" src="https://github.com/user-attachments/assets/4d6918ec-a248-4980-a748-63ec2840a62c" />

When doing so we get an error. Now we will try to ping R3 by it's IP address of 10.10.20.1

<img width="502" height="119" alt="image" src="https://github.com/user-attachments/assets/27421a48-a839-4ea5-b7fb-6542bdc443f5" />

Pinging to the IP address also failed. Next, based on our topology we can see there is R2 in the middle, we will test it out with a traceroute command

<img width="246" height="127" alt="image" src="https://github.com/user-attachments/assets/e7d9ac6c-ce00-481e-b7d2-6d2476aaa114" />

The trace command to 10.10.20.1 also failed.

Next we will test to see if R2 is able to ping R3 by it's IP address

<img width="495" height="99" alt="image" src="https://github.com/user-attachments/assets/b7295bfd-a8f9-4624-bbdb-5fbc19084ebb" />

Since the pings were successful, the next step would be to see if the interface, on R2 connected to SW1, is down.

In order to do that we would enter the command, _Show Ip Interface Brief_

<img width="575" height="104" alt="image" src="https://github.com/user-attachments/assets/d84bf515-67e0-4025-8216-73bb04d61394" />

As we can see from the results we see that the status of the interface is administratively down/down

To change this we will specify the interface we want, FastEthernet0/0, and use the _No Shutdown_ command to bring the interface up.
>Enable
>
>Config T
>
>Interface f0/0
>
>no shutdown
>
>end
>
>show ip interface brief

Now after doing these steps we can now see that the f0/0 interface status is now up/up

<img width="602" height="318" alt="image" src="https://github.com/user-attachments/assets/ba8a87cd-4e01-4567-b124-8aa8f445bb39" />



