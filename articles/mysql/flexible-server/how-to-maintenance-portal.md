---
title: Mantenimiento programado de un servidor flexible de Azure Database for MySQL (versión preliminar) mediante Azure Portal
description: Aprenda a configurar las opciones de mantenimiento programado para un servidor flexible de Azure Database for MySQL mediante Azure Portal.
author: niklarin
ms.author: nlarin
ms.service: mysql
ms.topic: how-to
ms.date: 9/21/2020
ms.openlocfilehash: c8251eb2a89a7481ebc981f2b89668c363651b39
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "91315021"
---
# <a name="manage-scheduled-maintenance-settings-for-azure-database-for-mysql--flexible-server"></a>Administración de la configuración del mantenimiento programado para un servidor flexible de Azure Database for MySQL
 
En la suscripción de Azure puede especificar opciones de mantenimiento para cada servidor flexible. Las opciones incluyen la programación de mantenimiento y la configuración de notificación para eventos de mantenimiento próximos y finalizados.

> [!IMPORTANT]
> La opción de implementación Servidor flexible de Azure Database for MySQL está en versión preliminar.
 
## <a name="prerequisites"></a>Requisitos previos
Para completar esta guía, necesita:
- Un [servidor flexible de Azure Database for MySQL](quickstart-create-server-portal.md).
 
## <a name="specify-maintenance-schedule-options"></a>Especificación de opciones de programación de mantenimiento
 
1. En la página del servidor MySQL, bajo el título **Configuración**, elija **Mantenimiento** para abrir las opciones de mantenimiento programado.
2. La programación predeterminada (administrada por el sistema) es un día de la semana aleatorio y una ventana de 60 minutos para el mantenimiento que se inicia entre las 23:00 y las 7:00 (hora del servidor local). Si quiere personalizar esta programación, elija **Programación personalizada**. Después, puede seleccionar el día de la semana que prefiera y una ventana de 60 minutos para la hora de inicio del mantenimiento.
 
## <a name="notifications-about-scheduled-maintenance-events"></a>Notificaciones sobre eventos de mantenimiento programado
 
Puede usar Azure Service Health para [ver notificaciones](../../service-health/service-notifications.md) sobre el próximo mantenimiento programado y realizado en el servidor flexible. También puede [configurar](../../service-health/resource-health-alert-monitor-guide.md) alertas en Azure Service Health para recibir notificaciones sobre los eventos de mantenimiento.
 
## <a name="next-steps"></a>Pasos siguientes  
 
* Información sobre el [mantenimiento programado de un servidor flexible de Azure Database for MySQL](concepts-maintenance.md).
* Información sobre [Azure Service Health](../../service-health/overview.md)
