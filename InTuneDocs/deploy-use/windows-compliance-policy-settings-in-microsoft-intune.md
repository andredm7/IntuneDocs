---
# required metadata

title: Compliance policy settings for Windows devices| Microsoft Docs
description: This topic describes the rules and settings you can configure for a compliance policy for Windows devices.
keywords:
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 12/15/2016
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: f996842c-e9a4-4819-acb4-ee66e8fb35b8

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chrisgre
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Compliance policy settings for Windows devices in Microsoft Intune

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

The policy settings described in this topic apply to devices running the Windows operating system. The following sections describe the supported Windows versions.

If you are looking for information about other platforms, select one of these:
> [!div class="op_single_selector"]
- [Compliance policy settings for iOS devices](ios-compliance-policy-settings-in-microsoft-intune.md)
- [Compliance policy settings for Android devices](android-compliance-policy-settings-in-microsoft-intune.md)
- [Compliance policy settings for Android for Work](afw-compliance-policy-settings-in-microsoft-intune.md)

## Compliance policy settings for Windows Phone devices
The settings listed in this section are supported on Windows Phone 8.1 and later.

### System security settings
#### Password
- **Require a password to unlock mobile devices**: Set this to **Yes** to require the user to enter a password before
  they can access their device.

- **Allow simple passwords**: Set this
   to **Yes** to let the user create a simple password
   like **1234** or **1111**.

-  **Minimum password length**: Specify the minimum number of digits or characters that
  the user’s password must have.
- **Required password type**: Specify whether the user must create
an **Alphanumeric** password or a **Numeric** password.

  For devices that run Windows and are accessed with a Microsoft account, the compliance policy will fail to evaluate correctly if the minimum password length is greater than eight characters or if the minimum number of character sets is more than two.

- **Minimum number of character sets**: If **Required password type** is set to
**Alphanumeric**, this setting specifies the minimum number of
character sets that the password must have. The four character sets are:
  -   Lowercase letters
  -   Uppercase letters
  -   Symbols
  -   Numbers

  Setting a higher number for this setting will require the user to create a password that is more complex. For devices that run Windows and are accessed with a Microsoft account, the compliance policy will fail to evaluate correctly if the minimum password length is greater than eight characters or if the minimum number of character sets is more than two.

- **Minutes of inactivity before password is required**: This setting specifies the idle time before the user must reenter their password.

- **Password expiration (days)**: Choose the number of days before the user’s password expires
  and they must create a new one.

- **Remember password history**: Use this setting in conjunction with **Prevent reuse of previous passwords** to restrict the user from
  creating previously used passwords.

- **Prevent reuse of previous passwords**: If **Remember password history** is selected, specify the
  number of previously used passwords that cannot be reused.
- **Require a password when the device returns from an idle state**: Use this setting together with the **Minutes of inactivity before password is required** setting. The user is prompted to enter a password to access a device that has been inactive for the time specified in the **Minutes of inactivity before password is required** setting.

  > [!NOTE]
  > This setting applies only to Windows 10 Mobile devices.

#### Encryption
- **Require encryption on mobile device**: Set this to **Yes** to require the device to be
  encrypted in order to connect to resources.

### Device health settings
- **Require devices to be reported as healthy**: You can set a rule to require that **Windows 10 Mobile** devices must be reported as healthy in new or existing compliance policies.  If this setting is enabled, Windows 10 devices are evaluated via the Health Attestation Service (HAS) for these data points:
  -  **BitLocker is enabled**: When BitLocker is on, the device can help protect data that is stored on the drive from unauthorized access, when the system is turned off or goes to hibernation. Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the TPM to help protect the Windows operating system and user data. BitLocker also helps ensure that a computer is not tampered with, even if it is left unattended, lost, or stolen. If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that help protect the data. As a result, the keys cannot be accessed until the TPM has verified the state of the computer.
  -  **Code integrity is enabled**: Code integrity is a feature that validates the integrity of a driver or system file each time it is loaded into memory. Code integrity detects whether an unsigned driver or system file is being loaded into the kernel. It also detects whether a system file has been modified by malicious software that is being run by a user account with administrator privileges.
  - **Secure Boot is enabled**: When Secure Boot is enabled, the system is forced to boot to a factory trusted state. Also, when Secure Boot is enabled, the core components used to boot the machine must have correct cryptographic signatures that are trusted by the organization that manufactured the device. The UEFI firmware verifies this before it lets the machine start. If any files have been tampered with, breaking their signature, the system will not boot.

  For information on how the HAS service works, see [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).
###  Device property settings
- **Minimum OS required**: When a device does not meet the minimum OS
    version requirement, it is reported as noncompliant.
    A link with information on how to upgrade is displayed. The user can choose to upgrade their device, and then they can access company resources.

- **Maximum OS version allowed**: When a device is using an
    OS version later than the one specified in the rule, access to company resources is blocked and the user is asked to contact their IT admin. Until there is a change in rule to allow the OS version, this device cannot be used to access company resources.


## Compliance policy settings for Windows PCs
The settings listed in this section are supported on Windows PCs.
### System security settings
#### Password
- **Minimum password length**: Supported on Windows 8.1.

  Specify the minimum number of digits or characters that the user’s password must have.

  For devices that are accessed with a Microsoft account, the compliance policy will fail to evaluate correctly if **Minimum password length** is greater than eight characters or if **Minimum number of character sets** is more than two characters.

- **Required password type**: Supported on Windows RT, Windows RT 8.1, and Windows 8.1.

  Specify whether the user must create an **Alphanumeric** password or a **Numeric** password.

- **Minimum number of character sets**: Supported on Windows RT, Windows RT 8.1, and Windows 8.1.

  If **Required password type** is set to **Alphanumeric**, this setting specifies the minimum number of character sets that the password must have. The four character sets are:
  -   Lowercase letters
  -   Uppercase letters
  -   Symbols
  -   Numbers     

  Setting a higher number for this setting will require the user to create a password that is more complex. For devices that are accessed with a Microsoft account, the compliance policy will fail to evaluate correctly if **Minimum password length** is greater than eight characters or if **Minimum number of character sets** is more than two characters.

- **Minutes of inactivity before password is required**: Supported on Windows RT, Windows RT 8.1, and Windows 8.1.

  Specify the idle time before the user must reenter their password.

- **Password expiration (days)**: Supported on Windows RT, Windows RT 8.1, and Windows 8.1.

  Choose the number of days before the user’s password expires and they must create a new one.

- **Remember password history**: Supported on Windows RT, Windows RT, and Windows 8.1.

  Use this setting in conjunction with **Prevent reuse of previous passwords** to restrict the user from creating previously used passwords.

- **Prevent reuse of previous passwords**: Supported on Windows RT, Windows RT 8.1, and Windows 8.1.

  If **Remember password history** is selected, specify the number of previously used passwords that cannot be reused.

### Device health settings
- **Require devices to be reported as healthy**: Supported on Windows 10 devices.
You can set a rule to require that Windows 10 devices must be reported as healthy in new or existing compliance policies. If this setting is enabled, Windows 10 devices are evaluated via the Health Attestation Service (HAS) for  these data points:
  -  **BitLocker is enabled**: When BitLocker is on, the device can help protect data that is stored on the drive from unauthorized access, when the system is turned off or goes to hibernation. Windows BitLocker Drive Encryption encrypts all data stored on the Windows operating system volume. BitLocker uses the TPM to help protect the Windows operating system and user data. BitLocker also helps ensure that a computer is not tampered with, even if it is left unattended, lost, or stolen. If the computer is equipped with a compatible TPM, BitLocker uses the TPM to lock the encryption keys that help protect the data. As a result, the keys cannot be accessed until the TPM has verified the state of the computer.
  -  **Code integrity is enabled**: Code integrity is a feature that validates the integrity of a driver or system file each time it is loaded into memory. Code integrity detects whether an unsigned driver or system file is being loaded into the kernel. It also detects whether a system file has been modified by malicious software that is being run by a user account with administrator privileges.
  - **Secure Boot is enabled**: When Secure Boot is enabled, the system is forced to boot to a factory trusted state. Also, when Secure Boot is enabled, the core components used to boot the machine must have correct cryptographic signatures that are trusted by the organization that manufactured the device. The UEFI firmware verifies this before it lets the machine start. If any files have been tampered with, breaking their signature, the system will not boot.
  - **Early-launch antimalware is enabled**: Early launch anti-malware (ELAM) provides protection for the computers in your network when they start up and before third-party drivers are initialized.

  For information on how the HAS service works, see [Health Attestation CSP](https://msdn.microsoft.com/library/dn934876.aspx).

### Device property settings
- **Minimum OS required**: Supported on Windows 8.1 and Windows 10.

  Specify the major.minor.build number here. The version number must correspond to the version that the **winver** command returns.

  When a device has a earlier version than the specified OS version, it is reported as noncompliant. A link with information on how to upgrade is displayed. The user can choose to upgrade their device, and then they can access company resources.

- **Maximum OS version allowed**: Supported on Windows 8.1 and Windows 10.

  When a device is using an OS version later than the one specified in the rule, access to company resources is blocked and the user is asked to contact their IT admin. Until there is a change in rule to allow the OS version, this device cannot be used to access company resources.

To find the OS version to use for the **Minimum OS required** and **Maximum OS version allowed** settings, run the **winver** command from the command prompt. The **winver** command returns the reported version of the OS.

- Windows 8.1 PCs return a version of **6.3**. If the OS version rule is set to Windows 8.1 for Windows, then the device is reported as noncompliant even if the device has Windows 8.1.

- For PCs running Windows 10, the version should be set as **10.0** plus the OS build number that the **winver** command returns. For example, it might be something like 10.0.10586.
> ![OS build version highlighted in the "About Windows" dialog box](./media/ca_win10-os-version.png)
