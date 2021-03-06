---
title: Administración de un bot | Microsoft Docs
description: Aprenda a administrar un bot mediante el portal de Bot Service.
keywords: azure portal, administración de bots, probar en chat web, MicrosoftAppID, MicrosoftAppPassword, configuración de la aplicación
author: v-ducvo
ms.author: rstand
manager: kamrani
ms.topic: article
ms.service: bot-service
ms.subservice: abs
ms.date: 12/13/2017
ms.openlocfilehash: fef82d27c6dd4fb61c9a0cf864e76a88128847d7
ms.sourcegitcommit: 05ddade244874b7d6e2fc91745131b99cc58b0d6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2019
ms.locfileid: "56591166"
---
# <a name="manage-a-bot"></a>Administración de un bot

En este tema se explica cómo administrar un bot mediante Azure Portal.

## <a name="bot-settings-overview"></a>Introducción a la configuración de bots

![Introducción a la configuración de bots](~/media/azure-manage-a-bot/overview.png)

En la hoja **Información general**, puede encontrar información general sobre el bot. Por ejemplo, puede ver el **identificador de suscripción**, el **plan de tarifa** y el **punto de conexión de mensajería** del bot.

## <a name="bot-management"></a>Administración de bots

 La mayoría de las opciones de administración del bot se pueden encontrar en la sección **ADMINISTRACIÓN DE BOTS**. Esta es una lista de opciones para ayudarle a administrar su bot.

![Administración de bots](~/media/azure-manage-a-bot/bot-management.png)

| Opción |  DESCRIPCIÓN |
| ---- | ---- |
| **Compilar** | La pestaña Compilar proporciona opciones para realizar cambios en el bot. Esta opción no está disponible para **Registration Only Bot** (Solo bot de registro). |
| **Probar en Chat en web** | Use el control de chat web integrado para ayudarle a probar rápidamente su bot. |
| **Analytics** | Si el análisis está activado para el bot, puede ver los datos de análisis que Application Insights ha recopilado para el bot. |
| **Channels** | Configure los canales que usa su bot para comunicarse con los usuarios. |
| **Configuración** | Administre varias configuraciones de perfiles de bots, como nombre para mostrar, análisis y punto de conexión de mensajería. |
| **Preparación para la voz** | Administre las conexiones entre la aplicación de LUIS y el servicio Bing Speech... |
| **Precios de Bot Service** | Administre el plan de tarifa del servicio de bots. |

## <a name="app-service-settings"></a>Configuración de App Service

![Configuración de App Service](~/media/azure-manage-a-bot/app-service-settings.png)

La hoja **Configuración de la aplicación** contiene información detallada sobre su bot, como el entorno del bot y las claves de configuración de depuración y clave de configuración de la aplicación como botFilePath y botFileSecret.

### <a name="microsoftappid-and-microsoftapppassword"></a>MicrosoftAppID y MicrosoftAppPassword

**MicrosoftAppID** y **MicrosoftAppPassword** se guardan en el archivo `.bot` del bot. Para recuperarlos, descargue el archivo del bot y descífrelo, porque puede ser necesario para probar localmente el identificador y la contraseña.

### <a name="bot-file-path-and-secret"></a>Secreto y la ruta de acceso del archivo de bot

Encontrará los valorse de **botFilePath** y **botFileSecret** del bot en la hoja **Configuración de la aplicación**.

![Secreto y la ruta de acceso del archivo de bot de Microsoft](~/media/azure-manage-a-bot/app-settings.png)

> [!NOTE]
> El servicio de bots **Registro de canales de bots** incluye un valor *MicrosoftAppID*, pero como no hay un servicio de aplicaciones asociado con este tipo de servicio, no hay una hoja **Configuración de la aplicación** para que consulte el valor *MicrosoftAppPassword*. Para obtener la contraseña, debe generar una. Para generar la contraseña para un **registro de canales de Bot**, consulte [Bot Channels Registration password](bot-service-quickstart-registration.md#bot-channels-registration-password) (Contraseña de registro de canales de bots).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha explorado la hoja de Bot Service en Azure Portal, aprenda a usar el Editor de código en línea para personalizar su bot.
> [!div class="nextstepaction"]
> [Uso del editor de código en línea](bot-service-build-online-code-editor.md)
