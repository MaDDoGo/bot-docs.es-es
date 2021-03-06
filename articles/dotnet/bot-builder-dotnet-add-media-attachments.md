---
title: Incorporación de datos adjuntos con elementos multimedia a mensajes | Microsoft Docs
description: Obtenga información sobre cómo agregar datos adjuntos con elementos multimedia a los mensajes mediante Bot Framework SDK para .NET.
author: RobStand
ms.author: kamrani
manager: kamrani
ms.topic: article
ms.service: bot-service
ms.subservice: sdk
ms.date: 12/13/2017
monikerRange: azure-bot-service-3.0
ms.openlocfilehash: 6dcfe6595f1c5961151a90783dd8ceee9c7684dd
ms.sourcegitcommit: b15cf37afc4f57d13ca6636d4227433809562f8b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2019
ms.locfileid: "54224340"
---
# <a name="add-media-attachments-to-messages"></a>Incorporación de datos adjuntos con elementos multimedia a mensajes

[!INCLUDE [pre-release-label](../includes/pre-release-label-v3.md)]

> [!div class="op_single_selector"]
> - [.NET](../dotnet/bot-builder-dotnet-add-media-attachments.md)
> - [Node.js](../nodejs/bot-builder-nodejs-send-receive-attachments.md)
> - [REST](../rest-api/bot-framework-rest-connector-add-media-attachments.md)

Un intercambio de mensajes entre el usuario y el bot puede contener datos adjuntos con elementos multimedia (por ejemplo, imágenes, vídeo, audio, archivos). La propiedad `Attachments` del objeto <a href="https://docs.botframework.com/en-us/csharp/builder/sdkreference/dc/d2f/class_microsoft_1_1_bot_1_1_connector_1_1_activity.html" target="_blank">Activity</a> contiene una matriz de objetos <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.attachments?view=botconnector-3.12.2.4" target="_blank">Attachment</a> que presentan los datos adjuntos con elementos multimedia y las tarjetas enriquecidas dentro del mensaje. 

> [!NOTE]
> [Incorporación de tarjetas enriquecidas a mensajes](bot-builder-dotnet-add-rich-card-attachments.md)

## <a name="add-a-media-attachment"></a>Incorporación de datos adjuntos con elementos multimedia  

Para agregar datos adjuntos con elementos multimedia a un mensaje, cree un objeto `Attachment` para la actividad `message` y establezca las propiedades `ContentType`, `ContentUrl` y `Name`. 

[!code-csharp[Add media attachment](../includes/code/dotnet-add-attachments.cs#addMediaAttachment)]

Si los datos adjuntos son una imagen, un audio o un vídeo, el servicio del conector comunicará los datos adjuntos al canal de una manera que permita que el [canal](bot-builder-dotnet-channeldata.md) presente esos datos adjuntos dentro de la conversación. Si los datos adjuntos son un archivo, la dirección URL del archivo se presentará como un hipervínculo dentro de la conversación.

## <a name="additional-resources"></a>Recursos adicionales

- [Preview features with the Channel Inspector][inspector] (Vista previa de las características con el Inspector de canales)
- [Activities overview](bot-builder-dotnet-activities.md) (Introducción a las actividades)
- [Create messages](bot-builder-dotnet-create-messages.md) (Creación de mensajes)
- [Incorporación de tarjetas enriquecidas a mensajes](bot-builder-dotnet-add-rich-card-attachments.md)
- <a href="https://docs.botframework.com/en-us/csharp/builder/sdkreference/dc/d2f/class_microsoft_1_1_bot_1_1_connector_1_1_activity.html" target="_blank">Clase Activity</a>
- <a href="https://docs.microsoft.com/en-us/dotnet/api/microsoft.bot.connector.attachments?view=botconnector-3.12.2.4" target="_blank">Clase Attachment</a>

[inspector]: ../bot-service-channel-inspector.md


