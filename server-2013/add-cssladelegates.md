﻿---
title: Add-CsSlaDelegates
TOCTitle: Add-CsSlaDelegates
ms:assetid: 2d446e73-82f1-4542-8df8-3ff982406ffa
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Mt703199(v=OCS.15)
ms:contentKeyID: 72808510
ms.date: 04/12/2016
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Add-CsSlaDelegates

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2016-04-12_

Use the **Add-CsSlaDelegates** cmdlet to add a delegate to a shared number in Shared Line Appearance (SLA). A shared number in SLA is an Enterprise Voice user that is capable of receiving multiple calls at a time and forwarding them to its delegates, who answer the call.

<div>

## Syntax

    Add-CsSlaDelegates -Identity <UserIdParameter> -Delegate <Uri> [-Confirm [<SwitchParameter>]] [-PassThru <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

</div>

<span id="Examples"></span>

<div>

## Examples

<div>

## Example 1

This example adds a delegate “delegate\_1@contosohealth.com” to an SLA configuration identified by “emergency”.

    Add-CsSlaDelegates -Identity emergency -Delegate sip:delegate_1@contosohealth.com

</div>

</div>

<span id="DetailedDescription"></span>

<div>

## Detailed Description

SLA is a feature in Skype for Business (SfB) for handling multiple calls on a specific number called a shared number. SLA can configure any enterprise voice enabled SfB user as a shared number with multiple lines to respond to multiple calls. The calls are not actually received on the shared number, instead they are forwarded to users that act as delegates for the shared number. Any one of the delegates can pick up the call while the rest of the delegates get a notification on their phone about who picked up the call and which line has become busy as a result. Both the number of lines and the delegates are configurable for a shared number in SLA. In addition, advanced options such as BusyOption (what happens in a situation when all lines are busy) and MissedCallOption (the case in which none of the delegates pick up a call) can also be configured for a shared number.

The **Add-CsSlaDelegates** cmdlet provides a way to retrieve a shared number configuration.

<div class="alert">


> [!NOTE]
> Logging in with the account created for the SLA number is not supported. Using the SLA number account with any device or Desktop Client can result in unpredictable behavior. It is not necessary to use that account for the Shared Line Appearance feature to function.



</div>

By default, members of the RTCUniversalServerAdmins group are authorized to run the **Add-CsSlaDelegates**. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

    Get-CsAdminRole | Where-Object {$_.Cmdlets -match "Add-CsSlaDelegates"}

</div>

<div>

## Parameters


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Required</th>
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Delegate</em></p></td>
<td><p>Required</p></td>
<td><p>System.Uri</p></td>
<td><p>Specifies a user that will respond to a call on the shared number specified by the <em>Identity</em> parameter. This parameter requires a valid sip address.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.AD.UserIdParameter</p></td>
<td><p>Indicates the identity of the shared number to which the delegate will be added.</p>
<p>UNRESOLVED_TOKENBLOCK_VAL(PS_PD_User_Updated_Specification)</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="even">
<td><p><em>PassThru</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>UNRESOLVED_TOKEN_VAL(PS_PD_Passthru_Generic_CurrentObjects)</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<span id="InputTypes"></span>

<div>

## Input Types

None.

</div>

<span id="ReturnTypes"></span>

<div>

## Return Types

The **Add-CsSlaDelegates** cmdlet returns a Microsoft.Rtc.Management.SlaConfiguration object.

</div>

</div>

<span> </span>

</div>

</div>

</div>

