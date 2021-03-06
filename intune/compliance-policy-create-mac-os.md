---
# required metadata

title: Create a macOS device compliance policy in Microsoft Intune
titleSuffix:
description: Create a Microsoft Intune device compliance policy for macOS devices so you can specify requirements that a device must meet to be compliant.
keywords:
author: msmimart
ms.author: mimart
manager: dougeby
ms.date: 02/22/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: muhosabe
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure

---

# Create a device compliance policy for macOS devices with Intune


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

An Intune device compliance policy for macOS specifies the rules and settings that macOS devices must meet to be considered compliant. You can use these policies with conditional access to allow or block access to company resources, and you can get device reports and take actions for non-compliance. You create device compliance policies for each platform in the Intune Azure portal.

## Before you begin

Before creating and assigning a device compliance policy, review the Intune device compliance policy concepts.

- To learn more about device compliance policies, see [get started with device compliance policies](device-compliance.md).

> [!IMPORTANT]
> You need to create device compliance policies for each platform. Intune device compliance policy settings depend on platform capabilities, which are settings exposed through the MDM protocol.

The following table describes how noncompliant settings are managed when a compliance policy is used with a conditional access policy:


| Policy setting | macOS 10.11 and later |
| --- | --- |
| **PIN or password configuration** | Remediated |   
| **Device encryption** | Remediated (by setting PIN) |
| **Email profile** | Quarantined |
|**Minimum OS version** | Quarantined |
| **Maximum OS version** | Quarantined |  


**Remediated** = The device operating system enforces compliance. (For example, the user is forced to set a PIN.)

**Quarantined** = The device operating system does not enforce compliance. (For example, Android devices do not force the user to encrypt the device.) When the device is not compliant, the following actions take place:

- The device is blocked if a conditional access policy applies to the user.
- The company portal notifies the user about any compliance problems.

## MacOS compliance policy settings

You have different categories with different settings to choose from when creating a new device compliance with Intune:

- Device Health

- Device Properties

- System Security

### Device Health

- **Require a system integrity protection** - Set to **Require** to check if your macOS devices have system integrity protection enabled.

### Device properties

- **Minimum OS version** - When a device does not meet the minimum OS version requirement, it is reported as noncompliant. A link with information on how to upgrade appears. The user can choose to upgrade their device. After that, they can access company resources.

- **Maximum OS version** - When a device is using an OS version later than the one specified in the rule, access to company resources is blocked and the user is asked to contact their IT admin. Until there is a change in rule to allow the OS version, this device cannot be used to access company resources.

### System security settings

#### Password

- **Require a password to unlock mobile devices** - Set to **Require** so users need to enter a password before they can access their device.

- **Simple passwords** - Set to **Block** so user can't create a simple password like **1234** or **1111**.

- **Minimum password length** - Specify the minimum number of digits or characters that the password must have.

- **Password type** - Specify whether the user must create an **Alphanumeric** password or a **Numeric** password.

- **Number of non-alphanumeric characters in password** - If you set **Required password type** to **Alphanumeric**, use this setting to specify the minimum number of character sets that the password must have. 

	> [!NOTE]
	> Setting a higher number requires the user to create a password that is more complex.

	> [!IMPORTANT]
	> For macOS devices, this setting refers to the number of special characters (for example, **!** , **#** , **&amp;** ) that must be included in the password.

- **Maximum minutes of inactivity before password is required** - Specify the idle time before the user must reenter their password.

- **Password expiration (days)** - Select the number of days (between 1 and 250) before the password expires and they must create a new one.

- **Number of previous passwords to prevent reuse** - Specify the number of previously used passwords that cannot be reused.

	> [!IMPORTANT]
	> When the password requirement is changed on a macOS device, it doesn’t take effect until the next time the user changes their password. For example, if you set the password length restriction to eight digits and the macOS device currently has a six digits password, the device remains compliant until the next time the user updates their password on the device.

## To create a device compliance policy

1. Go to the [Azure portal](https://portal.azure.com), and sign in with your Intune credentials.

2. After you've successfully signed in, you can see the **Azure Dashboard**.

3. Choose **All services** from the left menu, then type **Intune** in the text box filter.

4. Choose **Intune**, you can see the **Intune Dashboard**.

5. Choose **Device compliance**, then choose **Policies** under **Manage**.

6. Choose **Create policy**.

7. Type a name, description, and choose the platform that you want this policy to apply to.

8. The **Mac compliance policy** pane opens, choose the device compliance setting categories **System Security**, **Device Health**, and **Device Properties** to specify your settings.

10. Once you are done choosing your settings, choose **OK** under each device compliance setting category.

11. Choose **OK**, then choose **Create**.

## Assign user groups

To assign a compliance policy to users, choose a policy that you have configured. Existing policies can be found in the **Device compliance - Policies** pane.

1. Choose the device compliance policy you want to assign to users and choose **Assignments**. This opens the pane where you can select **Azure Active Directory security groups** and assign them to the policy.

2. Choose **Selected groups** to open the pane that displays the Azure AD security groups.

3. Choose **Save** to assign the device compliance policy to Azure AD security groups.

4. Once you're done assigning the device compliance policy to your groups, you can close the **Assignments** pane.

	> [!TIP]
	> By default, devices check for compliance every eight hours but users can force this process through the Intune company portal app.

## Next steps

[How to monitor device compliance policies](compliance-policy-monitor.md)
