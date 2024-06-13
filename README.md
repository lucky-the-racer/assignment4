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
#commnds for peering

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

#commands for ping

az vm list-ip-addresses --name ManagementVM --resource-group MyResourceGroup --output table

ssh azureuser@<public_ip>

az vm list-ip-addresses --name ProductionVM --resource-group MyResourceGroup --output table

az vm list-ip-addresses --name TestingVM --resource-group MyResourceGroup --output table

az vm list-ip-addresses --name DevelopingVM --resource-group MyResourceGroup --output table

ping <private_ip_of_ProductionVM>

ping <private_ip_of_TestingVM>

ping <private_ip_of_DevelopingVM>

QUESTION-3

:Create Internal and External Load Balancer

•Internal Load Balancer:

1.Navigate to the Azure Portal:

•Go to the Azure Portal at portal.azure.com.

2.Create a New Resource:

•Click on "+ Create a resource" in the left menu.

3.Search for Load Balancer:

•In the search bar, type "Load Balancer" and press Enter.

4.Select Internal Load Balancer:

•Click on "Internal Load Balancer" from the search results.

5.Fill in Load Balancer Details:

•Subscription: Choose your subscription.

•Resource Group: Select or create a resource group.

•Name: Enter a name for your Internal Load Balancer.

•Region: Choose the region where you want to deploy the load balancer.

•Virtual network: Select the virtual network where you want to deploy the load balancer.

•Subnet: Choose a subnet within the selected virtual network.

•IP address: Specify the IP address for the internal load balancer.

•Configure Backend Pool and Health Probes:

6.Add backend pool by selecting the virtual machines or availability sets to be load balanced.

•Configure health probes to check the health of your backend VMs.

7.Review and Create:

•Review the settings and click "Create" to deploy the Internal Load Balancer.

:External Load Balancer:

1.Navigate to the Azure Portal:

•Go to the Azure Portal at portal.azure.com.

2.Create a New Resource:

•Click on "+ Create a resource" in the left menu.

3.Search for Load Balancer:

•In the search bar, type "Load Balancer" and press Enter.

4.Select External Load Balancer:

•Click on "External Load Balancer" from the search results.

5.Fill in Load Balancer Details:

•Follow steps 5-7 from the Internal Load Balancer section, but ensure you choose the appropriate settings for an external load balancer, including a public IP address.

6.Configure Frontend IP Configuration:

•For an external load balancer, you need to configure a public IP address as the frontend IP configuration.

7.Review and Create:

•Review the settings and click "Create" to deploy the External Load Balancer.

QUESTION- 4

Step 1: Create Application Gateway

1.Navigate to the Azure Portal:

 •Go to the Azure Portal at portal.azure.com.

2.Create a New Resource:

•Click on "+ Create a resource" in the left menu.

3.Search for Application Gateway:

•In the search bar, type "Application Gateway" and press Enter.

4.Select Application Gateway:

•Click on "Application Gateway" from the search results.

5.Fill in Application Gateway Details:

•Subscription: Choose your subscription.

•Resource Group: Select or create a resource group.

•Name: Enter a name for your Application Gateway.

•Region: Choose the region where you want to deploy the Application Gateway.

•SKU: Choose the appropriate SKU based on your requirements (Standard_v2 is recommended for most scenarios).

•Tier: Select the appropriate tier (Standard or WAF).

•Virtual network: Select the virtual network where you want to deploy the Application Gateway.

•Subnet: Choose a subnet within the selected virtual network.

6.Configure Backend Pool and HTTP Settings:

•Add backend pool by specifying the IP addresses or DNS names of the backend servers.

•Configure HTTP settings like port, protocol, and cookie-based affinity.

7.Configure Frontend IP and Listener:

•Define the frontend IP configuration, including a public IP address (if needed).

•Add a listener with appropriate settings (port, protocol, and SSL if required).

8.Configure Routing Rules:

•Define routing rules to route incoming requests to appropriate backend pools based on the request path or host header.

9.Review and Create:

•Review the settings and click "Create" to deploy the Application Gateway.

Step 2: Test Application Gateway

1.Access Application Gateway's Public IP:

•Once the Application Gateway is deployed, note down its public IP address.

2.Access Backend Service:

•Ensure that your backend service (e.g., a web server) is running and accessible within your virtual network.

3.Test Access to Backend Service:

•Open a web browser and navigate to the public IP address of the Application Gateway.

•You should be able to access your backend service through the Application Gateway.

4.Test Load Balancing and Routing:

•If you configured multiple backend pools and routing rules, test the load balancing and routing by accessing different paths or hostnames defined in your routing rules.

5.Monitor Application Gateway Metrics:

•After testing, monitor the performance and health of your Application Gateway using Azure Monitor metrics and logs.

•By following these steps, you can create and test an Azure Application Gateway to manage and optimize traffic to your web applications.

QUESTION - 5

To set up a domain, configure a DNS server, and direct traffic to your server using the Azure CLI, you would follow these general steps:

Step 1: Create a Resource Group

az group create --name MyResourceGroup --location <location>

Step 2: Create a Virtual Network and Subnet

az network vnet create --resource-group MyResourceGroup --name MyVnet --address-prefixes 10.0.0.0/16 --subnet-name MySubnet --subnet-prefixes 10.0.0.0/24

Step 3: Create a Virtual Machine

az vm create --resource-group MyResourceGroup --name MyVM --image UbuntuLTS --admin-username azureuser --generate-ssh-keys --vnet-name MyVnet --subnet MySubnet

Step 4: Assign a Public IP Address to the VM (if needed)

az network public-ip create --resource-group MyResourceGroup --name MyPublicIP
az network nic ip-config update --resource-group MyResourceGroup --name ipconfigmyvm --nic-name MyVMVMNic --public-ip-address MyPublicIP

Step 5: Install and Configure DNS Server on the VM
SSH into the VM and install a DNS server software such as BIND or dnsmasq.

Step 6: Configure DNS Records
Add DNS records for your domain pointing to the public IP address of your VM.

Step 7: Update DNS Server Settings
Update the DNS server settings in your virtual network to point to your DNS server.

az network vnet update --resource-group MyResourceGroup --name MyVnet --dns-servers <private-ip-of-your-dns-server>

Step 8: Verify and Test

Verify that your domain resolves to the correct IP address by using tools like nslookup or dig. You can also try accessing your domain in a web browser to see if it loads your server.

Ensure that your DNS server is properly configured to handle incoming traffic and direct it to the appropriate resources on your VM.

These steps should guide you through setting up a domain, configuring a DNS server, and directing traffic to your server using the Azure CLI. Remember to replace placeholders like <location> and <private-ip-of-your-dns-server> with appropriate val
