# Incoming and outgoing domains and IPs - Rewst Classic

{% hint style="warning" %}
These domains and addresses apply only to the Rewst Classic product, not our new Rewst product. For domain and address info for new Rewst, see our guidance [here](https://docs.rewst.help/rewst-documentation/security/security-policy).&#x20;
{% endhint %}

## **Outgoing IP addresses**

Rewst Classic uses static NAT Gateway IPs for outbound connections from our services hosted in AWS. These IPs should be included in any necessary allow lists for outbound connections.

### North America

* US
  * `13.58.15.14`
  * `18.218.107.198`
  * `3.139.170.31`

### Europe

* UK
  * `18.132.221.226`
  * `18.171.196.2`
  * `3.9.62.134`
* DE
  * `3.67.166.23`
  * `3.69.14.222`
  * `3.76.128.23`

### Australia

* `13.210.158.91`
* `13.237.143.171`
* `52.65.55.149`

## **Hostnames with dynamic IPs**

For the following services, Rewst employs application load balancers, resulting in dynamic IP addresses. We recommend using DNS names when adding these services to your allow list.

### **North America**

* US
  * `app.rewst.io`: Front-end web application for user logins.
  * `engine.rewst.io`: Back-end application handling workflow execution, including webhooks.
  * `api.rewst.io`: API for app and engine communication.

### **Europe**

* UK
  * `app.eu.rewst.io`: Front-end web application for user logins.
  * `engine.eu.rewst.io`: Back-end application handling workflow execution, including webhooks.
  * `api.eu.rewst.io`: API for app and engine communication.
* DE
  * `app.rewst.eu`: Front-end web application for user logins.
  * `engine.rewst.eu`: Back-end application handling workflow execution, including webhooks.
  * `api.rewst.eu`: API for app and engine communication.

### Australia

* `app.rewst.asia`: Front-end web application for user logins.
* `engine.rewst.asia`: Back-end application handling workflow execution, including webhooks.
* `api.rewst.asia`: API for app and engine communication.

### **Third-party services**

* `featureassets.org`: A Statsig API for feature flagging
* `prodregistryv2.org`: A Statsig API for feature flagging

## **Guidance for App Builder users**

### **Wildcard domains**

Rewst Classic customers can create subdomains (\*.rew.st) to host their App Builder apps. These domains are fully managed by Rewst, making them easier to set up and maintain. Depending on your integration needs, you should also include these domains in your allow lists to ensure proper connectivity.

### **Custom domains**

{% hint style="info" %}
For more on the use of custom domains with App Builder, see our documentation [here](https://docs.rewst.help/documentation/app-builder/domains#custom-subdomains).
{% endhint %}

In addition to wildcard subdomains, Rewst Classic customers can configure and use their own custom domains to host their App Builder apps. These custom domains should also be added to your allow lists as needed for integrations. Hosting apps on a domain you own helps maintain a professional and consistent brand presence for your customers and internal users.

## **Important information for RMM integrations and Agent Smith**

When Rewst Classic initiates a PowerShell task through an RMM platform, it is the endpoint located within the customer’s environment — such as a domain controller, Exchange server, or workstation at the customer’s office — that connects to a webhook. This webhook is dynamically created during the execution of the associated Rewst Classic workflow. The connection targets the dynamic hostname beginning with engine.\*, based on the customer’s region.

These webhook URLs are designed for one-time use. If a security system outside the endpoint attempts to scan, inspect, or pre-fetch the URL before the PowerShell task executes, it can consume or invalidate the link. This can prevent the customer’s device from successfully completing the connection. Examples of systems that may cause such interference include:

* ThreatLocker
* Hardware firewalls with URL filtering: e.g., Fortinet, Palo Alto Networks, SonicWall, Sophos
* Web security gateways: e.g., Cisco Umbrella, Zscaler
* DNS filtering services: e.g., DNSFilter, OpenDNS
* Proxy servers performing content or URL inspection
* Antivirus or EDR platforms with network traffic scanning features: e.g., CrowdStrike Falcon, Sophos Intercept X

It is important to note that SSL inspection or filtering performed directly on the endpoint, such as a server or workstation, generally does not cause problems. However, if SSL inspection, URL filtering, or pre-fetching occurs at the network level — for example, by a firewall, proxy, or upstream security device — it may prematurely trigger the webhook URL.

To avoid disruption, it’s recommended to configure allowlists or bypass rules in network security systems to exclude these one-time webhook URLs from scanning, pre-fetching, or blocking.

### ThreatLocker whitelisting

Depending on their level of security and permissions, ThreatLocker users may also need to click the following buttons in the ThreatLocker app to allow the server to look up the DNS hostname.

1. Click **Devices**.
2. Select the relevant row from the **Name / Operating System** column.
3. Click **Options**.
4. Use the drop-down selector to add **UseDNSCacheTooGetHostnames**.
5. Click **Save**.

<figure><img src="../.gitbook/assets/image (94).png" alt=""><figcaption></figcaption></figure>

## **Email filter considerations**

In environments where Rewst Classic webhook URLs are sent via email, such as in workflow notifications, approval requests, or alert messages, it's important to consider how email security systems interact with these links.

Many modern email protection platforms automatically scan, rewrite, or pre-fetch links to check for threats. This behavior can prematurely trigger a one-time-use webhook URL, making it unavailable when the actual endpoint tries to connect.

Examples of email security solutions that could interfere include:

* Microsoft Defender for Office 365 (Safe Links)
* Proofpoint Email Protection
* Mimecast Secure Email Gateway
* Barracuda Essentials
* Sophos Email
* Cisco Email Security Appliance (ESA)

### **Recommendations**

* Add the Rewst Engine\* Hostnames for your region in any Safe Links or URL Rewriting policies.
* Exclude Rewst Engine\* Hostnames for your region in URLs from pre-click scanning and link validation where possible.
* Review email security logs if webhook links fail immediately after being sent via email.

Taking these precautions helps ensure that webhook URLs embedded in emails are not consumed before they are properly triggered by the intended device or user action.

## **Additional domain troubleshooting**

If issues persist, it may be necessary to extend allowlisting beyond just the one-time webhook URLs. Some security systems could also interfere with broader Rewst operations by inspecting or blocking traffic to core Rewst services. In these cases, ensure that the following endpoints are allowed and not inspected or altered:

* [app.rewst.io](http://app.rewst.io)
* [api.rewst.io](http://api.rewst.io)
* .rew.st (wildcard for all Rewst App Builder subdomains)

### **Best practice**

First review logs — including firewall logs, proxy logs, endpoint protection logs, and email filtering logs — to determine whether connections or emails containing Rewst Classic webhook URLs are being blocked, inspected, or altered. Only after confirming should allowlisting or bypass rules be added.
