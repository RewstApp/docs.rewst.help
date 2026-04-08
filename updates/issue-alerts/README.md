---
icon: circle-exclamation
---

# Alerts

## 2026

<details>

<summary>⚠️ Planned: Rewst database maintenance, April 11, 2026</summary>

Rewst will be performing infrastructure maintenance in all regions on Saturday, April 11, from 2:00 PM ET to 2:30 PM ET. Our engineering team will be conducting database maintenance to ensure continued platform stability and performance.\
During this brief window, workflow executions will be paused. The expected disruption in each region is approximately 5-7 minutes, and the paused workflows will resume immediately after the work is complete.

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️Resolved: SQL Database Integration – Refactor Issues - AU, EU, UK, and US Region January 13, 2026</summary>

Release 4.83 SQL Database integration refactor triggered multiple related issues over 4 days,\
including configuration loss for some organizations, custom SSL certificates breaking, and\
MSSQL datetime handling failure. Full mitigation was achieved through multiple hotfixes and\
manual configuration restoration through January 9th.

Customers should review any SQL Database configurations and workflows using the integration to ensure they are set as expected and have run correctly. Workflows that failed during the issues may need to be re-run; for any customers with large numbers of workflows that have not already been re-run, please reach out to your Customer Success representative so we can support you.

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Resolved: Microsoft Azure Secret Expiration - AU, EU, UK, and US Region January 12, 2026. </summary>

On Sunday, January 11th at 2:17 AM ET, an issue was identified that affected workflows using\
Microsoft integrations. This was caused by an authentication credential that required renewal, which also impacted Slack and PagerDuty integrations. The Rewst team responded immediately and the production environment was fully restored by 2:44 am ET.

Any workflows that failed during the outage should be re-run if they have not already. For customers with large numbers of impacted workflows that still need to be re-run, please reach out to your Customer Success representative for support.

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>



## 2025

<details>

<summary>⚠️ Resolved: Service performance issue - US region December 10th, 2025</summary>

On December 10th, from 6:25 pm ET to 8:27 pm ET, the Rewst platform experienced intermittent delays in workflow processing. We recommend checking any workflows that were expected to run during this time to ensure that they executed as expected.

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Concluded: Planned maintenance window - US region November 16th, 2025</summary>

On Sunday, November 16th at 9:00 AM EDT, Rewst will be performing brief maintenance on the US instance [app.rewst.io](http://app.rewst.io/). Our engineering team will be migrating US users to our new permissions system. Due to the size of our US region, we expect up to 30 minutes where creating new entities, such as organizations or users, will result in under-provisioning or lack of access. Affected entities include:

* Organizations
* Users
* Custom roles
* App Builder apps

Normal operation will resume immediately after the work is complete, at which point we'll also provide a detailed report of all entities created during the affected period. We recommend that you plan to not update any of the affected entities during the window.

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Resolved: Service performance issue - US region October 8th, 2025</summary>

On October 8, 2025, following a routine platform deployment, our US region experienced degraded performance affecting workflow execution speeds. From 10:30 AM EDT to 12:31 PM EDT, customers may have noticed slower task completion times and some webhook timeouts.

During this platform update, we introduced an enhancement to improve task log storage by writing data to cloud storage in addition to the existing database storage method. However, the new implementation opened a new AWS connection for each task log operation instead of reusing existing connections. This led to excessive resource use on our workflow processing servers and temporary performance degradation.\
\
Our engineering team identified the issue within approximately 30 minutes of the update’s completion and deployed a fix. Service was fully restored by 12:31 PM EDT. It's recommended that all customers verify that tasks executed in their workflows executed as expected during this degradation window.\
\
We apologize for any inconvenience this incident caused. We take platform stability seriously and are committed to learning from this incident to provide you with more reliable service. The swift detection and resolution demonstrates our team's ability to respond quickly to issues, and the improvements we're implementing will help prevent similar issues in the future.&#x20;

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Concluded: Planned maintenance window - US region August 9th, 2025</summary>

On Saturday, August 9th, at 11:45 PM EDT, Rewst will be performing brief maintenance on the US instance [app.rewst.io](http://app.rewst.io/). Our engineering team will be conducting work involving database connection management to ensure continued platform stability and performance. During this brief window, the Rewst platform, including the user interface, API access, and workflow execution, will be temporarily unavailable. The duration of this work outage will be approximately five minutes. Normal operation will resume immediately after the work is complete. We believe that disruption will be minimal, but recommend that you monitor for failed workflows after the maintenance is conducted, and rerun workflows as needed.&#x20;

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Concluded: Planned maintenance window - All Regions June 19th, 2025</summary>

On Saturday, July 19th, the Rewst engineering team will be performing regional critical PostgreSQL upgrades and infrastructure enhancements. The Rewst platform—including the user interface, API access, and all workflow execution—may be intermittently unavailable during the maintenance window. While the duration may be as little as 15 minutes, there is potential for it to last as much as two hours. Our team will work to minimize service disruption in each region. We recommend rescheduling any critical automations during those periods. Please check your region's maintenance time window in the list below. While we'll try to minimize disruptions, we do recommend rescheduling any critical automations during that period.

The maintenance is scheduled across multiple regions during off-hours as follows:<br>

* US Instance:
  * Date: Saturday, July 19, 2025 10:00 PM – Sunday, July 20, 2025 12:00 AM EDT
  * Sunday, July 20, 2025 02:00 – 04:00 UTC
* UK Instance:
  * Date: Saturday, July 19, 2025 2:00 AM – 4:00 AM BST
  * Saturday, July 19, 2025 01:00 – 03:00 UTC
* EU Instance:
  * Date: Saturday, July 19, 2025 3:00 AM – 5:00 AM CEST
  * Saturday, July 19, 2025 01:00 – 03:00 UTC
* AU Instance:
  * Date: Sunday, July 20, 2025 2:00 AM – 4:00 AM AEST
  * Saturday, July 19, 2025 16:00 – 18:00 UTC

#### Updates

You can monitor live updates and service status at: [https://status.rewst.io/](https://status.rewst.io/)

#### Need help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Resolved: Performance degradation due to memory exhaustion - US region June 6th, 2025</summary>

On June 6, 2025, from 8:15 AM to 10:00 AM EDT, we detected that workflow processing in Rewst was experiencing significant delays in the US region. The issue has since been resolved, and workflows are now processing normally.&#x20;

We appreciate your patience as we continue to strengthen our systems. Our team has taken steps to improve monitoring and infrastructure responsiveness to help prevent similar incidents across all regions in the future.

#### Updates

For ongoing status updates, please visit: [https://status.rewst.io/](https://status.rewst.io/)

#### Need Help?

Rewst support is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)

#### Create a Ticket

[Email the team](mailto:roc@rewst.io)  and someone will be in touch ASAP.

</details>

<details>

<summary>⚠️ Issues with Sherweb service provider API - April 15th, 2025</summary>

We are currently experiencing issues with the Sherweb Service Provider API, which is impacting functionality in Sherweb-related integrations. Our team is in active communication with Sherweb to better understand the root cause and work toward a resolution. We'll provide updates as more information becomes available.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [Email the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Issues with workflow processing - April 11th, 2025</summary>

On April 11 at 1:30 ET, we detected some functionalities within Rewst are currently impaired. Users are experiencing issues related to multi-level default values not properly populating. This is primarily being experienced with certain ITGlue functionalities. We have identified a fix and are rolling it out on a region-by-region basis.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [Email the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Resolved: Integration authentication failures - April 9th, 2025</summary>

On April 9th, Our monitoring system detected that authentication for some integrations in Rewst are experiencing failures. We are currently investigating the issue and will provide more information as soon as it is available.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [Email the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Resolved: Interrupted workflow execution in US instance - April 4th, 2025</summary>

On April 4, Rewst identified an issue that interrupted workflow execution in the US instance from 2:30 PM EDT to 2:45 PM EDT. Running workflows may have been interrupted and may need to be restarted.&#x20;

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [Email the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Resolved: Service degradation in US instance - April 3rd, 2025</summary>

As of April 3, 2025 at 5:00 PM EDT, Rewst has identified an issue that is causing service degradation in the US instance. We are actively working to resolve the issue. We will update you when a permanent fix is implemented.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ New Crates available with old Crate deprecation - March 26th, 2025</summary>

We're thrilled to announce the launch of four new crates in the Crate Marketplace:

* Microsoft: User Onboarding
* Google: User Onboarding
* Microsoft: User Offboarding
* Google: User Offboarding

These new crates come with the latest features and enhancements to make your user onboarding and user offboarding processes smoother and more efficient. **The following crates will no longer be available in the Crate Marketplace as of April 4, 2025**:

* Rewst: User Onboarding
* User Offboarding v2
* User Offboarding Crate

While these crates will still function, they will not receive any additional feature enhancements. We recommend migrating to the new crates listed above to take advantage of the latest updates.\
For crate migration assistance, please reference the [migrating-between-crate-versions.md](../../documentation/crates/migrating-between-crate-versions.md "mention") and [crate-deprecation-faq.md](../../prebuilt-automations/crates/crate-deprecation-faq.md "mention").

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ App Builder incorrectly displays HTML containers - March 14th, 2025</summary>

On Friday, March 14th, some Rewst users experienced disruptions with App Builder where their HTML containers were not displaying correctly. The issue has been identified and a resolution has been implemented.&#x20;

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Routine system maintenance - March 8th, 2025</summary>

We will be performing maintenance on: **Saturday**, **March 8th, 2025 from 1000 - 1300 EST (1500 – 1800 UTC).**

You may experience periodic service interruptions during the maintenance window across all regions.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Routine system maintenance for UK - March 7th / March 8th, 2025</summary>

We will be performing maintenance on:\
**March 7th, 2025** 2100–2300 EST / March 8th, 2025 0200–0400 UTC

No outages or end user impacts are expected. Thank you for your understanding.&#x20;

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Routine system maintenance - February 8th and 15th, 2025</summary>

We will be performing maintenance on:\
**Saturday**, February 8th, 2025 from 2:00PM – 4:00PM EST (19:00–21:00 UTC)\
**Saturday**, February 15th, 2025 from 2:00PM – 4:00PM EST (19:00–21:00 UTC)

Please note: You may experience periodic service interruptions during the maintenance windows for instances hosted in the US region.

If you have any urgent concerns, please contact your support team.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>

<details>

<summary>⚠️ Transition to OAuth 2.0 authentication for Pax8 APIs - January 7th, 2025</summary>

As of **January 31st, 2025**, Pax8 will retire API Key requests as a method of authentication. To ensure uninterrupted access to the Pax8 integration, Rewst customers are required to transition to OAuth 2.0 for API authentication.

To continue using the Pax8 integration with Rewst, you will need to transition to OAuth 2.0 authentication before January 31st, 2025. For information on how to update the configuration in Rewst, check this page: [Broken link](/broken/pages/JTewUNxCZGcGg3FdP57W "mention")

This transition to OAuth 2.0 provides enhanced security, streamlined user experience, and improved API access management.&#x20;

If you have any questions or need assistance with the transition, our team is here to help.

* **Discord** - The ROC is always available here: [https://discord.gg/rewst](https://discord.gg/rewst)
* **Create a Ticket** - [E-mail the team](mailto:roc@rewst.io) and someone will be in touch ASAP!

</details>
