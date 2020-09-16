---
title: "Project: Prepare SQL Server 2000 database for migration to Azure SQL Database"
date: 2020-09-20
---

The goal is to upgrade a Microsoft SQL Server 2000 to Azure SQL Database.

Migrating to Azure SQL Database directly from SQL Server using the *Azure Database Migration Service* requires at least SQL Server 2005. We need to upgrade our database to a newer version. In this example I chose to upgrade to SQL Server 2008.

# Upgrade SQL Server 2000 to 2008

## Pre migration steps - Upgrade Advisor
The first thing we must do is to check weather 

The SQL Server 2000 must have installed SP4. If it's not installed we need to install it first.

1. Download and install the Microsoft SQL Server 2008 Upgrade Advisor in **same server** where the SQL Server 2000 is installed.
  <https://www.microsoft.com/en-us/download/details.aspx?id=11455>
2. Run Microsoft SQL Server 2008 Upgrade Advisor
   We launch the wizard, our database should be detected:
   ![SQL Server Upgrade Wizard database options](../images/sql-server-2000-export-to-azure-sql/sql-server-2008-upgrade-wizard-1.png)
3. Select authentication options:
   ![SQL Server Upgrade Wizard authentication](../images/sql-server-2000-export-to-azure-sql/sql-server-2008-upgrade-wizard-2.png)
4. Choose database to analyze:
   ![SQL Server Upgrade Wizard analyze database](../images/sql-server-2000-export-to-azure-sql/sql-server-2008-upgrade-wizard-3.png)
5. Select Next and on the next screen choose your options for analyzing the rest of SQL Server components if you need to:
   ![SQL Server Upgrade Wizard progress](../images/sql-server-2000-export-to-azure-sql/sql-server-2008-upgrade-wizard-4.png)
6. After a few minutes a report will be generated with warnings. These items may include Full Text Search, replication, objects that no longer exist or have been modified in the new version:
![SQL Server Upgrade Wizard report](../images/sql-server-2000-export-to-azure-sql/sql-server-2008-upgrade-wizard-5.png)

Once you fix the warnings or at least you are aware of the features you may lose in SQL Server 2008 the process of migration begins.

## Make a backup of the SQL Server 2000 database
Find url----

## Import SQL Server 2000 backup to SQL Server 2008
### Create interim SQL server 2008 in Azure
For the interim SQL server 2008 DB we'll create a VM in Azure.

We'll be using the image in Azure for SQL Server 2008 R2 that comes in Windows Server 2008 R2.
![SQL Server 2008 installation in Azure](../images/sql-server-2000-export-to-azure-sql/azure-sql-server-2008-install.png)

We create the VM in Azure
![SQL Server 2008 installation](../images/sql-server-2000-export-to-azure-sql/azure-sql-server-2008-install-2.png)

Now, we need to transfer the SQL Server 2000 backup to the VM in Azure. One easy way to do this is to RDP from the server that has the backup to the VM in Azure with the options to access local resources:
![RDP access local resources](../images/sql-server-2000-export-to-azure-sql/rdp-access-local-resources.png)

From our Windows Server 2008 VM in Azure we can now access our local drive to copy the backup:
![RDP access C drive](../images/sql-server-2000-export-to-azure-sql/rdp-access-local-resources-2.png)

### Import SQL Server 2000 backup to SQL Server 2008
1. For the actual importing we'll use SQL Server Management Studio (SSMS) according to these instructions: <https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms>
2. We launch SSMS 2008 from our VM running SQL Server 2008:
   ![SQL Server Management Studio](../images/sql-server-2000-export-to-azure-sql/ssms-2008-import-db.png)
3. Right click Databases and select **Restore Database**:
   ![SQL Server Management Studio restore database](../images/sql-server-2000-export-to-azure-sql/ssms-2008-import-db-2.png)
4. Select backup:
![SQL Server Management Studio select backup](../images/sql-server-2000-export-to-azure-sql/ssms-2008-import-db-3.png)
5. Select destination for restore:
![SQL Server Management Studio backup](../images/sql-sql-server-2000-export-to-azure-sql/../sql-server-2000-export-to-azure-sql/ssms-2008-import-db-4.png)
Once that finishes we'll see a message saying that the import was successful. 
6. I won't cover it in detail but if you also need to copy the database users and SQL Server Agent jobs you can do it the following through scripts you can find on the internet or using the following:

- Copy database users / logins
  - SQL Server Integration Services using "Transfer Login task"
  - SQL Server Management Studio, with "Copy Database Wizard"

- Copy SQL Server Agent jobs
  - You can migrate your SQL Server Agent jobs using Enterprise Manager 2000. You can find more detail in the documentation: [How to script jobs using Transact-SQL (Enterprise Manager)](http://msdn.microsoft.com/en-us/library/aa177024(SQL.80).aspx)



References:
- [Migration SQL Server 2000 to SQL Server 2008](https://docs.microsoft.com/en-us/archive/blogs/mdegre/migration-sql-server-2000-to-sql-server-2008)