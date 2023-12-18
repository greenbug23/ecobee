# ecobee
Keep Ecobee thermostat online
Fixing Ecobee WiFi Drops with Automated Pings
This document outlines a solution to fix the issue of an Ecobee thermostat repeatedly dropping off the home wireless network, based on a community workaround discovered on Reddit.

Problem:

Ecobee thermostat keeps disconnecting from WiFi, despite multiple resets and other troubleshooting attempts.
Solution:

A Reddit user ("Crysawn") identified a potential bug in the thermostat software requiring periodic network interaction to stay online.
This script automatically pings the Ecobee's IP address every hour, keeping it connected to the network.
Requirements:

Linux machine on the same network as the Ecobee thermostat.
Bash scripting knowledge (basic level).
Instructions:

Save the following script as ecobee_ping.sh:
Bash
#!/bin/bash

# Replace 192.168.1.1 with your Ecobee's IP address
while true; do
  ping -c 1 192.168.1.1
  sleep 3600
done

# Schedule script to run every hour using sleep command
sleep 3600

# Save
Use code with caution. Learn more
Make the script executable:
Bash
chmod +x ecobee_ping.sh
Use code with caution. Learn more
Add the script to systemctl for automatic execution on boot:
Bash
sudo systemctl enable ecobee_ping.sh
sudo systemctl start ecobee_ping.sh
Use code with caution. Learn more
Verify the script is running:
Bash
sudo systemctl status ecobee_ping.sh
Use code with caution. Learn more
Notes:

Adjust the IP address in the script to match your Ecobee thermostat.
You can modify the ping frequency by changing the "0" within the crontab line. Higher frequency might consume more battery, but lower frequency might increase disconnect risk.
This solution is a workaround and may not be a permanent fix. Consider contacting Ecobee support for further assistance.
Credits:

Crysawn (Reddit user) for identifying the potential software bug and proposing the ping solution.
Additional Resources:

Reddit thread discussing Ecobee WiFi drop issue: https://www.reddit.com/r/ecobee/comments/6lgq07/fix_ecobee4_loses_wifi_connection/
By following these steps, you should be able to automatically keep your Ecobee thermostat online using periodic pings. Hopefully, this workaround provides a reliable solution until a permanent fix becomes available.
