---
title: Enable Real Time Text
titleSuffix: An Azure Communication Services article
description: This article describes how to enable Real Time Text in your application.
author: ahammer
ms.author: adamhammer
ms.service: azure-communication-services
ms.subservice: calling
ms.topic: how-to
ms.date: 06/24/2025
ms.custom: template-how-to
zone_pivot_groups: acs-programming-languages-javascript-java-swift-csharp
---

# Enable Real Time Text (RTT)

>[!NOTE]
>RTT is an accessibility compliance requirement for voice and video platforms in the EU starting June 30, 2025. For more information, see [Directive 2019/882](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX%3A32019L0882).

Integrate Real Time Text (RTT) into your calling applications to enhance accessibility and ensure that all participants can communicate effectively during meetings.

RTT allows users who have difficulty speaking to participate actively by typing their messages, which are then broadcast in near real-time to other meeting participants. This feature operates seamlessly alongside existing captions and ensures that typed messages are promptly delivered without disrupting the flow of conversation.

## Real Time Text Feature Overview

Real Time Text (RTT) facilitates communication for users who might have difficulty speaking during calls. By enabling users to type their messages, RTT ensures that everyone in the meeting can stay engaged and informed. Messages are transmitted over Data Channels (ID 24) and are always active, appearing automatically when the first message is sent.

On supported platforms, RTT data can display alongside captions derived from Speech to Text, providing a comprehensive view of all communications during a call.

>[!NOTE]
>RTT for PSTN or Teams Interop isn't available at this time

## Naming Conventions

Different platforms might use varying terminology for RTT-related properties. The following table summarizes the differences:

| Mobile (Android/iOS) | Windows (C#)  |
| -------------------- | ------------- |
| **Type**             | **Kind**      |
| **Info**             | **Details**   |

These aliases are functionally equivalent and are used to maintain consistency across different platforms.

## RealTimeTextInfo/Details Class

The `RealTimeTextInfo` (or `RealTimeTextDetails` on Windows) class encapsulates information about each RTT message. The following table shows key properties:

| Property          | Description                                           |
| ----------------- | ----------------------------------------------------- |
| `SequenceId`      | Unique identifier for the message sequence.          |
| `Text`            | The content of the RTT message.                      |
| `Sender`          | Information about the sender of the message.          |
| `ResultType`/<br>`Kind` | Indicates whether the message is partial or final. |
| `IsLocal`         | Determines if a local user sent the message. |
| `ReceivedTime`    | Timestamp when the message was received.              |
| `UpdatedTime`     | Timestamp when the message was last updated.          |

::: zone pivot="programming-language-javascript"
[!INCLUDE [Real Time Text with Web](./includes/real-time-text/real-time-text-web.md)]
::: zone-end

::: zone pivot="programming-language-java"
[!INCLUDE [Real Time Text with Android](./includes/real-time-text/real-time-text-android.md)]
::: zone-end

::: zone pivot="programming-language-swift"
[!INCLUDE [Real Time Text with iOS](./includes/real-time-text/real-time-text-ios.md)]
::: zone-end

::: zone pivot="programming-language-csharp"
[!INCLUDE [Real Time Text with Windows](./includes/real-time-text/real-time-text-windows.md)]
::: zone-end

## Next steps

- Learn more about RTT in our [Real Time Text Conceptual Doc](../../concepts/voice-video-calling/real-time-text.md).
- Learn more with our [Azure Communication Services Calling Documentation](../../concepts/voice-video-calling/calling-sdk-features.md).
- Learn more about [Closed captions](../../concepts/voice-video-calling/closed-captions.md).
