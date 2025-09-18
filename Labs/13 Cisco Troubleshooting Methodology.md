# Troubleshoot Connectivity to DNS Server

1. The host with IP address 10.10.10.10 has been configured as a DNS server and should be able to resolve requests for ‘R1’, ‘R2’ and ‘R3’. Members of staff have complained that DNS is not working.

2. When you have verified that DNS is not working, troubleshoot and fix the problem. You have fixed the problem when R3 can ping R1 by hostname. Note that there may be more than one issue causing the problem.

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

# Objective 2

Now that we have the interface set up for R2, we can now try to ping R1 from R3 by their hostname.

<img width="395" height="59" alt="image" src="https://github.com/user-attachments/assets/8b58db08-c5d2-4257-b471-3b246dcac57d" />

We still can not ping by the hostname of R1. Next we will try to ping by the IP address.

<img width="519" height="120" alt="image" src="https://github.com/user-attachments/assets/65ff19a3-52f4-4b94-9a38-caebd4f0a42b" />

The pings were successful.
Upon further investigation I noticed that the IP address of the domain server configured in R3 was incorrect. It is set to 10.10.10.1 instead of 10.10.10.10

1. Firstly we will remove the incorrect entry of the name server with
   - no ip name-server 10.10.10.1 (in config t)
2. Then we will add the correct entry
   - ip name-server 10.10.10.10 (in config t)
3. Now we retest
<img width="439" height="162" alt="image" src="https://github.com/user-attachments/assets/a58d21d6-ce3e-4f09-970b-8b0cd403dfb2" />

Although we have the correct IP address for the DNS, it is still giving me an error.
After more investigation, I noticed that the error points out that the protocol may not be running

After checking the DNS server itself we can see that the DNS service has been toggled off.
<img width="699" height="203" alt="image" src="https://github.com/user-attachments/assets/6bf3a02d-5a77-4a42-88ec-9f66bb5b37ce" />

Once I have turned it back on, I retested once again. Now it was successful.

<img width="492" height="90" alt="image" src="https://github.com/user-attachments/assets/c6a76a31-02ab-412d-b57a-0e0535a45b5d" />

# Conclusion

In this lab we were given a task to troubleshoot connectivity between our DNS server and 3 routers. We first tested it out to see if any of our routers were pingable by their hostname. Our first steps showed that R1 was unable to ping R3 by hostname or IP address.
From there we took a look at our network topology and decided to doa  trace command to R3, which ended up failing.

Next we tested the conenctivty between R2 and R3. Although they were not able to ping each other by hostname they were still able to ping each other by IP address. This confirmed that there was a connectivity issue between R1 and R2 somewhere. I decided to go into R2 and use the command _show ip interface brief_ to view the statuses of the interfaces of the router. When given the command is shown that R2's f0/0 interface was administratively down. So in order to establish a connection we brought the interface back up. Entering the interface with _Interface f0/0_ and doing a _no shutdown_ would bring the interface back online. We would test this out again with the _show ip interface brief_ command. Once we saw that the interface has been brought back online, we were able to ping R1 by it's IP address.

Now there was still the problem of the hostnames not being able to be pinged. From R3 we retested the ping by hostname of R1 and it still gave us an error. When investigating the issue it is clearly shown that the DNS server configured in R3 had the wrong IP address. The IP address was shown as 10.10.10.1 (which is R1 IP address) and it should have been 10.10.10.10, for the DNS. The first step to fix this issue was to remove the incorrect entry of the DNS. By entering _config t_ we would put in the command _no ip name-server 10.10.10.1_ to delete the incorrect entry, then _ip name-server 10.10.10.10_ to put in the correct one. But even after this the hostname still refused to be pinged. Then once I did some more digging around the error also states that the protocol could also not be running. So from here we would check the DNS service in the server and saw that the DNS service has been turned off.

In this lab I used commands to test connectivity, configured interfaces, configured a router as a DNS client, as well as inspected the devices to make sure that there could be more than one issue.
