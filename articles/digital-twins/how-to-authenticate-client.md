---
title: Escritura de código de autenticación de aplicación
titleSuffix: Azure Digital Twins
description: Vea cómo escribir código de autenticación en una aplicación cliente
author: baanders
ms.author: baanders
ms.date: 4/22/2020
ms.topic: how-to
ms.service: digital-twins
ms.custom: devx-track-js
ms.openlocfilehash: 0438632a36fe14d35210cb5acb8d3a50d0f038b7
ms.sourcegitcommit: d9ba60f15aa6eafc3c5ae8d592bacaf21d97a871
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2020
ms.locfileid: "91767822"
---
# <a name="write-client-app-authentication-code"></a>Escritura de código de autenticación de aplicación cliente

Después de [configurar una instancia y la autenticación de Azure Digital Twins](how-to-set-up-instance-portal.md), puede crear una aplicación cliente para usarla para interactuar con la instancia. Una vez configurado un proyecto cliente de inicio, en este artículo se muestra **cómo escribir código en esa aplicación cliente para autenticarla** en la instancia de Azure Digital Twins.

Hay dos enfoques para el código de ejemplo en este artículo. Puede usar el que sea más adecuado en su caso, en función del lenguaje que haya elegido:
* En la primera sección del código de ejemplo se usa el SDK de .NET (C#) de Azure Digital Twins. El SDK es parte del SDK de Azure para .NET y se encuentra aquí: [*Biblioteca cliente de Digital Twins de Azure IoT para .NET*](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core). También hay SDK compatibles para [Java](https://search.maven.org/artifact/com.azure/azure-digitaltwins-core/1.0.0-beta.1/jar ) y [JavaScript](https://www.npmjs.com/package/@azure/digital-twins/v/1.0.0-preview.1), que se pueden usar de forma similar.
* La segunda sección del código de ejemplo es para los usuarios que no usan el SDK proporcionado y, en su lugar, usan SDK generados por AutoRest en otros lenguajes. Para obtener más información sobre esta estrategia, vea [*Creación de SDK personalizados para Azure Digital Twins con AutoRest*](how-to-create-custom-sdks.md).

También puede leer más sobre las API y los SDK de Azure Digital Twins en [*Uso de las API y los SDK de Azure Digital Twins*](how-to-use-apis-sdks.md).

## <a name="prerequisites"></a>Requisitos previos

En primer lugar, realice los pasos de configuración de [*Configuración de una instancia y autenticación*](how-to-set-up-instance-portal.md). Así se asegura de tener una instancia de Azure Digital Twins, de que el usuario tiene permisos de acceso y de que ha configurado permisos para las aplicaciones cliente. Después de toda esta configuración, está listo para escribir el código de la aplicación cliente.

Para continuar, necesita un proyecto de aplicación cliente en el que escribir el código. Si aún no tiene un proyecto de aplicación cliente configurado, cree un proyecto básico en el lenguaje que prefiera para usarlo con este tutorial.

## <a name="authentication-and-client-creation-net-c-sdk"></a>Autenticación y creación de cliente: SDK de .NET (C#)

En esta sección se muestra un ejemplo en C# sobre el uso del SDK para .NET proporcionado.

En primer lugar, incluya los siguientes paquetes en el proyecto para poder usar el SDK de .NET y las herramientas de autenticación para este artículo de procedimientos:
* `Azure.DigitalTwins.Core`
* `Azure.Identity`

En función de las herramientas que elija, puede incluir los paquetes con el administrador de paquetes de Visual Studio o con la herramienta de línea de comandos `dotnet`. 

También necesitará las siguientes instrucciones using:

```csharp
using Azure.Identity;
using Azure.DigitalTwins.Core;
```
Para autenticarse con el SDK de .NET, use uno de los métodos de obtención de credenciales que se definen en la biblioteca [Azure.Identity](https://docs.microsoft.com/dotnet/api/azure.identity?view=azure-dotnet&preserve-view=true). A continuación, se muestran dos que se usan habitualmente (incluso juntos en la misma aplicación):

* [InteractiveBrowserCredential](https://docs.microsoft.com/dotnet/api/azure.identity.interactivebrowsercredential?view=azure-dotnet&preserve-view=true) está diseñado para aplicaciones interactivas y se puede usar para crear un cliente de SDK autenticado.
* [ManagedIdentityCredential](https://docs.microsoft.com/dotnet/api/azure.identity.managedidentitycredential?view=azure-dotnet&preserve-view=true) funciona bien en los casos en los que necesita identidades administradas (MSI) y es un buen candidato para trabajar con Azure Functions.

### <a name="interactivebrowsercredential-method"></a>Método InteractiveBrowserCredential
El método [InteractiveBrowserCredential](https://docs.microsoft.com/dotnet/api/azure.identity.interactivebrowsercredential?view=azure-dotnet&preserve-view=true) está pensado para aplicaciones interactivas y abrirá un explorador web para la autenticación.

Para usar las credenciales interactivas del explorador para crear un cliente de SDK autenticado, agregue este código:

```csharp
// Your client / app registration ID
private static string clientId = "<your-client-ID>"; 
// Your tenant / directory ID
private static string tenantId = "<your-tenant-ID>";
// The URL of your instance, starting with the protocol (https://)
private static string adtInstanceUrl = "<your-Azure-Digital-Twins-instance-URL>";

//...

DigitalTwinsClient client;
try
{
    var credential = new InteractiveBrowserCredential(tenantId, clientId);
    client = new DigitalTwinsClient(new Uri(adtInstanceUrl), credential);
} catch(Exception e)
{
    Console.WriteLine($"Authentication or client creation error: {e.Message}");
    Environment.Exit(0);
}
```

>[!NOTE]
> Aunque puede especificar el identificador de cliente, el identificador de inquilino y la dirección URL de la instancia directamente en el código, como se muestra arriba, se recomienda que, en su lugar, el código obtenga estos valores de un archivo de configuración o una variable de entorno.

### <a name="managedidentitycredential-method"></a>Método ManagedIdentityCredential
 El método [ManagedIdentityCredential](https://docs.microsoft.com/dotnet/api/azure.identity.managedidentitycredential?view=azure-dotnet&preserve-view=true) funciona muy bien en los casos en los que necesita [identidades administradas (MSI)](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview), por ejemplo, al trabajar con Azure Functions.
En una función de Azure, puede usar las credenciales de identidad administrada de la siguiente manera:

```csharp
ManagedIdentityCredential cred = new ManagedIdentityCredential(adtAppId);
DigitalTwinsClientOptions opts = 
    new DigitalTwinsClientOptions { Transport = new HttpClientTransport(httpClient) });
client = new DigitalTwinsClient(new Uri(adtInstanceUrl), cred, opts);
```

Vea [*Configuración de una función de Azure para procesar datos*](how-to-create-azure-function.md) para obtener un ejemplo más completo en el que se explican algunas de las opciones de configuración importantes en el contexto de las funciones.

Además, para usar la autenticación en una función, recuerde:
* [Habilitar una entidad administrada](https://docs.microsoft.com/azure/app-service/overview-managed-identity?tabs=dotnet).
* Usar [variables de entorno](https://docs.microsoft.com/sandbox/functions-recipes/environment-variables?tabs=csharp) según sea necesario
* Asignar permisos a la aplicación de funciones que le permiten acceder a las API de Digital Twins. Para obtener más información sobre los procesos de Azure Functions, vea [ *Configuración de una función de Azure para procesar datos*](how-to-create-azure-function.md).

## <a name="authentication-with-an-autorest-generated-sdk"></a>Autenticación con un SDK generado por AutoRest

Si no usa ninguno de los SDK proporcionados (.NET, Java, JavaScript), puede optar por compilar una biblioteca de SDK en el lenguaje que prefiera, como se explica en [*Creación de SDK personalizados para Azure Digital Twins con AutoRest*](how-to-create-custom-sdks.md).

En esta sección se explica cómo realizar la autenticación en ese caso.

### <a name="prerequisites"></a>Requisitos previos

En primer lugar, debe realizar los pasos para crear un SDK personalizado con AutoRest de [*Creación de SDK personalizados para Azure Digital Twins con AutoRest*](how-to-create-custom-sdks.md).

En este ejemplo, se usa un SDK de Typescript generado con AutoRest. Como resultado, también requiere:
* [msal-js](https://github.com/AzureAD/microsoft-authentication-library-for-js)
* [ms-rest-js](https://github.com/Azure/ms-rest-js)

### <a name="minimal-authentication-code-sample"></a>Ejemplo de código de autenticación mínimo

Para autenticar una aplicación con servicios de Azure, puede usar el siguiente código mínimo dentro de la aplicación cliente.

Necesitará el *Id. de la aplicación (cliente)* y el *Id. de directorio (inquilino)* anteriores, así como la dirección URL de la instancia de Azure Digital Twins.

> [!TIP]
> La dirección URL de la instancia de Azure Digital Twins se crea con la adición de *https://* al principio del *nombre de host* de la instancia de Azure Digital Twins. Para ver el *nombre de host*, junto con todas las propiedades de la instancia, puede ejecutar `az dt show --dt-name <your-Azure-Digital-Twins-instance>`. Puede usar el comando `az account show --query tenantId` para ver el *Id. de directorio (inquilino)* . 

```javascript
import * as Msal from "msal";
import { TokenCredentials } from "@azure/ms-rest-js";
// Autorest-generated SDK
import { AzureDigitalTwinsAPI } from './azureDigitalTwinsAPI';

// Client / app registration ID
var ClientId = "<your-client-ID>";
// Azure tenant / directory ID
var TenantId = "<your-tenant-ID>";
// URL of the Azure Digital Twins instance
var AdtInstanceUrl = "<your-instance-URL>"; 

var AdtAppId = "https://digitaltwins.azure.net";

let client = null;

export async function login() {

    const msalConfig = {
        auth: {
            clientId: ClientId,
            redirectUri: "http://localhost:3000",
            authority: "https://login.microsoftonline.com/"+TenantId
        }
    };

    const msalInstance = new Msal.UserAgentApplication(msalConfig);

    msalInstance.handleRedirectCallback((error, response) => {
        // handle redirect response or error
    });

    var loginRequest = {
        scopes: [AdtAppId + "/.default"] 
    };

    try {
        await msalInstance.loginPopup(loginRequest)
        var accessToken;
        // if the user is already logged in you can acquire a token
        if (msalInstance.getAccount()) {
            var tokenRequest = {
                scopes: [AdtAppId + "/.default"]
            };
            try {
                const response = await msalInstance.acquireTokenSilent(tokenRequest);
                accessToken = response.accessToken;
            } catch (err) {
                if (err.name === "InteractionRequiredAuthError") {
                    const response = await msalInstance.acquireTokenPopup(tokenRequest)
                    accessToken = response.accessToken;
                }
            }
        }
        if (accessToken!=null)
        {
            var tokenCredentials = new TokenCredentials(accessToken);
                
            // Add token and server URL to service instance
            const clientConfig = {
                baseUri: AdtInstanceUrl
            };
            client = new AzureDigitalTwinsAPI(tokenCredentials, clientConfig);
            appDataStore.client = client;
        }
    } catch (err) {
        ...
    }
}
```

Tenga en cuenta una vez más que donde el código anterior especifica el identificador de cliente, el identificador de inquilino y la dirección URL de la instancia directamente en el código para simplificar, se recomienda que, en su lugar, el código obtenga estos valores de un archivo de configuración o una variable de entorno.

MSAL tiene muchas más opciones que puede usar para implementar elementos, como el almacenamiento en caché y otros flujos de autenticación. Para obtener más información sobre esto, vea [*Introducción a la Biblioteca de autenticación de Microsoft (MSAL)* ](../active-directory/develop/msal-overview.md).

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre cómo funciona la seguridad en Azure Digital Twins:
* [*Conceptos: Seguridad para las soluciones de Azure Digital Twins*](concepts-security.md)

O bien, ahora que la autenticación está configurada, continúe con la creación de modelos en la instancia:
* [*Procedimiento: Administración de modelos personalizados*](how-to-manage-model.md)