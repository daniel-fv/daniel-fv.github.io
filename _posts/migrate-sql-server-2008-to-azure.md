---
title: "Project: Migrate SQL Server 2008 to Azure SQL"
date: 2020-09-20
---

# Migrate SQL Server 2008 to Azure SQL
Now that we have our database upgraded to SQL Server 2008 we can [migrate using the Azure Database Migration Service](https://datamigration.microsoft.com/scenario/sql-to-azuresqldb?step=1).

The steps involved are:
 1. Install Data Migration Assistant (DMA) in our local server
 2. Create a Database Migration Service (DMS) in Azure
 3. Use Azure DMS to migrate

## Data Migration Assistant (DMA) installation
1. We need to [download the DMA](https://www.microsoft.com/en-us/download/details.aspx?id=53595) to our local server.
   
2. After that's installed we create a new assesment project:
   ![Data Migration Assistant](../images/sql-server-2000-export-to-azure-sql/data-migration-assistant-2.png)
3. After the assessment is finished and we have checked that everything is okay with the compatability issues we can proceed.
4. 

![Data Migration Assistant](../images/sql-server-2000-export-to-azure-sql/data-migration-assistant-3.png)