---
title: "Migración de AD RMS-Azure Information Protection: fase 4"
description: "La fase 4 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos 8 al 9 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: d36f47e586ac1295dcc79e43a9e061b4c7c7fe1e
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="migration-phase-4---post-migration-tasks"></a>Fase de migración 4: Tareas posteriores a la migración

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*


Use la información siguiente para la fase 4 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos 8 y 9 de la [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-8-decommission-ad-rms"></a>Paso 8. Retire AD RMS

Quite el punto de conexión de servicio (SCP) de Active Directory para evitar que los equipos detecten la infraestructura local de Rights Management. Esta acción es opcional para los clientes existentes de los que ha migrado debido al redireccionamiento que ha configurado en el registro (por ejemplo, al ejecutar el script de migración). Sin embargo, quitar el SCP impedirá que nuevos clientes y servicios y herramientas potencialmente relacionados con RMS puedan encontrar el SCP cuando la migración haya finalizado y todas las conexiones deban pasar a Azure Rights Management Service. 

Para quitar el SCP, asegúrese de que ha iniciado sesión como administrador empresarial de un dominio y, posteriormente, use el siguiente procedimiento:

1. En la consola de Active Directory Rights Management Services, haga clic con el botón derecho en el clúster de AD RMS y, después, haga clic en **Propiedades**.

2. Haga clic en la pestaña **SCP** .

3. Active la casilla **Cambiar SCP** .

4. Seleccione **Quitar SCP actual** y después haga clic en **Aceptar**.

Supervise la actividad de los servidores de AD RMS. Para ello, por ejemplo, compruebe las [solicitudes en el informe de mantenimiento del sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [tabla ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) o realice una [auditoría del acceso de los usuarios a contenido protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Cuando haya confirmado que los clientes de RMS ya no se comunican con estos servidores y que los clientes usan Azure Information Protection correctamente, puede quitar el rol de servidor de AD RMS de estos servidores. Si usa servidores dedicados, le recomendamos que, como precaución, primero apague los servidores durante un período de tiempo para asegurarse de que no haya ningún problema notificado que necesite reiniciar estos servidores (de esta forma, se garantiza la continuidad del servicio mientras investiga el motivo por el que los clientes no usan Azure Information Protection).

Después de retirar los servidores de AD RMS, seguramente le interese revisar las plantillas en el Portal de Azure clásico y consolidarlas para que los usuarios tengan menos opciones entre las que elegir, volver a configurarlas o incluso agregar plantillas nuevas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para más información, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

## <a name="step-9-re-key-your-azure-information-protection-tenant-key"></a>Step 9. Volver a generar la clave de inquilino de Azure Information Protection
Este paso es necesario cuando la migración está completa si la implementación de AD RMS usaba el modo criptográfico 1 de RMS, porque al volver a generar la clave se crea una nueva clave de inquilino que usa el modo criptográfico 2 de RMS. Se admite el uso de Azure RMS con el modo criptográfico 1 únicamente durante el proceso de migración.

Este paso es opcional pero recomendado cuando se completa la migración, incluso si se estaba ejecutando en el modo criptográfico 2 de RMS. Si vuelve a generar la clave en este escenario, protegerá su clave de inquilino de Azure Information Protection ante posibles infracciones de seguridad en la clave de AD RMS.

Si vuelve a generar la clave de inquilino de Azure Information Protection (que también se conoce como “revertir la clave”), se creará una clave y se archivará la clave original. Pero, como el cambio de una clave a otra no es inmediato, sino que se necesitan varias semanas, vuelva a generar la clave de inquilino de Azure Information Protection en cuanto se complete la migración, sin esperar hasta sospechar de una infracción de la clave original.

Para volver a generar la clave de inquilino de Azure Information Protection:

- Si Microsoft administra la clave de inquilino, póngase en contacto con el [soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) y abra una incidencia de soporte técnico de **Azure Information Protection con una solicitud para volver a generar la clave de Azure Information Protection después de la migración desde AD RMS**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Standard; la acción de volver a escribir la clave de inquilino no es un servicio de soporte técnico gratuito.

- Si usted administra la clave de inquilino (BYOK), en Azure Key Vault debe volver a generar la clave que usa para el inquilino de Azure Information Protection y, luego, ejecutar nuevamente el cmdlet [Use-AadrmKeyVaultKey](/powershell/aadrm/vlatest/use-aadrmkeyvaultkey) para especificar la nueva dirección URL de la clave. 

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo administrar la clave de inquilino de Azure Information Protection, vea [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
