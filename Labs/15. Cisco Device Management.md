# Lab Exercise

In this lab you will perform a factory reset, password recovery, configuration
backup, and system image backup and recovery on a Cisco router. You will also
perform an IOS upgrade on a Cisco switch.

## Lab Topology

<img width="691" height="236" alt="image" src="https://github.com/user-attachments/assets/479c595b-1a64-490d-9f0b-745f66715509" />

## Factory Reset

1) View the running configuration on R1. Note that the hostname and
interface have been configured.
  - We can view the running configuration on R1 with _show running-config_. We can view the version, hostname, interfaces, and much more.
  - <img width="307" height="160" alt="image" src="https://github.com/user-attachments/assets/bd7cf748-1a18-4426-b362-2284e160e652" />
  - <img width="367" height="340" alt="image" src="https://github.com/user-attachments/assets/88e7ebab-19f2-433b-bda8-861e9ddacf29" />
2) Factory reset R1 and reboot.
  - In order to factory reset any router or switch you can use the command _write erase_ then we will use the _reload_ command to reboot the router.
  - <img width="617" height="297" alt="image" src="https://github.com/user-attachments/assets/ea92d077-83a3-41b6-aecf-ef3820e43b9b" />
3) Watch the boot up process as the router boots.
4) The router should boot into the Setup Wizard. Exit out of the wizard and
then confirm the startup and running configurations are empty.
  - We will type 'N' for no for the setup
  - <img width="493" height="159" alt="image" src="https://github.com/user-attachments/assets/8a05220d-e3cd-4437-bd92-8c6447661c93" />
5) Paste the configuration for R1 from the ‘15 Cisco Device Management
Configs.zip’ file back into the configuration and save. Neil Anderson has provided this to input into the lab.
>enable
>!
>configure terminal
>!
>hostname R1
>!
>!
>interface GigabitEthernet0/0
 ip address 10.10.10.1 255.255.255.0
 duplex auto
 speed auto
 no shutdown
>!
>line con 0
 exec-timeout 30 0
>!
>end
 - We will copy and paste this into R1

## Password Recovery

1) Set the enable secret on R1 and save the running-
configuration.
  - In global configuration use the command _enable secret_ then you can type in your encrypted password. Then we will use _copy run start_ to save the running the configuration.
  -  <img width="429" height="227" alt="image" src="https://github.com/user-attachments/assets/78476f28-a68f-466d-b5a3-5c5650813666" />
2) Configure the router to boot into the rommon prompt on next reload with
an appropriate command and reboot the router.
  - In global configuration we will enter the command _config-register 0x2120_. 0x2120 is the specific command to boot into rommon mode on the next reload of the device.
  - <img width="601" height="182" alt="image" src="https://github.com/user-attachments/assets/d6950f6e-6dad-4dac-9ab7-e089c4090ac0" />
3) In rommon mode, configure the router to ignore the startup-config when
booting up, and reload the router.
  - Then from the rommon prompt we will be entering the command _confreg 0x2142_. 0x2142 is the command to ignore the startup config and boot from flash memory.
  - Then we will reset, then on the reset the Router will boot from the flash memory.
  - <img width="577" height="311" alt="image" src="https://github.com/user-attachments/assets/79250b6c-f936-4eba-bbcd-03131ce15159" />
4) The router should boot into the Setup Wizard. Exit out of the wizard.
5) What do you expect to see if you view the running and startup
configurations? Confirm this.
  - When we do a show run, we don't see any configurations made.
  - When we do a show start, we will see our previous configurations made because the starting config has been untouched.
6) Copy the startup config to the running config. Do not miss this step or you
will factory reset the router!
  - We will use the command _copy start run_. This will copy our start config to our running config. Then when we do _show running config_, we can see that everything has been configured.
  - <img width="354" height="272" alt="image" src="https://github.com/user-attachments/assets/36a6eae3-f071-432e-97bd-4afd716c3b02" />
7) Verify the status of interface GigabitEthernet0/0. Why is it down?
  - With _show ip interface brief_ we can see that G0/0 is administratively down. So we will need to bring the interface back up.
  - <img width="566" height="50" alt="image" src="https://github.com/user-attachments/assets/810d1784-ee6b-46e9-b174-023c691fb99c" />
8) Bring interface GigabitEthernet0/0 up.
  - <img width="625" height="136" alt="image" src="https://github.com/user-attachments/assets/92979da4-c805-40c6-aed0-d75885883f76" />
9) Remove the enable secret.
  - In global config use the command _no enable secret_ then we can verify it in our running config
  - <img width="374" height="241" alt="image" src="https://github.com/user-attachments/assets/62f6488a-ec7c-4c8b-b0d8-c1a7d9c264a1" />
  - We can see that our encrypted secret password is no longer present.
10) Ensure the router will reboot normally on the next reload and that you will
be able to access the router.
  - Next we will go back to _config-register_ but this time use the code 0x2102. 0x2102 tells the device that on the next reboot it will boot from NVRAM. We will also need to copy our running config to our startup config so that our changes can be saved.
11) Reboot the router and confirm it has the expected configuration.
  - After rebooting the router we can enable the command prompt and use _show running-config_ to verify everything was saved. Everything has been saved and the link on G0/0 is still up.
  - <img width="279" height="112" alt="image" src="https://github.com/user-attachments/assets/b2f60e8e-c8f2-4558-ac82-d10a582ea3b6" />

## Configuration Backup
1) Backup the running configuration to Flash on R1. Use a suitable name for
the backup file. Verify the configuration has been backed up.
  -
2) Backup the R1 startup configuration to the TFTP server. Use a suitable
name for the backup file. Verify the configuration has been backed up.

## IOS System Image Backup and Recovery
1) Backup the IOS system image on R1 to the TFTP server. Verify the
configuration has been backed up.
  -
2) Delete the system image from Flash and reload.
3) Use Internet search to find system recovery instructions for your model of
router. Recover the system image using the TFTP server.

## IOS Image Upgrade
1) Verify SW1 is running C2960 Software (C2960-LANBASE-M), Version
12.2(25)FX
  -
2) Use the TFTP server to upgrade to c2960-lanbasek9-mz.150-2.SE4.bin
3) Reboot and verify the switch is running the new software version.
