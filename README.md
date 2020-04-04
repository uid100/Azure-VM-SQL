# Deploy-SQLServer-on-Azure-VM

Currently unable to deploy Azure database server resources. This is a temporary, tested workaround.

-----

## Step 1. 

### Build and Deploy (Windows) Virtual Machine

Create VM use Windows 10
From the Size diaglog, sort by cost and select the minimum configuration. This is adequate for student database requirements. This setting may be unsatisfactory for running any developer or activities beyond a single SQL Server instance.  We can scale up if we need to. 

This estimated cost is very reasonable, but can be reduced further by using Linux instead of Windows 10.

Enable RDP port, review and deploy.


![Screen Capture Create VM][CreateVM]

_note: the first deployment failed. steps were repeated using SqlDbWinVM1 and assigned a new IP address: 13.78.132.132.  Results will be the same but the actual machine instance may not match the screenshots_

-----

## Step 2.

### Configure Azure network firewall

From the Networking settings, **Add Inbound Port Rule** to enable inbound SQL TCP port traffic (typically: 1433)

![Screen Capture Add Inbound Port Rule][AddInboundPortRule]

-----

## Step 3.

### Connect to VM, Install & Configure SQL Server 

Connect to VM using Remote Desktop (on port 3389), enter credentials and accept security certificate.

![Screen Capture Remote Desktop][RDP]


The first connection on startup to the Windows machine may take some time.

Download and install SQL Server. _I used Developer Edition for this demonstration_

### Configure SQL Server to use TCP/IP

After the installation completes, open Sql Server Configuration Manager and enable TCP/IP protocol.

Run SQL Configuration

[SqlConfiguration]:[SqlConfiguration]

![EnableTCPIP][EnableTCPIP]

![EnableTCPPorts][EnableTCPPorts]

And restart the SQL Service to enable the changes

![SqlRestart][SqlRestart]

-----

## Step 4.

### Configure SQL Authentication 

Configuring SQL Server can be done from the command line, but SQL Server Management Studio (SSMS) will simplify this task.

Connect to the SQL Server (with SSMS), using Windows Authentication and setup SQL Authentication

Add Sql Login

[AddSqlLogin][AddSqlLogin]

[SqlPassword][SqlPassword]

[DbMapping][DbMapping]

[SetUserRoles][SetUserRoles]

-----

## Step 5.

### Configure Windows Firewall

Windows also installs a Firewall by default and the port exception needs to be added there as well.

Set port 1433 to allow connections and save changes

![Add Inbound Port Exception to Windows Firewall][WinFirewallConfig]

-----

Log out of the VM, leaving it running (or simply close the remote desktop session). 

Test the remote connection.


[AddInboundPortRule]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/AddInboundPortRule.JPG
[AddSqlLogin]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/AddSqlLogin.JPG
[CreateVM]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/CreateVM.JPG
[DbMapping]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/DbMapping.JPG
[EnableTCPIP]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/EnableTCPIP.JPG
[EnableTCPPorts]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/EnableTCPPorts.JPG
[RDP]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/RDP.JPG
[SetUserRoles]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/SetUserRoles.JPG
[SqlConfiguration]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/SqlConfiguration.JPG
[SqlPassword]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/SqlConfiguration.JPG
[SqlRestart]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/SqlRestart.JPG
[WinFirewallConfig]: https://raw.githubusercontent.com/uid100/Deploy-SQLServer-on-Azure-VM/master/WinFirewallConfig.JPG

