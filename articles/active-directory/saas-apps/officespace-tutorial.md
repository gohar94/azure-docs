---
title: 'Tutorial: Azure Active Directory single sign-on (SSO) integration with OfficeSpace Software | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and OfficeSpace Software.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 05/14/2021
ms.author: jeedes
---

# Tutorial: Azure Active Directory single sign-on (SSO) integration with OfficeSpace Software

In this tutorial, you'll learn how to integrate OfficeSpace Software with Azure Active Directory (Azure AD). When you integrate OfficeSpace Software with Azure AD, you can:

* Control in Azure AD who has access to OfficeSpace Software.
* Enable your users to be automatically signed-in to OfficeSpace Software with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.

## Prerequisites

To get started, you need the following items:

* An Azure AD subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/free/).
* OfficeSpace Software single sign-on (SSO) enabled subscription.

## Scenario description

In this tutorial, you configure and test Azure AD SSO in a test environment.

* OfficeSpace Software supports **SP** initiated SSO.
* OfficeSpace Software supports [**automated user provisioning and deprovisioning**](officespace-software-provisioning-tutorial.md) (recommended).
* OfficeSpace Software supports **Just In Time** user provisioning.

## Add OfficeSpace Software from the gallery

To configure the integration of OfficeSpace Software into Azure AD, you need to add OfficeSpace Software from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **OfficeSpace Software** in the search box.
1. Select **OfficeSpace Software** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

## Configure and test Azure AD SSO for OfficeSpace Software

Configure and test Azure AD SSO with OfficeSpace Software using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user in OfficeSpace Software.

To configure and test Azure AD SSO with OfficeSpace Software, perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    1. **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    1. **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
1. **[Configure OfficeSpace Software SSO](#configure-officespace-software-sso)** - to configure the single sign-on settings on application side.
    1. **[Create OfficeSpace Software test user](#create-officespace-software-test-user)** - to have a counterpart of B.Simon in OfficeSpace Software that is linked to the Azure AD representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **OfficeSpace Software** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Edit Basic SAML Configuration](common/edit-urls.png)

1. On the **Basic SAML Configuration** section, perform the following steps:

	a. In the **Sign on URL** text box, type a URL using the following pattern:
    `https://<company name>.officespacesoftware.com/users/sign_in/saml`

    b. In the **Identifier (Entity ID)** text box, type a URL using the following pattern:
    `<company name>.officespacesoftware.com`

	> [!NOTE]
	> These values are not real. Update these values with the actual Sign on URL and Identifier. Contact [OfficeSpace Software Client support team](mailto:support@officespacesoftware.com) to get these values. You can also refer to the patterns shown in the **Basic SAML Configuration** section in the Azure portal.

1. OfficeSpace Software application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes, where as **nameidentifier** is mapped with **user.userprincipalname**. OfficeSpace Software application expects **nameidentifier** to be mapped with **user.mail**, so you need to edit the attribute mapping by clicking on **Edit** icon and change the attribute mapping.

	![image](common/edit-attribute.png)

1. In addition to above, OfficeSpace Software application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated but you can review them as per your requirement.

	| Name | Source Attribute|
	| ---------------| --------------- |
	| email | user.mail |
	| name | user.displayname |
	| first_name | user.givenname |
	| last_name | user.surname |

1. In the **SAML Signing Certificate** section, click **Edit** button to open **SAML Signing Certificate** dialog.

	![Edit SAML Signing Certificate](common/edit-certificate.png)

1. In the **SAML Signing Certificate** section, copy the **Thumbprint Value** and save it on your computer.

    ![Copy Thumbprint value](common/copy-thumbprint.png)

1. On the **Set up OfficeSpace Software** section, copy the appropriate URL(s) based on your requirement.

	![Copy configuration URLs](common/copy-configuration-urls.png)

### Create an Azure AD test user

In this section, you'll create a test user in the Azure portal called B.Simon.

1. From the left pane in the Azure portal, select **Azure Active Directory**, select **Users**, and then select **All users**.
1. Select **New user** at the top of the screen.
1. In the **User** properties, follow these steps:
   1. In the **Name** field, enter `B.Simon`.  
   1. In the **User name** field, enter the username@companydomain.extension. For example, `B.Simon@contoso.com`.
   1. Select the **Show password** check box, and then write down the value that's displayed in the **Password** box.
   1. Click **Create**.

### Assign the Azure AD test user

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to OfficeSpace Software.

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
1. In the applications list, select **OfficeSpace Software**.
1. In the app's overview page, find the **Manage** section and select **Users and groups**.
1. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
1. If you are expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
1. In the **Add Assignment** dialog, click the **Assign** button.

## Configure OfficeSpace Software SSO

1. In a different web browser window, sign in to your OfficeSpace Software tenant as an administrator.

2. Go to **Settings** and click **Connectors**.

	![Screenshot that shows the "Settings" drop-down with "Connectors" selected.](./media/officespace-tutorial/settings.png)

3. Click **SAML Authentication**.

	![Screenshot that shows the "Authentication" section with the "S A M L Authentication" action selected.](./media/officespace-tutorial/authentication.png)

4. In the **SAML Authentication** section, perform the following steps:

	![Configure Single Sign-On On App Side](./media/officespace-tutorial/configuration.png)

	a. In the **Logout provider url** textbox, paste the value of **Logout URL** which you have copied from Azure portal.

	b. In the **Client idp target url** textbox, paste the value of **Login URL** which you have copied from Azure portal.

	c. Paste the **Thumbprint** value which you have copied from Azure portal, into the **Client IDP certificate fingerprint** textbox. 

	d. Click **Save Settings**.

### Create OfficeSpace Software test user

In this section, a user called B.Simon is created in OfficeSpace Software. OfficeSpace Software supports just-in-time user provisioning, which is enabled by default. There is no action item for you in this section. If a user doesn't already exist in OfficeSpace Software, a new one is created after authentication.

> [!NOTE]
> If you need to create an user manually, you need to Contact [OfficeSpace Software support team](mailto:support@officespacesoftware.com).

## Test SSO 

In this section, you test your Azure AD single sign-on configuration with following options. 

* Click on **Test this application** in Azure portal. This will redirect to OfficeSpace Software Sign-on URL where you can initiate the login flow. 

* Go to OfficeSpace Software Sign-on URL directly and initiate the login flow from there.

* You can use Microsoft My Apps. When you click the OfficeSpace Software tile in the My Apps, this will redirect to OfficeSpace Software Sign-on URL. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Next steps

Once you configure OfficeSpace Software you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Cloud App Security](/cloud-app-security/proxy-deployment-aad).