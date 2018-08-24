---
title: 'Migración de AD RMS-Azure Information Protection: fase 5'
description: Fase 5 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 10 al 12 de la migración de AD RMS a Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/22/2018
ms.topic: article
ms.service: information-protection
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: b1092a8a23af5249a3b74968d2de2ee1cc2b71fe
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42805832"
---
# <a name="migration-phase-5---post-migration-tasks"></a>Fase 5 de la migración: tareas posteriores a la migración

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Use la información siguiente para la fase 5 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos del 10 al 12 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

## <a name="step-10-deprovision-ad-rms"></a>Paso 10. Desaprovisionamiento de AD RMS

Quite el punto de conexión de servicio (SCP) de Active Directory para evitar que los equipos detecten la infraestructura local de Rights Management. Esta acción es opcional para los clientes existentes de los que ha migrado debido al redireccionamiento que ha configurado en el registro (por ejemplo, al ejecutar el script de migración). Sin embargo, si quita el SCP, impide que nuevos clientes y servicios y herramientas potencialmente relacionados con RMS puedan encontrar el SCP cuando la migración haya finalizado. En ese momento, todas las conexiones del equipo deberían pasar al servicio Azure Rights Management. 

Para quitar el SCP, asegúrese de que ha iniciado sesión como administrador empresarial de un dominio y, posteriormente, use el siguiente procedimiento:

1. En la consola de Active Directory Rights Management Services, haga clic con el botón derecho en el clúster de AD RMS y, después, haga clic en **Propiedades**.

2. Haga clic en la pestaña **SCP** .

3. Active la casilla **Cambiar SCP** .

4. Seleccione **Quitar SCP actual** y después haga clic en **Aceptar**.

Supervise ahora la actividad de los servidores de AD RMS. Por ejemplo, compruebe las [solicitudes en el informe de mantenimiento del sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [tabla ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) o realice una [auditoría del acceso de los usuarios a contenido protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). 

Cuando haya confirmado que los clientes de RMS ya no se comunican con estos servidores y que los clientes usan Azure Information Protection correctamente, puede quitar el rol de servidor de AD RMS de estos servidores. Si usa servidores dedicados, es preferible aplicar una medida de cautela basada en cerrar primero los servidores durante un período de tiempo. De este modo, tiene tiempo de asegurarse de que no hay ningún problema notificado que requiera reiniciar estos servidores para garantizar la continuidad del servicio mientras investiga por qué los clientes no usan Azure Information Protection.

Después de desaprovisionar los servidores de AD RMS, seguramente le interese revisar las plantillas en Azure Portal. Por ejemplo, puede convertirlas en etiquetas, consolidarlas para que los usuarios tengan menos opciones entre las que elegir o volver a configurarlas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](./configure-policy-templates.md).

>[!IMPORTANT]
> Al final de esta migración, no se puede usar el clúster de AD RMS con Azure Information Protection y la opción Hold your own key (HYOK). Si decide usar HYOK para una etiqueta de Azure Information Protection, debido a los redireccionamientos que hay ahora, el clúster de AD RMS que use debe tener direcciones URL de licencias diferentes de las de los clústeres que ha migrado.

## <a name="step-11-complete-client-migration-tasks"></a>Paso 11. Completar tareas de migración de cliente

En los clientes de dispositivos móviles y los equipos Mac, quite los registros de DNS SRV que creó al implementar la [extensión de AD RMS para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx).

Cuando estos cambios de DNS se hayan propagado, dichos clientes detectarán y empezarán a usar automáticamente el servicio Azure Rights Management. Sin embargo, los equipos Mac que ejecutan Office Mac almacenan en caché la información de AD RMS. En el caso de estos equipos, este proceso puede tardar hasta 30 días. 

Para obligar a los equipos Mac a ejecutar el proceso de detección inmediatamente, en la cadena de claves, busque "adal" y elimine todas las entradas ADAL. Luego, ejecute los siguientes comandos en estos equipos:

````

rm -r ~/Library/Cache/MSRightsManagement

rm -r ~/Library/Caches/com.microsoft.RMS-XPCService

rm -r ~/Library/Caches/Microsoft\ Rights\ Management\ Services

rm -r ~/Library/Containers/com.microsoft.RMS-XPCService

rm -r ~/Library/Containers/com.microsoft.RMSTestApp

rm ~/Library/Group\ Containers/UBF8T346G9.Office/DRM.plist

killall cfprefsd

````

Una vez que se han migrado todos los equipos Windows existentes a Azure Information Protection, no hay ninguna razón para seguir usando los controles de incorporación y mantener el grupo **AIPMigrated** que ha creado para el proceso de migración. 

Quite primero los controles de incorporación y, después, puede eliminar el grupo **AIPMigrated** y cualquier método de implementación de software que haya creado para implementar los scripts de migración.

Para quitar los controles de incorporación:

1. En una sesión de PowerShell, conéctese al servicio de Azure Rights Management y, cuando se le pida, especifique las credenciales de administrador global:

        Connect-Aadrmservice

2. Ejecute el siguiente comando y escriba **Y** para confirmar:

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False
    
    Tenga en cuenta que este comando quita cualquier obligatoriedad de licencia del servicio de protección Azure Rights Management, de modo que todos los equipos pueden proteger documentos y correos electrónicos.

3. Confirme que ya no están establecidos los controles de incorporación:

        Get-AadrmOnboardingControlPolicy

    En la salida, en **Licencia** debería aparecer **False**, tampoco debería mostrarse ningún GUID para **SecurityGroupOjbectId**.

Por último, si usa Office 2010 y ha habilitado la tarea **Administración de plantillas de directiva de derechos de AD RMS (automatizada)** en la biblioteca del Programador de tareas de Windows, deshabilítela porque no se usa en el cliente de Azure Information Protection. Esta tarea normalmente se habilita mediante la directiva de grupo y admite una implementación de AD RMS. Puede encontrar esta tarea en la ubicación siguiente: **Microsoft** > **Windows** > **Active Directory Rights Management Services Client**

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Paso 12. Regenerar su clave de inquilino de Azure Information Protection

Este paso está recomendado al finalizar la migración si la implementación de AD RMS usaba el modo criptográfico 1 de RMS. Con la regeneración de la clave, la protección pasa a usar el modo criptográfico 2 de RMS. 

Aunque la implementación de AD RMS usase el modo criptográfico 2, le recomendamos que realice este paso, ya que una clave nueva le ayuda a proteger su inquilino de posibles infracciones de seguridad en la clave de AD RMS.

Al regenerar la clave de inquilino de Azure Information Protection, se archivará la clave activa, y Azure Information Protection empezará a usar la clave que especifique. Esta clave podría ser una clave que cree en Azure Key Vault, o bien la clave predeterminada que se creó automáticamente para su inquilino.

El paso de una clave a otra no es inmediato, sino que requiere unas cuantas semanas. Por este motivo, no espere hasta sospechar que se ha producido una infracción en la clave original e inicie este proceso en cuanto finalice la migración.

Para regenerar su clave de inquilino de Azure Information Protection:

- **Si Microsoft administra su clave de inquilino**: ejecute el cmdlet de PowerShell [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) y especifique el identificador de la clave que se creó automáticamente para su inquilino. Puede identificar el valor que debe especificar mediante el cmdlet [Get-AadrmKeys](/powershell/module/aadrm/get-aadrmkeys). La clave que se creó automáticamente para el inquilino tiene la fecha de creación más antigua, por lo que se puede identificar mediante el comando siguiente:
    
        (Get-AadrmKeys) | Sort-Object CreationTime | Select-Object -First 1

- [Si usted administra la clave de inquilino (BYOK)](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey): debe repetir el proceso de creación de una clave en Azure Key Vault para el inquilino de Azure Information Protection y, luego, ejecutar nuevamente el cmdlet **Use-AadrmKeyVaultKey** para especificar el URI de esta clave nueva. 

Para más información sobre cómo administrar la clave de inquilino de Azure Information Protection, consulte [Operaciones para la clave de inquilino de Azure Information Protection](./operations-tenant-key.md).


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.

