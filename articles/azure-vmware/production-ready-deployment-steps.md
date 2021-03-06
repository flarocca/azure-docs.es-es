---
title: Planificación de la implementación de Azure VMware Solution
description: En este artículo se describe el flujo de trabajo de implementación de Azure VMware Solution.  El resultado final es un entorno listo para la creación y migración de máquinas virtuales (VM).
ms.topic: tutorial
ms.date: 10/02/2020
ms.openlocfilehash: e279f14406d464171f0879d85cc33f9844d22ec3
ms.sourcegitcommit: 23aa0cf152b8f04a294c3fca56f7ae3ba562d272
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91802215"
---
# <a name="planning-the-azure-vmware-solution-deployment"></a>Planificación de la implementación de Azure VMware Solution

En este artículo, le proporcionamos el proceso de planificación para identificar y recopilar los datos que se usan durante la implementación. [Use la lista de comprobación previa a la implementación](pre-deployment-checklist.md) para documentar la información y para facilitar la referencia durante la implementación.  

Los procesos de este inicio rápido generan un entorno listo para la producción, para la creación de máquinas virtuales (VM) y la migración. 

>[!IMPORTANT]
>Antes de crear el recurso de Azure VMware Solution, debe enviar una incidencia de soporte técnico para que se asignen los nodos. Una vez que el equipo de soporte técnico recibe su solicitud, se tarda hasta cinco días laborables en confirmar su solicitud y asignar los nodos. Si tiene una nube privada de Azure VMware Solution existente y desea asignar más nodos, repasará el mismo proceso. Para más información, consulte [Habilitación del recurso de Azure VMware Solution](enable-azure-vmware-solution.md). 

## <a name="subscription"></a>Suscripción

Identifique la suscripción que piensa usar para implementar Azure VMware Solution.  Puede crear una nueva suscripción o reutilizar una existente.

>[!NOTE]
>La suscripción debe estar asociada a un Contrato Enterprise de Microsoft.

## <a name="resource-group"></a>Resource group

Identifique el grupo de recursos que quiere usar para Azure VMware Solution.  Por lo general, se crea un grupo de recursos específicamente para Azure VMware Solution, pero puede usar un grupo de recursos existente.

## <a name="region"></a>Region

Identifique la región en la que desea implementar Azure VMware Solution.  Para más información, consulte la [Guía de productos Azure disponibles por región](https://azure.microsoft.com/en-us/global-infrastructure/services/?products=azure-vmware).

## <a name="resource-name"></a>Nombre del recurso

Defina el nombre del recurso que va a usar durante la implementación.  El nombre del recurso es un nombre descriptivo en el que se le da un título a la nube privada de Azure VMware Solution.

## <a name="size-nodes"></a>Nodos de tamaño

Identifique los nodos de tamaño que quiere usar al implementar Azure VMware Solution.  Para obtener una lista completa, consulte la documentación de [nubes privadas y clústeres de Azure VMware Solution](concepts-private-clouds-clusters.md#hosts).

## <a name="number-of-hosts"></a>Número de hosts

Defina el número de hosts que quiere implementar en la nube privada de Azure VMware Solution.  El número mínimo de nodos es tres y el máximo es 16 por clúster.  Para más información, consulte la documentación de [nubes privadas y clústeres de Azure VMware Solution](concepts-private-clouds-clusters.md#clusters).

Siempre puede extender el clúster más adelante si necesita aumentar el número de implementación inicial.

## <a name="vcenter-admin-password"></a>Contraseña del administrador de vCenter
Defina la contraseña del administrador de vCenter.  Durante la implementación, creará una contraseña de administrador de vCenter. La contraseña es para la cuenta de administrador de cloudadmin@vsphere.local durante la compilación de vCenter. La usará para iniciar sesión en vCenter.

## <a name="nsx-t-admin-password"></a>Contraseña de administrador de NSX-T
Defina la contraseña del administrador de NSX-T.  Durante la implementación, creará una contraseña de administrador de NSX-T. La contraseña se asigna al usuario administrador en la cuenta de NSX durante la compilación de NSX. La usará para iniciar sesión en NSX-T Manager.

## <a name="ip-address-segment"></a>Segmento de dirección IP

El primer paso para planificar la implementación es planificar la segmentación de IP.  Azure VMware Solution ingiere una red /22 que le proporciona. Después, la divide en segmentos menores y usa esos segmentos IP para vCenter, VMware HCX, NSX-T y vMotion.

Azure VMware Solution se conecta a su instancia de Microsoft Azure Virtual Network a través de un circuito ExpressRoute interno. En la mayoría de los casos, se conecta a su centro de datos a través de ExpressRoute Global Reach. 

Azure VMware Solution, el entorno de Azure existente y el entorno local (normalmente) intercambian rutas. Dicho esto, el bloque de direcciones de red CIDR /22 que define en este paso no se debe superponer a nada que ya tenga en el entorno local o en Azure.

**Ejemplo**: 10.0.0.0/22

Para más información, consulte [Lista de comprobación de planificación de la red](tutorial-network-checklist.md#routing-and-subnet-considerations).

:::image type="content" source="media/pre-deployment/management-vmotion-vsan-network-ip-diagram.png" alt-text="Identificación: segmento de dirección IP" border="false":::  

## <a name="ip-address-segment-for-virtual-machine-workloads"></a>Segmento de dirección IP para cargas de trabajo de máquina virtual

Identifique un segmento IP para crear su primera red (segmento NSX) en la nube privada.  Dicho de otra forma, debe crear un segmento de red en Azure VMware Solution para que pueda implementar máquinas virtuales en Azure VMware Solution.   

Incluso si solo tiene previsto extender las redes L2, cree un segmento de red que será útil para validar el entorno.

Recuerde que los segmentos IP creados deben ser únicos en la superficie de Azure y local.  

**Ejemplo**: 10.0.4.0/24

:::image type="content" source="media/pre-deployment/nsx-segment-diagram.png" alt-text="Identificación: segmento de dirección IP" border="false":::     

## <a name="optional-extend-networks"></a>(Opcional) Extensión de redes

Puede extender los segmentos de red del entorno local a Azure VMware Solution y, si lo hace, identificar esas redes.  

Tenga en cuenta que:

- Si tiene previsto extender las redes del entorno local, esas redes deben conectarse a [vSphere Distributed Switch (vDS)](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.networking.doc/GUID-B15C6A13-797E-4BCB-B9D9-5CBC5A60C3A6.html) en el entorno local de VMware.  
- Si las redes que desea extender se encuentran en [vSphere Standard Switch](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.networking.doc/GUID-350344DE-483A-42ED-B0E2-C811EE927D59.html), no se pueden extender.

## <a name="expressroute-global-reach-peering-network"></a>Red de emparejamiento ExpressRoute Global Reach

Identifique un bloque de direcciones de la red CIDR `/29`, que es necesario para el emparejamiento de ExpressRoute Global Reach. Recuerde que los segmentos IP creados deben ser únicos en la superficie de Azure VMware Solution y local. Las direcciones IP de este segmento se usan en cada extremo de la conexión de ExpressRoute Global Reach para conectar el circuito ExpressRoute de Azure VMware Solution con el circuito ExpressRoute local. 

**Ejemplo**: 10.1.0.0/29

:::image type="content" source="media/pre-deployment/expressroute-global-reach-ip-diagram.png" alt-text="Identificación: segmento de dirección IP" border="false":::

## <a name="azure-virtual-network-to-attach-azure-vmware-solution"></a>Azure Virtual Network para conectar Azure VMware Solution

Para acceder a la nube privada de Azure VMware Solution, el circuito ExpressRoute, que se incluye con Azure VMware Solution, debe asociarse a una instancia de Azure Virtual Network.  Durante la implementación, puede definir una nueva red virtual o elegir una existente.

El circuito ExpressRoute de Azure VMware Solution se conecta a una puerta de enlace de ExpressRoute en la instancia de Azure Virtual Network que va a definir en este paso.  

>[!IMPORTANT]
>Si elige una red virtual existente, debe seleccionar una que no tenga una subred de puerta de enlace ya existente.  

Si desea conectar el circuito ExpressRoute de Azure VMware Solution a una puerta de enlace de ExpressRoute existente, puede hacerlo después de la implementación.  

En resumen, ¿desea conectar Azure VMware Solution a una puerta de enlace existente de ExpressRoute?  

* **Sí** = identifique la red virtual que no se usa durante la implementación.
* **No** = seleccione una red virtual existente o cree una nueva durante la implementación.

En cualquier caso, documente lo que quiere hacer en este paso.

>[!NOTE]
>El entorno local y Azure VMware Solution ven esta red virtual, por lo que debe asegurarse de que el segmento IP que use en esa red virtual y las subredes no se superponen.

:::image type="content" source="media/pre-deployment/azure-vmware-solution-expressroute-diagram.png" alt-text="Identificación: segmento de dirección IP" border="false":::

## <a name="vmware-hcx-network-segments"></a>Segmentos de red de VMware HCX

VMware HCX es una tecnología incluida en Azure VMware Solution. Los casos de uso principales de VMware HCX son las migraciones de cargas de trabajo y la recuperación ante desastres. Si tiene previsto realizar alguna de ellas, es mejor planificar las redes ahora.   En otro caso, puede omitirla y continuar en el paso siguiente.

[!INCLUDE [hcx-network-segments](includes/hcx-network-segments.md)]

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha recopilado y documentado la información necesaria, continúe en la siguiente sección para crear la nube privada de Azure VMware Solution.

> [!div class="nextstepaction"]
> [Implementación de Azure VMware Solution](deploy-azure-vmware-solution.md)
