---
title: 'Tutorial: Azure Active Directory single sign-on (SSO) integration with Paylocity | Microsoft Docs'
description: Learn how to configure single sign-on between Azure Active Directory and Paylocity.
services: active-directory
author: jeevansd
manager: CelesteDG
ms.reviewer: celested
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.topic: tutorial
ms.date: 11/21/2022
ms.author: jeedes
---

# Tutorial: Azure Active Directory single sign-on (SSO) integration with Paylocity

In this tutorial, you'll learn how to integrate Paylocity with Azure Active Directory (Azure AD). When you integrate Paylocity with Azure AD, you can:

* Control in Azure AD who has access to Paylocity.
* Enable your users to be automatically signed-in to Paylocity with their Azure AD accounts.
* Manage your accounts in one central location - the Azure portal.

## Prerequisites

To get started, you need the following items:

* An Azure AD subscription. If you don't have a subscription, you can get a [free account](https://azure.microsoft.com/free/).
* Paylocity single sign-on (SSO) enabled subscription.

## Scenario description

In this tutorial, you configure and test Azure AD SSO in a test environment.

* Paylocity supports **SP and IDP** initiated SSO

## Add Paylocity from the gallery

To configure the integration of Paylocity into Azure AD, you need to add Paylocity from the gallery to your list of managed SaaS apps.

1. Sign in to the Azure portal using either a work or school account, or a personal Microsoft account.
1. On the left navigation pane, select the **Azure Active Directory** service.
1. Navigate to **Enterprise Applications** and then select **All Applications**.
1. To add new application, select **New application**.
1. In the **Add from the gallery** section, type **Paylocity** in the search box.
1. Select **Paylocity** from results panel and then add the app. Wait a few seconds while the app is added to your tenant.

 Alternatively, you can also use the [Enterprise App Configuration Wizard](https://portal.office.com/AdminPortal/home?Q=Docs#/azureadappintegration). In this wizard, you can add an application to your tenant, add users/groups to the app, assign roles, as well as walk through the SSO configuration as well. [Learn more about Microsoft 365 wizards.](/microsoft-365/admin/misc/azure-ad-setup-guides)

## Configure and test Azure AD SSO for Paylocity

Configure and test Azure AD SSO with Paylocity using a test user called **B.Simon**. For SSO to work, you need to establish a link relationship between an Azure AD user and the related user in Paylocity.

To configure and test Azure AD SSO with Paylocity, perform the following steps:

1. **[Configure Azure AD SSO](#configure-azure-ad-sso)** - to enable your users to use this feature.
    * **[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with B.Simon.
    * **[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable B.Simon to use Azure AD single sign-on.
1. **[Configure Paylocity SSO](#configure-paylocity-sso)** - to configure the single sign-on settings on application side.
    * **[Create Paylocity test user](#create-paylocity-test-user)** - to have a counterpart of B.Simon in Paylocity that is linked to the Azure AD representation of user.
1. **[Test SSO](#test-sso)** - to verify whether the configuration works.

## Configure Azure AD SSO

Follow these steps to enable Azure AD SSO in the Azure portal.

1. In the Azure portal, on the **Paylocity** application integration page, find the **Manage** section and select **single sign-on**.
1. On the **Select a single sign-on method** page, select **SAML**.
1. On the **Set up single sign-on with SAML** page, click the pencil icon for **Basic SAML Configuration** to edit the settings.

   ![Edit Basic SAML Configuration](common/edit-urls.png)

1. On the **Basic SAML Configuration** section, the user does not have to perform any step as the app is already pre-integrated with Azure.

1. Click **Set additional URLs** and perform the following step if you wish to configure the application in **SP** initiated mode:

    In the **Sign-on URL** text box, type the URL:
    `https://access.paylocity.com/`

1. Click **Save**.

1. Paylocity application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration. The following screenshot shows the list of default attributes.

	![image](common/default-attributes.png)

1. In addition to above, Paylocity application expects few more attributes to be passed back in SAML response which are shown below. These attributes are also pre populated, but you have to update these attributes with the real values.

	| Name |  Source Attribute|
	| ---------------| --------------- |
	| PartnerID | `P8000010` |
	| PaylocityUser | `user.mail`|
	| PaylocityEntity | < `PaylocityEntity` > |

    > [!NOTE]
    > The PaylocityEntity is Paylocity Company ID.

1. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section,  find **Federation Metadata XML** and select **Download** to download the certificate and save it on your computer.

	![The Certificate download link](common/metadataxml.png)

1. On the **Set up single sign-on with SAML** page, in the **SAML Signing Certificate** section, click **Edit Icon**.

	![Screenshot that shows the "S A M L Signing Certificate" with the "Download" action for "Federation Metadata X M L" selected.](./media/paylocity-tutorial/edit-samlassertion.png)

1. Select **Signing Option** as **Sign SAML response and assertion** and click **Save**.

    ![The SAML Signing Certificate Edit](./media/paylocity-tutorial/saml-assertion.png)

1. On the **Set up Paylocity** section, copy the appropriate URL(s) based on your requirement.

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

In this section, you'll enable B.Simon to use Azure single sign-on by granting access to Paylocity.

1. In the Azure portal, select **Enterprise Applications**, and then select **All applications**.
1. In the applications list, select **Paylocity**.
1. In the app's overview page, find the **Manage** section and select **Users and groups**.
1. Select **Add user**, then select **Users and groups** in the **Add Assignment** dialog.
1. In the **Users and groups** dialog, select **B.Simon** from the Users list, then click the **Select** button at the bottom of the screen.
1. If you are expecting a role to be assigned to the users, you can select it from the **Select a role** dropdown. If no role has been set up for this app, you see "Default Access" role selected.
1. In the **Add Assignment** dialog, click the **Assign** button.

## Configure Paylocity SSO

To configure single sign-on on the **Paylocity** side,

1. Download the **Federation Metadata XML**.
1. In Paylocity, navigate to **HR & Payroll** > **User Access** > **SSO Configuration**.
1. Select **Add SSO Integration** under **SSO Integrations**. A new drawer opens.
1. Select **Microsoft Azure** as the SSO Provider from dropdown.
1. Select **Status** from dropdown.
1. Drag and drop metadata file in the drop area. Paylocity attempts to parse the Issuer, Post Redirect and Binding URLs and Security Certificate(s).
1. Select **Save** to confirm the changes. The integration should display under **SSO Integrations**.

### Create Paylocity test user

In this section, you create a user called B.Simon in Paylocity. Work with [Paylocity support team](mailto:service@paylocity.com) to add the users in the Paylocity platform. Users must be created and activated before you use single sign-on.

## Test SSO

In this section, you test your Azure AD single sign-on configuration with following options. 

#### SP initiated:

* Click on **Test this application** in Azure portal. This will redirect to Paylocity Sign on URL where you can initiate the login flow.  

* Go to Paylocity Sign-on URL directly and initiate the login flow from there.

#### IDP initiated:

* Click on **Test this application** in Azure portal and you should be automatically signed in to the Paylocity for which you set up the SSO. 

You can also use Microsoft My Apps to test the application in any mode. When you click the Paylocity tile in the My Apps, if configured in SP mode you would be redirected to the application sign on page for initiating the login flow and if configured in IDP mode, you should be automatically signed in to the Paylocity for which you set up the SSO. For more information about the My Apps, see [Introduction to the My Apps](https://support.microsoft.com/account-billing/sign-in-and-start-apps-from-the-my-apps-portal-2f3b1bae-0e5a-4a86-a33e-876fbd2a4510).

## Next steps

Once you configure Paylocity you can enforce session control, which protects exfiltration and infiltration of your organization’s sensitive data in real time. Session control extends from Conditional Access. [Learn how to enforce session control with Microsoft Defender for Cloud Apps](/cloud-app-security/proxy-deployment-any-app).
