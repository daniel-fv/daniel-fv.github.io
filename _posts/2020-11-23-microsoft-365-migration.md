---
title: "Microsoft 365 Migration"
date: 2020-11-23
---

# Plan migration of user data
We first will need to identify the data that will be migrated, the mailbox to migrate, and how to migrate users.

When assessing which data needs to be migrated to Microsoft 365 we have to consider the following:

- **What data is critical to the organization?** Assess whether all of the data actually needs to be retained.
- **What data needs to be moved?** Not every file and folder needs to be migrated to Microsoft 365. Consider whether files on file servers that haven't been accessed for the last two years need to be migrated.
- **What data will remain on-premises** Due to compliance reasons certain types of data must remain within specific geographic boundaries and cannot be stored in Microsoft's cloud.
- **Where is the data currently located?** Are file share servers used? Is the data located on end-user computers?

Once we've determined which data needs to be migrated to Microsoft 365, we can determine the appropriate method to perform the migration.

# Moving data to SharePoint Online

| **Method**                | **Description**                                                                                    |
| ------------------------- | -------------------------------------------------------------------------------------------------- |
| Migration Manager         | For enterprise-scale migrations of  network file shares                                            |
| SharePoint Migration Tool | Migrate files from on-premises SharePoint *document libraries*, *lists* and *regular file shares.* |
| OneDrive sync client      | Sync client computers files with either OneDrive or SharePoint Online                              |
| Manual upload             | Manually upload files to SharePoint Online                                                         |
| Mover                     | For cloud to cloud migrations (Google Drive, Dropbox, etc)                                         |

---
For more information about migrating data to SharePoint Online: [Migrate your content to Microsoft 365
](https://docs.microsoft.com/en-us/sharepointmigration/migrate-to-sharepoint-online)

# Migrating user mailboxes to Exchange Online

## Remote move migration method
For when you have an Exchange hybrid deployment and *need coexistence* between an on-premises Exchange deployment and an Exchange Online deployment. 

Recommended uses:
- When you need to move more than 2000 mailboxes to Exchange Online.
- Compatible with **Exchange 2010, 2013, 2016**.

Advantages:
- User accounts managed through your on-premises tools.
- Directory synchronization connects your on-premises Exchange with Exchange Online including calendar sharing.
- Email is routed securely between the on-premises Exchange and Exchange Online.

Requirements:
- A hybrid deployment has already been configured.
- The user doing the mailbox moves needs to be a member of the Organization Management or the Recipient Management role groups.
- Have already deployed the Mailbox Replication Proxy Service (MRSProxy) on Exchange 2013/2016 Client Access servers.

Steps:
1. **Create migration endpoint** host connection settings for an on-premises Exchange server running the MRSProxy service. 
2. **Enable MRSProxy service** on the on-premises client access servers.
3. **Move mailboxes** using a migration batch or using the Office 365 tab in the Exchange Admin Console, or by using PowerShell.
4. **Remove completed migration batches**
5. **Re-enable offline access for Outlook on the web** for users that have already been migrated. 

For more information on the steps required: [Move mailboxes between on-premises and Exchange Online](https://docs.microsoft.com/en-us/exchange/hybrid-deployment/move-mailboxes)

## Staged migration method
This method migrates mailboxes in groups or termed batches. This method assumes you intend to *completely move* to Office 365 but the period is in the timeframe of *several weeks or months*.

Recommended uses:
- When you need to migrate more than 2000 mailboxes.
- Compatible with **Exchange 2007** only.

Notes:
- You still manage user accounts using the on-premises management tools synchronized with Azure Active Directory.
- The primary domain name used for your on-premises Exchange must be configured as a domain in the Office 365 tenant.

Steps:
1. **Create a CSV file** containing every on-premises mailbox user that you want to migrate in a particular batch.
2. **Create a staged migration batch** using the Exchange Admin Center or PowerShell.
3. **Trigger the migration batch** 
4. **Get the status report** from the migration. Successfully migrated users can start using Exchange Online mailboxes.
5. **Convert the mailboxes** of successfully migrated on-premises users to mail-enabled users.
6. **Configure a new batch** of users to migrate and delete the current one.
7. **Assign licenses** to Office 365 users and **configure MX records** to point to Exchange Online.
8. **Decommission the on-premises Exchange deployment**.

More information: [What you need to know about a staged email migration](https://docs.microsoft.com/en-us/exchange/mailbox-migration/what-to-know-about-a-staged-migration)

## Cutover migration method
With this method *all on-premises Exchange mailboxes are migrated to Office 365* in a single batch.







