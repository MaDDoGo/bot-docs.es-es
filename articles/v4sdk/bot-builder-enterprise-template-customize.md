---
title: Personalización de bots de empresa | Microsoft Docs
description: Aprenda a personalizar el blob creado mediante la plantilla de empresa.
author: darrenj
ms.author: darrenj
manager: kamrani
ms.topic: article
ms.service: bot-service
ms.date: 02/7/2019
monikerRange: azure-bot-service-4.0
ms.openlocfilehash: 115c81bef6f555bb3404dfb2249dc751d7eed7e5
ms.sourcegitcommit: b2245df2f0a18c5a66a836ab24a573fd70c7d272
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57568212"
---
# <a name="enterprise-bot-template---customize-your-bot"></a>Plantilla de bot de empresa: personalización del bot

> [!NOTE]
> Este tema se aplica a la versión v4 del SDK. 

Después de haber implementado y comprobado que la plantilla de bot de empresa funciona de un extremo a otro como se muestra [aquí](bot-builder-enterprise-template-getting-started.md) en las instrucciones, puede personalizar fácilmente el bot según su escenario y sus necesidades. El objetivo de la plantilla es proporcionar una base sólida sobre la que crear su experiencia conversacional.

## <a name="project-structure"></a>Estructura del proyecto

La estructura de carpeta del bot se muestra a continuación y representa nuestro procedimiento recomendado para estructurar el proyecto del bot y procesar los mensajes entrantes.

    | - YourBot.bot         // The .bot file containing all of your Bot configuration including dependencies
    | - README.md           // README file containing links to documentation
    | - Program.cs          // Default Program.cs file
    | - Startup.cs          // Core Bot Initialisation including Bot Configuration LUIS, Dispatcher, etc. 
    | - <BOTNAME>State.cs   // The Root State class for your Bot
    | - appsettings.json    // References above .bot file for Configuration information. App Insights key
    | - CognitiveModels     
        | - LUIS            // .LU file containing base conversational intents (Greeting, Help, Cancel)
        | - QnA             // .LU file containing example QnA items
    | - DeploymentScripts   // msbot clone recipes for deployment
        | - de              // Deployment files for German
        | - en              // Deployment files for English        
        | - es              // Deployment files for Spanish
        | - fr              // Deployment files for French
        | - it              // Deployment files for Italian
        | - zh              // Deployment files for Chinese
    | - Dialogs             // All Bot dialogs sit under this folder
        | - Main            // Root Dialog for all messages
            | - MainDialog.cs       // Dialog Logic
            | - MainResponses.cs    // Dialog responses
            | - Resources           // Adaptive Card JSON, Resource File
        | - Onboarding
            | - OnboardingDialog.cs       // Onboarding dialog Logic
            | - OnboardingResponses.cs    // Onboarding dialog responses
            | - OnboardingState.cs        // Localised dialog state
            | - Resources                 Resource File
        | - Cancel
        | - Escalate
        | - Signin
    | - Middleware          // Telemetry, Content Moderator
    | - ServiceClients      // SDK libraries, example GraphClient provided for Auth example
   
## <a name="update-introduction-message"></a>Actualización del mensaje de introducción

El mensaje de introducción hace uso de una [tarjeta adaptable](https://www.adaptivecards.io). Para personalizar esta introducción del bot, puede encontrar el archivo JSON llamado ```Intro.json``` dentro de la carpeta Dialogs/Main/Resources. Use el [visualizador de tarjetas adaptables](http://adaptivecards.io/visualizer) para modificar la tarjeta adaptable de acuerdo con las necesidades del bot.

## <a name="update-bot-responses"></a>Actualización de las respuestas del bot

Cada diálogo del proyecto tiene un conjunto de respuestas que se almacenan en archivos de recursos complementarios (.resx). Estos archivos se pueden encontrar en la carpeta de recursos, debajo de cada diálogo.

Puede cambiar las respuestas en el editor de recursos de Visual Studio como se muestra a continuación para ajustar cómo responde el bot.

![Personalización de las respuestas del bot](media/enterprise-template/EnterpriseBot-CustomisingResponses.png)

Este enfoque es compatible con respuestas multilingües que usan el enfoque de localización de archivos de recursos estándar. Se puede encontrar más información [aquí.](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/localization?view=aspnetcore-2.1)

## <a name="updating-your-cognitive-models"></a>Actualización de los modelos cognitivos

De forma predeterminada, la plantilla de empresa incluye dos modelos cognitivos: una base de conocimientos de QnA Maker con P+F de ejemplo y un modelo de LUIS para intenciones generales (saludo, ayuda, cancelar, etc.). Estos modelos se pueden personalizar de acuerdo a sus necesidades. También puede agregar nuevos modelos de LUIS y bases de conocimientos de QnA Maker para expandir las funcionalidades del bot.

### <a name="updating-an-existing-luis-model"></a>Actualización de un modelo de LUIS existente
Para actualizar un modelo de LUIS existente para la plantilla de empresa, siga estos pasos:
1. Realice los cambios en el modelo de LUIS en el [portal de LUIS](http://luis.ai) o mediante las herramientas de la CLI [LuDown](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/Ludown) y [Luis](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/LUIS). 
2. Ejecute el siguiente comando para actualizar el modelo de distribución de modo que refleje los cambios (garantiza el enrutamiento adecuado de los mensajes):
    ```shell
    dispatch refresh --bot "YOUR_BOT.bot" --secret YOUR_SECRET
    ```
3. Ejecute el siguiente comando desde la raíz del proyecto con cada modelo actualizado a fin de actualizar sus clases LuisGen asociadas: 
    ```shell
    luis export version --appId [LUIS_APP_ID] --versionId [LUIS_APP_VERSION] --authoringKey [YOUR_LUIS_AUTHORING_KEY] | luisgen --cs [CS_FILE_NAME] -o "\Dialogs\Shared\Resources"
    ```

### <a name="updating-an-existing-qna-maker-knowledge-base"></a>Actualización de una base de conocimiento de QnA Maker existente
Para actualizar una base de conocimientos de QnA Maker existente, realice los pasos siguientes:
1. Realice cambios en la base de conocimiento de QnA Maker mediante las herramientas de la CLI [LuDown](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/Ludown) y [QnA Maker](https://github.com/Microsoft/botbuilder-tools/tree/master/packages/QnAMaker) o [QnA Maker Portal](https://qnamaker.ai).
2. Ejecute el siguiente comando para actualizar el modelo de distribución de modo que refleje los cambios (garantiza el enrutamiento adecuado de los mensajes):
    ```shell
    dispatch refresh --bot "YOUR_BOT.bot" --secret YOUR_SECRET
    ```

### <a name="adding-a-new-luis-model"></a>Incorporación de un nuevo modelo de LUIS

En escenarios donde quiera agregar un nuevo modelo de LUIS al proyecto, deberá actualizar la configuración del bot y el Dispatcher para tener la seguridad de que se tiene en cuenta el modelo adicional. 
1. Cree el modelo de LUIS mediante las herramientas de la CLI LuDown/LUIS o el portal de LUIS.
2. Ejecute el comando siguiente para conectar la nueva aplicación de LUIS al archivo .bot:
    ```shell
    msbot connect luis --appId [LUIS_APP_ID] --authoringKey [LUIS_AUTHORING_KEY] --subscriptionKey [LUIS_SUBSCRIPTION_KEY] 
    ```
3. Agregue este nuevo modelo de LUIS al Dispatcher mediante el siguiente comando:
    ```shell
    dispatch add -t luis -id LUIS_APP_ID -bot "YOUR_BOT.bot" --secret YOURSECRET
    ```
4. Actualice el modelo de distribución para que refleje los cambios en el modelo de LUIS mediante el comando siguiente:
    ```shell
    dispatch refresh -bot "YOUR_BOT.bot" --secret YOUR_SECRET
    ```

### <a name="adding-an-additional-qna-maker-knowledge-base"></a>Adición de una base de conocimiento de QnA Maker adicional

En algunos escenarios puede que desee agregar una base de conocimiento de QnA Maker adicional al bot; esto se puede realizar mediante los pasos siguientes.

1. Cree una nueva base de conocimiento de QnA Maker desde un archivo JSON con la ejecución del siguiente comando en el directorio del asistente
    ```shell
    qnamaker create kb --in <KB.json> --msbot | msbot connect qna --stdin --bot "YOUR_BOT.bot" --secret YOURSECRET
    ```
2. Ejecute el siguiente comando para actualizar el modelo de Dispatch de modo que refleje los cambios
    ```shell
    dispatch refresh --bot "YOUR_BOT.bot" --secret YOUR_SECRET
    ```
3. Actualice la clase Dispatch fuertemente tipada para reflejar el nuevo origen de QnA
    ```shell
    msbot get dispatch --bot "YOUR_BOT.bot" | luis export version --stdin > dispatch.json
    luisgen dispatch.json -cs Dispatch -o Dialogs\Shared
    ```
4.  Actualice el archivo `Dialogs\Main\MainDialog.cs` para incluir la intención de Dispatch correspondiente para el nuevo origen de QnA siguiendo el ejemplo proporcionado.

Ahora podrá aprovechar varios orígenes de QnA como parte del bot.

## <a name="adding-a-new-dialog"></a>Incorporación de un nuevo diálogo

Para agregar un nuevo diálogo al bot, primero debe crear una nueva carpeta debajo de los diálogos y asegurarse de que esta clase se obtenga de `EnterpriseDialog`. A continuación, debe conectar la infraestructura del diálogo. El diálogo de incorporación muestra un ejemplo sencillo al que puede hacer referencia y, luego, se muestra un extracto junto con información general de los pasos.

- Agregar un diálogo de cascada al constructor
- Definir los pasos de la cascada
- Crear los pasos de la cascada
- Llamar a AddDialog pasando la cascada
- Llamar a AddDialog pasando los avisos que se usan en la cascada
- Establecer el InitialDialogId en el primer diálogo donde quiere que se ejecute el componente

```
    InitialDialogId = nameof(OnboardingDialog);

    var onboarding = new WaterfallStep[]
    {
        AskForName,
        AskForEmail,
        AskForLocation,
        FinishOnboardingDialog,
    };

    AddDialog(new WaterfallDialog(InitialDialogId, onboarding));
    AddDialog(new TextPrompt(DialogIds.NamePrompt));
    AddDialog(new TextPrompt(DialogIds.EmailPrompt));
    AddDialog(new TextPrompt(DialogIds.LocationPrompt));
```

A continuación, debe crear el Administrador de plantillas para gestionar las respuestas. Cree una clase y derívela de TemplateManager; se proporciona un ejemplo en el archivo OnboardingResponses.cs y, a continuación, se muestra un extracto.

```    
 ["default"] = new TemplateIdMap
            {
                { ResponseIds.EmailPrompt,
                    (context, data) =>
                    MessageFactory.Text(
                        text: OnboardingStrings.EMAIL_PROMPT,
                        ssml: OnboardingStrings.EMAIL_PROMPT,
                        inputHint: InputHints.ExpectingInput)
                },
                { ResponseIds.HaveEmailMessage,
                    (context, data) =>
                    MessageFactory.Text(
                        text: string.Format(OnboardingStrings.HAVE_EMAIL, data.email),
                        ssml: string.Format(OnboardingStrings.HAVE_EMAIL, data.email),
                        inputHint: InputHints.IgnoringInput)
                },
                { ResponseIds.HaveLocationMessage,
                    (context, data) =>
                    MessageFactory.Text(
                        text: string.Format(OnboardingStrings.HAVE_LOCATION, data.Name, data.Location),
                        ssml: string.Format(OnboardingStrings.HAVE_LOCATION, data.Name, data.Location),
                        inputHint: InputHints.IgnoringInput)
                },
                
                ...
```

Para representar las respuestas, puede usar una instancia del Administrador de plantillas para acceder a estas respuestas mediante `ReplyWith` o `RenderTemplate` en los avisos. A continuación se muestran ejemplos.

```
Prompt = await _responder.RenderTemplate(sc.Context, sc.Context.Activity.Locale, OnboardingResponses.ResponseIds.NamePrompt)
await _responder.ReplyWith(sc.Context, OnboardingResponses.ResponseIds.HaveNameMessage, new { name });
```

La última pieza de la infraestructura del diálogo es la creación de una clase de estado con ámbito solo para su diálogo. Cree una clase y asegúrese de que se deriva de `DialogState`.

Una vez finalizado el diálogo, deberá agregarlo al componente `MainDialog` mediante `AddDialog`. Para usar el nuevo diálogo, llame a `dc.BeginDialogAsync()` en el método `RouteAsync` y desencadénelo con la intención de LUIS adecuada si lo desea.
