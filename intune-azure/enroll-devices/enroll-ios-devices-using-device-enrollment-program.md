---
# required metadata

title: Enroll iOS devices - Device Enrollment Program | Intune Azure preview | Microsoft Docs
description: "Intune Azure preview: Learn how to enroll corporate-owned iOS devices using the Device Enrollment Program."
keywords:
author: staciebarker
ms.author: stabar
manager: angrobe
ms.date: 02/03/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 7981a9c0-168e-4c54-9afd-ac51e895042c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: dagerrit
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Enroll iOS devices using Device Enrollment Program

[!INCLUDE[azure_preview](../includes/azure_preview.md)]

Microsoft Intune can deploy an enrollment profile that enrolls iOS devices that were bought through the Device Enrollment Program (DEP) “over the air.” A profile contains management settings that you want to apply to devices. The enrollment package can include Setup Assistant options for the device. Devices enrolled through DEP cannot be unenrolled by users.

>[!NOTE]
>This enrollment method can't be used with the [device enrollment manager](enroll-devices-using-device-enrollment-manager.md) method.

To manage corporate-owned iOS devices with Apple’s Device Enrollment Program (DEP), your organization must join Apple DEP and get devices through that program. Details of that process are available at:  [https://deploy.apple.com](https://deploy.apple.com). Advantages of the program include hands-free setup of devices without using a USB cable to connect each device to a computer.

Before you can enroll corporate-owned iOS devices with DEP, you need to [get a DEP token](get-apple-dep-token.md) from Apple. This token lets Intune sync information about DEP-participating devices that your corporation owns. It also permits Intune to perform Enrollment Profile uploads to Apple and to assign devices to those profiles.

Other methods of enrolling iOS devices are described in [Choose how to enroll iOS devices in Intune](choose-ios-enrollment-method.md).

## Prerequisites

Complete the following prerequisites before setting up iOS device enrollment:

- [Configure domains](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-2)
- [Set the MDM Authority](set-mdm-authority.md)
- [Create groups](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-5)
- Assign user licenses in the [Office 365 portal](http://go.microsoft.com/fwlink/p/?LinkId=698854)
- [Get an Apple MDM push certificate](get-an-apple-mdm-push-certificate.md)
- [Get an Apple DEP token](get-apple-dep-token.md)

## Create an Apple DEP profile for devices

A device enrollment profile defines the settings applied to a group of devices. The following steps show how to create a device enrollment profile for iOS devices enrolled by using DEP.

1. In the Azure portal, choose **More Services**, enter **Intune** in the text box, and then choose **Other** > **Intune**.

2. On the Intune blade, choose **Enroll devices**, and then choose **Apple Enrollment**.

3. Under **Manage Apple Device Enrollment Program (DEP) Settings**, select **DEP Profiles**.

4. On the **Apple DEP Profiles** blade, select **Create**.

5. On the **Create Enrollment Profile** blade, enter a name and description for the profile.

6. For **User Affinity** choose whether devices with this profile will enroll with or without user affinity.

 - **Enroll with user affinity** - The device must be affiliated with a user during initial setup and can then be permitted to access company data and email. Choose user affinity for DEP-managed devices that belong to users and that need to use the company portal for services like installing apps. Note that Multifactor authentication (MFA) doesn't work during enrollment on DEP devices with user affinity. After enrollment, MFA works as expected on these devices.

	>[!NOTE]
	>DEP with user affinity requires WS-Trust 1.3 Username/Mixed endpoint to be enabled to request user token.

 - **Enroll without user affinity** - The device is not affiliated with a user. Use this affiliation for devices that perform tasks without accessing local user data. Apps requiring user affiliation (including the Company Portal app used for installing line-of-business apps) won’t work.

7. Select **Device Management Settings**, configure the following profile settings, and then select **Save**:

	- **Supervised** - a management mode that enables more management options and disabled Activation Lock by default. If you leave the check box blank, you have limited management capabilities.

	- **Locked enrollment** - (Requires Management Mode = Supervised) Disables iOS settings that could allow removal of the management profile. If you leave the check box blank, it allows the management profile to be removed from the Settings menu. This item is set during activation and cannot be changed without a factory reset.

	- **Allow Pairing** - specifies whether iOS devices can sync with computers. If you choose **Allow Apple Configurator by certificate**, you must choose a certificate under **Apple Configurator Certificates**.

	- **Apple Configurator Certificates** - If you chose **Allow Apple Configurator by certificate** under **Allow Pairing**, select an Apple Configurator Certificate to import.

8. Select **Setup Assistant Settings**, configure the following profile settings, and then select **Save**:

	- **Department Name** - Appears when users tap **About Configuration** during activation.

	- **Department Phone** - Appears when the user clicks the Need Help button during activation.
    - **Setup Assistant Options** - These optional settings can be set up later in the iOS **Settings** menu.
        - **Passcode** - Prompt for passcode during activation. Always require a passcode unless the device will be secured or have access controlled in some other manner (that is, kiosk mode that restricts the device to one app).
        - **Location Services** - If enabled, Setup Assistant prompts for the service during activation
        - **Restore** - If enabled, Setup Assistant prompts for iCloud backup during activation
        - **Apple ID** - If enabled, iOS will prompt users for an Apple ID when Intune attempts to install an app without an ID. An Apple ID is required to download iOS App Store apps, including those installed by Intune.
        - **Terms and Conditions** - If enabled, Setup Assistant prompts users to accept Apple's terms and conditions during activation
        - **Touch ID** - If enabled, Setup Assistant prompts for this service during activation
        - **Apple Pay** - If enabled, Setup Assistant prompts for this service during activation
        - **Zoom** - If enabled, Setup Assistant prompts for this service during activation
        - **Siri** - If enabled, Setup Assistant prompts for this service during activation
        - **Diagnostic Data** - If enabled, Setup Assistant prompts for this service during activation

9. To save the profile settings, select **Create** on the **Create Enrollment Profile** blade.

## Assign Apple DEP serial numbers to your MDM server

1. Go to the [Device Enrollment Program Portal](https://deploy.apple.com) (https://deploy.apple.com) and sign in with your company Apple ID. 

2. Go to  **Deployment Program** &gt; **Device Enrollment Program** &gt; **Manage Devices**. 

3. Specify how you will **Choose Devices**, and then provide device information and specify details by device **Serial Number**, **Order Number**, or **Upload CSV File**. 

4. Choose **Assign to Server** and choose the &lt;ServerName&gt; specified for Microsoft Intune, and then choose **OK**.

## Synchronize DEP-managed devices

1. On the Intune blade of the Azure portal, choose **Enroll Devices**, and then choose **Apple Enrollment**.

2. Under **Manage Apple Device Enrollment Program (DEP) Settings**, select **DEP Serial Numbers**.

4. On the **Apple DEP Serial Numbers** blade, select **Sync**.

5. On the **Sync** blade, select **Request Sync**. The progress bar shows the amount of time you must wait before requesting Sync again.

    To comply with Apple’s terms for acceptable DEP traffic, Intune imposes the following restrictions:
     -	A full DEP sync can run no more than once every seven days. During a full sync, Intune refreshes every serial number that Apple has assigned to Intune whether the serial has previously been synced or not. If a full sync is attempted within seven days of the previous full sync, Intune only refreshes serial numbers that are not already listed in Intune.
     -	Any sync request is given 10 minutes to finish. During this time or until the request succeeds, the **Sync** button is disabled.

>[!NOTE]
>You can also assign DEP serial numbers to profiles from the **Apple DEP Serial Numbers** blade.

## Distribute devices to users

You can now distribute corporate-owned devices to users. When an iOS device is turned on, it will be enrolled for management by Intune.


## How users install and use the Company Portal on their devices

Devices that are configured with user affinity can install and run the Company Portal app to download apps and manage devices. After users receive their devices, they must complete the additional steps described below to complete the Setup Assistant and install the Company Portal app.

### How users enroll corporate-owned iOS devices with user affinity 

1. When users turn on their device, they are prompted to complete the Setup Assistant. During setup, users are prompted for their credentials. They must use the credentials (i.e., the unique personal name or UPN) that are associated with their subscription in Intune.

2. During setup, users are prompted for an Apple ID. They must provide an Apple ID to allow the device to install the Company Portal. They can also provide the ID from the iOS settings menu after setup is finished.

3. After completing setup, users must install the Company Portal app from the App Store.

4. Users now sign in to the Company Portal by using the UPN that they used when setting up the device.

5. After logging in, users are prompted to enroll their device. The first step is to identify their device. The app presents a list of iOS devices that have already been corporate enrolled and assigned to the user’s Intune account. They should choose the matching device. If this device is not already corporate enrolled, they should choose new device to continue with the standard enrollment flow.

6. On the next screen, users confirm the serial number of the new device. To do this, users select a link that appears. The link launches the Settings app, which then enables users to verify their serial number. Users must then enter the last four characters of the serial number into the Company Portal app.

   This step verifies that the device is the corporate device enrolled in Intune. If the serial number on the device does not match, the user selected the wrong device. The user must go back to the previous screen and select a different device.

7. After the serial number is verified, the Company Portal app redirects to the Company Portal website to finalize enrollment. Then the website prompts users to return to the app.

Enrollment is now complete, and users can now use this device with the full set of capabilities.
