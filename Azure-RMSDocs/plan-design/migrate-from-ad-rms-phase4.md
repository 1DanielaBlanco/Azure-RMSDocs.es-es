---
# required metadata

title: Migración desde AD RMS a Azure Rights Management - Fase 4 | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d


# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Fase de migración 4: Tareas posteriores a la migración

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Use la siguiente información para la fase 4 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen los pasos 8 y 9 del tema [Migrating from AD RMS to Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md) (Migración desde AD RMS a Azure Rights Management)..


## Paso 8. Retire AD RMS

Opcional: quite el punto de conexión de servicio (SCP) de Active Directory para evitar que los equipos detecten la infraestructura local de Rights Management. Esta acción es opcional debido al redireccionamiento configurado en el registro (por ejemplo, al ejecutar el script de migración). Para quitar el punto de conexión de servicio, use la herramienta de registro de AD SCP del [kit de herramientas de administración de Rights Management Services](http://www.microsoft.com/download/details.aspx?id=1479)..

Supervise la actividad de los servidores de AD RMS. Para ello, por ejemplo, compruebe las [solicitudes en el informe de mantenimiento del sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [tabla ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) o realice una [auditoría del acceso de los usuarios a contenido protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Cuando haya confirmado que los clientes de RMS ya no se comunican con estos servidores y que los clientes están utilizando Azure RMS correctamente, puede quitar el rol de servidor de AD RMS de estos servidores. Si usa servidores dedicados, es preferible aplicar una medida de cautela basada en cerrar primero los servidores durante un período de tiempo para asegurarse de que no hay ningún problema notificado que requiera reiniciar estos servidores para garantizar la continuidad del servicio mientras investiga por qué los clientes no usan Azure RMS.

Después de retirar los servidores de AD RMS, seguramente le interese revisar las plantillas en el Portal de Azure clásico y consolidarlas para que los usuarios tengan menos opciones entre las que elegir, volver a configurarlas o incluso agregar plantillas nuevas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para obtener más información, consulte [Configuring custom templates for Azure Rights Management](../deploy-use/configure-custom-templates.md) (Configurar plantillas personalizadas para Azure Rights Management)..

## Step 9. Vuelva a escribir su clave de inquilino de Azure RMS.
Este paso es necesario cuando la migración está completa si la implementación de AD RMS usaba el modo criptográfico 1 de RMS, porque al volver a generar la clave se crea una nueva clave de inquilino que usa el modo criptográfico 2 de RMS. Se admite el uso de Azure RMS con el modo criptográfico 1 únicamente durante el proceso de migración.

Este paso es opcional pero se recomienda cuando la migración se ha completado incluso si estuviera ejecutando el modo criptográfico 2 de RMS, porque ayuda a proteger la clave de inquilino de Azure RMS de posibles infracciones de seguridad para su clave de AD RMS. Si vuelve a definir la clave del inquilino de Azure RMS (lo que también se conoce como "revertir su clave"), se crea una nueva clave y se archiva la clave original. Sin embargo, dado que el paso de una clave a otra no es inmediato, sino que requiere unas cuantas semanas, no espere hasta sospechar de una infracción de la clave original y, en su lugar, vuelva a definir la clave del inquilino de RMS en cuanto se complete la migración.

Vuelva a definir la clave del inquilino de Azure RMS:

-   Si Microsoft administra su clave de inquilino de RMS: llame a los servicios de soporte técnico de Microsoft (CSS) y demuestre que es el administrador del inquilino de RMS.

-   Si la clave de inquilino de RMS está administrada por el usuario (BYOK): Repita el procedimiento BYOK para generar y crear una nueva clave a través de Internet o en persona.

Para obtener más información sobre cómo administrar la clave de inquilino de RMS, consulte [Operations for your Azure Rights Management tenant key](../deploy-use/operations-tenant-key.md) (Operaciones para la clave de inquilino de Azure Rights Management)..

## Pasos siguientes

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.



<!--HONumber=Apr16_HO4-->


