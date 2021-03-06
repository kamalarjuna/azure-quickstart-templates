# Azure Sql Database Managed Instance (SQL MI) Creation inside New Virtual Network
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-sqlmi-new-vnet%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>
<a href="http://armviz.io/#/?load=https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-sqlmi-new-vnet%2Fazuredeploy.json" target="_blank">
    <img src="http://armviz.io/visualizebutton.png"/>
</a>

This template allows you to create a [Azure SQL Database Managed Instances](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-managed-instance) inside a new virtual network.

`Tags: Azure, SqlDb, Managed Instance`

## Solution overview and deployed resources

This deployment will create an Azure Virtual Network with properly configured _ManagedInstance_ subnet and deploy Managed Instance inside.

## Deployment steps

You can click the "Deploy to Azure" button at the beginning of this document or follow the instructions for command line deployment using the scripts in the root of this repo, and populate following parameters:
 - Name of the Managed Instance that will be create including Managed Instance admin name and password
 - Name of the Azure Virtual Network that will be created and configured, including the address range that will be associated to this VNet. Default address range is 10.0.0.0/16 but you could change it to fit your needs.
 - Name of the subnet where Managed Instance will be created. The name will be _ManagedInstance_, if you don't want to change it. Default address range is 10.0.0.0/24 but you could change it to fit your needs.
 - Sku name that combines service tear and hardware generation, number of virtual cores and storage size in GB. The table below shows supported combinations.
 - License type that could be _BasePrice_ if you are eligable for [Azure Hybrid Use Benefit for SQL Server](https://azure.microsoft.com/en-us/pricing/hybrid-benefit/) or _LicenseIncluded_ otherwise

||GP_Gen4|GP_Gen5|BC_Gen4|BC_Gen5|
|----|------|-----|------|-----|
|Tier|General Purpose|General Purpose|Business Critical|Busines Critical|
|Hardware|Gen 4|Gen 5|Gen 4|Gen 5|
|Min vCores|8|8|8|8|
|Max vCores|24|80|32|80|
|Min storage size|32|32|32|32|
|Max storage size|8192|8192|1024|<ul><li>1024 GB for 8, 16 vCores</li><li>2048 GB for 24 vCores</li><li>4096 GB for 32, 40, 64, 80 vCores</ul>|

## Important

During the public preview deployment might take up to 48h (average time is 3-6h). This is because virtual cluster that hosts the instances needs some time to deploy. Each subsequent instance creation in the same virtual cluster takes just about a few minutes.

After the last Managed Instance is deprovisioned, cluster stays a live for up to 24h. This is to avoid waiting for a new cluster to be provisioned in case that customer just wants to recreate the instance. During that period of time Resource Group and virtual network could not be deleted. This is a known issue and Managed Instance team is working on resolving it.


