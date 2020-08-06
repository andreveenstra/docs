---
title: Configure AEP model
---

# Configure AEP model

## Login to web interface

To start configuring your conduit connect a computer to its LAN interface and open a browser to `http://192.168.2.1/`. This opens the login dialog for the configuration interface of the conduit:

![Login](login-aep.png)

The default credentials are:

* **Username**: `admin`
* **Password**: `admin`

## First-Time Setup Wizard
After login (be patient, it takes a while) the **First-Time Setup Wizard** opens:

![First-Time Setup Wizard](wizard.png)

Click **Next** to begin.

### Choose Password

The first step it to change the current default password (`admin`):

![Choose Password](password.png)

> Keep your new password in a safe place, you will have to reset to factory defaults if you lose it!

### Time Configuration

Select your time zone and update both date and time if required.

![Time Configuration](time.png)

Click **Next** to proceed.

### Internet Configuration

Set the **Mode** to *DHCP Client* if you use DHCP on your network (most likely) or manually configure your internet connection. Click **Finish** once you are done.

![IP Setup - eth0](ip.png)

If you changed the IP Address or selected DHCP a popup will appear warning you that the DHCP Server of the Conduit itself will be disabled. This is fine, so click **OK** to continue.

![DHCP](dhcp.png)

## Update firmware

Before you continue, verify that the Conduit AEP runs Firmware 1.3.2 or later. This is display in the header of the web interface. If it is out-dated, follow the [instructions to upgrade](http://www.multitech.net/developer/software/aep/upgrading-the-aep-firmware/) to the latest version. The ttn-packer-forwarder might not work otherwise.

## Access & Network Configuration

As the LAN interfaces do not allow specifying a DNS server and we need DNS to work later on we will now change to network to WAN. However as this would lock us out we need to allow remote access for the management first.

> Skip this step if you are using a cellular modem to connect the gateway to the internet. Just configure the cellular modem per instructions on the MultiTech website.

### Access Configuration

In the left hand menu choose **Administration** followed by **Access Configuration**:

![Administration / Access Configuration](menu-access.png)

On the next screen tick the boxes marked yellow in the next screenshot:

![Access Configuration](access.png)

When you select **Via WAN** under HTTPS a warning will appear. Just click **Continue**.

![HTTPS WAN Access](wan-access.png)

Once you have selected the 3 checkboxes, click **Submit** to save the changes.

### Network Interfaces

Select **Setup > Network Interfaces** from the left menu:

![Setup / Network Interfaces](menu-network.png)

In the next screen select the pencil in the **eth0** row:

![Network Interfaces Configuration](interfaces.png)

In the configuration popup change the **Type** from *LAN* to *WAN*.

> If you use a static IP, fill out the gateway and DNS entries. Use 8.8.8.8 for Google's public DNS if you do not have (or know) the local DNS server information.

![Network Interfaces Configuration - eth0](interface.png)

Click **Finish** to save.

Now select **Save and Restart** from the menu:

![Save and Restart](menu-restart.png)

You will be prompted to confirm the restart. Choose **OK** to proceed.

Disconnect the temporary network cable and connect the Conduit to the target network while it is restarting.

## TTN Configuration {#ttn-configuration-aep}

Once the Conduit has finished restarting and is connected to the target network, connect a computer to the same network and login to the Conduit by entering its IP in a browser.

> If you have not configured your Conduit with a static IP, you will have to [find out which IP the DHCP assigned to it](http://apple.stackexchange.com/questions/19783/how-do-i-know-the-ip-addresses-of-other-computers-in-my-network).

Click the LoRaWAN tab on the left.

In the **Mode** dropdown, choose Packet Forwarder.

In the **Channel Plan** dropdown, choose the channel plan for your area. This must match the channel plan you configure in the Console.

![LoRa Settings](lora-settings-1.png)

For the **Server Address**, you will need to add the [address of the router region](https://www.thethingsnetwork.org/docs/gateways/packet-forwarder/semtech-udp.html#router-addresses) - for example, for the EU region, it will be `router.eu.thethings.network`.

Unless you’re running the network yourself on specific ports, the **upstream** and **downstream ports** will be 1700 and 1700.

![LoRa Settings](lora-settings-2.png)

After you have entered all of the configuration settings, press **Submit** at the bottom.

Press the **Save and Apply** button in the left hand menu to apply the settings.

![Save and Apply](save-and-apply.png)