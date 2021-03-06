---
title: Enlaces de Azure Cosmos DB para Functions 2.x y superior
description: Descubra cómo utilizar desencadenadores y enlaces de almacenamiento de Azure Cosmos DB en Azure Functions.
author: craigshoemaker
ms.topic: reference
ms.date: 02/24/2017
ms.author: cshoe
ms.openlocfilehash: 2c6efd14bd974de1b01b1725b9810f153df74bf8
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85482180"
---
# <a name="azure-cosmos-db-trigger-and-bindings-for-azure-functions-2x-and-higher-overview"></a>Información general sobre el desencadenador y los enlaces de Azure Cosmos DB para Azure Functions 2.x y versiones superiores

> [!div class="op_single_selector" title1="Seleccione la versión del entorno de ejecución de Azure Functions que usa: "]
> * [Versión 1](functions-bindings-cosmosdb.md)
> * [Versión 2 y superiores](functions-bindings-cosmosdb-v2.md)

En este conjunto de artículos se explica cómo trabajar con enlaces de [Azure Cosmos DB](../cosmos-db/serverless-computing-database.md) en Azure Functions 2.x y versiones superiores. Azure Functions enlaces de desencadenador, de entrada y de salida para Azure Cosmos DB.

| Acción | Tipo |
|---------|---------|
| Ejecución de una función cuando se crea o modifica un documento de Azure Cosmos DB | [Desencadenador](./functions-bindings-cosmosdb-v2-trigger.md) |
| Lectura de un documento de Azure Cosmos DB | [Enlace de entrada](./functions-bindings-cosmosdb-v2-input.md) |
| Guardar cambios en un documento de Azure Cosmos DB  |[Enlace de salida](./functions-bindings-cosmosdb-v2-output.md) |

> [!NOTE]
> Esta referencia va dirigida a [Azure Functions, versión 2.x y superiores](functions-versions.md).  Para obtener información acerca del uso de estos enlaces en Functions 1.x, consulte [Enlaces de Azure Cosmos DB para Azure Functions 1.x](functions-bindings-cosmosdb.md).
>
> Este enlace se llamaba originalmente DocumentDB. En Functions, versión 2.x y superiores, tanto el desencadenador, como los enlaces y el paquete se denominan Cosmos DB.

## <a name="supported-apis"></a>API admitidas

[!INCLUDE [SQL API support only](../../includes/functions-cosmosdb-sqlapi-note.md)]

## <a name="add-to-your-functions-app"></a>Adición a la aplicación de Functions

### <a name="functions-2x-and-higher"></a>Functions 2.x y superiores

Para trabajar con el desencadenador y los enlaces, es necesario hacer referencia al paquete adecuado. En las bibliotecas de clases de .NET se usa el paquete NuGet, mientras que en los demás tipos de aplicaciones se emplea el conjunto de extensiones.

| Idioma                                        | Agregar mediante...                                   | Observaciones 
|-------------------------------------------------|---------------------------------------------|-------------|
| C#                                              | Instalación del [paquete NuGet], versión 3.x | |
| Script de C#, Java, JavaScript, Python, PowerShell | Registro de [conjunto de extensiones]          | Se recomienda usar la [extensión Azure Tools] con Visual Studio Code. |
| Script de C# (solo en línea en Azure Portal)         | Adición de un enlace                            | Para actualizar extensiones de enlace existentes sin tener que volver a publicar la aplicación de funciones, consulte [Actualización de las extensiones]. |

[Paquete NuGet]: https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB
[core tools]: ./functions-run-local.md
[conjunto de extensiones]: ./functions-bindings-register.md#extension-bundles
[Actualización de las extensiones]: ./install-update-binding-extensions-manual.md
[Extensión Azure Tools]: https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack

### <a name="functions-1x"></a>Functions 1.x

Las aplicaciones de Functions 1.x tienen automáticamente una referencia al paquete NuGet [Microsoft.Azure.WebJobs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs), versión 2.x.

## <a name="next-steps"></a>Pasos siguientes

- [Ejecución de una función cuando se crea o modifica un documento de Azure Cosmos DB (desencadenador)](./functions-bindings-cosmosdb-v2-trigger.md)
- [Lectura de un documento de Azure Cosmos DB (enlace de entrada)](./functions-bindings-cosmosdb-v2-input.md)
- [Guardar los cambios en un documento de Azure Cosmos DB (enlace de salida)](./functions-bindings-cosmosdb-v2-output.md)
