﻿---
title: Set-CsTrunkConfiguration
TOCTitle: Set-CsTrunkConfiguration
ms:assetid: 18152388-68de-4a6b-b5a1-248534ecde72
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Gg398238(v=OCS.15)
ms:contentKeyID: 48183516
ms.date: 07/23/2014
mtps_version: v=OCS.15
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic" data-xmlns="http://www.w3.org/1999/xhtml" data-msxsl="urn:schemas-microsoft-com:xslt" data-cs="http://msdn.microsoft.com/en-us/">

<div data-asp="http://msdn2.microsoft.com/asp">

# Set-CsTrunkConfiguration

</div>

<div id="mainSection">

<div id="mainBody">

<span> </span>

_**Topic Last Modified:** 2013-03-25_

Modifies an existing trunk configuration that describes the settings for a trunking peer entity such as a public switched telephone network (PSTN) gateway, IP-public branch exchange (PBX), or Session Border Controller (SBC) at the service provider. This cmdlet was introduced in Lync Server 2010.

<div>

## Syntax

    Set-CsTrunkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsTrunkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-ConcentratedTopology <$true | $false>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Enable3pccRefer <$true | $false>] [-EnableBypass <$true | $false>] [-EnableFastFailoverTimer <$true | $false>] [-EnableLocationRestriction <$true | $false>] [-EnableMobileTrunkSupport <$true | $false>] [-EnableOnlineVoice <$true | $false>] [-EnablePIDFLOSupport <$true | $false>] [-EnableReferSupport <$true | $false>] [-EnableRTPLatching <$true | $false>] [-EnableSessionTimer <$true | $false>] [-EnableSignalBoost <$true | $false>] [-Force <SwitchParameter>] [-ForwardCallHistory <$true | $false>] [-ForwardPAI <$true | $false>] [-MaxEarlyDialogs <UInt32>] [-NetworkSiteID <String>] [-OutboundCallingNumberTranslationRulesList <PSListModifier>] [-OutboundTranslationRulesList <PSListModifier>] [-PstnUsages <PSListModifier>] [-RemovePlusFromUri <$true | $false>] [-RTCPActiveCalls <$true | $false>] [-RTCPCallsOnHold <$true | $false>] [-SipResponseCodeTranslationRulesList <PSListModifier>] [-SRTPMode <Required | Optional | NotSupported>] [-WhatIf [<SwitchParameter>]]

</div>

<div>

## Examples

<div>

## EXAMPLE 1

This example modifies a trunk configuration with the Identity site:Redmond to enable media bypass. Media bypass is enabled by assigning the value $True to the EnableBypass parameter. The remaining properties for this configuration will retain their existing values.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnableBypass $True

</div>

<div>

## EXAMPLE 2

This example modifies an outbound translation rule defined for the trunk configuration with the Identity site:Redmond. Notice that we don’t actually make a call to the **Set-CsTrunkConfiguration** cmdlet to make this change. Changes made using the **Set-CsOutboundTranslationRule** cmdlet will be automatically reflected in the trunk configuration with an Identity matching the scope portion of the Identity of the outbound translation rule.

    Set-CsOutboundTranslationRule -Identity site:Redmond/OTR1 -Translation '$1'

</div>

<div>

## EXAMPLE 3

Example 3 sets the SRTPMode for all trunk configurations defined at the site scope to Optional. The first part of the command is a call to the **Get-CsTrunkConfiguration** cmdlet that uses the Filter parameter to retrieve all trunk configurations with an Identity beginning with site:, meaning all trunk configurations defined at the site level. This collection of configurations is then piped to the **Set-CsTrunkConfiguration** cmdlet, which sets the SRTPMode property of each to Optional.

    Get-CsTrunkConfiguration -Filter site:* | Set-CsTrunkConfiguration -SRTPMode "Optional"

</div>

<div>

## EXAMPLE 4

Example 4 modifies a trunk configuration with the Identity site:Redmond to enable PIDF-LO support. By default the EnablePIDFLOSupport parameter is False. In this example we’ve set the value to True to enable location support for emergency calls. You must set EnablePIDFLOSupport to True in order for location information to be sent to the trunk by the outbound routing application.

    Set-CsTrunkConfiguration -Identity site:Redmond -EnablePIDFLOSupport $True

</div>

</div>

<div>

## Detailed Description

Use this cmdlet to modify a trunking configuration applicable to PSTN gateway entities. Each configuration contains specific settings for a trunking peer entity such as a PSTN gateway, IP-PBX, or SBC at the service provider. These settings configure such things as whether media bypass is enabled on this trunk, whether real-time transport control protocol (RTCP) packets are sent under certain conditions, and whether to require secure real-time protocol (SRTP) encryption.

Who can run this cmdlet: By default, members of the following groups are authorized to run the **Set-CsTrunkConfiguration** cmdlet locally: RTCUniversalServerAdmins. To return a list of all the role-based access control (RBAC) roles this cmdlet has been assigned to (including any custom RBAC roles you have created yourself), run the following command from the Windows PowerShell prompt:

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsTrunkConfiguration"}

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
<td><p><em>ConcentratedTopology</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>The value of this parameter determines whether there is a well-known media termination point. (An example of a well-known media termination point would be a PSTN gateway where the media termination has the same IP as the signaling termination.) Set this value to False if the trunk does not have a well-known media termination point.</p>
<p>Default: True</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Prompts you for confirmation before executing the command.</p></td>
</tr>
<tr class="odd">
<td><p><em>Description</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>A string describing the purpose of the trunk configuration.</p></td>
</tr>
<tr class="even">
<td><p><em>Enable3pccRefer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Indicates whether the 3pcc protocol can be used to allow transferred calls to bypass the hosted site. 3pcc is also known as &quot;third party control,&quot; and occurs when a third-party is used to connect a pair of callers (for example, an operator placing a call from person A to person B). The REFER method is a standard SIP method which indicates that the recipient should contact a third-party by using information supplied by the sender. The default value is False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBypass</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>The value of this parameter determines whether media bypass is enabled for this trunk. Set this value to True to enable bypass. Note that in order for the media bypass to work successfully, certain capabilities must be supported by PSTN gateways, SBCs, and PBXs, including:</p>
<p>- The ability to receive forked responses to an Invite.</p>
<p>- Lync Server clients and the media termination point must be able to communicate directly without going through a Mediation Server.</p>
<p>- The gateway subnet must be defined as being at the same site as the client’s subnet or, if at a different site, the sites must not be separated by WAN links with constrained bandwidth.</p>
<p>Media bypass can be enabled only under the following circumstances:</p>
<p>- The ConcentratedTopology parameter is set to True</p>
<p>- The EnableReferSupport parameter is set to False and RTCPActiveCalls and RTCPCallsOnHold are set to False, or EnableReferSupport is set to True</p>
<p>Note that if EnableBypass is True and EnableReferSupport is False, bypass calls that are subsequently transferred will become non-bypass.</p>
<p>For media bypass to work for a particular trunk, it needs to be enabled globally and also for the trunk in question. Use the <strong>New-CsNetworkMediaBypassConfiguration</strong> cmdlet to enable media bypass globally.</p>
<p>Default: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableFastFailoverTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>When set to True, outbound calls that are not answered by the gateway within 10 seconds will be routed to the next available trunk; if there are no additional trunks then the call will automatically be dropped. In an organization with slow networks and gateway responses, that could potentially result in calls being dropped unnecessarily.</p>
<p>The default value is True.</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationRestriction</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>When set to True, location-based voice routing will be enabled for calls passing through the SIP trunks managed by the specified collection of SIP trunk configuration settings. With location-based voice routing, the locations of both the user making the call and the user receiving the call are taken into account when calls are routed. If this property is set to True (the default value is False) then you should also set the NetworkSiteId property.</p></td>
</tr>
<tr class="even">
<td><p><em>EnableMobileTrunkSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Defines whether the service provider is a mobile carrier.</p>
<p>Default: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableOnlineVoice</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Indicates whether the SIP trunks support online voice. With online voice, users have an on-premises Lync Server account but have their voicemail hosted by Lync Online. The default value is False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>EnablePIDFLOSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Defines whether to route emergency calls with Presence Information Data Format Location Object (PIDF-LO) through the defined gateway. Set this parameter to True if emergency calls are to be routed to a certified emergency services provider. (The location will be transmitted with the call.)</p>
<p>Default: False</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableReferSupport</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Defines whether this trunk supports receiving Refer requests from the Mediation Server.</p>
<p>Media bypass can be enabled only under the following circumstances:</p>
<p>- The ConcentratedTopology parameter is set to True</p>
<p>- The EnableReferSupport parameter is set to False and RTCPActiveCalls and RTCPCallsOnHold are set to False, or EnableReferSupport is set to True</p>
<p>Note that if EnableBypass is True and EnableReferSupport is False, bypass calls that are subsequently transferred will become non-bypass.</p>
<p>Default: True</p></td>
</tr>
<tr class="even">
<td><p><em>EnableRTPLatching</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Indicates whether or not the SIP trunks support RTP latching. RTP latching is a technology that enables RTP/RTCP connectivity through a NAT (network address translator) device or firewall. The default value is False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableSessionTimer</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Specifies whether the session timer is enabled. Session timers are used to determine whether a particular session is still active.</p>
<p>Note that even if this parameter is set to False, session timers can be applicable if the remote connection has session timer enabled. In such a case, the Mediation Server will reply to session timer probes from the remote entity.</p>
<p>Default: False</p></td>
</tr>
<tr class="even">
<td><p><em>EnableSignalBoost</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>When this parameter is set to True the PSTN gateway, IP-PBX, or SBC at the service provider will boost the audio volume in voice streams that are sent to the Mediation Server or Lync Server clients. If this value is set to False, audio will be boosted either at the Mediation Server (for non-bypass calls) or in Lync Server clients (for bypass calls).</p>
<p>Default: False</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Suppresses any confirmation prompts that would otherwise be displayed before making changes.</p></td>
</tr>
<tr class="even">
<td><p><em>ForwardCallHistory</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Indicates whether call history information will be forwarded through the trunk. The default value is False ($False).</p></td>
</tr>
<tr class="odd">
<td><p><em>ForwardPAI</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Indicates whether the P-Asserted-Identity (PAI) header will be forwarded along with the call. The PAI header provides a way to verify the identity of the caller. The default value is False ($False).</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Optional</p></td>
<td><p>XdsIdentity</p></td>
<td><p>A unique identifier that includes the scope of the trunk configuration. Trunk configurations can exist at the Global scope, the Site scope, or at the Service scope for a PSTN Gateway service. For example, site:Redmond (for site) or PstnGateway:Redmond.litwareinc.com (for service).</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>Optional</p></td>
<td><p>TrunkConfiguration</p></td>
<td><p>Allows you to pass a reference to an object to the cmdlet rather than set individual parameter values.</p>
<p>This parameter requires an object of type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration, which can be retrieved by calling the <strong>Get-CsTrunkConfiguration</strong> cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxEarlyDialogs</em></p></td>
<td><p>Optional</p></td>
<td><p>UInt32</p></td>
<td><p>The maximum number of forked responses a PSTN gateway, IP-PBX, or SBC at the service provider can receive to an Invite that it sent to the Mediation Server.</p>
<p>Default: 20</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>Optional</p></td>
<td><p>String</p></td>
<td><p>Site ID of the network site associated with the collection of trunk configuration settings. If the EnableLocationRestriction property is set to True then location-based voice routing through this trunk will be managed by using the settings configured for the specified site. Network site IDs can be retrieved by using this command:</p>
<p>Get-CsNetworkSite | Select NetworkSiteID</p></td>
</tr>
<tr class="even">
<td><p><em>OutboundCallingNumberTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection of outbound calling number translation rules assigned to the trunk. You can retrieve information about the available rules by running this command:</p>
<p>Get-CsOutboundCallingNumberTranslationRule</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>A collection of phone number translation rules that apply to calls handled by Outbound Routing (calls routed to PBX or PSTN destinations).</p>
<p>While this list and these rules can be modified directly with this cmdlet, we recommend that you modify the outbound translation rules with the <strong>Set-CsOutboundTranslationRule</strong> cmdlet. The <strong>Set-CsOutboundTranslationRule</strong> cmdlet will modify the rule, and these modifications will be automatically reflected in the trunk configuration. To modify the trunk configuration by adding a new outbound translation rule, call the <strong>New-CsOutboundTranslationRule</strong> cmdlet; the new rule will be added to the trunk configuration with the matching scope.</p></td>
</tr>
<tr class="even">
<td><p><em>PstnUsages</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>Collection of PSTN usages assigned to the trunk. You can retrieve information about the available usages by running this command:</p>
<p>Get-CsPstnUsage</p></td>
</tr>
<tr class="odd">
<td><p><em>RemovePlusFromUri</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>Setting this parameter to True will cause the Mediation Server to remove leading plus signs (+) from Uniform Resources Identifiers (URIs) before sending them on to the service provider.</p>
<p>Default: False</p></td>
</tr>
<tr class="even">
<td><p><em>RTCPActiveCalls</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>This parameter determines whether RTCP packets are sent from the PSTN gateway, IP-PBX, or SBC at the service provider for active calls. An active call in this context is a call where media is allowed to flow in at least one direction. If RTCPActiveCalls is set to True, the Mediation Server or Lync Server client can terminate a call if it does not receive RTCP packets for a period exceeding 30 seconds.</p>
<p>Note that disabling the checks for received RTCP media for active calls in Lync Server elements removes an important safeguard for detecting a dropped peer and should be done only if necessary.</p>
<p>Default: True</p></td>
</tr>
<tr class="odd">
<td><p><em>RTCPCallsOnHold</em></p></td>
<td><p>Optional</p></td>
<td><p>Boolean</p></td>
<td><p>This parameter determines whether RTCP packets continue to be sent across the trunk for calls that have been placed on hold and no media packets are expected to flow in either direction. If Music on Hold is enabled at either the Lync Server client or the trunk, the call will be considered to be active and this property will be ignored. In these circumstances use the RTCPActiveCalls parameter.</p>
<p>Note that disabling the checks for received RTCP media for active calls in Lync Server elements removes an important safeguard for detecting a dropped peer and should be done only if necessary.</p>
<p>Default: True</p></td>
</tr>
<tr class="even">
<td><p><em>SipResponseCodeTranslationRulesList</em></p></td>
<td><p>Optional</p></td>
<td><p>PSListModifier</p></td>
<td><p>A list of SIP response code translation rules that apply to response codes received from a PSTN gateway, IP-PBX, or SBC at the service provider. These rules allow the administrator to map SIP response codes with values between 400 and 699 received over a trunk to new values more consistent with Lync Server.</p>
<p>You can create this list and corresponding rules directly with this cmdlet. However, we recommend that you create the SIP response code translation rules by calling the <strong>New-CsSipResponseCodeTranslationRule</strong> cmdlet. That cmdlet will create the rule and assign it to the trunk configuration with the matching scope.</p></td>
</tr>
<tr class="odd">
<td><p><em>SRTPMode</em></p></td>
<td><p>Optional</p></td>
<td><p>SRTPMode</p></td>
<td><p>The value of this parameter determines the level of support for SRTP to protect media traffic between the Mediation Server and the PSTN gateway, IP-PBX, or SBC at the service provider. For media bypass cases, this value must be compatible with the EncryptionLevel setting in the media configuration. Media configuration is set by using the <strong>New-CsMediaConfiguration</strong> cmdlet and the <strong>Set-CsMediaConfiguration</strong> cmdlet.</p>
<p>Valid values:</p>
<p>- Required: SRTP encryption must be used.</p>
<p>- Optional: SRTP will be used if the service provider supports it.</p>
<p>- NotSupported: SRTP encryption is not supported and therefore will not be used.</p>
<p>Note: SRTPMode is used only if the gateway is configured to use Transport Layer Security (TLS). If the gateway is configured with Transmission Control Protocol (TCP) as the transport, SRTPMode is internally set to NotSupported.</p>
<p>Default: Required</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>Optional</p></td>
<td><p>SwitchParameter</p></td>
<td><p>Describes what would happen if you executed the command without actually executing the command.</p></td>
</tr>
</tbody>
</table>


</div>

<div>

## Input Types

Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration object. Accepts pipelined input of trunk configuration objects.

</div>

<div>

## Return Types

This cmdlet does not return a value; it modifies an object of type Microsoft.Rtc.Management.WritableConfig.Settings.TrunkConfiguration.TrunkConfiguration.

</div>

<div>

## See Also


[New-CsTrunkConfiguration](new-cstrunkconfiguration.md)  
[Remove-CsTrunkConfiguration](remove-cstrunkconfiguration.md)  
[Get-CsTrunkConfiguration](get-cstrunkconfiguration.md)  
[Test-CsTrunkConfiguration](test-cstrunkconfiguration.md)  
[New-CsOutboundTranslationRule](new-csoutboundtranslationrule.md)  
[Set-CsOutboundTranslationRule](set-csoutboundtranslationrule.md)  
  

</div>

</div>

<span> </span>

</div>

</div>

</div>

