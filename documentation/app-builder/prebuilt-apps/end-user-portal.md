# App Builder Prebuilt Apps: End user portal

{% hint style="info" %}
End user portals, like all Prebuilt Apps, are available by request only. To request Prebuilt Apps, send us a message in your dedicated Discord support channel.
{% endhint %}

The _end user portal_ is built around self-service automation, letting you manage tasks independently while still maintaining the ability to log tickets for more complex needs. With 24/7 access to essential automations, this portal reduces reliance on service desk calls and streamlines operations for both you and your end users.

<figure><img src="../../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

## Features

* Manage group memberships
* Onboard employees
* Offboard employees
* Reset passwords
* Reset accounts
* Log tickets for other requests
* View tickets that have been submitted, along with their status
* Export reports

## **Crate prerequisites for end user portal setup:**

* [User Onboarding](/broken/pages/KavoTPXKO8uBrA9YYMTW) Crate
* [User Offboarding](../../crates/existing-crate-documentation/user-offboarding-v2.md) V2 Crate
* [Reset Locked Accounts](https://app.rewst.io/marketplace/crates/7cd396a6-89e5-4d7a-b57d-70a97c71fa22) Crate
* [Change A User's Password](../../crates/existing-crate-documentation/change-a-users-password-crate.md) Crate
* [Add or Remove Group Membership](../../crates/existing-crate-documentation/add-or-remove-group-membership-crate.md) Crate

## **Integration prerequisites for end user portal setup:**

* View tickets feature
  * PSA: Connectwise PSA, Datto Autotask, Halo PSA
* Create ticket feature
  * PSA: Connectwise PSA, Datto Autotask, Halo PSA

## Custom branding with Rewst's Style Customization Crate

As a bonus, you can customize your End User Portal by unpacking our App Builder - Create Branding Variables Crate, which lets you update all of your Prebuilt Apps without manual CSS edits for a professional, client-ready appearance.\
<br>

<figure><img src="../../../.gitbook/assets/Screenshot 2025-08-08 at 4.40.40 PM.png" alt="" width="309"><figcaption><p>Find this Crate in the Crate Marketplace section of your Rewst platform.</p></figcaption></figure>

* Apply consistent branding across all apps
* Input hex codes, upload logos, and select themes to apply at the MSP or client level



## Troubleshoot the end user portal

### Validation errors

* The End User Portal has several workflows built in from Crates. A validation error typically occurs when an unsynced workflow shares the same name as one being cloned into the environment. If an unsynced workflow exists, at minimum rename it to avoid conflicts.
* The other cause of validation errors is usually from [support access](../../../support-and-community/roc-support/rewst-support-allow-write-access.md) not being enabled.

