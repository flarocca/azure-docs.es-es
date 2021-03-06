---
title: Pasos para importar una aplicación
services: cognitive-services
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: include
ms.date: 06/22/2020
ms.openlocfilehash: aa0ba1de63cbcf1d9485c71b6bec7a29afb5140f
ms.sourcegitcommit: f5580dd1d1799de15646e195f0120b9f9255617b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2020
ms.locfileid: "91545121"
---
1. En el [portal de LUIS](https://www.luis.ai), en la página **Mis aplicaciones**, seleccione **+ New app for conversation** (Nueva aplicación para conversación) y, a continuación, **Importar como JSON**. Busque el archivo JSON guardado en el paso anterior. No es necesario cambiar el nombre de la aplicación. Seleccione **Listo**

1. En la sección **Administrar**, en la pestaña **Versiones**, seleccione la versión `0.1`, luego seleccione **Clonar** para clonar la versión y asígnele el nuevo nombre de `ml-entity`. A continuación, seleccione **Listo** para finalizar el proceso de clonación. Dado que el nombre de la versión se usa como parte de la ruta de la dirección URL, el nombre no puede contener ningún carácter que no sea válido en una dirección URL.

    > [!TIP]
    > La clonación en una nueva versión es un procedimiento recomendado antes de modificar la aplicación. Cuando finalice un cambio en una versión, exporte la versión (como archivo .json o .lu), y compruebe el archivo en el sistema de control de código fuente.

1. Seleccione **Compilar** y después **Intenciones** para ver las intenciones, los principales bloques de creación de una aplicación de LUIS.

    ![Cambie de la página Versiones a la página Intenciones.](../media/tutorial-machine-learned-entity/new-version-imported-app.png)
