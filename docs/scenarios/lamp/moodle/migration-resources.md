---
title: Moodle migration resources
description: Learn about resources for a Moodle migration.
author: BrianBlanchard
ms.author: brblanch 
ms.date: 11/06/2020
ms.topic: conceptual
ms.service: cloud-adoption-framework
ms.subservice: plan
---

# Moodle migration resources

When the Azure Resource Manager template is used, the following resources are created within Azure:

- **Network template:** The network template will create virtual network, network security group, network interface, subnet, public IP address, Azure Load Balancer/Application Gateway, Redis cache, and more.

The network template also creates a virtual network with string as name, apiVersion, location, and DNS server name. The `AddressSpace` contains a range of IP addresses that can be used by subnets.

- **Virtual network:** Azure Virtual Network is a representation of your own network in the cloud. It's a logical isolation of the Azure cloud that's specifically dedicated to your subscription. When you create a virtual network, your services and virtual machines within it can communicate directly and securely in the cloud. For more information, see [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview).

- **Network security group:** A network security group (NSG) is a networking filter (firewall) containing a list of security rules allowing or denying network traffic to resources connected to an Azure Virtual Network. Explore [network security group](/azure/virtual-network/network-security-groups-overview) for more information.

- **Network interface:** A network interface enables an Azure Virtual Machine to communicate with internet, Azure, and on-premises resources. Explore [network interface](/azure/virtual-network/virtual-network-network-interface) for more information.

- **Subnet:** A subnet or subnetwork is a smaller network inside a large network. By default, an IP in a subnet can communicate with any other IP inside the virtual network. Explore [subnet](/azure/virtual-network/virtual-network-manage-subnet) for more information.

- **Public IP:** Public IP addresses are used to communicate Azure resources to the Internet. The address is dedicated to the Azure resource. Explore [public IP](/azure/virtual-network/public-ip-addresses#:~:text=Public%20IP%20addresses%20enable%20Azure,IP%20assigned%20can%20communicate%20outbound) for more information.

- **Azure Load Balancer:** An efficient distribution of network or application traffic across multiple servers in a server farm. Ensures high availability and reliability by sending requests only to servers that are online. Explore [Azure Load Balancer](/azure/virtual-machines/windows/tutorial-load-balancer#:~:text=An%20Azure%20load%20balancer%20is,traffic%20to%20an%20operational%20VM) for more information.

Any of the four predefined templates will deploy Azure Load Balancer. In a fully configurable deployment, the user can choose Azure Application Gateway instead of Load Balancer.

- **Azure Application Gateway:** A web traffic Azure Load Balancer that enables you to manage traffic to your web applications. Application Gateway can make routing decisions based on additional attributes of an HTTP request, as with a URI path or host headers. Explore [Azure Application Gateway](/azure/application-gateway/overview) for more information.

- **Redis cache:** Azure Cache for Redis provides an in-memory data store based on the open-source software, Redis. Redis improves the performance and scalability of an application heavily stores back-end data. It can process large volumes of application requests by keeping frequently accessed data in the server memory, and this data can be written to and read from quickly. Explore [Redis cache](/azure/azure-cache-for-redis/cache-overview) for more information.

- **Storage template:** A storage account template will create a storage account with FileStorage Kind and Premium locally redundant storage (LRS) replication that's 1 terabyte (TB). Per the predefined template, a storage account with Azure Files creates file shares.

An Azure storage account contains blobs, files, queues, tables, and disks, all of which are Azure Storage data objects. The storage account provides a unique namespace for your Azure Storage data that's accessible from anywhere in the world over HTTP or HTTPS. The types of Azure storage accounts are general-purpose V1, general-purpose V2, BlockBlobStorage, FileStorage, and Blob storage. Replication types are LRS and zone-redundant or geo-redundant storage. The performance types are standard and premium, and an individual storage account can store up to 500 TB of data like any other Azure service.

The following storage account types feature Azure Resource Manager template support:

- NFS: A network file system (NFS) allows remote hosts to mount file systems over a network and interact with those file systems as though they're mounted locally. This enables system administrators to consolidate resources onto centralized servers on the network. Explore [NFS](/windows-server/storage/nfs/nfs-overview) for more information.

- GluserFS: An open-source distributed file system that can scale out in building-block fashion to store multiple petabytes of data. Explore [Gluster FS](/azure/virtual-machines/workloads/sap/high-availability-guide-rhel-glusterfs) for more information.

- Azure Files: The only public cloud file storage that delivers secure, SMB-based, and fully managed cloud file shares that can also be cached on-premises for performance and compatibility. Explore [Azure files](/azure/storage/files/storage-files-introduction) for more information. For NFS and glusterFS, the replication is standard LRS, and the storage type is general purpose v1. For Azure Files, the replication is premium locally-redundant storage, LRS, and the type is FileStorage.

These storage mechanisms will differ according to the deployment selected. NFS and glusterFS will create a container, and Azure Files will create a file share. For Minimal and short2mid, the template will support NFS, and for large and maximal, the template will support Azure Files. To access the containers and file share, navigate to portal, and select the storage account in the resource group.

![A storage account.](images/storage-account.png)

Explore [storage account](/azure/storage/common/storage-account-overview) to learn more about storage accounts.

- **Database template:** A database template will create an [Azure Database for MySQL server](/azure/mysql/). Azure Database for MySQL server is easy to set up, manage, and scale. It automates the management and maintenance of your infrastructure and database server, including routine updates, backups, and security. Build with the latest community edition of MySQL, including versions 5.6, 5.7, and 8.0. To access the database server created, navigate to the **Resource group** provided during deployment, and go to **Azure Database for MySQL server.** The database server will have a server name, server admin login name, MySQL version, and a performance configuration.

- **Virtual machine template:** This template will distinguish a virtual Machine as a controller virtual machine. The operating system for a controller virtual machine is Ubuntu 18.04.

- **Virtual machine extension:** Virtual machine extensions can be small applications that provide post-deployment configuration and automation tasks on [Azure Virtual Machines](/azure/virtual-machines/extensions/overview). A virtual machine extension will executes a shell script file that installs Moodle on the controller virtual machine and captures log files. Log files `stderr` and `stdout` are created at the `/var/lib/waagent/custom-script/download/0/`, and the user can view them as a root user.

- **Scale set template:** This template creates a [virtual machine scale set](/azure/virtual-machine-scale-sets/overview). A virtual machine scale set allows you to deploy and manage a set of autoscaling virtual machines. You can scale the number of virtual machines in the scale set manually or define rules to autoscale based on resource usage like CPU, memory demand, or network traffic. Autoscaling virtual machine instances depends on [CPU utilization](/visualstudio/profiling/average-cpu-utilization). While scaling up an instance, a virtual machine is deployed, and a shell script executes to install Moodle prerequisites and set up cron jobs. Virtual machine instances have a private IP. Follow the steps in [how to create a virtual network gateway and connect through a private IP](./vpn-gateway.md) to connect to virtual machines on a scale set with a private IP.

## Next steps

Continue to [how to create a virtual network gateWay and connect through a private IP](./vpn-gateway.md) for more information about the Moodle migration process.
