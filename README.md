**Project Title: Wazuh Security Operations Lab**

**Overview**
A self-hosted Security Operations Center (SOC) lab environment built to practice incident detection, log analysis, and endpoint monitoring using the Wazuh SIEM.

**Lab Architecture**

*Core Setup Steps*
**Environment Provisioning:**

#Set up two VMs (Ubuntu 22.04 LTS for the Manager, Windows 11 Enterprise for the Endpoint).

#Configure network adapters to Bridged Mode to ensure both VMs are on the same subnet as the host machine.

**Wazuh Manager Installation:**

#Download the Wazuh installation script: **curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh.**

#Generate configuration files: **sudo bash ./wazuh-install.sh -g.**

**Crucial Step:** Edit config.yml to specify the static local IP of the Ubuntu VM (192.168.x.x). This prevents certificate mismatches.

#Execute full deployment: sudo bash ./wazuh-install.sh -a.

**Agent Deployment:**

#Access the Wazuh Dashboard at https://<Ubuntu_VM_IP>.

#Navigate to Agents Management > Deploy new agent.

#Select Windows and input the Manager's IP address.

**Agent Enrollment:**

#Run the generated PowerShell command on the Windows VM as Administrator to install the agent.

#Use the manage_agents tool on the Ubuntu host to extract an authentication key (E option) for the specific agent ID.

#Import the key into the Wazuh Agent manager UI on the Windows endpoint to finalize the "Active" handshake.

**Validation:**

#Verify connectivity via the Wazuh Dashboard under the Agents tab.

#Test alert ingestion by triggering Event ID 4625 (Failed Logon) on the Windows endpoint and verifying the detection in the Threat Hunting module.
