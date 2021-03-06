---
title: Uso de Holographic Remoting y Remote Rendering en Unity
description: Cómo se puede usar la versión preliminar de Holographic Remoting en combinación con Azure Remote Rendering
author: christophermanthei
ms.author: chmant
ms.date: 03/23/2020
ms.topic: how-to
ms.openlocfilehash: 180af30f57a8123b6e90cc8b11848b92b3c86db1
ms.sourcegitcommit: 23aa0cf152b8f04a294c3fca56f7ae3ba562d272
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91802181"
---
# <a name="use-holographic-remoting-and-remote-rendering-in-unity"></a>Uso de Holographic Remoting y Remote Rendering en Unity

[Holographic Remoting](https://docs.microsoft.com/windows/mixed-reality/holographic-remoting-player) y Azure Remote Rendering se excluyen mutuamente dentro de una aplicación. Por tanto, el [modo de reproducción de Unity](https://docs.microsoft.com/windows/mixed-reality/unity-play-mode) tampoco está disponible.

En cada ejecución del editor de Unity, solo se puede usar uno de los dos. Para usar el otro, reinicie Unity primero.

## <a name="use-unity-play-mode-to-preview-on-hololens-2"></a>Uso del modo de reproducción de Unity para obtener una vista previa en HoloLens 2

 El modo de reproducción de Unity todavía se puede usar, por ejemplo, para probar la interfaz de usuario de la aplicación. Sin embargo, es vital que ARR nunca se inicialice. De lo contrario, se bloqueará.

## <a name="use-a-wmr-vr-headset-to-preview-on-desktop"></a>Uso de un casco de realidad virtual de WMR para obtener una vista previa en el escritorio

Si se dispone de un casco de realidad virtual de Windows Mixed Reality, se puede usar para obtener una vista previa dentro de Unity. En este caso, es preciso inicializar ARR; sin embargo, no será posible conectarse a una sesión mientras se use el casco de WMR.
