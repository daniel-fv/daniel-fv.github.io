---
title: "Options for Azure Active Directory authentication"
date: 2020-12-08
---
Options for authenticating users with Azure Active Directory synchronized with an on-premises Active Directory using AD Connect.

# Password hash synchronization
Synchronizes a hash of the user's on-premises password with Azure AD. Azure AD has a copy of the password hashes (encrypted passwords), actual passwords are never sent to Azure AD and are not stored in Azure AD.

When the user authenticates to Azure AD, the submitted password is hashed using the same process and if the hashes match, the user is authenticated.

Each time the user updates their password on-premises, the updated password hash synchronizes to Azure AD. This allows us to use cloud services like Microsoft 365 with our on-premises user and password.

## Password write-back (optional)
Password synchronization also allow us to enable **password write-back** for self service password reset functionality.

Allows users to change their passwords in the cloud and have the changed password written back to the on-premises Active Directory instance.

**Password Hash Synchronization works like this:**

<img src="https://docs.microsoft.com/en-us/azure/active-directory/hybrid/media/plan-connect-user-signin/passwordhash.png" width="600">

-----
# Pass-through authentication
When authenticating to Azure AD, the user's password is validated against an on-premises Active Directory domain controller. Passwords and password hashes are not present in Azure AD.

Pass-through authentication allows for on-premises policies to apply because we are authenticating against the on-premises server. Some of these policies could be sign-in hour restrictions that we can apply to cloud services.

## Single sign-on (SSO) (optional)
Single sign-on allow us to enter our credentials once. A user doesn't have to sign in to every application they use. The user logs in one and that credential is used for other apps to.

That's why when you login to Outlook for Android and later you need to access OneDrive on your smartphone also you don't need to login twice.

Single sign-on is only available when we use pass-through authentication.

**Pass-through authentication works like this:**

<img src="https://docs.microsoft.com/en-us/azure/active-directory/hybrid/media/plan-connect-user-signin/pta.png" width="600">

-----
# Active Directory Federation
This allows users to authenticate to Azure AD resources using on-premises credentials but requires the deployment of an Active Directory Federation Services infrastructure.

This type type of authentication is only likely to be implemented in environments with complicated identity configurations and will not be covered below.

-----
# When to use what

Do you want **Azure AD to handle authentications completely in the cloud** and not depend on on-premises AD servers to be online?
- Yes -> password hash synchronization. 
- No -> pass-through authentication.

Do we need to enforce on-premises **AD security policies** such as hour restrictions? 
- Yes -> pass-through authentication.
- No -> password hash synchronization. 

Do we want users to **change their password on the cloud**?
- Yes ->  password hash synchronization + password write back.
- No -> pass-through authentication.

Do we need **single sign-on (SSO)** for users?
- Yes -> pass-through authentication + single sign-on.
- No -> password hash synchronization.


**Note:**

We can also enable **all four options** and have for signing in pass-through authentication which will also provides us on-premises AD security policies with single sign-on and at the same time enable the options for password synchronization which will provide us with password write back capabilities to reset passwords from the cloud to the on-premises AD servers.
 

----
More information:
- [https://docs.microsoft.com/en-us/azure/active-directory/hybrid/plan-connect-user-signin](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/plan-connect-user-signin)
- [https://docs.microsoft.com/en-us/azure/active-directory/hybrid/choose-ad-authn](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/choose-ad-authn)


