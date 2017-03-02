---
title: "Migración de AD RMS-Azure Information Protection: fase 4"
description: "La fase 4 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos 8 al 9 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: fc45ae10101460ea46bf2aa599b213a772eb5626
ms.lasthandoff: 02/24/2017


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
Este paso solo es válido si la topología de claves de inquilino que ha elegido es administrada por Microsoft, en lugar de ser administrada por el cliente (BYOK con el Almacén de claves de Azure).

Aunque este paso es opcional, se recomienda completarlo cuando la clave de inquilino de Azure Information Protection es administrada por Microsoft y se ha migrado desde AD RMS. Si vuelve a generar la clave en este escenario, protegerá su clave de inquilino de Azure Information Protection ante posibles infracciones de seguridad en la clave de AD RMS.

Si vuelve a generar la clave de inquilino de Azure Information Protection (que también se conoce como “revertir la clave”), se creará una clave y se archivará la clave original. Pero, como el cambio de una clave a otra no es inmediato, sino que se necesitan varias semanas, vuelva a generar la clave de inquilino de Azure Information Protection en cuanto se complete la migración, sin esperar hasta sospechar de una infracción de la clave original.

Para volver a generar la clave de inquilino de Azure Information Protection administrada por Microsoft, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) y abra una **incidencia de soporte técnico de Azure Information Protection con una solicitud para volver a generar la clave de Azure Information Protection después de la migración desde AD RMS**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Standard; la acción de volver a escribir la clave de inquilino no es un servicio de soporte técnico gratuito.


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo administrar la clave de inquilino de Azure Information Protection, vea [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

