### Azure resources and structure.

Azure is a cloud enviroment that allows the user to deploy enhanced versions of already available on-premise resources with the advantage of cloud prespective and the implementation of automation based on IaC.  

This new perspective on infrastructure solutions and administration branches in many resources and structural units such as :

#### Users and Groups
#### Users:

When we talk about users we have to keep in mind that there are ***2 main***  types of users atending to  _the way they interact with the infrastructure_  

Cloud only users --> ***They are created and managed exclusively from azure***
	Cloud only users can be deployed by Azure portal, Azure PowerShell, and the Azure        command-line interface.

Synchronized users -->  are already created users that obtain a sync with the cloud ad.

#### Bulk User Updates: 

Users can be mass deployed using the bulk deploy tool located in users with the name "Bulk create " and "Bulk invite". To proceed with a bulk deploy we will use a csv file, we can download a template. The standard ***mandatory attributes*** are :
	- Name
	- User Name
	- Initial Password
	- Block sign in.

Nevertheless you can also set a bunch of optional parameters such as : 
	- First Name
	- Last Name
	- Job title

#### Manage Guest Accounts :

Guests users can be invited to a directory, group or application. Inviting a guest automatically triggers the creation of an AD account with the type set to "guest". Guests can be invited by all users and admins (By default), to restrict this policy you have to go to "Manage External Collaboration Settings".
#### Groups:

Deployment fields: 

- When you create a group in azure you have 2 main options to choose from 
    Security 
	   Allows to share access to resources to a gorup of users

    Office 365 
	   Allows to use a shared mailbox, calendar and similar resources.

- Membership type: 
		**Assigned** --> Allows you to manually add and remove one or multiple users.
		**Dynamic User** --> Allows you to use dynamic rules to add and remove users automatically 
		**Dynamic Device** --> Allows you to use dynamic rules to add and remove devices
		automatically.
### Azure AD: 

Azure ad adds the ability to manage device identity setting a perfect scenario to apply a SSI (single sign in) to the applications and services managed throught Azure Active Directory.

Managed devices include both **enterprise devices** and **BYOD** "bring-your-own-device" this allows the personal to work with their devices without compromising the enterprise compliance policy.

#### Device registration: 

Its configured under the Devices/Device Settings blade. The settings you can configure from this window are the following: 

- **Users may join Devices**: allows you to select the users and groups that can intorduce devices to az ad. (*This setting only applies to w10 devices*)

- **Aditional local administrators for joined devices**: With Azure AD Premium or with the Enterprise Mobility Suite you can choose wich users have rigths to each device. (*The default value is none*)

- **Users May Register Their Devices with Azure AD**: Allow users to register their devices with Azure AD

- **Require Multi-Factor Auth To Join Devices**: Multifactor authentication is recommended when adding devices to Azure AD. When set to Yes, users who are adding devices from the Internet must first use a second method of authentication.

- **Maximum Number Of Devices Per User**: Valid values for this setting are 5, 10, 20, 50, 100, and Unlimited.

- **Manage Enterprise State Roaming Settings**: Clicking this link at the bottom of the blade takes you to new blade where you will see the Users May Sync Settings And App Data Across Devices.

#### Self service password reset: 

SSPR allows users to reset their own password saving time to administrators and overall reducing the charge of easy taks such as password resetting. SSPR can be enabled under the Password Reset button on AD tenant, and its values can scope from a group to a whole org, you may also select authentication methods for SSPR such as "Mobile App Notification, Mobile App Code, Email, Mobile Phone, Office Phone, and/or Security Questions".

#### Role based access control

RBAC allows the administrator to manage entities or "**Security principals**" that must access azure resources and regulate the actions that those security principals my perform on said resources. Roles applied to groups will be inhereted, so its important to apply them carefully.

We must distinguish between Azure Roles (Roles are those that manage access to resources.)
and Azure Administrative roles (Those wich authorize the administrators to perform identity tasks).

#### Azure AD Authentication: 

Its a benefitial solution for large customers that want to authenticate the access to the resources on a enterprise scope of the security compliance scope.

### Storage management:  

Sa´s are a cloud based storage service  that  within itself contains multiple permutations adapted for different propouses: 

- Blobs:  Highly scalable service dor storing arbitrary data.

- Tables: Non relational data tables with a NoSQL-style format without a fixed schema.

- Queues: Provides a message queueing between application components.

- Disks: persistent storage volumes that can be attached to VM´s.

##### Naming: 

The names must be unique across all SA´s in azure, it also must be between 3/24 characters.

##### Performance Tiers: 

- Standard: Provides all types of storage services within a SA but you must note they only work based on HDD disks.

- Premium: It only support General propouse  SA´s with disk blobs,page blobs,block blobs and append blobs.

##### Access Tiers: 

- Hot: Used to store frecuently accessed information data access costs are low but storage costs are higher.

- Cool: Used to store large amounts of data that are not frequently accessed and its stored for at least 30 days. Higher data access costs and lower storage ones.

- Archive:  Used to store long therm data that is rarely accessed it can tolerate several hours of retrieval latency and will be stored for at least 180 days.

#### Secure storage

An azure storage account its an az resource used to store azure data objects.
It can contain blobs,files,queues,tables and disks.
Its accesible via http or https (40 and 443 respectibly).


#### Network access to an storage account.

Sa´s are managed throught Azure resource manager, this means that all management operations have to validate the request via either Azure active Directory and RBAC. 

Each Sa has its own endpoint used to manage the storage nevertheless they arent exposed to Azure resource Manager, they are internet-faced endpoints. 

##### Endpoints 

To keep the security compliance of the Sa´s this internet-facing endpoints require a couple of added features. This features are : 

- *Storage firewall*: allows the administrator to limit or manage the specific ip addresses or ranges available to interact with said Sa. The firewall includes also a list of trusted Microsoft services.

- *Virtual Network service endpoints*: When a Sa´s are only managed throught a specific az Vnet its desirable to block internet access. Endpoints are also quite beneficial since they optimize the routing by creating a direct network from the Sa to the Vnet. If you apply a force tunneling solution on a system that forces internet trafic onto a on-premises network the Sa traffic chose the same path. 

##### Azure files 

Its a managed file-share that work based on SMB. And support  On-premise Active directory auth and entra id domain service. Supports up to 5tib per share and with a large file-share enabled up to 100 tib.

To set authentication via Active directory authentication the steps are: 

- Enable AD DS authentication on your storage account.
- Assign share-level access permissions to an Azure AD identity
- Assign directory/file-level permissions using Windows ACLs
- Mount the Azure file share
- Update the password of your storage account identity in AD DS.

Azure file-shares can be accessed with a variety of methods wich are: 

- Outside of azure: Since file-shares work based on SMB protocol you can connect from outside of azure as long as the 445 port is open in your local network. (Note that express route sets 445 so it cant be unblocked)

- Windows file explorer: you can mount the fileshare from windows mapping a new network drive.

##### Configure file-sync:

File-Sync extends to azure files to allow on-premise files services to be extended to az.
Its key functionalities are : 

- multi site access .
- cloud tiering .
- azure backup integration.
- fast disaster recovery.


##### Manage storage: 

If the data stored is large enougth or if you dont have conectivity between your data and the internet, you migth want to migrate it to the cloud but for solutions of such a scale, the price can be prohibitive or the solution migth not even fit the case. Azure import/export (only available for blobs an az files) migth be handy. (Max of 10 hdd disks and 10 ssd disks  and a mix of any size.)


##### Blob storage access levels: 

- Private: Only the owner has access to the content. 

- Blob: only blobs within the container may be accessed anonymously.

- Container: Blobs and their containers can be accessed anonymously.

***Access level can be changed throught Azure portal, Azure PowerShell, Azure CLI, programmatically using the REST API, or by using Azure Storage Explorer 

##### Blob replication: 

It provides asynchronous data replication of blobs from an SA to another. Replication can be setted to only trigger when versioning is also enabled for both the target and the source. The benefits from blob replication are : 

- You can analyze the data of a specific region and apply the results to the remaining regions.

- Users can access data from replicated regions reducing the latency of the requests.

- Compute workloads can process the same information in different regions.

- You can reduce costs applying a lifecycle policy to set data to archive.

Limitations of blob object replication: 

- Dosnt work on archive tier.
- Blob snapshots and inmutable snapshots not supported
- Accounts with hyerarchal namespace not supported.
- No SLA on.
- 2 maximun destinations.
- sets destination on read-only.

##### Blob types: 

- Page blobs: optimized for random read/access operations. Used to store vhd  files with a max size of 8tb.

- Block blobs: Optimized for uploads and downloads for video,images and general propouse storage with a max size of 4.75tb.

- Append blobs: Optimized for append operations, update and delete blocks are not supported, maximun of 195gbs 

##### Soft delete: 

In default settings, when a blob is deleted, its lost forever, soft delete is a feature that prevents losing accidentally this blobs or blob snapshots.
##### SaS tokens: 
A SaS tokens is a URI query string that grants access to a specific container,blob,queue and table. They are mostly used to give access to a certain resource of an SA without having to give them full access to the SA.  ***SaS tokens work on a time margin***  with a specified set of permisions. This tokens are mostly used to authorize read-write operations to users or to copy  blobs/files to another SA.

Each SAS token is a query string parameter that can be appended to the full URI of the blob or other storage resource for which the SAS token was created. Create the SAS URI by appending the SAS token to the full URI of the blob or other storage resource.

##### SaS levels: 

- *Account level SaS*: its a storage account level SaS it lets you perform administrative tasks in the resources listed inside the SA.

- *User delegation SaS*: its **only supported by the blob storage** and it can grant access to containers and blobs.

-  *Service SAS*: its supported by blob, queue,table, and azure files.


##### Stored access policy: 

When you create a SaS it has a set of parameters such as expire time, start time or permissions that cannot be changed and can only be altered by generating a new token. The only way to revoke a SaS token is to roll over the keys of the sa related to its permissions. A stored access policy de-attaches the parameters from the SaS. The access policy is generated independently from the token and said token is generated with a refference to the access policy instead of the parameters. This allows the administrator to modify the parameters. 






### Implement and manage virtual networking.
#### Vnets and subnets: 

Just like on premise Vnets and subnets work based on a range of ips, this ip ranges are defined  using classless inter-domain routing or CIDR.
All the az resources are deployed on subnets, that are contained themselfs inside vnets. The name of each vnet must be unique and cannot be changed.

#### Subnet endpoints: 

Service endpoints are a way to avoid your traffic going throught the internet and instead to flow throught microsofts backbone. Service endpoints can be enabled in subnets and can be added to multiple subnets.

#### Private endpoints:

A private endpoint stablishes a private connection between azure services and your virtual network. 
#### Vnet peering: 

Vnet peering allows two VMs to be able to comunicate being in diferent networks, the Vnets can also be in differente regions or subscriptions. Peering between vnets in different regions is called Global Vnet Peering.  The trafic of this peerings does not travel throught the internet but instead throught microsofts backbone.

Vnet peering is not transitive wich means that in a three net relation where VNETA is peered with VNETB and VNETB is peered with VNETC there is no relation in between VNETA and VNETC. For those to comunicate you must set another peering.

##### Network gateways: 

Vnets can share gateways once they are peered to avoid having to waste resources deploying a gateway for each one.  There are two ways to acomplish this: 

- Remote Gateways: (This setting must be manually enabled in the peering config) allows the vnets to share the same gateway by communicating the existance of said gateway to all peered vnets with the feature enabled.

- Allow Gateway transit: (this feature must be enabled in the peering config) this allows the vnet to send the requests to the other vnets gateway it uses p2s, s2s and vnet2vnet.

##### Private IP addresses: 

Private Ips are configured within the range of a network interface and they are not deployed like a standalone resource. There are two types of Private ips, static and dynamic. (Note that this ips are only viewed inside azure and do not face the internet)

##### Public Ip addresses:

Public ips are the ones that once assigned, they enable the resource to be viewed from the internet. Public ip addresses hace two pricing tiers or SKUS: 

- Standard: supports zone-redundant deployments allowing the use of availability zones, they only support static allocation, closed by default you must open them by using NSGS, Supports ip prefixes.

- Basic: supports both static and dynamic allocation, they are open by default and you must set a NSG to close them, dont support availabilitiy zones, dont support public prefixes. 

#### DNS: 

Dns or domain name servers are svs dedicated to provide name resolution of different types of registers to its clients. To save this name relations we use records and this are the types of record: 

- A : this type of record saves ip addresses. 
- CNAME: this type of record is used to relate a name to another name this type of record dosnt allow to change the root of the name "www.julianlocodelaspoliticas.com" can be translated to "www.juliangraciasportodo.com" but will never be possible to set it as "juliantequeremos.com".
- ALIAS: works the same as a A record but updates with dynamic ips.   
- AAAA: used to map ipv6 addresses 
- MX: used to configure mail servers.
- NS: its the apex in each zone and its required
- SOA: its created and deleted with the zone.


##### DNS services in azure: 

- Azure dns: allows you to host and create dns records for a domain and to provide name servers. It also defines dns zones for intranet-based name resolution.

- Azure traffic manager: Works like a normal dns server but with a little twist, the responses that it offers are based on a set of parameters set by the administrator and this allows to obtain different results with the same query based on said parameters.

- app service domains: allows the administrator to purchase domain names.

- azure provided dns: also known as internal dns, its used to allow the resources you deploy to comunicate in between them. (requires your vms name )

- recursive dns: also called bring you own dns is used to resolve the names of the vms that you bring to a domain controller.

- reverse dns: provides with the ability to configure the reverse lookup for azure asigned public ips.

#### DNS zones: 

Zones allow a dns server to allocate records and administer them .

#### Forced tunneling: 
when routes are configured with 0.0.0.0./0 as a destination this configures the traffic destined to any ips not covered by any other rules.

##### NSGS: 

Network security groups are an azure resource that is used to determine wich comunications or routes can be used or not in your azure networks. All NSGS contain list of rules with allow or deny rules that limit said comunications. 

##### Service tags: 

Service tags are a group of ips that are specifically reserved for the use of a certain resource type. They are mainly used to define firewall rules and to provide routing.
