---
title: 'Creación de una máquina virtual a partir de una instantánea (Linux): ejemplo de PowerShell'
description: 'Ejemplo de script de Azure PowerShell: creación de una máquina virtual a partir de una instantánea con un ejemplo de Linux.'
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankumarlive
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc, devx-track-azurepowershell
ms.openlocfilehash: e39c703452b5bb6855062c1c3efbde29d2becd1e
ms.sourcegitcommit: 32c521a2ef396d121e71ba682e098092ac673b30
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/25/2020
ms.locfileid: "91320156"
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell-linux"></a>Creación de una máquina virtual a partir de una instantánea con PowerShell (Linux)

Este script crea una máquina virtual a partir de una instantánea de un disco del SO.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

 

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación

Ejecute el siguiente comando para quitar el grupo de recursos, la máquina virtual y todos los recursos relacionados.

```powershell
Remove-AzResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicación del script

Este script usa los siguientes comandos para obtener las propiedades de las instantáneas, crear un disco administrado a partir de una instantánea y crear una máquina virtual. Cada elemento de la tabla incluye vínculos a la documentación específica del comando.

| Get-Help | Notas |
|---|---|
| [Get-AzSnapshot](/powershell/module/az.compute/get-azsnapshot) | Obtiene una instantánea con el nombre de la instantánea. |
| [New-AzDiskConfig](/powershell/module/az.compute/new-azdiskconfig) | Crea una configuración de disco. Esta configuración se utiliza con el proceso de creación del disco. |
| [New-AzDisk](/powershell/module/az.compute/new-azdisk) | Crea un disco administrado. |
| [New-AzVMConfig](/powershell/module/az.compute/new-azvmconfig) | Crea una configuración de máquina virtual. Esta configuración incluye diversa información, como el nombre de la máquina virtual, sistema el operativo y las credenciales administrativas. La configuración se utiliza durante la creación de las máquinas virtuales. |
| [Set-AzVMOSDisk](/powershell/module/az.compute/set-azvmosdisk) | Conecta el disco administrado como disco del SO a la máquina virtual. |
| [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) | Crea una dirección IP pública. |
| [New-AzNetworkInterface](/powershell/module/az.network/new-aznetworkinterface) | Crea una interfaz de red. |
| [New-AzVM](/powershell/module/az.compute/new-azvm) | Crea una máquina virtual. |
|[Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Quita un grupo de recursos y todos los recursos incluidos en él. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/).

Encontrará más ejemplos de scripts de PowerShell de máquina virtual en la [documentación sobre máquinas virtuales Linux de Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
