# Deploy-SQLServer-on-Azure-VM

Currently unable to deploy Azure database server resources. This is a temporary, tested workaround.
-----

## Step 1. 
### Build and Deploy (Windows) Virtual Machine

Create VM use Windows 10
From the Size diaglog, sort by cost and select the minimum. This setting is probably unsatisfactory
for running any developer or activities beyond a single SQL Server instance.  We can scale up if we need to.

Enable RDP port, review and deploy.

![Screen Capture CreateVM](https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/CreateVM.JPG "Create Azure VM")

(note: the first deployment failed. steps were repeated using SqlDbWinVM1 and assigned IP address: 13.78.132.132.  Results will be the same but the actual machine instance won't match the screenshots)


## Step 2.
### Configure Azure network firewall

From the Networking settings, **Add Inbound Port Rule** to enable SQL TCP port access (typically: 1433)

![Screen Capture Add Inbound Port Rule](https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/AddInboundPortRule.JPG)


## Step 3.
### Install SQL Server and Configure Windows Firewall

Connect to VM using Remote Desktop (on port 3389), enter credentials and accept security certificate.

![Screen Capture Remote Desktop](https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/RDP.JPG)

The first connection on startup to the Windows machine will take some time.

Login and download and install SQL Server (developer edition). SSMS is not needed since we will be connecting remotely.

After the installation completes, open Sql Server Configuration Manager and enable TCP/IP protocol.


