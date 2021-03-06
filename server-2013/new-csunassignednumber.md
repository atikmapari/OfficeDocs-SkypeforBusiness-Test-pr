﻿---
title: New-CsUnassignedNumber
TOCTitle: New-CsUnassignedNumber
ms:assetid: 81b5d355-56d4-4325-8518-653de8e1fab4
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg398651(v=OCS.15)
ms:contentKeyID: 48184665
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# New-CsUnassignedNumber

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-02-22_

Creates a new range of unassigned numbers and the routing rules that apply to those numbers. Running this cmdlet will add an entry to the unassigned number routing table. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    New-CsUnassignedNumber -AnnouncementName <String> -AnnouncementService <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    New-CsUnassignedNumber -ExUmAutoAttendantPhoneNumber <String> -Identity <XdsGlobalRelativeIdentity> -NumberRangeEnd <String> -NumberRangeStart <String> <COMMON PARAMETERS>

    COMMON PARAMETERS: -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-Priority <Int32>] [-WhatIf [<SwitchParameter>]]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

This example creates an unassigned number range with the name UNSet1. We use the NumberRangeStart (+14255551000) and NumberRangeEnd (+14255551100) parameters to define the range of unassigned numbers to which the specified announcement will apply. Finally, we specify the Announcement by first supplying the AnnouncementService parameter with the service ID of the Announcement service, and then passing the value "Welcome Announcement" to the parameter AnnouncementName. Keep in mind that an Announcement with that name must already exist in the system.

    New-CsUnassignedNumber -Identity UNSet1 -NumberRangeStart "+14255551000" -NumberRangeEnd "+14255551100" -AnnouncementService ApplicationServer:redmond.litwareinc.com -AnnouncementName "Welcome Announcement"

</div>

<div>

## EXAMPLE 2

This example creates an unassigned number range with the name UNSet2. As in Example 1 we use the NumberRangeStart (+14255552100) and NumberRangeEnd (+14255552200) parameters to define the range of unassigned numbers to which the specified announcement will apply. However, in this example, instead of using the Announcement service, this number range will use the Exchange UM Auto Attendant. (The Auto Attendant is a single number designated as the organization’s main number that guides users through voice prompts to help them reach the appropriate party.) We pass a phone number to the ExUmAutoAttendantPhoneNumber parameter to complete this command. Note that Exchange UM must be set up and this number must be an existing contact object phone number in Active Directory Domain Services. The contact must be an Auto Attendant contact (the AutoAttendant property for the contact must be True).

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234"

</div>

<div>

## EXAMPLE 3

Example 3 is almost identical to Example 2: It creates an unassigned number range with the name UNSet2. The difference in this example is that we’ve added the Priority parameter, in this case with a value of 2. This means that if an unassigned number range has been defined that overlaps this one and that number range has a higher priority (a lower priority number, such as 1), calls will be routed based on the settings for that range rather than this one.

    New-CsUnassignedNumber -Identity UNSet2 -NumberRangeStart "+14255552100" -NumberRangeEnd "+14255552200" -ExUmAutoAttendantPhoneNumber "+12065551234" -Priority 2

</div>

</div>

<div>

## Detailed Description

Unassigned numbers are phone numbers that have been assigned to an organization but that have not been assigned to specific users or phones. Lync Server can be set up to route calls to appropriate destinations when an unassigned number is called. This cmdlet creates the settings that define that routing.

Before running this cmdlet, your system must already either have Announcements defined or an Exchange Unified Messaging (UM) Auto Attendant set up. To determine whether you have Announcements, call the **Get-CsAnnouncement** cmdlet. To create a new Announcement, call the **New-CsAnnouncement** cmdlet. To check on Exchange UM Auto Attendant settings, run the **Get-CsExUmContact** cmdlet.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **New-CsUnassignedNumber** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsUnassignedNumber"}

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
<td><p><em>AnnouncementName</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The name of the Announcement that will be used to handle calls to this range of numbers.</p></td>
</tr>
<tr class="even">
<td><p><em>AnnouncementService</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The fully qualified domain name (FQDN) or service ID of the Announcement service. This parameter is required only if you have not specified a value for the ExUmAutoAttendantPhoneNumber parameter.</p></td>
</tr>
<tr class="odd">
<td><p><em>ExUmAutoAttendantPhoneNumber</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The phone number of the Exchange UM Auto Attendant to route calls in this range to. This field is required only if you are not using an Announcement Service (in which case you do not supply values for the AnnouncementService or AnnouncementName parameters). The Exchange UM Auto Attendant contact must already be set up in order to assign a value to this parameter.</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Required</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>A unique name for the range of unassigned numbers being created. All unassigned number ranges have a global scope, so the name specified here must be unique throughout the Lync Server deployment.</p></td>
</tr>
<tr class="odd">
<td><p><em>NumberRangeEnd</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The last number in the range of unassigned numbers. Must be greater than or equal to the number supplied for NumberRangeStart. To specify a range of one number, use the same number for the NumberRangeStart and NumberRangeEnd.</p>
<p>The number must match the regular expression (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. This means the number may begin with the string tel: (if you don’t specify that string it will be automatically added for you), a plus sign (+), and a digit 1 through 9. The phone number can be up to 17 digits and may be followed by an extension in the format ;ext= followed by the extension number.</p></td>
</tr>
<tr class="even">
<td><p><em>NumberRangeStart</em></p></td>
<td><p>Required</p></td>
<td><p>System.String</p></td>
<td><p>The first number in the range of unassigned numbers. Must be less than or equal to the value supplied for NumberRangeEnd.</p>
<p>The number must match the regular expression (tel:)?(\+)?[1-9]\d{0,17}(;ext=[1-9]\d{0,9})?. This means the number may begin with the string tel: (if you don’t specify that string it will be automatically added for you), a plus sign (+), and a digit 1 through 9. The phone number can be up to 17 digits and may be followed by an extension in the format ;ext= followed by the extension number.</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="odd">
<td><p><em>InMemory</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>Creates an object reference without actually committing the object as a permanent change. If you assign the output of this cmdlet called with this parameter to a variable, you can make changes to the properties of the object reference and then commit those changes by calling this cmdlet’s matching Set- cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>Priority</em></p></td>
<td><p>Optional</p></td>
<td><p>System.Int32</p></td>
<td><p>It is possible for unassigned number ranges to overlap. If a number falls within more than one range, the range with the highest priority will take effect.</p></td>
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

<div>

## Input Types

None.

</div>

<div>

## Return Types

Creates an object of type Microsoft.Rtc.Management.Voice.Helpers.DisplayAnnouncementVacantNumberRange.

</div>

<div>

## See Also


[Remove-CsUnassignedNumber](remove-csunassignednumber.md)  
[Set-CsUnassignedNumber](set-csunassignednumber.md)  
[Get-CsUnassignedNumber](get-csunassignednumber.md)  
[New-CsAnnouncement](new-csannouncement.md)  
[Get-CsAnnouncement](get-csannouncement.md)  
[Get-CsExUmContact](get-csexumcontact.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

