---
title: API REST de Bot Framework | Microsoft Docs
description: Introducción a las API REST de Bot Framework que se pueden usar para crear bots y los clientes que se conectan a ellos.
author: RobStand
ms.author: kamrani
manager: kamrani
ms.topic: article
ms.service: bot-service
ms.subservice: sdk
ms.date: 12/13/2017
ms.openlocfilehash: eace4852feaadcc180f7329261990fc8eaf7f522
ms.sourcegitcommit: b15cf37afc4f57d13ca6636d4227433809562f8b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2019
ms.locfileid: "54224270"
---
# <a name="bot-framework-rest-apis"></a>Las API REST de Bot Framework
> [!div class="op_single_selector"]
> - [.NET](../dotnet/bot-builder-dotnet-overview.md)
> - [Node.js](../nodejs/bot-builder-nodejs-overview.md)
> - [REST](../rest-api/bot-framework-rest-overview.md)

Las API REST de Bot Framework le permiten crear bots que intercambian mensajes con canales configurados en el <a href="https://dev.botframework.com/" target="_blank">portal de Bot Framework</a>, almacenar y recuperar datos de estado y conectar sus propias aplicaciones cliente a sus bots. Todos los servicios de Bot Framework usan REST y JSON estándar a través de HTTPS.

## <a name="build-a-bot"></a>Creación de un bot

Puede crear un bot con cualquier lenguaje de programación mediante el servicio Bot Connector para intercambiar mensajes con canales configurados en el portal de Bot Framework. 

> [!TIP]
> Bot Framework proporciona bibliotecas cliente que se pueden usar para crear bots en C# o Node.js. Para crear un bot con C#, use [Bot Framework SDK para C#](../dotnet/bot-builder-dotnet-overview.md). Para crear un bot con Node.js, use [Bot Framework SDK para Node.js](../nodejs/index.md). 

Para más información sobre la creación de bots con el servicio Bot Connector, consulte [Conceptos clave](bot-framework-rest-connector-concepts.md).

## <a name="build-a-client"></a>Creación de un cliente

Para permitir que su propia aplicación cliente se comunique con el bot, puede usar Direct Line API. Direct Line API implementa un mecanismo de autenticación que emplea patrones estándar de secreto/token y proporciona un esquema estable, incluso si el bot cambia la versión de su protocolo. Para más información sobre el uso de Direct Line API para habilitar la comunicación entre un cliente y el bot, consulte [Conceptos clave](bot-framework-rest-direct-line-3-0-concepts.md). 