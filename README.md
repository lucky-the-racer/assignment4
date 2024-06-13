QUESTION -1
Resources : https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview

QUESTION-2
A. Create a VNet with Two Subnets
so for creating a virtual network i go on azure portal and then use these steps
1. Create a Resource Group:

• Go to the Azure portal.

• Navigate to "Resource groups" and click "Add."

• Enter the Resource Group name (e.g., "mygroup') and select a region (e.g., East US').

• Click "Review + Create" and then "Create."

2. Create the Virtual Network with Subnets:

• Go to "Virtual networks" and click "Add."

• Enter the VNet name (e.g., "myvnet:") and select the resource group 'mygroup.

• Under the "IP Addresses" tab, set it default as it .

• Under "Subnets," add two subnets:

• Subnet-1: Address range as it as

• Subnet-2: Address range as it as

• Click "Review + Create" and then "Create."

3.Now We  Create VMs in Subnet-1:

• For Linux VM:

• Go to azure portal and click on create a resource and then we choose "Virtual machines" and click "Add."

• now we Select the resource group "mygroup", and enter the VM name (e.g., mylinuxvm).

• now we Choose the region, and under "Image," select "Ubuntu LTS".

•We  Set the authentication type to SSH public key and configure the rest of the VM settings.

• Now Under the "Networking" tab, select the virtual network myvnet and subnet Subnet-1.

• Click "Review + Create" and then "Create."
  

• For Windows VM:

•We  Follow similar steps as above, but choose "Windows Server 2019 Datacenter as the image.

• Now We Set the authentication type to Password and enter the credentials like I'd and password.

• Under the "Networking" tab, select the virtual network "myvnet and subnet Subnet-1.

• Click "Review + Create" and then "Create."

4.Now We Create SQL Database in Subnet-2:

• So first Create SQL Server:

•Go to azure portal then create a resource and choose "SQL servers" and click "Add."

• Select the resource group 'mygroup', and enter the server name (e.g. "myservermy"), region, and admin login credentials.

• Click "Review + Create" and then "Create."

•For Creating SQL Database:

• Go to "SQL databases" and click "Add."

• Select the resource group "mygroup, and choose the SQL server "myservermy".

• Enter the database name (e.g., "mydatabase").

• Click "Review + Create" and then "Create."


B. Create Four VNets and Configure Hub-and-Spoke Architecture
Resources:
•Virtual Network Documentation
•Create Management VNet (HUB):

•Go to "Virtual networks" and click "Add.
•Enter the VNet name (e.g., managementvnet), select the resource group mygroup, and set the address space to 10.1.0.0/16.
•Click "Review + Create" and then "Create."
•Create Production, testing, and developing VNets:

•Repeat the steps for creating VNets for:
•productionvnet: Address space 10.2.0.0/16
•testingvnet: Address space 10.3.0.0/16
•developingVNet: Address space 10.4.0.0/16
•Now for peering we use the bash and these commands
 1.Peering productionvnet with managementvnet:
 2.Peering TestingVNet with ManagementVNet:
 3.Peering DevelopingVNet with ManagementVNet:
•BY COMMAND LINE: (BASH)
az network vnet peering create --name prodTomgmtPeering --resource-group mygroup --vnet-name productionvnet --remote-vnet managementvnet --allow-vnet-access
az network vnet peering create --name mgmtToprodPeering --resource-group mygroup --vnet-name managementvnet --remote-vnet productionvnet --allow-vnet-access
az network vnet peering create --name TestToMgmtPeering --resource-group MyResourceGroup --vnet-name TestingVNet --remote-vnet ManagementVNet --allow-vnet-access
az network vnet peering create --name MgmtToTestPeering --resource-group MyResourceGroup --vnet-name ManagementVNet --remote-vnet TestingVNet --allow-vnet-access
az network vnet peering create --name DevToMgmtPeering --resource-group MyResourceGroup --vnet-name DevelopingVNet --remote-vnet ManagementVNet --allow-vnet-access
az network vnet peering create --name MgmtToDevPeering --resource-group MyResourceGroup --vnet-name ManagementVNet --remote-vnet DevelopingVNet --allow-vnet-access

•Now we Create Virtual Machines in Each VNet
•we use bash and create virtual machine in each virtual network.
•Now we Verify Connectivity
1.SSH into ManagementVM:
•Retrieve the public IP of ManagementVM:
•SSH into the ManagementVM (replace <public_ip> with the actual IP):

2.Ping Other VMs:
•Retrieve the private IP addresses of the other VMs:
•Use the private IP addresses to ping each VM from ManagementVM

•BY COMMAND LINE: (BASH)
az vm list-ip-addresses --name ManagementVM --resource-group MyResourceGroup --output table
ssh azureuser@<public_ip>
az vm list-ip-addresses --name ProductionVM --resource-group MyResourceGroup --output table
az vm list-ip-addresses --name TestingVM --resource-group MyResourceGroup --output table
az vm list-ip-addresses --name DevelopingVM --resource-group MyResourceGroup --output table
ping <private_ip_of_ProductionVM>
ping <private_ip_of_TestingVM>
ping <private_ip_of_DevelopingVM>

QUESTION-3
