---
title: Control de acceso basado en roles de Custom Vision
titleSuffix: Azure Cognitive Services
description: En este artículo se muestra cómo configurar el control de acceso basado en roles para sus proyectos de Custom Vision.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: custom-vision
ms.topic: conceptual
ms.date: 09/11/2020
ms.author: pafarley
ms.openlocfilehash: 4eea87d7b5ef543551b789ddc6b045358fa98631
ms.sourcegitcommit: d2222681e14700bdd65baef97de223fa91c22c55
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91826935"
---
# <a name="role-based-access-control"></a>Control de acceso basado en roles.

Custom Vision admite el control de acceso basado en roles de Azure (Azure RBAC), un sistema de autorización que permite administrar el acceso individual a los recursos de Azure. Con RBAC, se asignan diferentes miembros del equipo a distintos niveles de permisos para los proyectos de Custom Vision. Para más información sobre RBAC, consulte la [documentación de Azure RBAC](https://docs.microsoft.com/azure/role-based-access-control/).

## <a name="add-role-assignment-to-custom-vision-resource"></a>Adición de asignaciones de roles a Custom Vision recurso

Azure RBAC se puede asignar a un recurso de Custom Vision. Para conceder acceso a un recurso de Azure, se agrega una asignación de roles.
1. En [Azure Portal](https://ms.portal.azure.com/), seleccione **Todos los servicios**. 
1. A continuación, seleccione la opción **Cognitive Services** y navegue hasta el recurso de entrenamiento de Custom Vision específico.
   > [!NOTE]
   > También puede configurar RBAC para grupos de recursos completos, suscripciones o grupos de administración. Para ello, seleccione el nivel de ámbito que quiera y navegue hasta el elemento deseado (por ejemplo, seleccione **Grupos de recursos** y, a continuación, haga clic en el grupo de recursos que quiera).
1. Seleccione **Control de acceso (IAM)** en el panel de navegación izquierdo.
1. Seleccione la pestaña **Asignaciones de roles** para ver todas las asignaciones de roles en este ámbito.
1. Seleccione **Agregar** -> **Agregar asignación de roles**.
1. En la lista desplegable **Rol**, seleccione el rol que quiere agregar.
1. En la lista **Seleccionar**, seleccione un usuario, grupo, entidad de servicio o identidad administrada. Si no ve la entidad de seguridad en la lista, puede escribir en el cuadro Seleccionar para buscar nombres para mostrar, direcciones de correo electrónico e identificadores de objeto en el directorio.
1. Seleccione **Guardar** para asignar el rol.

En cuestión de minutos, al destino se le asignará el rol seleccionado en el ámbito seleccionado.

## <a name="custom-vision-role-types"></a>Tipos de rol de Custom Vision

Use la tabla siguiente para determinar las necesidades de acceso para los recursos de Custom Vision.

|Role  |Permisos  |
|---------|---------|
|`Cognitive Services Custom Vision Contributor`     | Acceso completo a los proyectos, incluida la capacidad de crear, editar o eliminar un proyecto.        |
|`Cognitive Services Custom Vision Trainer`     | Acceso completo, salvo por la capacidad de crear o eliminar un proyecto. Los instructores pueden ver y editar proyectos y entrenar, publicar, anular publicaciones o exportar los modelos.        |
|`Cognitive Services Custom Vision Labeler`     | Capacidad de cargar, editar o eliminar imágenes de entrenamiento, además de crear, agregar, quitar o eliminar etiquetas. Los etiquetadores pueden ver los proyectos, pero no pueden actualizar nada más que las imágenes de entrenamiento y las etiquetas.         |
|`Cognitive Services Custom Vision Deployment`     | Capacidad de publicar, anular publicaciones o exportar los modelos. Los implementadores pueden ver los proyectos, pero no pueden actualizar nada más que las imágenes de entrenamiento y las etiquetas.        |
|`Cognitive Services Custom Vision Reader`     | Capacidad de ver los proyectos. Los lectores no pueden realizar ningún cambio.        |
