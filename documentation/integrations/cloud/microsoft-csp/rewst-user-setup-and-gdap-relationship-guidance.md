---
description: Step by Step
---

# Rewst User Setup and GDAP Relationship Guidance

## Introduction

This guide specifically goes over the following:

* Creating the Rewst service account user.
* Creating the Rewst group that GDAP permissions will be assigned to.
* Adding the Rewst user to the AdminAgents group.
* Creating a new admin relationship with the roles specifically required by Rewst. (Depending on your current GDAP relationship setup(s) this may not be necessary as long as your relationship contains the right roles and groups are available with the necessary permissions for the user)

{% hint style="warning" %}
Other applications/your technicians might need additional roles added to the relationship. Adding new roles after the relationship has been created requires recreating the relationship.
{% endhint %}

* Adding the Rewst group to the admin relationship.
* Adding the roles for the Rewst group in the admin relationship.

{% embed url="https://www.youtube.com/embed/EtnO8VAHnGo?si=lsQ1a7fwVwMxxF2W" %}

{% hint style="danger" %}
IMPORTANT:
As of January 2024 it was discovered that there is an issue on Microsoft's end that can cause issues with RBAC settings for certain APIs.

Because of this it is recommended to break each individual role out into seperate groups within the GDAP relationship, failure to do so can result in intermittent GET, PATCH, and POST failures on API calls.

In the video and text guide for this document the instructions state to create one group, however the document and video will be updated at a later date to reflect this.

When setting up the group(s) in Entra you should do the following:

Create a corresponding group for each role that will be assigned per [#recommended-roles-for-gdap](../authorization-best-practices.md#recommended-roles-for-gdap "mention"), an example of this would be:
GDAP - Application Administrator
GDAP - Exchange Administrator
etc.

In the admin relationship within the Partner Center you will need to add each group to the relationship and assign the corresponding role to the corresponding group in the relationship.

Example: GDAP - Application Administrator -> Application Administrator

The user used to authorize the integration(s) will need to be a member of each of these groups.
{% endhint %}

Below are the manual steps for completing this task

## Azure Active Directory (In Partner Tenant)

1. **Login** to [Microsoft Entra ID](https://portal.azure.com/#view/Microsoft\_AAD\_IAM/ActiveDirectoryMenuBlade/\~/Overview).
2. &#x20;**Navigate** to _Users_.

<figure><img src="../../../../.gitbook/assets/entra-id-users.png" alt=""><figcaption></figcaption></figure>

3. **Click** _New User_ → _Create User_.

<figure><img src="../../../../.gitbook/assets/create-user-entra.png" alt=""><figcaption></figcaption></figure>

4. **Provide** the user principal name.
   * example: rewst
5. **Provide** a display name.
   * example: Rewst Integration
6. **Provide** a password.
   * document this for later usage
7. **Click** _Next: Properties._

<figure><img src="../../../../.gitbook/assets/create-user-properties.png" alt=""><figcaption></figcaption></figure>

8. **Click** _Next: Assignments._
9. **Click** _Add Role_ while under the assignments tab.
10. **Search** for _Global Administrator_ in the role selection.
11. **Select** the _Global Administrator role_.

{% hint style="warning" %}
Note: This role is required for installing the Enterprise Applications used when Rewst first authorizes.
{% endhint %}

12. **Click** _Select._

<figure><img src="../../../../.gitbook/assets/add-global-admin-role.png" alt=""><figcaption></figcaption></figure>

13. **Verify** the role is now listed in the main pane.
14. **Click** _Next: Review + Create_ If the role is there.
    * Verify the information is correct on the _Review + Create page_.
15. **Click** _Create_.
16. **Navigate** back to _Microsoft Entra ID._
17. **Click** _Groups_.

<figure><img src="../../../../.gitbook/assets/entra-id-create-new-group.png" alt=""><figcaption></figcaption></figure>

18. **Click** on _New Group_ on the _Groups_ page.&#x20;

<figure><img src="../../../../.gitbook/assets/add-security-group.png" alt=""><figcaption></figcaption></figure>

19. **Select** _Security_ for Group type.
20. **Enter** _Rewst – GDAP_ for the group name.
21. **Enter** _Rewst GDAP Permissions Group_ for the group description.
22. **Set** _Microsoft Entra roles can be assigned to the group_ to _Yes._&#x20;
23. **Click** on _No members selected_.
24. **Select** the Rewst account created in the previous steps in the new pane type in _Rewst_.
25. **Click** _Select._

<figure><img src="../../../../.gitbook/assets/finish-group-creation-entra.png" alt=""><figcaption></figcaption></figure>

26. **Select** _Yes_ when prompted with the following:
    * _"Creating a group to which Microsoft Entra roles can be assigned is a setting that cannot be changed later. Are you sure you want to add this capability?"_

{% hint style="warning" %}
It is also necessary to add the user to the ‘AdminAgents’ group on the group's page as well after the previous steps are done.
{% endhint %}

## Partner Center

1. **Navigate** to the [Microsoft Partner Center](https://partner.microsoft.com).
2. **Click** on _Customers_ once on the Partner Center home page.

<figure><img src="../../../../.gitbook/assets/partner-home-customers.png" alt=""><figcaption></figcaption></figure>

3. **Click** on the name of the customer you would like to create the admin relationship for once the customer list loads.

<figure><img src="../../../../.gitbook/assets/customer-admin.png" alt=""><figcaption></figcaption></figure>

4. **Click** on _Admin Relationships_ in the left nav pane once in the customer page.

<figure><img src="../../../../.gitbook/assets/admin-relationships.png" alt="" width="269"><figcaption></figcaption></figure>

5. **Press** _Request for new admin relationship_ once on the relationship page.
6. **Provide** a name for the admin relationship.

{% hint style="info" %}
Note: This value must be unique per relationship/customer.
{% endhint %}

7. **Provide** a duration.
   * max is 730 days
8. **Click** _Select Microsoft Entra Roles_.

<figure><img src="../../../../.gitbook/assets/admin-duration.png" alt=""><figcaption></figcaption></figure>

9. **Select** the roles listed in [#recommended-roles-for-gdap](../authorization-best-practices.md#recommended-roles-for-gdap "mention").

{% hint style="info" %}
Note: The list is not in alphabetical order and it is recommended that you use CTRL + F to search the page to make finding the roles easier.
{% endhint %}

10. **Click** the _Save_ button once all roles are selected.
11. **Click** _Finalize Request_ once you've verified all the roles you selected are listed.

<figure><img src="../../../../.gitbook/assets/verify-roles-finalize.png" alt="" width="563"><figcaption></figcaption></figure>

You will be redirected to a page that shows the request.

{% hint style="info" %}
At this point, your customer will need to accept the request or you will need to log in as a global administrator on the tenant to accept the request using the link in the _Click to review and accept_ section.
{% endhint %}

12. **Click** _Done_.

{% hint style="info" %}
Once the request has been approved the admin relationship will be established.
{% endhint %}

13. **Verify** that the relationship is established by returning to the _Admin Relationships_ page and confirming the status is active.
14. **Click** on the relationship name if the status is _Active._

<figure><img src="../../../../.gitbook/assets/active-admin-relationship.png" alt=""><figcaption></figcaption></figure>

This will bring you to the page that shows all the available roles in the relationship and the list of available security groups.

15. **Click** _Add security groups._

<figure><img src="../../../../.gitbook/assets/add-security-groups-partner.png" alt=""><figcaption></figcaption></figure>

16. **Select** the group created earlier.

<figure><img src="../../../../.gitbook/assets/security-group-rewst-gdap.png" alt="" width="258"><figcaption></figcaption></figure>

17. Click _Next._
18. **Select** the roles required for Rewst in the relationship as per [#recommended-roles-for-gdap](../authorization-best-practices.md#recommended-roles-for-gdap "mention").\


<figure><img src="../../../../.gitbook/assets/select-all-gdap-roles.png" alt="" width="230"><figcaption></figcaption></figure>

19. **Click** _Save_.
20. **Wait** for the status to change to _Active_ (manual page refresh is needed).

<figure><img src="../../../../.gitbook/assets/status-change-to-active.png" alt=""><figcaption></figcaption></figure>

These steps will need to be performed for each customer (creating the admin relationship/assigning the group to the relationship/assigning the roles to the group in the relationship)
