---
title: Get local capabilities
titleSuffix: An Azure Communication Services article
description: Use Azure Communication Services SDK to get capabilities of the local user in a call.
author: elavarasid
ms.author: elavarasid
ms.service: azure-communication-services
ms.subservice: calling
ms.topic: how-to
ms.date: 06/20/2025
ms.custom: template-how-to
zone_pivot_groups: acs-plat-web-ios-android-windows
---

# Get local capabilities

During a call, does a participant have permission to turn on video, turn on mic, or share screen?

These permissions are examples of participant capabilities that you can learn from the capabilities API operation. You can use capabilities to build a user interface that only shows the buttons related to the actions the local user can perform.

## Prerequisites

- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- A deployed Communication Services resource. [Create a Communication Services resource](../../quickstarts/create-communication-resource.md).
- A user access token to enable the calling client. For more information, see [Create and manage access tokens](../../quickstarts/identity/access-tokens.md).
- Optional: Complete the quick start to [add voice calling to your application](../../quickstarts/voice-video-calling/getting-started-with-calling.md).

::: zone pivot="platform-web"
[!INCLUDE [Capabilities JavaScript](./includes/capabilities/capabilities-web.md)]
::: zone-end

::: zone pivot="platform-android"
[!INCLUDE [Capabilities Android](./includes/capabilities/capabilities-android.md)]
::: zone-end

::: zone pivot="platform-windows"
[!INCLUDE [Capabilities Windows](./includes/capabilities/capabilities-windows.md)]
::: zone-end

::: zone pivot="platform-ios"
[!INCLUDE [Capabilities iOS](./includes/capabilities/capabilities-ios.md)]
::: zone-end

## Supported call types

The following tables define the ability to get capabilities using the Azure Communication Services Calling SDK.

### Identities and call types

| Identities | Teams meeting | Room | 1:1 call | Group call | 1:1 Teams interop call | Group Teams interop call |
| --- | --- | --- | --- | --- | --- | --- |
| Communication Services user | ✔️ | ✔️ |  |  |  |  |
| Microsoft 365 user | ✔️ | ✔️ |  |  |  |  |

## Reasons

The following table provides additional information about why action isn't available and provides tips how to make the action available. 

| Reason | Description | Resolution |
| --- | --- | --- |
| Capable | Action is enabled. | |
| CapabilityNotApplicableForTheCallType | Call type blocks the action. | Consider other type of call if you need this action. The call types are: 1:1 call, group call, 1:1 Teams interop call, 1:1 Teams interop group call, Room, and Meeting. |
| ClientRestricted | The runtime environment is blocking this action | Unblock the action on your device by changing operating system, browsers, platform, or hardware. You can find supported environment in our documentation. |
| UserPolicyRestricted | Microsoft 365 user's policy blocks the action. | Enable this action by changing policy that is assigned to the organizer of the meeting, initiator of the call or Microsoft 365 user using ACS SDK. The target user depends on the type of action. Learn more about Teams policy in Teams. Teams administrator can change policies. |
| RoleRestricted | Assigned role blocks the action. | Promote user to different role to make the action available. |
| FeatureNotSupported | The capabilities feature isn't supported in this call type. | Let us know in Azure Feedback channel that you would like to have this feature available for this call type. |
| MeetingRestricted | Teams meeting option blocks the action. | Teams meeting organizer or co-organizer needs to change meeting option to enable this action. |
| NotInitialized | The capabilities feature isn't initialized yet. | Subscribe to event `capabilitiesChanged` on `this.call.feature(Features.Capabilities)` to know when capability is initialized. |
| NotCapable | User type blocks the action. | The action is only enabled for specific identities. Enable this action by using Microsoft 365 identity. |
| TeamsPremiumLicenseRestricted | Microsoft 365 user needs to have Teams Premium license assigned. | Enable this action by assigning Teams Premium license to the Teams meeting organizer or the Microsoft 365 user using SDK. The target user depends on the type of action. Microsoft 365 admin can assign required license. |
| ExplicitConsentRequired | Consent is required to allow the action. | Provide the consent for recording or transcription by calling method `grantTeamsConsent()` under `this.call.feature(Features.Recording)` or `this.call.feature(Features.Transcription)` .|

## Next steps

- [Learn how to manage video](./manage-video.md)
- [Learn how to manage calls](./manage-calls.md)
- [Learn how to record calls](./record-calls.md)
