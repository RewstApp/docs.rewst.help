# Microsoft Cloud Integration Bundle

{% hint style="warning" %}
Rewst's previous setup for Microsoft was separate integrations for each Microsoft app. If you are an older Rewst customer and have not yet migrated from our individual integration to bundle configuration, please see the below section for how to [Migrate to the Microsoft Cloud Integration Bundle.](./#migrate-legacy-microsoft-integrations-to-the-new-microsoft-cloud-integration-bundle)&#x20;
{% endhint %}

## What is the Microsoft Cloud Integration Bundle?

The Microsoft Cloud Integration Bundle is Rewst’s solution for integrating your most common Microsoft tools. It’s a little different from our other integrations in that we group multiple integrations together, by brand, to allow for easier and more custom integration options during setup.

{% hint style="info" %}
Though you’ll be working from one integration menu tile to set up all integrations, each integration will appear as its own section with its own actions in the actions list of the workflow builder.

For detailed permission breakdown for all Microsoft integrations in the bundle, see our separate documentation [here](microsoft-cloud-permissions.md).&#x20;
{% endhint %}

## Why use the Microsoft Cloud Integration Bundle?

* Customize permissions tailored to your organization’s needs.
* Centralize the management of all Microsoft integrations through the Rewst platform.
* Protect your data with enhanced security measures.
* Keep your integrations current with continuous updates and enhancements.

## **What integrations are in the Microsoft Cloud Integration Bundle?**

You'll be prompted to check off any or all of the following integrations to be included in your setup process. The Microsoft Cloud Integration Bundle contains integrations for:

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-06-24 at 3.36.15 PM (1).png" alt="&#x22;Microsoft Cloud Integration Bundle” setup interface. At the top, icons represent Rewst, a link, and Microsoft Cloud. A progress bar shows four steps: 1) Select Integrations, 2) Configuration Parameters, 3) Tenant Permissions, and 4) Authorize Integrations, with step 1 highlighted. The main section lists integration options with checkboxes: Microsoft Graph (checked, required), Microsoft Exchange Online, Microsoft CSP, and Microsoft Azure. Each option includes its logo and a description of what the integration enables. At the bottom right, there is a turquoise “Next” button. The interface has a dark background with white text."><figcaption><p>The <strong>Select Integrations</strong> screen of the Microsoft Cloud Integration Bundle's configuration process</p></figcaption></figure>

1. **Microsoft Graph:** A unified API that provides a single endpoint for accessing and managing data and intelligence across Microsoft 365, Windows, and Enterprise Mobility and Security.\
   :point\_right: You should check this box to install the integration to allow Rewst to make API calls. This is necessary for the bundle to work.
2. **Microsoft Exchange Online:** The cloud-hosted version of the traditional Microsoft Exchange Server, offering similar functionalities but without the need for on-premises server infrastructure.\
   :point\_right: You should check this box to install the integration to allow you to send Exchange Online PowerShell commands.
3. **Microsoft Cloud Solution Provider (CSP)**: This allows for the resale of Microsoft cloud services like Azure, Microsoft 365, and Dynamics 365 to businesses, often with added value services. It's a subscription-based model where MSPs can bill customers.\
   :point\_right: You should check this box if you use the Microsoft Partner Center and want to run Rewst actions against your customer tenants.
4. **Microsoft Azure**: A cloud computing platform, Azure offers a range of cloud infrastructure services, including computing, analytics, storage, networking, and AI. Note that Microsoft formerly called a different tool Azure, and renamed that tool Microsoft Entra.\
   :point\_right: You should check this box to install the integration if you are already an Azure user and have an existing [Azure key vault ](https://learn.microsoft.com/en-us/azure/key-vault/general/basic-concepts)set up with Microsoft. If you don't have a key vault, you'll need to create an empty one to complete bundle setup, then check this box. Instructions for how to do this can be found [here](https://learn.microsoft.com/en-us/azure/key-vault/secrets/quick-create-portal).

## Set up the Microsoft Cloud Integration Bundle

{% hint style="info" %}
We've broken down instructions into three  larger steps, each with its own section. Read through the entire process before starting step 1 to familiarize yourself with what will be needed.

Click each expander to open and view that substep's instructions and information.
{% endhint %}

### Step 1: Create a Microsoft service account in Microsoft Entra

{% hint style="info" %}
To set up Rewst integration, you'll need a new service account that has Global Admin settings. Once the integration has been completed, this can be removed. If you need to uninstall and re-integrate the integration, however, and you've removed the Global Admin settings, you'll need to recreate this before reintegrating.
{% endhint %}

<details>

<summary>Create a user in Microsoft Entra to use as your Rewst service account.</summary>



1. Navigate to **Overview > +Add > User > Create new user** in Microsoft Entra.

<figure><img src="../../../../.gitbook/assets/image (209).png" alt=""><figcaption></figcaption></figure>

2. Name the user `Rewst`.
3. Check the box **derive from user principal name**.
4. Enter a display name of `Rewst Service Account`.
5. Auto generate a password.&#x20;
6. Document all the user's information within your documentation platform. Be sure to note the user principal name.\
   \
   ![](<../../../../.gitbook/assets/image (210).png>)
7. Click the **Properties** tab. Leave all the options on this screen as default.
8. Click **Assignments > Add Role**.
9. Search for **`Global Administrator`** in the role selection. Select the role.
10. Click **Select**. Verify that the role is now listed in the main pane.<br>

<figure><img src="../../../../.gitbook/assets/image (211).png" alt=""><figcaption></figcaption></figure>

11. Make sure the service account is part of the **admin agents** group in Microsoft Entra.\
    <br>

<figure><img src="../../../../.gitbook/assets/image (73) (1).png" alt=""><figcaption><p>The group selection list</p></figcaption></figure>



<figure><img src="../../../../.gitbook/assets/image (74) (1).png" alt=""><figcaption><p>How the group will appear in the <strong>Assignments</strong> list if you have this properly enabled</p></figcaption></figure>

12. Click **Review + Create**, then **Create**.

</details>

<details>

<summary>Turn on MFA requirement for the user</summary>



1. Log in to the Microsoft 365 Admin Center.
2. Navigate to **Users > Active Users > Multifactor Authentication**.
3. Locate and select your Rewst service account user in the list that appears.
4. Click **Enable** under the **Quick Steps** menu.
5. Select the Rewst service account user again.
6. Click **Enforce** under the **Quick Steps** menu.&#x20;
7. Click **Enforce multi-factor**.

{% hint style="warning" %}
Only Microsoft authentication is permissible. Providers like Duo are incompatible. For more information, see Microsoft's page on [Supported MFA options](https://learn.microsoft.com/en-us/partner-center/partner-security-requirements-mandating-mfa#supported-mfa-options).
{% endhint %}

</details>

<details>

<summary>Modify conditional access policy in Microsoft Azure</summary>

#### Set up your MSP's policies

{% hint style="info" %}
This step is unnecessary if the tenant is under Microsoft default security settings. If you have no conditional access policies and are operating under security defaults, which already require MFA, skip to the next section.
{% endhint %}

1. Navigate to the [Conditional Access Policies](https://portal.azure.com/#view/Microsoft_AAD_ConditionalAccess/ConditionalAccessBlade/~/Policies) blade in Azure.
2. Remove the Rewst service account from any existing policies which may have been inherited at the time of its creation. If there are no existing policies, move on to the next step.
3. Create a New Policy.
   * **Include Rewst User**: Add the Rewst user to the policy
   * **Enforce MFA**: Mandate Azure Multi-factor Authentication for each login and application if you have not done so already
   * **Policy Name**: Save this policy under the name `Rewst Conditional Access Policy`

#### Set up your Client's policies

Granular access is influenced by your clients' [conditional access policies](https://learn.microsoft.com/en-us/entra/identity/conditional-access/overview). To ensure seamless access to your clients using your Rewst integration user, follow these steps

1. Navigate to your client's [Conditional Access Policies](https://portal.azure.com/#view/Microsoft_AAD_ConditionalAccess/ConditionalAccessBlade/~/Policies) blade in Azure.
2. &#x20;For each policy listed, add an exclusion to **Users and Groups** with these settings:
   * Guest or external users
   * Service Provider Users
   * **Tenant ID**: Enter your tenant ID. If unknown, find it at [What Is My Tenant ID](https://whatismytenantid.com/).

{% hint style="info" %}
**Note**: Excluding the MSP from the Conditional Access Policy is recommended as per [Microsoft's GDAP Documentation](https://learn.microsoft.com/en-us/partner-center/gdap-faq#what-is-the-recommended-next-step-if-the-conditional-access-policy-set-by-the-customer-blocks-all-external-access-including-csps-access-aobo-to-the-customers-tenant).

**Post-modification behavior**

* **Propagation time**: Changes may take up to an hour to become active in the Rewst environment.
* **Quick refresh**: Click the blue shield icon next to the client's name on the Microsoft Cloud Integration Bundle page in Rewst to expedite propagation.
{% endhint %}



</details>

### Step 2: Register the enterprise app and authorize the Rewst integration

<details>

<summary>Register the enterprise app</summary>

1.  Choose how to register the app.



    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-06-18 at 3.16.36 PM.png" alt=""><figcaption></figcaption></figure>

    1. Most users should select the Rewst-created enterprise app. It simplifies setup, includes the required permissions, and is secure. Unless you’re absolutely sure you need your own, choose the default option.
    2. If you are absolutely certain that you must bring your own app rather than using the Rewst-created one, choose this registration option. Owned app registration instructions can be found here: [https://docs.rewst.help/documentation/configuration/integrations/integration-guides/microsoft-cloud-integration-bundle/owned-app-registration](https://docs.rewst.help/documentation/configuration/integrations/integration-guides/microsoft-cloud-integration-bundle/owned-app-registration)
    3. Click **Next**.
2.  Set permissions for Microsoft Graph.



    <figure><img src="../../../../.gitbook/assets/Screenshot 2026-03-19 at 3.41.50 PM.png" alt=""><figcaption></figcaption></figure>

    1. You can pick and choose from a set of recommended pre-selected Graph permissions, or edit based on your org’s security preferences.
    2. These permissions are carefully chosen to support Crates without authentication issues. If you modify permissions from the stock ones suggested by Rewst, it’s your responsibility to verify that your custom permissions don’t interfere with Rewst’s functionality.
    3. If you deselect one of the recommended permissions, and doing so would break functionality for the integration or Crates in Rewst, you'll receive an error message. Until you re-select the permission, you'll be blocked from proceeding with setup.
    4. Note that Microsoft has an 8000 character limit for its permission granting communication. If you experience an error message about this limit, deselect some of the unnecessary permissions from your list of choices and try again.\
       ![](<../../../../.gitbook/assets/Screenshot 2026-03-19 at 3.45.22 PM.png>)
    5. For more detail, consult Microsoft Graph’s [official permissions documentation](https://learn.microsoft.com/en-us/graph/permissions-reference).
    6. Microsoft can take up to 48 hours for all scopes to appear in the Rewst integration. If scopes are not appearing for you, pause integration setup, and return later to allow time for Microsoft to update.
3. Grant additional access for other Microsoft integrations. Exchange, CSP, and Azure, if needed, are simpler and allow you to toggle access as desired.
4. Click **Next**.

</details>

<details>

<summary>Authorize Rewst</summary>

1. Review your configuration decisions in the **Authorize Integrations** screen. Click **Back** if you wish to make updates. Click **Authorize** when satisfied with your choices.

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-08-12 at 4.12.50 PM.png" alt=""><figcaption></figcaption></figure>

2. After authorizing, you’ll see:
   1. What authorized successfully
   2. Which user was used
   3. The tenant ID
   4. A corresponding Enterprise App created in Entra

</details>

### Step 3: Link your customers to Rewst child organizations

{% hint style="info" %}
This section covers the different ways you can set up your child organizations. Please read through the entire section before beginning, to determine which of the situational steps are right for you.  How you complete this step will depend on the way you choose to use Rewst: If you're unsure of which of these situations apply to you, contact Rewst Support for assistance.\
\
If you are part of the Microsoft Cloud Solution Provider (CSP) program and have access to GDAP, follow the instructions below to configure GDAP before linking customers.
{% endhint %}

#### What is GDAP and why is it important to the setup process?

In 2024, Microsoft moved away from regular user-based access, where users logged into Microsoft Entra with an individually permissioned account. Instead, they now operate via delegated admin permissions, where permissions are assigned from the top level down, for more secure access management. This is known as _Granulated Delegated Admin Permissions_, or _GDAP_.

As part of the bundle setup process, you were asked to create a dedicated user to act as your Microsoft service account. The way this is done and the roles you adopt are important, as GDAP dictates that this will now have a direct effect on how Rewst interacts with Microsoft.

For example, let’s say that 12 roles map to 177 permissions.

* Rewst will try to make an API call.
* The enterprise app will look for permissions.
* The enterprise app will ask if it is making the call at customer level, and if there are roles at the customer level.

#### Click to expand instructions and choose your situation from these three methods&#x20;

<details>

<summary>Link customers using GDAP - CSP Partners: Rewst-recommended option for setting up GDAP</summary>

{% hint style="info" %}
If you are part of the Microsoft Cloud Solution Provider (CSP) program and have access to GDAP, follow the instructions below to configure GDAP before linking customers.
{% endhint %}

1. Unpack the [Rewst Microsoft GDAP Assistant Crate](../../../crates/existing-crate-documentation/rewst-microsoft-gdap-assistant-crate.md). This will create the relationship and generate a link for your customer to accept the relationship. Once the customer manually accepts, you'll be given a second link to kick off another workflow that adds all groups to the relationship, and maps them to the relevant roles.\
   \
   ![](<../../../../.gitbook/assets/image (331).png>)<br>
2. Return to your Rewst platform. Navigate to **Marketplace > Integrations > Microsoft Cloud Bundle**.
3. Use the **organization mapping** menu that appears at the bottom of the screen to choose the customer organizations you wish to map the bundle to.&#x20;

<figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-11 at 12.21.58 PM.png" alt=""><figcaption></figcaption></figure>

3. Click **consent** next to your organization to consent for just that customer. Alternatively, click <img src="../../../../.gitbook/assets/Screenshot 2025-12-11 at 12.23.48 PM.png" alt="" data-size="line"> to consent to delegated admin permissions for all linked customers. If you haven't completed GDAP set up for all customers, this button will fail on the uncompleted customers.
4. Check for each of your organizations to ensure that the consent process was successful.&#x20;
   1. A green shield to the right of the integration name means the GDAP relationship is working and API access is valid.
   2. A blue shield or error means setup failed, and permissions are missing or incorrectly configured.



</details>

<details>

<summary>Link customers using GDAP without using the Rewst Microsoft GDAP Assistant Crate</summary>

Follow these instructions to set up GDAP relationships without the Rewst Microsoft GDAP Assistant Crate. Note that Rewst recommends using the Crate if possible, for a better setup experience.

#### Assign the security group to the service account user you created previously&#x20;

1. Navigate to **Manage > Groups**. Click **+New Group**.
   1. Choose **security group** as the group type.&#x20;
   2. Name the group `Rewst GDAP-[ROLE NAME]`.
   3. Enter `for SCP GDAP role assignment` as the description.
   4. Choose **Yes** for **Microsoft Entra roles can be assigned to the group**.
   5. Add the Rewst user you created in the previous steps as a member of the group.
   6. Click **Create**.
   7. Click **Yes** in the dialog that appears.
2. You will need to complete step 1 a total of 12 times, to create 12 security groups, each named differently to indicate the role it is associated with. For example, `Rewst GDAP-[NEXT ROLE NAME]`, etc.
3. Wait for the status to change to **Active**. Note that this can take anywhere from a few minutes to 24 hours depending on Microsoft's response time.&#x20;

#### Assign recommended roles for GDAP

1. Navigate to [partner.microsoft.com](http://partner.microsoft.com) and sign in.
2. Click **Partner Center > Customers > Customer List**.\
   ![](<../../../../.gitbook/assets/image (212).png>)
3. Click on the name of the customer you would like to create the admin relationship for once the customer list loads.\
   ![](<../../../../.gitbook/assets/image (213).png>)
4. Click **Admin Relationships > Request a New Relationship**.
5. Name the relationship, keeping in mind that this name must be unique for each customer or relationship. We suggest the `customer's initials`, followed by `GDAP`. For example, `ABC-GDAP.`
6. Enter the maximum duration of `730` days in the **Duration in Days** field.
7. Click **Select Microsoft Entra roles**.\
   ![](<../../../../.gitbook/assets/image (214).png>)
8. Add the 12 roles explained in this list by checking off the boxes. Note that the total list of roles is not alphabetized. Use control + F or command + F to search for your relevant roles.
   1. [**Application Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#application-administrator) **-** Can create and manage all applications, service principals, app registration, enterprise apps, consent requests. Cannot manage directory roles, security groups.
   2. [**Authentication Policy Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#authentication-policy-administrator) **-** Configures authentication methods policy, MFA settings, manages Password Protection settings, creates/manages verifiable credentials, Azure support tickets. Restrictions on updating sensitive properties, deleting/restoring users, legacy MFA settings.
   3. [**Cloud App Security Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-app-security-administrator) **-** Manages all aspects of the Defender for Cloud App Security in Azure AD, including policies, alerts, and related configurations.
   4. [**Cloud Device Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-device-administrator) **-** Enables, disables, deletes devices in Azure AD, reads Windows 10 BitLocker keys. Does not grant permissions to manage other properties on the device.
   5. [**Exchange Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#exchange-administrator) **-** Manages all aspects of Exchange Online, including mailboxes, permissions, connectivity, and related settings. Limited access to related Exchange settings in Azure AD.
   6. [**Intune Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#intune-administrator) **-** Manages all aspects of Intune, including all related resources, policies, configurations, and tasks.
   7. [**User Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#user-administrator) **-** Manages all aspects of users, groups, registration, and resets passwords for limited admins. Cannot manage security-related policies or other configuration objects.
   8. [**Privileged Authentication Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-authentication-administrator) **-** Sets and resets authentication methods for all users (admin or non-admin), deletes/restores any users. Manages support tickets in Azure and Microsoft 365. Restrictions on managing per-user MFA in legacy MFA portal.
   9. [**Privileged Role Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-role-administrator) **-** Manages role assignments in Azure AD, Azure AD Privileged Identity Management, creates/manages groups, manages all aspects of Privileged Identity Management, administrative units. Allows managing assignments for all Azure AD roles including Global Administrator.
   10. [**Security Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#security-administrator) **-** Can read security information and reports, and manages security-related features, including identity protection, security policies, device management, and threat management in Azure AD and Office 365.
   11. [**SharePoint Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#sharepoint-administrator) **-** Manages all aspects of SharePoint Online, Microsoft 365 groups, support tickets, service health. Scoped permissions for Microsoft Intune, SharePoint, and OneDrive resources.
   12. [**Teams Administrator**](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#teams-administrator) **-** Manages all aspects of Microsoft Teams, including telephony, messaging, meetings, teams, Microsoft 365 groups, support tickets, and service health.
9. Click **Save**.
10. Review your selection and click **Finalize Request**. \
    ![](<../../../../.gitbook/assets/image (216).png>)
11. You'll be redirected to a page that shows the request. Copy the link in that page.&#x20;
12. Email the link to your customer. They will need to accept the request to continue your bundle set up steps. Once approved, the relationship will show as **Active** in the **Admin Relationships** list. \
    You may also approve on the customer's behalf since you have Global Administrative privileges. To do this, choose to send the email to yourself. Note that if you choose this option, it will still send an email to your customer. You may want to notify them that they can disregard the email.
13. Add the 12 Security Groups created to the relationship. This can only be done after the request is accepted.
14. Return to your Rewst platform. Navigate to **Configuration > Integrations > Microsoft Cloud Bundle**.
15. Use the **organization mapping** menu that appears at the bottom of the screen to choose the customer organizations you wish to map the bundle to.&#x20;
16. Click **consent** next to your organization to consent for just that customer. Alternatively, click <img src="../../../../.gitbook/assets/Screenshot 2025-12-11 at 12.23.48 PM.png" alt="" data-size="line"> to consent to delegated admin permissions for all linked customers. If you haven't completed GDAP set up for all customers, this button will fail on the uncompleted customers.
17. Check for each of your organizations to ensure that the consent process was successful.&#x20;

    1. A green shield to the right of the integration name means the GDAP relationship is working and API access is valid.
    2. A blue shield or error means setup failed, and permissions are missing or incorrectly configured.

    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-12-11 at 12.21.58 PM.png" alt=""><figcaption></figcaption></figure>





</details>

<details>

<summary>Link customers using an enterprise application - you do not have a CSP or do not wish to use GDAP</summary>

{% hint style="warning" %}
Follow these instructions to link customers if you don't have a CSP or want to use a Global Admin account instead of GDAP. Please note that this should be a Global Admin account in your customer's Microsoft 365 tenant. This not the service account created in step 1 of this integration setup process, used for linking up to Rewst. If you would like to create a new service account for your customer, you can follow the process in step 1 in your customer's Microsoft 365 account.
{% endhint %}

1. Return to your Rewst platform.
2. Use the drop-down organization selector at the top left of your screen to choose your relevant child organization for your customer.
3. Complete the authorization process as prompted on the screen.
   1. Check off all boxes in the **Select Integrations** screen. If you don't use a CSP, you can uncheck this box, and check all other boxes as desired.
   2. Choose **Rewst Microsoft Cloud Connector**.\
      \
      ![](<../../../../.gitbook/assets/Screenshot 2025-09-05 at 12.19.46 PM.png>)
   3. &#x20;Click **Next**.
   4. Choose your tenant permissions. Click the **Microsoft Graph Permissions** accordion menu to expand and view the total permission list. Unless you have specific, verified reasons for unchecking any of these boxes, we recommend leaving our stock settings checked.
   5. Click **Next**.
   6.  Double check your choices and click **Authorize**.\
       <br>

       <figure><img src="../../../../.gitbook/assets/Screenshot 2025-09-05 at 12.20.33 PM.png" alt=""><figcaption></figcaption></figure>
   7.  Once Rewst has received the successful authorization callback from Microsoft, a background process will be initiated to authorize each of the integrations you installed for the bundle. Once that is complete, the permissions that you previously selected will be assigned to the Enterprise App installed in your tenant for the Rewst MS Cloud Connector.

       This process may take a few moments to complete. Don't navigate away from this page until the process is finished.
4. Repeat these delegated admin permission consent steps for each customer organization you where wish to set up the Microsoft Cloud integration bundle.
5.  Check for each of your organizations to ensure that the consent process was successful.&#x20;

    1. A green shield to the right of the integration name means the GDAP relationship is working and API access is valid.
    2. A blue shield or error means setup failed, and permissions are missing or incorrectly configured.



    <figure><img src="../../../../.gitbook/assets/Screenshot 2025-09-05 at 12.22.37 PM.png" alt=""><figcaption></figcaption></figure>



{% hint style="success" %}
#### Once you have completed the integration under your child organization, you can remove the Global Admin permission and add these 12 roles the Rewst Service account you have created for your customer.&#x20;
{% endhint %}

1. [Application Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#application-administrator) - Can create and manage all applications, service principals, app registration, enterprise apps, consent requests. Cannot manage directory roles, security groups.
2. [Authentication Policy Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#authentication-policy-administrator) - Configures authentication methods policy, MFA settings, manages Password Protection settings, creates/manages verifiable credentials, Azure support tickets. Restrictions on updating sensitive properties, deleting/restoring users, legacy MFA settings.
3. [Cloud App Security Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-app-security-administrator) - Manages all aspects of the Defender for Cloud App Security in Azure AD, including policies, alerts, and related configurations.
4. [Cloud Device Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-device-administrator) - Enables, disables, deletes devices in Azure AD, reads Windows 10 BitLocker keys. Does not grant permissions to manage other properties on the device.
5. [Exchange Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#exchange-administrator) - Manages all aspects of Exchange Online, including mailboxes, permissions, connectivity, and related settings. Limited access to related Exchange settings in Azure AD.
6. [Intune Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#intune-administrator) - Manages all aspects of Intune, including all related resources, policies, configurations, and tasks.
7. [User Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#user-administrator) - Manages all aspects of users, groups, registration, and resets passwords for limited admins. Cannot manage security-related policies or other configuration objects.
8. [Privileged Authentication Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-authentication-administrator) - Sets and resets authentication methods for all users (admin or non-admin), deletes/restores any users. Manages support tickets in Azure and Microsoft 365. Restrictions on managing per-user MFA in legacy MFA portal.
9. [Privileged Role Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-role-administrator) - Manages role assignments in Azure AD, Azure AD Privileged Identity Management, creates/manages groups, manages all aspects of Privileged Identity Management, administrative units. Allows managing assignments for all Azure AD roles including Global Administrator.
10. [Security Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#security-administrator) - Can read security information and reports, and manages security-related features, including identity protection, security policies, device management, and threat management in Azure AD and Office 365.
11. [SharePoint Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#sharepoint-administrator) - Manages all aspects of SharePoint Online, Microsoft 365 groups, support tickets, service health. Scoped permissions for Microsoft Intune, SharePoint, and OneDrive resources.
12. [Teams Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#teams-administrator) - Manages all aspects of Microsoft Teams, including telephony, messaging, meetings, teams, Microsoft 365 groups, support tickets, and service health.

</details>

## Manage your organizations that have been registered with enterprise apps in Rewst

If you’d like to manage your internal organization with Rewst and enable it to run automations, you’ll need to assign specific roles to your Rewst service account. If you don't want to manage your internal MSP, you can remove the Global Administrator Role now.  If you wish to continue managing your MSP organization, add the 12 roles indicated below to the Rewst service account. Then, remove the Global Administrator Role.  Removing the role will not remove the 12 added roles.

* If you used the Rewst Microsoft GDAP Assistant Crate to set up your GDAP roles, you'll still need to manually add these roles to your Rewst service account. The Crate does not add them at the MSP parent organization level for you.
* If you chose to set up the GDAP roles manually without using the Crate, you'll also need to manually add these roles to your Rewst service account. Note that they're the same 12 roles that you used previously.

Once this has been completed, you can remove the Global Administrator Role from your Service account

{% hint style="warning" %}
Important: Review your internal processes before proceeding, as Rewst will be able to make changes to your organization once these roles are applied.
{% endhint %}

### 12 roles to add to Rewst Service account at the MSP level organization

<details>

<summary>Click to read more</summary>

1. [Application Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#application-administrator) - Can create and manage all applications, service principals, app registration, enterprise apps, consent requests. Cannot manage directory roles, security groups.
2. [Authentication Policy Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#authentication-policy-administrator) - Configures authentication methods policy, MFA settings, manages Password Protection settings, creates/manages verifiable credentials, Azure support tickets. Restrictions on updating sensitive properties, deleting/restoring users, legacy MFA settings.
3. [Cloud App Security Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-app-security-administrator) - Manages all aspects of the Defender for Cloud App Security in Azure AD, including policies, alerts, and related configurations.
4. [Cloud Device Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#cloud-device-administrator) - Enables, disables, deletes devices in Azure AD, reads Windows 10 BitLocker keys. Does not grant permissions to manage other properties on the device.
5. [Exchange Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#exchange-administrator) - Manages all aspects of Exchange Online, including mailboxes, permissions, connectivity, and related settings. Limited access to related Exchange settings in Azure AD.
6. [Intune Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#intune-administrator) - Manages all aspects of Intune, including all related resources, policies, configurations, and tasks.
7. [User Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#user-administrator) - Manages all aspects of users, groups, registration, and resets passwords for limited admins. Cannot manage security-related policies or other configuration objects.
8. [Privileged Authentication Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-authentication-administrator) - Sets and resets authentication methods for all users (admin or non-admin), deletes/restores any users. Manages support tickets in Azure and Microsoft 365. Restrictions on managing per-user MFA in legacy MFA portal.
9. [Privileged Role Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#privileged-role-administrator) - Manages role assignments in Azure AD, Azure AD Privileged Identity Management, creates/manages groups, manages all aspects of Privileged Identity Management, administrative units. Allows managing assignments for all Azure AD roles including Global Administrator.
10. [Security Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#security-administrator) - Can read security information and reports, and manages security-related features, including identity protection, security policies, device management, and threat management in Azure AD and Office 365.
11. [SharePoint Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#sharepoint-administrator) - Manages all aspects of SharePoint Online, Microsoft 365 groups, support tickets, service health. Scoped permissions for Microsoft Intune, SharePoint, and OneDrive resources.
12. [Teams Administrator](https://learn.microsoft.com/en-us/azure/active-directory/roles/permissions-reference#teams-administrator) - Manages all aspects of Microsoft Teams, including telephony, messaging, meetings, teams, Microsoft 365 groups, support tickets, and service health.

</details>

## Migrate legacy Microsoft integrations to the new Microsoft Cloud Integration Bundle

{% hint style="info" %}
For users of the legacy setup, it's important to note that the static permissions associated with the legacy App Registration cannot be modified during this transition. Transitioning to the new bundle is highly recommended for continued functionality and security.
{% endhint %}

<details>

<summary>Migrate to new integration setup</summary>

1. Navigate to **Marketplace > Integrations** in the left side menu of your Rewst platform.
2. Search for the `Microsoft Cloud Bundle`.
3. Click on the integration tile.
4. Select the Microsoft services you wish to integrate.
5. Enter the necessary details to establish a connection.
6. Modify permissions as needed for enhanced control.
7. Complete the setup by authorizing the selected integrations.

</details>

<details>

<summary>Post-transition configuration</summary>

After migrating, you'll configure each integration according to your needs, including setting up OAuth configurations and mapping CSP customers to Rewst organizations.

* **Use CSP Delegated Admin permissions**: Manage permissions for Cloud Solution Provider integrations, ensuring they align with delegated admin roles.
* **Microsoft Graph OAuth configuration**: Set up OAuth configurations for Microsoft Graph to ensure seamless integration and data access.
* **CSP Customer to Rewst organization mapping**: Map CSP customers to Rewst organizations for streamlined management and reporting.
* **Microsoft Exchange Online OAuth configuration**: Configure OAuth for Exchange Online, enabling advanced email and calendar integration functionalities.

</details>

## Troubleshoot the Microsoft Cloud integration bundle setup

We have a separate guide with all bundle troubleshooting information. View that page [here](microsoft-cloud-integration-bundle-troubleshooting-guide.md).&#x20;
