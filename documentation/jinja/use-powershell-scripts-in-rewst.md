# Use PowerShell scripts in Rewst

Rewst gives you two ways to work with PowerShell:

1. [**PowerShell Interpreter (Beta)**](https://docs.rewst.help/documentation/rewst-tools/powershell-interpreter) – Write and run PowerShell inline in workflows using the `#ps` block, powered by secure Azure-hosted Function Apps.
2. Stored PowerShell scripts – Run traditional PowerShell scripts on external endpoints via RMMs, typically using prebuilt automations or webhooks.

This document describes the second method — using stored PowerShell scripts to execute on endpoints via Rewst automations.

### Execute PowerShell on endpoints using stored scripts

Rewst supports running PowerShell on devices, typically through your RMM, by storing and executing scripts via webhooks. This is useful for direct device interaction such as installing software or gathering logs.

### How it works

1. Store a PowerShell script in **Automations > Scripts**.
2. The script is assigned a unique URL ending in a GUID.
3. Call this script from a workflow or prebuilt automation, like **Run PowerShell Script on Selected Devices**.
4. Include a block in the script to send results back to Rewst.

### Return data from the script

Use `ConvertTo-Json` and `Invoke-WebRequest` to send structured data back to Rewst:

```powershell
$results = @{
  hostname = $env:COMPUTERNAME
  user     = $env:USERNAME
}
$json = $results | ConvertTo-Json
Invoke-WebRequest -Uri "{{ CTX.webhook_url }}" -Method POST -Body $json -ContentType "application/json"

```

The data returned won’t affect execution, but it enables further automation based on the results.

<figure><img src="../../.gitbook/assets/image (54) (3).png" alt=""><figcaption></figcaption></figure>

### Pass dynamic parameters with Jinja

Whether you're using the interpreter or calling a stored script, you can pass variables using Jinja.

#### Example: Pass a username

```powershell
$username = "{{ CTX.user.name }}"
$username.ToUpper()

```

This allows workflows to dynamically pass values into your scripts without hardcoding. Note that this example will only function correctly when the script is saved as a template.

### Use in Crates

For endpoint scripts, Rewst provides prebuilt automations such as the **Run PowerShell Script on Selected Devices** Crate.

<figure><img src="../../.gitbook/assets/Screenshot 2025-05-28 at 11.21.04 AM.png" alt=""><figcaption></figcaption></figure>

These use subworkflows to loop through device lists and run your stored script against each one.
