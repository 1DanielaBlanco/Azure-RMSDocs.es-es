---
title: "Administración de cliente: operaciones de ciclo de vida de clave de inquilino de AIP"
description: "Información sobre las operaciones del ciclo de vida que son relevantes si administra la clave de inquilino para Azure Information Protection (el escenario Bring Your Own Key o BYOK)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/22/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2f3ae7a0558cf209f3ec710a5114dbbc9a0dda9d
ms.sourcegitcommit: cd3320fa34acb90f05d5d3e0e83604cdd46bd9a9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2017
---
# <a name="customer-managed-tenant-key-life-cycle-operations"></a>Administración de cliente: operaciones de ciclo de vida de clave de inquilino

>*Se aplica a: Azure Information Protection, Office 365*

Si administra su clave de inquilino para Azure Information Protection (el escenario Bring Your Own Key o BYOK), en las secciones siguientes encontrará más información sobre las operaciones del ciclo de vida relevantes para esta topología.

## <a name="revoke-your-tenant-key"></a>Revocar su clave de inquilino
En Azure Key Vault puede cambiar los permisos en el almacén de claves que contiene su clave de inquilino de Azure Information Protection para que el servicio Azure Rights Management ya no pueda acceder a la clave. Pero, tras hacer esto, ningún usuario podrá abrir los documentos y correos electrónicos que se protegieron anteriormente con el servicio Azure Rights Management.

Al cancelar la suscripción a Azure Information Protection, la solución deja de usar la clave de inquilino y no es necesario realizar ninguna otra acción.

## <a name="rekey-your-tenant-key"></a>Regenerar su clave de inquilino
La acción de regenerar la clave también se conoce como revertir la clave. Al realizar esta operación, Azure Information Protection deja de usar la clave de inquilino existente para proteger documentos y correos electrónicos, y comienza a usar otra clave. Las directivas y las plantillas se retiran inmediatamente, pero el cambio es gradual para los clientes y los servicios existentes que usen Azure Information Protection. De este modo, durante cierto tiempo, parte del contenido nuevo sigue protegido por la clave de inquilino anterior.

Para regenerar la clave, debe configurar el objeto de clave de inquilino y especificar la clave alternativa que se usará. A continuación, se marcará automáticamente la clave usada anteriormente como archivada para Azure Information Protection. Esta configuración garantiza que el contenido que se haya protegido con esta clave seguirá estando disponible.

Ejemplos de cuándo tendrá que regenerar la clave de Azure Information Protection:

- La compañía se ha dividido en una o dos compañías. Cuando regenera la clave de inquilino, la nueva empresa no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

- Quiere cambiar de una topología de administración de claves a otra. 

- Cree que la copia maestra de su clave de inquilino (la copia en su posesión) está en peligro.

Para regenerar la clave en otra clave que administre, puede crear una clave nueva en Azure Key Vault o usar una distinta que ya esté en Azure Key Vault. Después, siga el mismo procedimiento que usó para implementar BYOK para Azure Information Protection.

1. Solo si la nueva clave está en un almacén de claves diferente al que ya está usando para Azure Information Protection: permita que Azure Information Protection use el almacén de claves mediante el cmdlet [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy).

2. Si Azure Information Protection aún no conoce la clave que quiere usar, ejecute el cmdlet [Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey).

3. Configure el objeto de clave de inquilino mediante el cmdlet [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties).

Para más información sobre cada uno de estos pasos:

- Para regenerar la clave a otra clave que administra, vea [Implementación de BYOK para la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

- Para regenerar la clave y cambiar a una clave administrada por Microsoft, vea la sección [Regenerar su clave de inquilino](operations-microsoft-managed-tenant-key.md#rekey-your-tenant-key) para operaciones administradas por Microsoft.

## <a name="backup-and-recover-your-tenant-key"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Es responsable de realizar copias de seguridad de su clave de inquilino. Si ha generado su clave de inquilino en un HSM de Thales, para realizar una copia de seguridad de la clave acortada, el archivo de Word y las tarjetas de administrador.

Como ha transferido la clave según el procedimiento de [Implementación de BYOK para la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key), Key Vault conservará el archivo de clave acortada como medida de protección en caso de que se produzcan errores en algún nodo de servicio. Este archivo está vinculado al mundo de la seguridad para la región o instancia específica de Azure. Sin embargo, no considere esto una copia de seguridad completa. Por ejemplo, si alguna vez necesita una copia de texto sin formato de la clave para usarla fuera de un HSM de Thales, Azure Key Vault no podrá recuperarla, ya que solo tiene una copia no recuperable.

## <a name="export-your-tenant-key"></a>Exportar su clave de inquilino
Si usa BYOK, no podrá exportar su clave de inquilino desde Azure Key Vault o desde Azure Information Protection. La copia del Almacén de claves de Azure no se puede recuperar. 

## <a name="respond-to-a-breach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegida, pueden encontrarse vulnerabilidades en la tecnología de generación de claves actual, así como en las longitudes y los algoritmos actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus recursos, Microsoft enviará una notificación por correo electrónico a los administradores de su inquilino de Azure Information Protection, usando para ello la dirección que haya especificado al suscribirse.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta depende de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Regenere su clave de inquilino. Consulte [Regenerar su clave de inquilino](#rkey-your-tenant-key).|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|Regenerar la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en la tecnología HSM de generación actual.|Microsoft debe actualizar los HSM. Si no hay motivos para creer que la vulnerabilidad haya afectado a las claves, Microsoft indicará a todos los clientes que renueven sus claves de inquilino.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft necesita actualizar Azure Key Vault o Azure Information Protection para que admitan nuevos algoritmos y claves más largas que sean resistentes, así como indicar a todos los clientes que renueven sus claves de inquilino.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

