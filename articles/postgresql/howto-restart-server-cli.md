---
title: 'Reinicio de servidor mediante la CLI de Azure de Azure Database for PostgreSQL: servidor único'
description: En este artículo se describe cómo reiniciar una instancia de Azure Database for PostgreSQL con un único servidor mediante la CLI de Azure.
author: lfittl-msft
ms.author: lufittl
ms.service: postgresql
ms.topic: how-to
ms.date: 5/6/2019
ms.custom: devx-track-azurecli
ms.openlocfilehash: 30770dd7ed71f4cde68c1a616a256bf60b5acaef
ms.sourcegitcommit: 19dce034650c654b656f44aab44de0c7a8bd7efe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2020
ms.locfileid: "91704763"
---
# <a name="restart-azure-database-for-postgresql---single-server-using-the-azure-cli"></a>Reiniciar una instancia de Azure Database for PostgreSQL con un único servidor con la CLI de Azure
En este tema se describe cómo reiniciar un servidor de Azure Database for PostgreSQL. Es posible que deba reiniciar el servidor por motivos de mantenimiento, lo que causa una breve interrupción del servicio mientras el servidor realiza la operación.

Si el servicio está ocupado, se bloqueará el reinicio del servidor. Por ejemplo, el servicio puede estar procesando una operación solicitada anteriormente, como el escalado de núcleos virtuales.
 
El tiempo necesario para completar un reinicio depende del proceso de recuperación de PostgreSQL. Para reducir el tiempo de reinicio, se recomienda que minimice la cantidad de actividades que se ejecutan en el servidor antes del reinicio.

## <a name="prerequisites"></a>Requisitos previos
Para completar esta guía, necesita:
- Un [servidor de Azure Database for PostgreSQL](quickstart-create-server-up-azure-cli.md).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

> [!IMPORTANT]
> Esta guía de procedimientos requiere el uso de la CLI de Azure versión 2.0 o posterior. Para confirmar la versión, en el símbolo del sistema de la CLI de Azure, escriba `az --version`. Para la instalación o la actualización, consulte [Instalación de la CLI de Azure]( /cli/azure/install-azure-cli).


## <a name="restart-the-server"></a>Reinicio del servidor

Reinicie el servidor con el siguiente comando:

```azurecli-interactive
az postgres server restart --name mydemoserver --resource-group myresourcegroup
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre [cómo establecer parámetros en Azure Database for PostgreSQL](howto-configure-server-parameters-using-cli.md)
