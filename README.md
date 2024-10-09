# Configuring-OPNsense
OPNsense is an open-source firewall and routing platform based on FreeBSD, known for its strong security and flexible configuration options. Below is a guide to help you set up and configure OPNsense.

1. Download and Install OPNsense

	•	Download OPNsense ISO: Head to the OPNsense official site and download the appropriate image for your system (x64 for most systems).
	•	Installation Method: You can install it on a physical server or as a virtual machine (VM) in a hypervisor (like VirtualBox, VMware, or Hyper-V).
	•	Burn the ISO: For physical servers, burn the ISO to a USB drive or CD and boot from it.
	•	Install OPNsense: Once the system boots, follow the on-screen instructions to install OPNsense to the disk. Choose defaults for most options unless you need custom partitioning.

2. Initial Setup

After installation, reboot and you’ll be presented with a command-line interface (CLI):

	•	Default login credentials:
	•	Username: root
	•	Password: opnsense

After logging in:

	•	Configure the network interfaces:
	•	Assign the WAN and LAN interfaces. Typically, the system will autodetect your network cards and ask you to assign WAN (external network) and LAN (internal network) interfaces.
	•	Optionally configure a DMZ if needed.
	•	Set IP addresses:
	•	For the LAN, you can assign a static IP, e.g., 192.168.1.1/24.
	•	For the WAN, you can assign static, DHCP, or PPPoE, depending on your provider.

3. Access the Web Interface

	•	Once network interfaces are assigned and configured, open a web browser on a client machine on the LAN.
	•	Access the OPNsense Web GUI by typing the LAN IP into the browser, e.g., https://192.168.1.1/. Use the default credentials to log in:
	•	Username: root
	•	Password: opnsense
	•	Change the password after logging in for security reasons (System > Access > Users).

4. Configure Basic Settings

	•	General Settings: Navigate to System > Settings > General. Here, you can set hostname, domain, and DNS servers.
	•	Time Settings: Set the correct time zone in System > Settings > Miscellaneous.

5. Set Up WAN/LAN Rules

OPNsense has a default firewall configuration that blocks incoming traffic on the WAN interface and allows traffic from the LAN interface. You can add additional firewall rules based on your needs.

	•	Firewall Rules for LAN:
	•	Go to Firewall > Rules > LAN.
	•	Add any necessary rules to allow or block traffic on the LAN side. By default, all outbound traffic is allowed.
	•	Firewall Rules for WAN:
	•	Go to Firewall > Rules > WAN.
	•	Add rules to allow inbound traffic if necessary (for example, if hosting a web server).

You can create rules based on the source, destination, protocol, and port.

6. NAT (Port Forwarding)

If you want to forward traffic from the WAN to internal servers, you will need to configure NAT port forwarding:

	•	Go to Firewall > NAT > Port Forward.
	•	Add a new rule:
	•	Interface: WAN
	•	Protocol: TCP/UDP (depending on your needs)
	•	Destination: WAN address
	•	Destination port range: The external port you’re forwarding (e.g., 80 for HTTP)
	•	Redirect target IP: The internal IP of your server (e.g., 192.168.1.100)
	•	Redirect target port: The internal port (e.g., 80 for HTTP)
	•	Save the rule and apply changes.

7. DHCP Configuration

OPNsense can act as a DHCP server for your LAN:

	•	Go to Services > DHCPv4 > LAN.
	•	Enable the DHCP service.
	•	Set the range of IP addresses that can be assigned to clients on the LAN, e.g., 192.168.1.100 to 192.168.1.200.
	•	You can also add static DHCP mappings if needed.

8. Configure Intrusion Detection System (IDS/IPS)

OPNsense includes an IDS/IPS system (powered by Suricata) for enhanced security:

	•	Go to Services > Intrusion Detection.
	•	Enable the IDS or IPS mode.
	•	Select which interfaces to monitor (typically WAN).
	•	Choose your rule sets, such as Emerging Threats.
	•	Apply the settings.

9. Enable VPN (Optional)

If you need to set up a VPN (e.g., OpenVPN):

	•	Go to VPN > OpenVPN > Wizards.
	•	Follow the wizard to configure a VPN server and client export package.
	•	You can also use IPsec or WireGuard, depending on your preferences.

10. Monitoring and Logging

	•	Real-time Traffic Monitoring: Go to Interfaces > Overview to see traffic on each interface.
	•	Firewall Logs: Check logs in Firewall > Log Files > Live View.
	•	System Health: For CPU, memory, and network usage monitoring, go to System > Health.

11. Backup and Restore

	•	Go to System > Configuration > Backups.
	•	Export the configuration regularly to ensure you have a backup in case of failure.
	•	You can also integrate the configuration backup with cloud services like Google Drive.

Conclusion

You’ve now set up a basic OPNsense firewall with WAN, LAN, DHCP, firewall rules, and potentially VPN and IDS/IPS. For further customizations, OPNsense offers a rich plugin system (System > Firmware > Plugins) where you can add additional functionality like DNS filtering, traffic shaping, and more.
