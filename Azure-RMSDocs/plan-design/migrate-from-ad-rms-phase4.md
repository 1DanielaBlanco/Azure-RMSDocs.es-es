---
title: "Migración desde AD RMS a Azure Rights Management - Fase 4 | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/29/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: d51e7bdd-2e5c-4304-98cc-cf2e7858557d
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ea4dd88ed749092fd02135d8ca25b621f74fe72f
ms.openlocfilehash: 7ed3569475362272ace055862fe8bb3ee072036a


---

# Fase de migración 4: Tareas posteriores a la migración

*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*


Use la siguiente información para la fase 4 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen los pasos 8 y 9 del tema [Migración desde AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Paso 8. Retire AD RMS

Opcional: quite el punto de conexión de servicio (SCP) de Active Directory para evitar que los equipos detecten la infraestructura local de Rights Management. Esta acción es opcional debido al redireccionamiento configurado en el registro (por ejemplo, al ejecutar el script de migración). Para quitar el punto de conexión de servicio, use la herramienta de registro de AD SCP desde el [kit de herramientas de administración de Rights Management Services](http://www.microsoft.com/download/details.aspx?id=1479).

Supervise la actividad de los servidores de AD RMS. Para ello, por ejemplo, compruebe las [solicitudes en el informe de mantenimiento del sistema](https://technet.microsoft.com/library/ee221012%28v=ws.10%29.aspx), la [tabla ServiceRequest](http://technet.microsoft.com/library/dd772686%28v=ws.10%29.aspx) o realice una [auditoría del acceso de los usuarios a contenido protegido](http://social.technet.microsoft.com/wiki/contents/articles/3440.ad-rms-frequently-asked-questions-faq.aspx). Cuando haya confirmado que los clientes de RMS ya no se comunican con estos servidores y que los clientes están utilizando Azure RMS correctamente, puede quitar el rol de servidor de AD RMS de estos servidores. Si usa servidores dedicados, es preferible aplicar una medida de cautela basada en cerrar primero los servidores durante un período de tiempo para asegurarse de que no hay ningún problema notificado que requiera reiniciar estos servidores para garantizar la continuidad del servicio mientras investiga por qué los clientes no usan Azure RMS.

Después de retirar los servidores de AD RMS, seguramente le interese revisar las plantillas en el Portal de Azure clásico y consolidarlas para que los usuarios tengan menos opciones entre las que elegir, volver a configurarlas o incluso agregar plantillas nuevas. También sería una buena oportunidad para publicar las plantillas predeterminadas. Para más información, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).

## Step 9. Vuelva a escribir su clave de inquilino de Azure RMS.
Este paso es necesario cuando la migración está completa si la implementación de AD RMS usaba el modo criptográfico 1 de RMS, porque al volver a generar la clave se crea una nueva clave de inquilino que usa el modo criptográfico 2 de RMS. Se admite el uso de Azure RMS con el modo criptográfico 1 únicamente durante el proceso de migración.

Este paso es opcional pero se recomienda cuando la migración se ha completado incluso si estuviera ejecutando el modo criptográfico 2 de RMS, porque ayuda a proteger la clave de inquilino de Azure RMS de posibles infracciones de seguridad para su clave de AD RMS. Si vuelve a definir la clave del inquilino de Azure RMS (lo que también se conoce como "revertir su clave"), se crea una nueva clave y se archiva la clave original. Sin embargo, dado que el paso de una clave a otra no es inmediato sino que requiere unas cuantas semanas, no espere hasta sospechar de una infracción de la clave original y vuelva a definir la clave de inquilino de Azure RMS en cuanto se complete la migración.

Vuelva a definir la clave del inquilino de Azure RMS:

-   Si Microsoft administra su clave de inquilino de Azure RMS: para hacer esto, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) para abrir un **caso de soporte técnico de Azure Rights Management con una solicitud para volver a escribir la clave de inquilino de Azure RMS**. Debe demostrar que es un administrador del inquilino de Azure RMS y comprender que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Standard; la acción de volver a escribir la clave de inquilino no es un servicio de soporte técnico gratuito.

-   Si el usuario (BYOK) administra la clave de inquilino de Azure RMS: repita el procedimiento BYOK para generar y crear una nueva clave a través de Internet o en persona.

Para obtener más información sobre cómo administrar la clave de inquilino de Azure RMS, vea [Operations for Your Azure Rights Management Tenant Key (Operaciones para la clave de inquilino de Azure Rights Management)](../deploy-use/operations-tenant-key.md).

## Pasos siguientes

Ahora que ha completado la migración, revise el [mapa de ruta de implementación](deployment-roadmap.md) para identificar las tareas de implementación que necesite realizar.




<!--HONumber=Jul16_HO3-->


