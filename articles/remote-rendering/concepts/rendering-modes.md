---
title: Modos de representación
description: Se describen los diferentes modos de representación del lado servidor.
author: florianborn71
ms.author: flborn
ms.date: 02/03/2020
ms.topic: conceptual
ms.custom: devx-track-csharp
ms.openlocfilehash: 0e61ea423cb94dc1192d6b189a95e5a5da3b38ad
ms.sourcegitcommit: f845ca2f4b626ef9db73b88ca71279ac80538559
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/09/2020
ms.locfileid: "89613914"
---
# <a name="rendering-modes"></a>Modos de representación

Remote Rendering ofrece dos modos de funcionamiento principales: **TileBasedComposition** y **DepthBasedComposition**. Estos modos determinan cómo se distribuye la carga de trabajo entre varias GPU del servidor. El modo debe especificarse en el momento de la conexión y no se puede cambiar durante el tiempo de ejecución.

Ambos modos incluyen ventajas, pero también limitaciones de características que son inherentes a ellos, por lo que la elección del modo más adecuado depende de cada caso.

## <a name="modes"></a>Modos

A continuación, se describen con más detalle los dos modos.

### <a name="tilebasedcomposition-mode"></a>El modo "TileBasedComposition"

En el modo **TileBasedComposition**, cada una de las GPU que intervienen representa subrectángulos (mosaicos) específicos en la pantalla. La GPU principal compone la imagen final de los mosaicos antes de enviarla como un fotograma de vídeo al cliente. Como consecuencia, todas las GPU deben tener el mismo conjunto de recursos para la representación, por lo que los recursos cargados deben caber en la memoria de una sola GPU.

La calidad de la representación en este modo es ligeramente mejor que en el modo **DepthBasedComposition**, ya que MSAA puede trabajar en el conjunto completo de geometría de cada GPU. En la captura de pantalla siguiente se muestra que el suavizado de contorno funciona correctamente en ambos bordes por igual:

![MSAA en TileBasedComposition](./media/service-render-mode-quality.png)

Además, en este modo, cada parte se puede cambiar a un material transparente o cambiar al modo **transparente** mediante [HierarchicalStateOverrideComponent](../overview/features/override-hierarchical-state.md).

### <a name="depthbasedcomposition-mode"></a>El modo "DepthBasedComposition"

En el modo **DepthBasedComposition**, cada una de las GPU que intervienen se representa en una resolución de pantalla completa, pero solo un subconjunto de mallas. La composición de la imagen final en la GPU principal se encarga de que las partes se combinen correctamente según su información de profundidad. Naturalmente, la carga de memoria se distribuye entre las GPU, lo que permite la representación de modelos que no cabrían en la memoria de una sola GPU.

Cada GPU usa MSAA para suavizar el contorno del contenido local. Sin embargo, puede haber un suavizado de contorno inherente entre los bordes de distintas GPU. Este efecto se mitiga mediante el posprocesamiento de la imagen final, pero la calidad de MSAA todavía es peor que en el modo **TileBasedComposition**.

En la imagen siguiente se ilustran los artefactos de MSAA: ![MSAA en DepthBasedComposition](./media/service-render-mode-balanced.png)

El suavizado de contorno funciona correctamente entre la escultura y la cortina, ya que ambas partes se representan en la misma GPU. Por otro lado, el borde entre la cortina y la pared muestra algún suavizado de contorno, ya que estas dos partes están compuestas desde distintas GPU.

La mayor limitación de este modo es que las partes de geometría no se pueden cambiar a materiales transparentes de forma dinámica, ni tampoco el modo **transparente** funciona para [HierarchicalStateOverrideComponent](../overview/features/override-hierarchical-state.md). Sin embargo, otras características de invalidación del estado (contorno, matiz de color, etc.) funcionan. Además, los materiales que se marcaron como transparentes en el momento de la conversión funcionan correctamente en este modo.

### <a name="performance"></a>Rendimiento

Las características de rendimiento de ambos modos varían según el caso de uso y es difícil sopesarlo o proporcionar recomendaciones generales. Si no está restringido por las limitaciones mencionadas anteriormente (memoria o transparencia/transparente), se recomienda probar ambos modos y supervisar el rendimiento mediante varias posiciones de la cámara.

## <a name="setting-the-render-mode"></a>Establecimiento del modo de representación

El modo de representación usado en un servidor de Remote Rendering se especifica durante `AzureSession.ConnectToRuntime` a través de `ConnectToRuntimeParams`.

```cs
async void ExampleConnect(AzureSession session)
{
    ConnectToRuntimeParams parameters = new ConnectToRuntimeParams();

    // Connect with one rendering mode
    parameters.mode = ServiceRenderMode.TileBasedComposition;
    await session.ConnectToRuntime(parameters).AsTask();

    session.DisconnectFromRuntime();

    // Wait until session.IsConnected == false

    // Reconnect with a different rendering mode
    parameters.mode = ServiceRenderMode.DepthBasedComposition;
    await session.ConnectToRuntime(parameters).AsTask();
}
```

## <a name="api-documentation"></a>Documentación de la API

* [AzureSession.ConnectToRuntime() de C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.remoterendering.azuresession.connecttoruntime)
* [Estructura ConnectToRuntimeParams de C#](https://docs.microsoft.com/dotnet/api/microsoft.azure.remoterendering.connecttoruntimeparams)
* [AzureSession::ConnectToRuntime() de C++](https://docs.microsoft.com/cpp/api/remote-rendering/azuresession#connecttoruntime)
* [Estructura ConnectToRuntimeParams de C++](https://docs.microsoft.com/cpp/api/remote-rendering/connecttoruntimeparams)

## <a name="next-steps"></a>Pasos siguientes

* [Sesiones](../concepts/sessions.md)
* [Componente de invalidación del estado jerárquico](../overview/features/override-hierarchical-state.md)
