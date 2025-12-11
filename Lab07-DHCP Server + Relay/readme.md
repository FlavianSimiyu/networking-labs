Concept Demonstrated
This lab demonstrates how a central DHCP server automatically assigns IP addresses to hosts and how a DHCP relay agent forwards DHCP broadcast messages across router boundaries. Because DHCP requests cannot traverse routers on their own, the relay ensures that devices on remote subnets can still obtain addressing information from the server. The lab confirms centralized IP management across multiple networks.

Tasks to Be Completed
-Build a multi-router topology with at least one DHCP Server router and one Relay router.
-Assign IP addresses to all router interfaces.
-Configure a DHCP server with excluded addresses, a DHCP pool, default gateway, and DNS settings.
-Configure a DHCP relay agent on the remote router using ip helper-address.
-Configure PCs to obtain IP addresses automatically via DHCP.
-Test connectivity between PCs and across the network using ping.
-Verify DHCP operation using show ip dhcp binding and interface status commands.