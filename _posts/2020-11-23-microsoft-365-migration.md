---
title: "Microsoft 365 users, data, mailboxes migration"
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
The methods to migrate mailboxes to Exchange Online that we will cover in this section are:

| **On-premises environment**     | **Number of mailboxes** | **On-premises user administration** | **Migration method**                       |
| ------------------------------- | ----------------------- | ----------------------------------- | ------------------------------------------ |
| Exchange 2010 or later          | Less than 2000          | No                                  | Cutover migration                          |
| Exchange 2007                   | Less than 2000          | No                                  | Staged migration                           |
| Exchange 2010 or later          | More than 2000          | Yes                                 | Remote move migration in hybrid deployment |
| Exchange 2010 or later          | No maximum              | No                                  | Minimal Hybrid or Express Migration        |
| Non-Exchange on-premises server | No maximum              | No                                 | IMAP migration                             |


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
This method migrates mailboxes in groups or termed batches. This method assumes you intend to *completely move* to Office 365.

Recommended uses:
- When you need to migrate more than 2000 mailboxes in the timeframe of *several weeks or months*.
- Compatible with **Exchange 2007** only.

Notes:
- You still manage user accounts using the on-premises management tools synchronized with Azure Active Directory.
- The primary domain name used for your on-premises Exchange must be configured as a domain in the Office 365 tenant.

Steps:
1. **Create a CSV file** containing every on-premises mailbox user that you want to migrate in a particular batch.
2. **Create a staged migration batch** using the Exchange Admin Center or PowerShell.
3. **Trigger the migration batch**. 
4. **Get the status report** from the migration. Successfully migrated users can start using Exchange Online mailboxes.
5. **Convert the mailboxes** of successfully migrated on-premises users to mail-enabled users.
6. **Configure a new batch** of users to migrate and delete the current one.
7. **Assign licenses** to Office 365 users and **configure MX records** to point to Exchange Online.
8. **Decommission the on-premises Exchange server**.

More information: [What you need to know about a staged email migration](https://docs.microsoft.com/en-us/exchange/mailbox-migration/what-to-know-about-a-staged-migration)

## Cutover migration method
With this method *all on-premises Exchange mailboxes are migrated to Office 365* in a single batch.

Recommended uses:
- When you need to migrate less than 2000 mailboxes in less than a week.
- You need to move mailboxes to Office 365. 
- Compatible with **Exchange 2010 or later**.

Notes:
- The primary domain name used for your on-premises Exchange must be configured as a domain in the Office 365 tenant.
- You will need to manage user accounts with Office 365 tools.
- On-premises distribution groups will also be migrated to Office 365.

Steps:
1. **Create an empty mail-enabled security group** in Office 365.
2. **Create a migration endpoint** that connects Office 365 to the on-premises Exchange server.
3. **Create a cutover migration batch** using Exchange Admin Center or PowerShell.
4. **Trigger the migration batch**.
5. **Get the status report** from the migration. The reports include automatically generated passwords for the new Exchange Online users.
6. **Incremental synchronization occurs every 24 hours** for newly created items on the on-premises mailboxes.
7. **Configure MX records** to point to Exchange Online
8. **Delete cutover migration batch**. This terminates synchronization between on-premises Exchange and Office 365.
9. **Assign licenses** to Office 365 users.
10. **Decommission the on-premises Exchange server**.

For more information: [Migrate email using the Exchange cutover method](https://docs.microsoft.com/en-us/exchange/mailbox-migration/cutover-migration-to-office-365)

## Minimal Hybrid or Express Migration
For when you need to *retire your on-premises Active Directory* infrastructure after the migration is complete.

Recommended uses:
- Compatible with **Exchange 2010 or later**.
- Your timetable is shorter than a few weeks.
- You need to move mailboxes to Office 365.

Steps:
1. **Add the domain** in the Microsoft 365 console.
2. **Start the Exchange Hybrid Configuration wizard** from the *Data Migration* blade in the Microsoft 365 admin console.
3. **Connect to the on-premises Exchange Server** using the Minimal Hybrid Configuration using the wizard.
4. **Synchronize users and passwords** one at a time. For this you will need to install Azure AD Connect for a one time synchronization.
5. **Configure Office 365 licenses** and begin **migrating user mailbox data**.
6. **Update MX records** to point to Exchange Online.

More information: [Use Minimal Hybrid to quickly migrate Exchange mailboxes to Microsoft 365](https://docs.microsoft.com/en-us/exchange/mailbox-migration/use-minimal-hybrid-to-quickly-migrate)

## IMAP migration
Uses the IMAP protocol to move the on-premises user mailboxes to Exchange Online.

Recommended uses:
- Where the on-premises mail server is not running Exchange Server.
- Supported for Courier-IMAP, Cyrus, Dovecot, and UW-IMAP messaging solutions.

Steps:
1. **Create Office 365 user accounts** and assign them Exchange Online licenses.
2. **Create a CSV file with mailbox user passwords**. It is recommended that you reset user passwords to simplify this process.
3. **Create and trigger an IMAP migration batch** from the *Data Migration* blade in the Microsoft 365 admin console.
4. **Messages from each user are copied** to their corresponding Exchange Online mailbox.
5. **Get the status report** from the migration. 
6. **Incremental synchronization occurs every 24 hours** and will move any new messages received on the on-premises environment to Exchange Online.
7. **Update MX records** to point to Exchange Online.

For more information: [What you need to know about migrating your IMAP mailboxes to Microsoft 365](https://docs.microsoft.com/en-us/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes)


# Plan migration of on-premises users and groups
Migration is different to hybrid coexistence. 

Decide if you need a particular user account to be moved to Microsoft 365:
- **Is the user account still active?** There is no reason to migrate inactive user accounts.
- **Should the account be migrated to Microsoft 365?** Service or administrative accounts for specific on-premises services that will not be migrated to Microsoft 365 are unlikely to be required in Microsoft 365. For example: accounts used for management of an on-premises SQL server database or other workloads.

## Bulk user import process
If you are planning to *completely migrate to Azure AD* as the primary identity provider and to decommission the on-premises Active Directory.

This process allows you to import a list of users from a formatted CSV file into Microsoft 365. This CSV file must have the following fields in the first row:
- User Name
- First Name
- Last Name
- Display Name
- Job Title
- Department
- Office Number
- Office Phone
- Mobile Phone
- Fax
- Address
- City
- State
- Zip
- Country

You upload this CSV file using the Microsoft 365 Admin Center. On the Users blade and then selecting the *Import Multiple Users* option.

Note:
Use the bulk import process when you want to move a large number of users. If you are migrating only a small number of users, it may be simpler to manually create those users using the Microsoft 365 administration tools.

## Understanding Office 365 groups
If you are planning to decommission the on-premises directory, the Active Directory group scope (domain local, domain global, and universal) is not relevant because we do not care whether a group is visible in other domains in an Active Directory forest as we are retiring the local Active Directory forest.

Office 365 groups allow us to set up a collection of resources that a set of users can share. This includes: 
- A shared calendar.
- SharePoint Online document library.
- Shared Exchange Online mailbox.
- Teams group chat.

Three methods through which Office 365 groups can be provisioned:
1. **Open**: Allows Microsoft 365 users to create their own groups as needed.
2. **IT-led**: Users request a group from IT.
3. **Controlled**: Group creation is limited to users that have been delegated the group creation role.

## Synchronize users and groups with Azure AD Connect
You can also use Azure AD Connect to synchronize accounts to Azure AD and then decommission your on-premises environment.

In this scenario we need to evaluate which identities we will replicate doing an audit of all the objects present on the on-premises Active Directory and determine if every on-premises identity needs to be present in the Azure Active Directory.

We also could take a phased approach and migrate small groups of users to Microsoft 365 rather than every user at once.