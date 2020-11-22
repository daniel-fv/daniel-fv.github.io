---
title: "Microsoft 365 Reports"
date: 2020-11-22
---
# Microsoft 365 Reports
Microsoft 365 security and compliance reports are split across four categories. These reports allow you to view how security and compliance rules and technologies are being used.

1. Auditing reports
2. Data Loss Prevention reports
3. Protection reports
4. Rules reports

To view reports in the [Security and Compliance](https://protection.office.com) center you need the following permissions:
- **Security Reader Role in Exchange**. Assigned by default to the Organization Management and Security Reader role groups.

- **DLP Compliance Management Role** in Security & Compliance Center to view DLP reports and policies. Assigned by default to the Compliance Administrator, Organization Management, adn Security Administrator role groups.

## 1- Auditing reports
Three reports are available through the [Security and Compliance Center](https://protection.office.com):

### Office 365 Audit Log report
View user and admin activity related to **email, groups, documents, permissions, directory services** including viewing changes made to administrator role groups.

Go directly to the [Office 365 Audit Log report](https://protection.office.com/unifiedauditlog).

[![Office 365 Audit Log report](../images/microsoft-365-reports-metrics/office-365-audit-log-report.png)](
https://protection.office.com/unifiedauditlog)

Read more in the Microsoft Docs: [Search the audit log in the compliance center](https://docs.microsoft.com/en-us/microsoft-365/compliance/search-the-audit-log-in-security-and-compliance?view=o365-worldwide)

### Azure AD Reports
View Azure Active Directory reports including reports for **unusual or suspicious sign-in activity**. 

The type of reports you can view will depend on the Azure Active Directory subscription. Some reports are included in the Microsoft 365 license, other more advanced reports require Azure Active Directory Premium 1 or Azure Active Directory Premium 2 licenses.

#### Azure AD sign-in activity
Go to the [Azure Active Directory sign-ins](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns) in the Azure Portal under Monitoring.

[![Azure Active Directory sign-ins](../images/microsoft-365-reports-metrics/azure-ad-sign-ins.png)](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/SignIns)

#### Azure AD audit logs
Go to the [Azure Active Directory audit logs](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit) in the Azure Portal under Monitoring.

[![Azure Active Directory audit logs](../images/microsoft-365-reports-metrics/azure-ad-audit-logs.png)](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Audit)

#### Azure AD risky users and sign-ins
First, go to the [Security blade](https://portal.azure.com/#blade/Microsoft_AAD_IAM/SecurityMenuBlade/GettingStarted)

[![Azure Active Directory Security Blade](../images/microsoft-365-reports-metrics/azure-ad-security-blade.png)](https://portal.azure.com/#blade/Microsoft_AAD_IAM/SecurityMenuBlade/GettingStarted)

Then, under **Monitoring** you will find the risky users and sign-ins.
![Azure Active Directory risky users](../images/microsoft-365-reports-metrics/azure-ad-risky-users.png)






