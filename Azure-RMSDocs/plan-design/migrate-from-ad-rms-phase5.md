---
title: "Migración de AD RMS-Azure Information Protection: fase 5"
description: "Fase 5 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 10 al 12 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: aeffd9780001f4c91ea8600f11d8fc3b36abce73
ms.sourcegitcommit: 238657f9450f18213c2b9fb453174df0ce1f1aef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2017
---
# <a name="migration-phase-5---post-migration-tasks"></a>Fase 5 de la migración: tareas posteriores a la migración

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


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

Después de desaprovisionar los servidores de AD RMS, seguramente le interese revisar las plantillas en Azure Portal. Por ejemplo, puede convertirlas en etiquetas, consolidarlas para que los usuarios tengan menos opciones entre las que elegir o volver a configurarlas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](../deploy-use/configure-policy-templates.md).

>[!IMPORTANT]
> Al final de esta migración, no se puede usar el clúster de AD RMS con Azure Information Protection y la opción Hold your own key (HYOK). Si decide usar HYOK para una etiqueta de Azure Information Protection, debido a los redireccionamientos que hay ahora, el clúster de AD RMS que use debe tener direcciones URL de licencias diferentes de las de los clústeres que ha migrado.

## <a name="step-11-remove-onboarding-controls"></a>Paso 11. Quitar controles de incorporación

Una vez que se han migrado todos los clientes existentes a Azure Information Protection, no hay ninguna razón para seguir usando los controles de incorporación y mantener el grupo **AIPMigrated** que ha creado para el proceso de migración. 

Quite primero los controles de incorporación y, después, podrá eliminar el grupo **AIPMigrated** y cualquier tarea de implementación de software que haya creado para implementar los redireccionamientos.

Para quitar los controles de incorporación:

1. En una sesión de PowerShell, conéctese al servicio de Azure Rights Management y, cuando se le pida, especifique las credenciales de administrador global:

        Connect-Aadrmservice

2. Ejecute el siguiente comando y escriba **Y** para confirmar:

        Set-AadrmOnboardingControlPolicy -UseRmsUserLicense $False

3. Confirme que ya no están establecidos los controles de incorporación:

        Get-AadrmOnboardingControlPolicy

    En la salida, en **Licencia** debería aparecer **False**, tampoco debería mostrarse ningún GUID para **SecurityGroupOjbectId**.

## <a name="step-12-rekey-your-azure-information-protection-tenant-key"></a>Paso 12. Regenerar su clave de inquilino de Azure Information Protection
Este paso es necesario al finalizar la migración si la implementación de AD RMS usaba el modo criptográfico 1 de RMS. Al regenerar las claves, se crea una clave de inquilino que usa el modo criptográfico 2 de RMS. Se admite el modo criptográfico 1 con Azure Information Protection únicamente durante el proceso de migración.

Si regenera la clave al finalizar la migración, también ayudará a proteger su clave de inquilino de Azure Information Protection ante posibles infracciones de seguridad en la clave de AD RMS.

Si regenera la clave de inquilino de Azure Information Protection (que también se conoce como "revertir la clave"), se creará una clave y se archivará la clave original. Pero el paso de una clave a otra no es inmediato, sino que requiere unas cuantas semanas. Por este motivo, no espere hasta sospechar que se ha producido una infracción en la clave original y vuelva a generar la clave de inquilino de Azure Information Protection en cuanto finalice la migración.

Para regenerar su clave de inquilino de Azure Information Protection:

- Si Microsoft administra la clave de inquilino, póngase en contacto con [Soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) y abra una incidencia de soporte técnico de **Azure Information Protection con una solicitud para regenerar la clave de Azure Information Protection después de la migración desde AD RMS**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Estándar; la acción de regenerar la clave de inquilino no es un servicio de soporte técnico gratuito.

- Si usted administra la clave de inquilino (BYOK), en Azure Key Vault debe regenerar la clave que usa para el inquilino de Azure Information Protection y, luego, ejecutar nuevamente el cmdlet [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) para especificar la nueva dirección URL de la clave. 

Para más información sobre cómo administrar la clave de inquilino de Azure Information Protection, vea [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
