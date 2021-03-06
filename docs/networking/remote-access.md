---
author:
  name: Linode
  email: docs@linode.com
description: Our guide to the remote access area of the Linode Manager.
keywords: 'remote access,ip addresses,ip failover,swapping ip addresses,console access'
license: '[CC BY-ND 3.0](http://creativecommons.org/licenses/by-nd/3.0/us/)'
alias: ['remote-access/']
modified: Saturday, September 6th, 2014
modified_by:
  name: Dave Russell Jr
published: 'Tuesday, April 24th, 2012'
title: Remote Access
---

The Remote Access section of the Linode Manager contains important network settings for your Linode. Use this tab to find your IP address, set the reverse DNS, configure IP failover, and swap IP addresses with another Linode. You can also access the Linode Shell (Lish) console to remotely connect to your Linode and troubleshoot problems.

Network Access
--------------

The Network Access section provides access to the settings for reverse DNS, IP failover, and swapping IP addresses. It also displays your Linode's IP addresses, default gateways, and DNS resolvers.

### Setting Reverse DNS

The ability to associate an IP address with a domain name is referred to as *forward* DNS resolution. *Reverse* DNS lookup is the inverse process, where an IP address resolves to its designated domain name. Official Internet documents state that "every Internet-reachable host should have a name," and that the name should match a reverse pointer record. (See [RFC 1033](http://tools.ietf.org/html/rfc1033) and [RFC 1912](http://tools.ietf.org/html/rfc1912).)

Here's how to set reverse DNS for your domain names:

 {: .note }
>
> Before setting reverse DNS, verify that you have created a matching forward DNS record for the IP address. For instructions, see [Adding DNS Records](/docs/hosting-website#sph_adding-dns-records). If you use a third-party DNS provider, create the forward DNS record with your provider's management tool.

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select your Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab.
5.  Select the **Reverse DNS** link, as shown in the below image.

[![The Reverse DNS link](/docs/assets/1697-remoteaccess_reversedns.png)](/docs/assets/1697-remoteaccess_reversedns.png)

6.  Enter a domain name in the **Hostname** field, as shown in the below image.

[![Adding the domain name for reverse DNS](/docs/assets/1695-ptr_lookup_marked.png)](/docs/assets/1695-ptr_lookup_marked.png)

7.  Click **Look up**. A message appears indicating that a match has been found for both your IPv4 and IPv6 addresses.

[![Reverse DNS Match found](/docs/assets/1691-ptr_lookup_match_found_small.png)](/docs/assets/1692-ptr_lookup_match_found.png)

8.  Click **Yes** beneath the desired address. Note that you can select only one address at a time. If you want to set up reverse DNS for both the IPv4 and IPv6 addresses, you can perform another lookup and select the other address.
9.  Repeat steps 1-8 for every other domain name you host on your Linode.

You have successfully configured reverse DNS.

 {: .note }
>
> If you receive the message that **no match was found**, this indicates that you need to update the forward DNS for this domain. Make sure the domain or subdomain in question resolves to the IP address for which you are trying to set the reverse DNS. If you've recently made a DNS change, you may need to wait 24-48 hours for it to propagate.

### Resetting Reverse DNS

To reset reverse DNS to the Linode domain, which will be something like **li12-345.members.linode.com**, follow these instructions:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select your Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab.
5.  Select the **Reverse DNS** link, as shown in the below image.

[![The Reverse DNS link](/docs/assets/1697-remoteaccess_reversedns.png)](/docs/assets/1697-remoteaccess_reversedns.png)

6.  Select the **Reset** link next to the reverse DNS setting you want to revert to the default Linode domain.

[![The Reset link](/docs/assets/1694-ptr_reset_marked_small.png)](/docs/assets/1693-ptr_reset_marked.png)

7.  Click **Yes** when asked to confirm the reset.

You'll see a confirmation message that the reverse DNS has been reset.

### Configuring IP Failover

If you're using two Linodes to make a website highly available with Heartbeat and Pacemaker , you can use the Linode Manager to configure IP failover. Here's how:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select the primary Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab.
5.  Select the **IP Failover** link. The webpage shown below appears.

[![Configuring IP failover](/docs/assets/963-remote-5.png)](/docs/assets/963-remote-5.png)

6.  Select the checkbox of the secondary Linode, as shown above.
7.  Click **Save Changes**.
8.  Reboot all Linodes that will bring up the floating IP.

You have successfully configured IP failover.

### Networking Restrictions

Linode's philosophy is to provide a plain Internet connection to every customer. We also implement some networking restrictions to prevent malicious activity and the abuse of our service.

By default, Linodes are able to send and receive traffic only for the MAC and IP addresses they are assigned. This restriction also applies to all ARP and IPv6 Neighbor Discovery traffic.

If you want to allow one Linode to use another Linode's IP address, such as for a high availability setup, you will need to enable IP Failover in the Linode Manager for every Linode that needs to use the IP address. For more information on enabling IP Failover, please see the [previous section](#configuring-ip-failover) of this guide.

### Swapping IP Addresses

If you have two Linodes in the same data center, you can use the *IP swap* feature to switch their IP addresses. This could be useful in several situations. For example, if you've built a new server to replace an old one, you could swap IP addresses instead of updating the DNS records.

Here's how to swap IP addresses:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select a Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab.
5.  Select the **IP Swap** link. The webpage shown below appears.

[![Linode selection page for IP swap](/docs/assets/971-remote-8.png)](/docs/assets/971-remote-8.png)

6.  From the **With Linode** menu, select a Linode.

 {: .note }
>
> The menu only displays Linodes hosted in the same data center as the current Linode.

7.  Click **Select**. The webpage shown below appears.

[![Adding the domain name for Reverse DNS](/docs/assets/961-remote-3-small.png)](/docs/assets/962-remote-3.png)

8.  Select both of the **Move It** checkboxes to verify that you want the IP addresses switched.
9.  Click **Do it**.

The IP address(es) will be swapped immediately as your Linode's networking is hotplugged. There may be a delay, however, of a few minutes (usually no more than five to ten) between the IP swap. There may be a brief period of time when your Linode's IP is unreachable due to this delay.

### Adding Private IP Addresses

The Linode Manager allows you to add private IP addresses for fast and secure connections between Linodes located in the same data center. Here's how to add a private IP address:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select a Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab.
5.  Select the **Add a Private IP** link, as shown below.

[![Adding Private IP addresses](/docs/assets/1696-remote_access_privateip.png)](/docs/assets/1696-remote_access_privateip.png)

6.  The Linode Manager assigns a private IP address to your Linode.
7.  Configure static networking. See the [Linux Static IP Configuration](/docs/networking/configuring-static-ip-interfaces) guide for instructions.

If you'd like to add more than one private IP address to your Linode, please [contact support](/docs/support).

### Adding Public IP Addresses

You can use the Linode Manager to add additional public IP addresses to your account. However, due to the [impending exhaustion of the IPv4 address space](http://en.wikipedia.org/wiki/IPv4_address_exhaustion), Linode requires users to provide technical justification. To add another public IP address, please [contact support](/docs/support) with your justification.

Console Access
--------------

The Lish console allows you to access your Linode at any time, even if you've messed up your network settings. To access Lish, use the Ajax console or an SSH client application installed on your computer. For more information about Lish, including usage tips, see [Using the Linode Shell](/docs/troubleshooting/using-lish-the-linode-shell).

### Using the Ajax Console

If you need to quickly access Lish, use the Ajax Console to open it directly from your web browser. Here's how:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select a Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab. Scroll down to the *Console Access* section.
5.  Select the **Launch Lish Ajax Console** link. The window shown below appears.

[![The Lish Ajax console](/docs/assets/1578-remote-7.2.png)](/docs/assets/1578-remote-7.2.png)

6.  Enter a username and password to log in.

You are now logged in to the Lish Ajax console.

### Using SSH

You can also access Lish with an SSH client application installed on your computer. Here's how:

1.  Log in to the [Linode Manager](https://manager.linode.com).
2.  Click the **Linodes** tab. A list of your virtual private servers appears.
3.  Select a Linode. The Linode's dashboard appears.
4.  Click the **Remote Access** tab. Scroll down to the *Console Access* section, as shown below.

[![The Console Access section of the Remote Access tab](/docs/assets/967-remote-6-small.png)](/docs/assets/968-remote-6.png)

5.  Accessing Lish via SSH requires additional authentication over and above your Linode's username and password. Enter a password for Lish in the **Lish via SSH Password** field, and then click **Change Password**. Or, if you use SSH key pair authentication, copy and paste your public key in to the **Lish via SSH Keys** field, and then click **Submit Keys**.
6.  Select the **Lish via SSH** link, as shown below.
7.  Your SSH client connects to your Linode via Lish. If you set a password for Lish, enter that first, and then enter a username and password to log in.

You are now logged in to Lish via SSH.



