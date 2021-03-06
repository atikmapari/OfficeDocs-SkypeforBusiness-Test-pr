﻿---
title: Remove-CsPublicProvider
TOCTitle: Remove-CsPublicProvider
ms:assetid: b9eec2f4-cf36-41b7-8023-67790cc8d4cd
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg412906(v=OCS.15)
ms:contentKeyID: 48185219
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Remove-CsPublicProvider

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-03-07_

Removes a public provider configured for use in your organization. A public provider is an organization that provides instant messaging (IM), presence, and related services to the general public. Lync Server ships with three public providers configured but not enabled: Yahoo\!, AIM (AOL), and Messenger (MSN). This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Remove-CsPublicProvider -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

Example 1 deletes the public provider with the Identity Messenger. After this command has completed, Messenger will no longer appear in the list of configured public providers; at that point, the only way to re-establish federation with Messenger is to re-create the provider.

    Remove-CsPublicProvider -Identity "Messenger"

</div>

<div>

## EXAMPLE 2

Example 2 deletes all the public providers configured for use in the organization. To do this, the command first uses the **Get-CsPublicProvider** cmdlet to return a collection of all the public providers currently configured for use. This collection is then piped to the **Remove-CsPublicProvider** cmdlet, which, in turn, deletes each provider in the collection.

    Get-CsPublicProvider | Remove-CsPublicProvider

</div>

<div>

## EXAMPLE 3

In Example 3, all the public providers that are currently disabled are removed from the set of configured pubic providers. To carry out this task, the command first uses the **Get-CsPublicProvider** cmdlet to return a collection of all the public providers currently configured for use. This collection is piped to the **Where-Object** cmdlet, which selects only those providers where the Enabled property is equal to False. That filtered collection is then piped to the **Remove-CsPublicProvider** cmdlet, which deletes all the items in the collection.

    Get-CsPublicProvider | Where-Object {$_.Enabled -eq $False} | Remove-CsPublicProvider

</div>

</div>

<div>

## Detailed Description

Federation is a means by which two organizations can set up a trust relationship that facilitates communication between the two groups. When a federation has been established, users in the two organizations can send each other instant messages, subscribe for presence notifications, and otherwise communicate with one another using SIP applications such as Lync 2013. Lync Server allows for three types of federation: 1) direct federation between your organization and another; 2) federation between your organization and a public provider; and, 3) federation between your organization and a third-party hosting provider.

A public provider is an organization which provides SIP communication services for the general public. When you establish a federation relationship with a public provider, you effectively establish federation with any user who has an account hosted by that provider. For example, if you federate with Messenger (MSN), then your users will be able to exchange instant messages and presence information with anyone who has a Messenger instant messaging account.

In order to federate with a public provider you need to create and enable a new public provider. (In addition, the public provider will need to create a federation relationship with you.) If you decide later on to terminate this relationship, you can use the **Remove-CsPublicProvider** cmdlet to delete the public provider. When you delete a public provider, the provider is removed from your list of federated partners; at that point, the only way to re-establish the relationship is to re-create the provider. If you want to temporarily suspend a relationship, use the **Disable-CsPublicProvider** cmdlet instead. When a public provider is disabled the provider is not deleted from the list of federated partners; instead, the provider is simply marked as disabled and communication between your organization and that provider is suspended. To re-establish the relationship you can use the **Enable-CsPublicProvider** cmdlet to re-enable the provider.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Remove-CsPublicProvider** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsPublicProvider"}

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
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>Unique identifier for the public provider to be removed. The Identity typically the name of the website providing the services (for example, Yahoo!; AOL; MSN; etc.).</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses the display of any non-fatal error message that might occur when running the command.</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider object. The **Remove-CsPublicProvider** cmdlet accepts pipelined instances of the public provider object.

</div>

<div>

## Return Types

None. Instead, the cmdlet deletes instances of the Microsoft.Rtc.Management.WritableConfig.Settings.Edge.DisplayPublicProvider object.

</div>

<div>

## See Also


[Disable-CsPublicProvider](disable-cspublicprovider.md)  
[Enable-CsPublicProvider](enable-cspublicprovider.md)  
[Get-CsPublicProvider](get-cspublicprovider.md)  
[New-CsPublicProvider](new-cspublicprovider.md)  
[Set-CsPublicProvider](set-cspublicprovider.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

