---
title: "Office 365 dev/test environment"
ms.author: josephd
author: JoeDavies-MSFT
manager: laurawi
ms.date: 12/15/2017
ms.audience: ITPro
ms.topic: article
ms.service: o365-solutions
localization_priority: Normal
ms.collection:
- Ent_O365
- Ent_O365_Hybrid
ms.custom:
- DecEntMigration
- Strat_O365_Enterprise
- Ent_TLGs
ms.assetid: 4f6035b8-2da3-4cf9-9657-5284d6364f7a
description: "Summary: Use this Test Lab Guide to create an Office 365 trial subscription for evaluation or dev/test."
---

# Office 365 dev/test environment

 **Summary:** Use this Test Lab Guide to create an Office 365 trial subscription for evaluation or dev/test.
  
You can use an Office 365 trial subscription and create an Office 365 dev/test environment for applications or to demonstrate features and capabilities of Office 365. There are two versions:
  
- The lightweight Office 365 dev/test environment consists of an Office 365 trial subscription that you access from your main computer.
    
    Use this environment when you want to quickly demonstrate a feature. For the lightweight Office 365 dev/test environment, complete phases 2 and 3 of this article.
    
- The simulated enterprise Office 365 dev/test environment consists of an Office 365 trial subscription and a simplified organization intranet connected to the Internet, which is hosted in Microsoft Azure infrastructure services. You can build this configuration completely in the Microsoft cloud.
    
    Use this environment when you want to demonstrate a feature or an app in an environment that resembles a typical organization network connected to the Internet, or for features that require this type of environment. For the simulated enterprise Office 365 dev/test environment, complete phases 1, 2, and 3 of this article.
    
> [!NOTE]
> You might want to print this article to record the specific values that you will need for this environment over the 30 days of the Office 365 trial subscription. You can easily extend the trail subscription for another 30 days. For a permanent dev/test environment, create a new paid subscription with a small number of licenses. 
  
![Test Lab Guides in the Microsoft Cloud](images/24ad0d1b-3274-40fb-972a-b8188b7268d1.png)
  
> [!TIP]
> Click [here](http://aka.ms/catlgstack) for a visual map to all the articles in the One Microsoft Cloud Test Lab Guide stack.
  
## Phase 1: Create the base configuration in Azure

Follow the instructions in [Base Configuration dev/test environment](base-configuration-dev-test-environment.md).
  
You will need an Azure subscription. You can use the [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/) for this configuration. If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).
  
Here is the resulting configuration.
  
![The Base Configuration dev/test environment in Azure](images/63108214-f716-46ae-9974-072ff15b44a2.png)
  
This configuration consists of the DC1, APP1, and CLIENT1 virtual machines on a subnet of an Azure virtual network.
  
## Phase 2: Create an Office 365 trial subscription

To start your Office 365 E5 trial subscription, you first need a fictitious company name and a new Microsoft account.
  
1. We recommend that you use a variant of the company name Contoso for your company name, which is a fictitious company used in Microsoft sample content, but it isn't required. Record your fictitious company name here: _____________________________________
    
2. To sign up for a new Microsoft account, go to [https://outlook.com](https://outlook.com) and create an account with a new email account and address. You will use this account to sign up for Office 365.
    
  - Record the first and last name of your new account here: _______________________________
    
  - Record the new email account address here: _____________________________@outlook.com
    
### Sign up for an Office 365 E5 trial subscription

1. For the lightweight Office 365 dev/test environment, open the Internet browser on your computer and go to [https://aka.ms/e5trial](https://aka.ms/e5trial). 
    
    For the simulated enterprise Office 365 dev/test environment:
    
  - From the [Azure portal](https://portal.azure.com), connect to CLIENT1 with the CORP\\User1 account.
    
  - Open an administrator-level Windows PowerShell command prompt, and then run these commands:
    
  ```
  Set-ItemProperty -Path "HKLM:\\SOFTWARE\\Microsoft\\Active Setup\\Installed Components\\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0
Set-ItemProperty -Path "HKLM:\\SOFTWARE\\Microsoft\\Active Setup\\Installed Components\\{A509B1A8-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0
Stop-Process -Name Explorer -Force
  ```

    > [!TIP]
    > Click [here](https://gallery.technet.microsoft.com/PowerShell-commands-for-fe3d7a34) to get a text file that contains all the PowerShell commands in this article.
  
  - From the Start screen, click **Internet Explorer** and go to [https://aka.ms/e5trial](https://aka.ms/e5trial).
    
2. On the **Welcome, let's get to know you** page, specify:
    
  - Your physical location
    
  - The first and last name of your new Microsoft account
    
  - Your new email account address
    
  - A business phone number
    
  - Your fictional company name
    
  - An organization size of 250-999 people
    
3. Click **Just one more step**.
    
4. On the **Create your user ID** page, type a user name based on your new email address, your fictional company after the @ sign (remove all spaces in the name), then a password (twice) for this new Office 365 account.
    
    Record the password that you typed in a secure location.
    
    Record your fictional company name, to be referred to as the **organization name**, here: ________________________________________
    
5. Click **Create my account**.
    
6. On the **Prove. You're. Not. A. Robot.** page, type the phone number of your text-capable phone, and then click **Text me**.
    
7. Type the verification code from the received text message, and then click **Next**.
    
8. Record the sign-in page URL here (select and copy): ___________________________________________
    
9. Record the user ID here (select and copy): __________________________________.onmicrosoft.com
    
    This value will be referred to as the **Office 365 global administrator name**.
    
10. When you see **You're ready to go**, click it.
    
11. On the next page, wait until Office 365 completes setting up and all the tiles are available.
    
You should see main Office 365 portal page from which you can access Office Online services and the Office 365 Admin center.
  
For the simulated enterprise Office 365 dev/test environment, here is your resulting configuration.
  
![The Office 365 dev/test environment](images/48fb91aa-09b0-4020-a496-a8253920c45d.png)
  
This configuration consists of: 
  
- The DC1, APP1, and CLIENT1 virtual machines on a subnet of an Azure virtual network.
    
- An Office 365 E5 Trial Subscription.
    
## Phase 3: Configure your Office 365 trial subscription

In this phase, you configure your Office 365 subscription with additional users and SharePoint Online team sites.
  
First, you add four new users and assign them E5 licenses.
  
Use the instructions in [Connect to Office 365 PowerShell](https://technet.microsoft.com/library/dn975125.aspx) to install the PowerShell modules and connect to your new Office 365 subscription from:
  
- Your computer (for the lightweight Office 365 dev/test environment).
    
- The CLIENT1 virtual machine (for the simulated enterprise Office 365 dev/test environment).
    
 In the Windows PowerShell Credential Request dialog box, type the Office 365 global administrator name (example: jdoe@contosotoycompany.onmicrosoft.com) and password.
  
Fill in your organization name (example: contosotoycompany), the two-character country code for your location, and then run the following commands from the Windows Azure Active Directory Module for Windows PowerShell prompt:
  
```
$orgName="<organization name>"
$loc="<two-character country code, such as US>"
$licAssignment= $orgName + ":ENTERPRISEPREMIUM"
$userName= "user2@" + $orgName + ".onmicrosoft.com"
New-MsolUser -DisplayName "User 2" -FirstName User -LastName 2 -UserPrincipalName $userName -UsageLocation $loc -LicenseAssignment $licAssignment
```

From the display of the **New-MsolUser** command, note the generated password for the User 2 account and record it in a safe location.
  
Run the following commands from the Windows Azure Active Directory Module for Windows PowerShell prompt:
  
```
$userName= "user3@" + $orgName + ".onmicrosoft.com"
New-MsolUser -DisplayName "User 3" -FirstName User -LastName 3 -UserPrincipalName $userName -UsageLocation $loc -LicenseAssignment $licAssignment
```

From the display of the **New-MsolUser** command, note the generated password for the User 3 account and record it in a safe location.
  
Run the following commands from the Windows Azure Active Directory Module for Windows PowerShell prompt:
  
```
$userName= "user4@" + $orgName + ".onmicrosoft.com"
New-MsolUser -DisplayName "User 4" -FirstName User -LastName 4 -UserPrincipalName $userName -UsageLocation $loc -LicenseAssignment $licAssignment
```

From the display of the **New-MsolUser** command, note the generated password for the User 4 account and record it in a safe location.
  
Run the following commands from the Windows Azure Active Directory Module for Windows PowerShell prompt:
  
```
$userName= "user5@" + $orgName + ".onmicrosoft.com"
New-MsolUser -DisplayName "User 5" -FirstName User -LastName 5 -UserPrincipalName $userName -UsageLocation $loc -LicenseAssignment $licAssignment
```

From the display of the **New-MsolUser** command, note the generated password for the User 5 account and record it in a safe location.
  
Next, you create three new SharePoint Online team sites for the Sales, Production, and Support departments.
  
### Create three new SharePoint Online team sites

1. Install the [SharePoint Online Management Shell](https://go.microsoft.com/fwlink/p/?LinkId=255251) (the x64 version).
    
2. Click **Start**, type **sharepoint**, and then click **SharePoint Online Management Shell**.
    
3. Fill in your organization name (example: contosotoycompany), and then run the following commands from the SharePoint Online Management Shell prompt to connect to the SharePoint Online service
```
$orgName="<organization name>"
$spURL="https://" + $orgName + "-admin.sharepoint.com"
Connect-SPOService -Url $spURL
```

4. In the **Microsoft SharePoint Online Management Shell** dialog box, type the Office 365 global administrator name (example: jdoe@contosotoycompany.onmicrosoft.com) and password, and then click **Sign in**.
    
5. To create three new team sites (Sales, Production, and Support), fill in the Office 365 global administrator name, and then run the following commands from the SharePoint Online Management Shell prompt:
    
  ```
  $owner = "<global administrator account name>"
$siteURL = "https://" + $orgName + ".sharepoint.com/sites/sales"
New-SPOSite -Url $siteURL -Owner $owner -StorageQuota 1000 -Title "Sales site collection" -Template "STS#0"
$siteURL = "https://" + $orgName + ".sharepoint.com/sites/production"
New-SPOSite -Url $siteURL -Owner $owner -StorageQuota 1000 -Title "Production site collection" -Template "STS#0"
$siteURL = "https://" + $orgName + ".sharepoint.com/sites/support"
New-SPOSite -Url $siteURL -Owner $owner -StorageQuota 1000 -Title "Support site collection" -Template "STS#0"
  ```

6. Run this command to list the URLs of these new sites:
    
  ```
  Get-SPOSite | Where URL -like "*/sites/*" | Sort URL | Select URL
  ```

7. In Internet Explorer, enter the URL of the Production site to see the default SharePoint Online team site for the Production department.
    
## Record values for future reference

Record these values for working with or deploying additional Test Lab Guides in this test environment:
  
- Office 365 global administrator name: ____________________________________.onmicrosoft.com (from step 9 of Phase 2)
    
    Also record the password for this account in a secure location.
    
- Your trial subscription organization name: _______________________________________________ (from step 4 of Phase 2)
    
- To list the accounts for User 2, User 3, User 4, and User 5, run the following command from the Windows Azure Active Directory Module for Windows PowerShell prompt:
    
  ```
  Get-MSolUser | Sort UserPrincipalName | Select UserPrincipalName
  ```

    Record the account names here:
    
  - User 2 account name: user2@_______________________________________________.onmicrosoft.com
    
  - User 3 account name: user3@_______________________________________________.onmicrosoft.com
    
  - User 4 account name: user4@_______________________________________________.onmicrosoft.com
    
  - User 5 account name: user5@_______________________________________________.onmicrosoft.com
    
    Also record the passwords for these accounts in a secure location.
    
- To list the URLs for the Sales, Production, and Support team sites, run the following command from the SharePoint Online Management Shell prompt:
    
  ```
  Get-SPOSite | Where URL -like "*/sites/*" | Sort URL | Select URL
  ```

  - Production site URL: https://______________________________________________.sharepoint.com/sites/production
    
  - Sales site URL: https://______________________________________________.sharepoint.com/sites/sales
    
  - Support site URL: https://______________________________________________.sharepoint.com/sites/support
    
## Next steps

Use these additional articles in your Office 365 dev/test environment:
  
- [DirSync for your Office 365 dev/test environment](dirsync-for-your-office-365-dev-test-environment.md)
    
- [Multi-factor authentication for your Office 365 dev/test environment](multi-factor-authentication-for-your-office-365-dev-test-environment.md)
    
- [Federated identity for your Office 365 dev/test environment](federated-identity-for-your-office-365-dev-test-environment.md)
    
- [Cloud App Security for your Office 365 dev/test environment](cloud-app-security-for-your-office-365-dev-test-environment.md)
    
- [Advanced Threat Protection for your Office 365 dev/test environment](advanced-threat-protection-for-your-office-365-dev-test-environment.md)
    
- [Advanced eDiscovery for your Office 365 dev/test environment](advanced-ediscovery-for-your-office-365-dev-test-environment.md)
    
- [Sensitive file protection in the Office 365 dev/test environment](sensitive-file-protection-in-the-office-365-dev-test-environment.md)
    
- [Isolated SharePoint Online team site dev/test environment](isolated-sharepoint-online-team-site-dev-test-environment.md)
    
- [Data classification and labeling in the Office 365 dev/test environment](data-classification-and-labeling-in-the-office-365-dev-test-environment.md)
    
Extend your Office 365 dev/test environment to include additional Microsoft cloud offerings:
  
- [The Microsoft 365 Enterprise dev/test environment](the-microsoft-365-enterprise-dev-test-environment.md)
    
- [Office 365 and Dynamics 365 dev/test environment](office-365-and-dynamics-365-dev-test-environment.md)
    
## See Also

[Cloud adoption Test Lab Guides (TLGs)](cloud-adoption-test-lab-guides-tlgs.md)
  
[Office 365 and Dynamics 365 dev/test environment](office-365-and-dynamics-365-dev-test-environment.md)
  
[Cloud adoption and hybrid solutions](cloud-adoption-and-hybrid-solutions.md)

