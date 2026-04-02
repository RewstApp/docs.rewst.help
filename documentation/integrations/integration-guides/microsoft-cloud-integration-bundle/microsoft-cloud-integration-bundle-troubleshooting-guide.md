# Microsoft Cloud integration bundle troubleshooting guide

{% hint style="success" %}
The error codes in this guide have been truncated. Your error code will contain some personal identifying information, based on your individual accounts. To find your relevant error, we recommend copying a small piece of your error code that is general text, without any of your PII or specific URL information, and searching in this page using **Command + F** for Mac or **Control + F**  for Windows to identify your relevant solutions.
{% endhint %}

## Common installation errors

{% hint style="info" %}
**If you set up your Microsoft integrations Prior to April 2024,** you are most likely leveraging the legacy Rewst Prod App Registration for authenticating with your Microsoft Tenant. This setup uses a fixed set of permissions and is scheduled for future deprecation. We recommend [transitioning to the newer Microsoft Cloud Integration Bundle](microsoft-cloud-integration-bundle-troubleshooting-guide.md#migrate-legacy-microsoft-integrations-to-the-new-microsoft-cloud-integration-bundle).
{% endhint %}

<details>

<summary>Issue: Auth app registration error</summary>

* **Symptom**: Failure to proceed past the authentication step, not even reaching the Microsoft Auth login screen.
* **Common Cause**: This may occur due to a delay on Microsoft's end  where the system is still processing the app registration.
* **Solution**: Wait a minute or two before attempting to re-authenticate. This allows time for the backend processes to complete.

</details>

<details>

<summary>Issue: Legacy app registration conflicts</summary>

* **Symptom**: Successful authentication only after switching between the new Rewst Cloud Connector and the legacy Rewst Prod App Registration.
* **Potential Cause**: Existing Rewst Prod installations in the Microsoft tenant might interfere with the new setup.
* **Solution**:
  * Restart the integration wizard from the beginning.
  * Make sure all configuration steps are correctly completed. Pay extra attention to step 2 and confirm that a notification appears, indicating that the configurations have been updated.

{% hint style="warning" %}
The Rewst Prod App is necessary for authentication and might already be installed in your Microsoft Tenant. Existing installations could influence the new authorization processes.

**Note**: The Rewst Prod App is mainly used for authentication purposes. It should be maintained but with limited permissions, only necessary for Rewst login.

**Future Updates**: The Rewst Prod App remains essential for Rewst login authentication. Upcoming updates will restrict its permissions to those strictly needed for logging in, improving security.
{% endhint %}

</details>

<details>

<summary>Issue: Missing scopes in Microsoft Graph list</summary>



* **Symptom**: The only scopes displaying are the base scopes. When viewing the Graph list of scopes, there should be over 140, if the client has left permissions intact.\
  Note that whenever you encounter this problem, actions such as List Users and running the GDAP relationship Crate will yield forbidden errors.
* **Potential Cause**: Microsoft's syncing is notoriously slow - it can take them up to a day to get this applied into Rewst's integration.
* **Solution**:
  * If you uninstall/reinstall the integration, and verify that the service account has the correct roles/groups, this may still be an issue on Microsoft's side of the integration.
  * Do another re-authorization and let it sit between 2 and 48 hours. Check the scopes to make sure they are displaying correctly at the end of that time period. If scopes are still missing after 48 hours, contact Rewst support.

</details>

<details>

<summary>Issue: Wizard hangs during uninstallation attempts</summary>



* **Symptom**: When trying to delete the MS Bundle form your instance, Rewst displays this screen and never progresses. \
  \
  ![](../../../../.gitbook/assets/image.png)<br>
* **Potential Cause**: This usually happens if Rewst can't find the enterprise app.
* **Solution**:
  * Switch to owned app registration
  * Fill out all required details
  * Click next until you reach the authorization phase of setup
  * Return to the integrations page and uninstall the bundle

</details>

## **Authorization issues**

If you encounter problems during the authorization step, ensure that you are using the correct account, and that all permissions are properly set.

## **Permission configuration errors**

Double-check the permissions if there are issues with accessing certain functionalities. Ensure that the appropriate permissions are enabled and correctly configured.

<details>

<summary>Issue: Consent to Client Permissions</summary>

* **Error Context:** Pertains to errors when consenting on a client (e.g., green shield button on CSP/Graph/EXO integration table).
* **Common Issue:** Transition to Microsoft's [Granular Delegated Admin Privileges (GDAP)](https://learn.microsoft.com/en-us/partner-center/gdap-introduction) introduces complexities in tenant access control.
* **About GDAP:**
  * **Purpose:** GDAP enables fine-grained control over tenant access, allowing the creation of groups in your MSP tenant, assignment of permissions, and user allocation.
  * **Example:** Create specific groups like "Standard M365 Clients - Exchange Administrator" or "Strict M365 Clients - Exchange Administrator" to manage access levels across different clients.
* **Rewst's Role:** Since Rewst can interact with various endpoints, the correct permissions in both your tenant and client tenant are essential.
*   **Potential Resolution: Understand and Implement GDAP**\
    Utilize GDAP to create groups and assign permissions, ensuring compliance with your security policies.



</details>

<details>

<summary>Issue: Access Denied - HTTP Status code 403</summary>

* **Root Cause:** Most commonly related to a misunderstanding of Application vs. Delegated permissions within Microsoft Graph Integration.
  * **Application Permissions:** Granted to applications, not tied to users. Allows access to data without user consent.
  * **Delegated Permissions:** Tied to specific users, requiring their consent for data access.
* **Microsoft's Direction:** Microsoft is shifting from Application permissions to Delegated permissions for security reasons. Application permissions lack an audit trail, hiding who accessed data and when. They also allow Microsoft Partners to have a tenant in their organization without the client's awareness.
* **Relevance to Tasks:**
  * **User Permissions:** For user-related endpoints, such as reading calendar items, or sending mail as a user, the authenticating account must have the necessary permissions.
  * **Example:** To send as `SendfromMe@rewstdemo.com` via Rewst, ensure `Rewst-Service Account` has **Send As** permission on the `SendfromMe` account.

{% hint style="info" %}
If you have a user in your tenant that needs permissions within a client tenant (e.g., to a mailbox, SharePoint site, etc.), granting those permissions directly to your user wont be possible due to the users belonging to different tenants. In this case, instead of using an integration override for that workflow, consider configuring the integration under that client's organization directly.
{% endhint %}

</details>

<details>

<summary>Issue: Request_BadRequest, Unsupported token. Unable to initialize the authorization context</summary>

* **Error Message & Context:** `Request_BadRequest`, `Unsupported token. Unable to initialize the authorization context`. This manifests as a **"Bad Request"** error when making calls to Graph, despite seemingly correct integration and tenant delegation credentials.
* **Suspected Cause:** The error may stem from a cached token or from the integration being authorized prior to setting the checkbox for CSP delegation in CSP, Graph, or Exchange Online.
* **Potential Resolution:**
  1. **Uninstall and Reinstall CSP Integration:** Go to CSP integration, click "Uninstall," wait, then click "Install."
  2. **Reauthorize CSP with Admin Access:** Use the recommended service account with admin access for reauthorization.
  3. **Repeat for Other Integrations:** Follow steps 1-2 for Exchange Online and Graph, checking `Use CSP Delegated Consent` before authorizing.
  4. **Re-Consent on Behalf of Managed Tenants:** Return to CSP integration and click the green shield to re-consent.

</details>

## Additional errors

{% hint style="info" %}
Use **command + F or CTRL + F** to search your your issue in the page and jump to the relevant error in our troubleshooting guide. Then, click on each header to expand and view the suggested solution.
{% endhint %}

<details>

<summary>Issue: Updating the password profile of a user fails with a forbidden error</summary>

As per Microsoft documentation the following needs to be true for resetting a user's password/modifying their password profile.

See [Microsoft Documentation](https://learn.microsoft.com/en-us/graph/api/user-update?view=graph-rest-1.0\&tabs=http#permissions)

In a delegated scenario the Rewst enterprise applications need to have the 'Directory.AccessAsUser.All' permission (and corresponding GDAP roles)

In a application call scenario(MSP Level/Integration installed at the customer level standalone from CSP) the application must be assigned a priviledged role such as Authentication Administrator or Priviledged Authentication Administrator.

</details>

<details>

<summary>Issue: The token has expired</summary>

If the refresh token couldn't be retrieved or stored, reauthorization must occur.

</details>

<details>

<summary>Issue: Presented multi-factor authentication has expired to the policies configured by your administrator, you must refresh your multi-factor authentication to access</summary>

A Conditional Access Policy may have set the maximum session time, causing this error. Consider changing the policy or following guidance under Conditional Access.

</details>

<details>

<summary>Issue: Due to a configuration change made by your administrator, or because you moved to a new location, you must use multi-factor authentication to access.</summary>

The absence of MFA setup or Conditional Access policies blocking Rewst's access may lead to this error. Check MFA settings and Conditional Access policies.

</details>

<details>

<summary>Issue: The provided grant has expired due to it being revoked. A fresh auth token is needed. The user might have changed their password.</summary>

Password changes, session revocations, or account disabling may lead to this error. Reauthorization will be needed.

</details>

<details>

<summary>Issue: Device object was not found in the tenant xxxxxxxxxx</summary>

This might occur when a trusted device used for the first authorization has been deleted from the Intune portal. Reauthorization is required.

</details>

<details>

<summary>Issue: Insufficient access rights to perform the operation</summary>

If the user lacks sufficient access rights or is missing the necessary Exchange role, check the user's rights and Exchange role information. When using GDAP, the user must be in the "Exchange Administrators" group.

</details>

<details>

<summary>Issue: AppLifecycle_2210</summary>

This is likely a failure to call Intune APIs. Check if the tenant has the necessary license available.

</details>

<details>

<summary>Issue: "Invalid Client" error message when authorizing</summary>

A [key vault ](microsoft-cloud-integration-bundle-troubleshooting-guide.md#what-integrations-are-in-the-microsoft-cloud-integration-bundle)is required in your Azure subscription. If you receive an "Invalid Client" error message when authorizing it is likely due to a missing key vault. [Creating an empty key vault](https://learn.microsoft.com/en-us/azure/key-vault/secrets/quick-create-portal) should resolve the issue.

</details>

<details>

<summary>Issue: Invalid or malformed</summary>

The request might be malformed if the body doesn't contain JSON or if variables haven't expanded. Look for syntax errors or incorrect bracket usage.

</details>

<details>

<summary>Issue: The user or administrator has not consented to use the application - AADSTS50020</summary>

Multiple causes could lead to this error, such as the user not authorizing the Rewst CSP integration or not being in the `AdminAgents` group. If you're using GDAP, ensure that the user is added to the correct group(s) for Rewst to function.

</details>

<details>

<summary>Issue: User was not found</summary>

This could indicate that the relationship between the tenant and the partner has been dissolved from the client side, or that a GDAP relationship has expired. Check the partner relationship information and ensure it is still active.

</details>

<details>

<summary>Issue: Subscription within the tenant has lapsed</summary>

This means that Exchange connections are no longer possible. Please verify Exchange subscription availability.

</details>

<details>

<summary>Issue: Provide valid credential</summary>

If GDAP has been deployed and you're seeing this error, it may be because the user is not in any GDAP groups. Verify the user's GDAP group membership.

</details>

<details>

<summary>Issue: Microsoft.Skype.Sync.Pstn.Tnm.Common.Http.HttpResponseException</summary>

If you're unable to connect to Teams Admin cente, this might mean the tenant is missing a Teams license. Check to ensure the necessary licenses are available.

</details>

<details>

<summary>Issue: Request not applicable to target tenant</summary>

This error is mainly seen around security tasks and is likely due to a missing license such as M365 BP or Azure AD P1. Check the tenant's license information to ensure that the necessary licenses are available for the requested operation.

</details>

<details>

<summary>Issue: Forbidden (403), MFA Required (401)</summary>

* **Cause:** Often related to Multi-Factor Authentication (MFA). Absence of MFA, incorrect MFA configuration, or unsupported third-party MFA provider.
* **Requirements:** Microsoft mandates the use of the `StrongAuthClaim` method in MFA requests, confirming additional security checks beyond username and password.
* **Potential Resolutions:**
  1. **Enable MFA with StrongAuthClaim:** Make sure the user account for Microsoft CSP integration has MFA enabled using the StrongAuthClaim method (usually with Microsoft MFA).
  2. **Confirm MFA at Sign-In:** If using Microsoft MFA and encountering errors, ensure MFA confirmation at sign-in. Try incognito browsing or sign out and back in if needed.
  3. **Create a Dedicated User Account:** Recommended for Microsoft CSP integration with specific requirements (e.g., Global Administrator permissions, MFA with StrongAuthClaim, `AdminAgents` role added in Partner Center to enable API access).

**Duo / Third Party MFA Notice:** Duo MFA was removed from Microsoft's supported list in 2022. Users must switch to Microsoft MFA to comply with requirements. See [Microsoft Partner Account - MFA Requirements](https://docs.microsoft.com/en-us/powershell/partnercenter/test-partner-security-requirements?view=partnercenterps-3.0)

</details>

<details>

<summary>Issue: Neither tenant is B2C or tenant doesn't have a premium license</summary>

This feature requires a P1 license or higher. Check the client's tenant license information to ensure that the necessary licenses are in place.

</details>

<details>

<summary>Issue: Client error 400 (Bad Request)</summary>

Client error `400 Bad Request` means there's an issue with the request. It's most likely that an incorrect value is being sent. Please verify the correctness of the values in the request.

When in the context of authorizing the Microsoft Cloud Bundle this error can sometimes be related to Conditional Access policies, either on the MSP tenant (if failing to authorize) or on the customer tenant (when performing CPV consent aka clicking the blue shield).

If the issue is during the initial authorization, then it is important to check your conditional access policies and modify them to either exclude the user used to authorize the integration (typically the Rewst@ user) or to address the conflict (as an example, limiting access by location).

If the issue is during CPV consent of a customer then you will need to check the customer's conditional access policies and modify them to exclude the service provider tenant or address the conflict (example from above could apply).



</details>

<details>

<summary>Issue: Client error 401 Unauthorized for...</summary>

This is an Azure specific error. The Azure APIs are using delegated permissions. If it was working before and then stopped working post migration, it's likely that the Azure integration was authorized with a different account than what was used post migration, and the user used to authorize probably doesn’t have the required roles assigned to it in Azure. Assign roles to the user to solve this issue.

Alternatively, it is possible that the tenant does not have licensed users in the Azure/O365. This means that you are missing service principals.

</details>

<details>

<summary>Issue: invalid_client - Failed to authorize one or more integrations: Permissions configuration not found for Azure integration</summary>

This is an Azure specific error and it happens when re-authorizing the Microsoft Cloud Integration Bundle. You must [set up an Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/secrets/quick-create-portal). It can be empty but it needs to be setup and available.<br>

</details>

<details>

<summary>Issue: There was an error configuring delegated admin… Client error ‘400 Bad Request’…</summary>

This happens when trying to re-consent a client or multiple clients. Make sure to check partner center relationships since you are likely missing one or more [GDAP roles](microsoft-cloud-integration-bundle-actions-and-endpoints.md).

Note that if the client has other relationships with interfering roles it will also cause the consent to fail. You'll need to terminate any other interfering relationships.

</details>

<details>

<summary>Issue: Entra UI pagination and permissions display </summary>

We've identified a recurring issue within the Entra UI concerning the inconsistent permissions display on the Enterprise App Permissions page. Users may encounter situations where the permissions are either fully paginated and visible or not all permissions are displayed as expected.

#### **Incomplete display of permissions** <a href="#incomplete-display-of-permissions" id="incomplete-display-of-permissions"></a>

If what you see resembles the screenshot below, it indicates that not all permissions are being displayed. In such cases, the seemingly absent permissions are assigned but not visible due to a limitation within the UI. This known issue stems from a bug on Microsoft's end, which unfortunately is beyond our ability to directly resolve. For visibility into the complete set of permissions under these circumstances, using the API is the recommended approach.

![](https://docs.rewst.help/~gitbook/image?url=https%3A%2F%2F1835401289-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FAQQ1EHVcEsGKBPVHmiav%252Fuploads%252FNHYWwCfHOfPPzEzUXens%252Fentra-ui-not-all-permissions-shown.png%3Falt%3Dmedia%26token%3D54e204ec-8bdb-4f97-9703-5557ece7a5ad\&width=768\&dpr=4\&quality=100\&sign=2d30e14d\&sv=2)

#### **Complete display of permissions** <a href="#complete-display-of-permissions" id="complete-display-of-permissions"></a>

If your Entra UI matches the below screenshot, this suggests that all permissions are being properly shown. So if any are missing, they are actually missing. Should there be any unexpected permissions missing in this scenario, it likely points to an bug or failure in the permissions assignment process on the Rewst side.

![](https://docs.rewst.help/~gitbook/image?url=https%3A%2F%2F1835401289-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FAQQ1EHVcEsGKBPVHmiav%252Fuploads%252FWTDzmTA6FgPmNIY4IBm4%252Fentra-ui-all-permissions-shown.png%3Falt%3Dmedia%26token%3Dedd0db06-85eb-43d7-9be8-9f760e4d7575\&width=768\&dpr=4\&quality=100\&sign=95906007\&sv=2)

</details>

<details>

<summary>Issue: Failed to get tenant resource id for… Please try again later.</summary>

This is a matter of allowing Microsoft time to do its work. It could take up to 48 hours for this to self resolve - just give it time and try to re-consent.

</details>

<details>

<summary>Issue: Error assigning application permission…</summary>

Note that this error will display all the multiple permissions that are missing, more than the example referenced. This happens when trying to re-consent a client or multiple clients. Check partner center relationships since there are likely missing one or more [recommended GDAP roles.](microsoft-cloud-integration-bundle-actions-and-endpoints.md)

</details>

<details>

<summary>Issue: Error during callback. error='invalid_client' error_description="AADSTS650051: Value length '8060' is out of the valid range of '1' to '8000' for property 'DelegationScope'.</summary>

This comes from the Microsoft side when the permissions exist and we try to add them back.

Initially attempt to remove some delegated permissions from the enterprise app in your Microsoft Entra portal. If that doesn’t work, you'll want to remove the integration and re-add it.

During the setup, do not click the select all permissions option. Just click next.

</details>

<details>

<summary>Issue - Delegated admin consent creation failed - Forbidden - GDAP relationship configuration needed</summary>



The error can be caused by multiple reasons and presents itself when consenting a child organization:

1. User has not authorized the app
2. User is a guest user in the tenant
3. Conditional Access policy is blocking access
4. User is not added to the correct group

This error likely happens if you skipped the step to use the Unpack our Configure New GDAP Relationship Crate. Unpack the Crate. Then, using the form: \[ROC] M365: Configure GDAP Relationships unpacked in the Crate, set up a new specific GDAP relationship for Rewst between you and your client. It will send you an email per CSP customer, with and approval link and then another link back to rewst to set everything up. It ensure consistency across your orgs.

Then check that it has been configured correctly. The[ 12 GDAP roles](microsoft-cloud-integration-bundle-actions-and-endpoints.md) would need to be in the admin relationships that are failing.

Make sure that the account you are using is a member of ADMINAGENTS and GLOBALADMIN while you sort the permissions. Once done, GA can be removed if desired.

Lastly, check your clients' [conditional access policies](microsoft-cloud-integration-bundle-actions-and-endpoints.md).



</details>

<details>

<summary>Issue: Failed to refresh options</summary>

This issue presents itself when you click the **Refresh Options** button in the integration page. To resolve this, add the Rewst Service account to AdminAgents at the top MSP parent level organization. After this action has been taken, the client must re-authorize the integration to fix.

</details>

<details>

<summary>Issue: Delegated admin consent creation failed… Due to a configuration change made by your administrator, or because you moved to a new location, you must use multi-factor authentication to access…</summary>

The error can be caused by multiple reasons and presents itself when consenting a child organization:

1. User has not authorized the app
2. User is a guest user in the tenant
3. Conditional Access policy is blocking access
4. User is not added to the correct group

</details>

<details>

<summary>Issue: Delegated admin consent creation failed… Access has been blocked by Conditional Access Policies</summary>

You must ensure that you have setup your clients’ policies as per our [guidance on conditional access](microsoft-cloud-integration-bundle-actions-and-endpoints.md).&#x20;

</details>

<details>

<summary>Issue: Unsupported token. Unable to initialize the authorization context</summary>

This error is an indication that you have either either not approved the created relationship or not added the required [GDAP roles](microsoft-cloud-integration-bundle-actions-and-endpoints.md) to it. Partner GDAP setup was not completed. You'll need to terminate the setup, and create a new one.

</details>

<details>

<summary>Issue: User is trying to authenticate Azure integration (may apply to other in the bundle) and gets example error:</summary>

Ensure that he secret being sent in the request is the client secret value, not the client secret ID.

The other error that may be related to this when consenting is **There was an error configuring delegated admin**. Here, the integration is trying to use old CSP App Registration. Uninstall and reinstall the entire Microsoft Cloud Integration Bundle. Note that only uninstalling and reinstalling Azure/CSP alone will not work. \
\
If you keep getting errors during reinstallation, remove the Rewst MS Cloud Connector Enterprise Application and then authorize.\
\
\
During the process, you may see the below error. You should be fine to proceed despite the error message. <br>

<figure><img src="../../../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

</details>

<details>

<summary>Issue: Invalid Tokens - Invalid_grant - device object was not found</summary>

Device Object was not found in tenant means that during authentication you used an approved device, and that device is no longer available.

The best way to fix is to rerun the authentication setup. When a dialog appears to log in, don't click on the account that's already logged in, even if it's the service account. Instead, click **sign in with a different account.** The&#x6E;**,** log on with the service account

If this doesn't fix your issue, manually delete the enterprise application, then  re-authorize. You may need to manually consent the app in Intune, then re-authorize again.

</details>

<details>

<summary>Issue: Invalid Tokens - Invalid_grant - The provided grant has expired</summary>

The first step in troubleshooting is to attempt reauthentication.&#x20;

1. Navigate to the Microsoft Cloud Integration Bundle settings in Rewst.
2. Click **Reauthenticate** and follow the prompts to complete the process.
3. If authentication is successful, your integration should resume normal operation.

If reauthentication fails, proceed to the next step. Tthe issue may be related to the service account credentials.

1. Reset the service account password in Microsoft.
2. Update the credentials in Rewst.
3. Update the credentials in Rewst.
4. Attempt to reauthenticate again.
5. If this works ensure you click the re-concent button.

If the issue persists, completely uninstall and reinstall the Microsoft Cloud Bundle Integration.



</details>

<details>

<summary>Issue: User account [tenant name] does not exist in tenant. The account needs to be added as an external user in the tenant first.</summary>

Ensure that the [CA Policies exclusions](microsoft-cloud-integration-bundle-actions-and-endpoints.md) have been set. If the Service Account is not added you will see this error

</details>

<details>

<summary>Issue: "Unknown auth_app_registration: None" Error</summary>

Remove Microsoft Cloud integration from the child organization only.

</details>

<details>

<summary>Issue: Delegated admin consent re-creation failed for ID {‘error’: {‘response’: {‘code’: 400, ‘message’: 'Application ID doesn’t exist</summary>

Confirm that the company uses and has Azure Storage enabled.

</details>

<details>

<summary>Issue: Company Using Owned APP Registration and getting errors in crates.</summary>

See our documentation on [Owned App Registration](owned-app-registration.md).

</details>

<details>

<summary>Issue: 403 - Authorization_RequestDenied (Duo External Authentication)</summary>

Here, a client has Duo as an External Authentication method that may be re-directing MFA. Configure a service provider exclusion for the problem tenant.

</details>

<details>

<summary>Issue: <strong>Error -3 while decompressing data: incorrect header check -</strong> Microsoft EXO </summary>

For MSP or parent organization

* Verify that the dedicated account used for Microsoft Cloud Bundle authorization has Exchange Administrator or Global Administrator role assigned.

For child organization

* If the tenant is a child org:
  * Ask the customer to confirm in their GDAP Relationship that they have Exchange Administrator role assigned.
  * If authentication is handled through the Microsoft Cloud Bundle, confirm that the linked service account has the Exchange Administrator role assigned.

</details>

<details>

<summary>Issue: User used to authorize integrations does not have Exchange Admin role</summary>

If there are limited mailboxes returned by `Get_Mailbox` when using the Exchange Online integration, this likely means that the user that authorized the integration bundle has not been granted proper permissions. The user must have the Exchange Administrator role. For more on the specifics of this role, please see Microsoft’s own documentation [here](https://learn.microsoft.com/en-us/powershell/exchange/app-only-auth-powershell-v2?view=exchange-ps#assign-microsoft-entra-roles-to-the-application).

</details>
