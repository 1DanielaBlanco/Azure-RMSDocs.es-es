---
title: Precio y restricciones de Bring your own key (BYOK, Traiga su propia clave) - Azure Information Protection
description: Conozca las restricciones de uso de claves administradas por el cliente, conocidas como "Bring Your Own Key" (BYOK) con Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/18/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: c27e94caa2a03c31d99b4fbfd702d5e205b86971
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39491078"
---
# <a name="byok-pricing-and-restrictions"></a>Precio y restricciones de BYOK

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*


Las organizaciones que tienen una suscripción con Azure Information Protection pueden configurar su inquilino de Azure Information Protection para usar una clave administrada por el cliente (BYOK) y [registrar su uso](./log-analyze-usage.md). 

La clave debe almacenarse en Azure Key Vault, lo que requiere una suscripción de Azure. Para usar una clave protegida por HSM, debe tener el nivel de servicio Premium de Azure Key Vault. El uso de las claves en el Almacén de claves de Azure conlleva un cargo mensual. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/pricing/details/key-vault/).

Si usa Azure Key Vault para la clave de inquilino de Azure Information Protection, se recomienda que use un almacén de claves dedicado para esta clave para asegurarse de que solo la use el servicio Azure Rights Management. Esta configuración garantiza que las llamadas de otros servicios no superen los [límites de servicio](/azure/key-vault/key-vault-service-limits) para el almacén de claves, lo que podría limitar los tiempos de respuesta del servicio Azure Rights Management.  

Además, debido a que cada servicio que utiliza Azure Key Vault normalmente tiene diferentes requisitos de administración de claves, se recomienda una suscripción de Azure independiente para este almacén de claves, lo que ayuda a protegerse contra los errores de configuración. 

Sin embargo, si desea compartir una suscripción de Azure con otros servicios que utilizan Azure Key Vault, asegúrese de que la suscripción comparte un conjunto común de administradores. Esta precaución significa que los administradores que utilizan esa suscripción tienen un buen conocimiento de todas las claves a las que tienen acceso, por lo que es menos probable que las configuren incorrectamente. Por ejemplo, una suscripción compartida de Azure si los administradores de la clave de inquilino de Azure Information Protection son los mismos que administran las claves de la clave de cliente de Office 365 y CRM Online. Pero si los administradores que administran las claves de la clave de cliente o CRM Online no son las mismas personas que administran su clave de inquilino de Azure Information Protection, le recomendamos que no comparta su suscripción de Azure para Azure Information Protection.

## <a name="benefits-of-using-azure-key-vault"></a>Ventajas de usar Azure Key Vault

Además de emplear el registro de uso de Azure Information Protection, para una mayor seguridad, puede hacer referencias cruzadas con el [registro de Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-logging/) para supervisar de manera independiente que solo el servicio Azure Rights Management use esta clave. Si es necesario, puede revocar de inmediato el acceso a la clave eliminando los permisos en el almacén de claves.

Otras ventajas de usar Azure Key Vault para la clave de inquilino de Azure Information Protection:

- Azure Key Vault proporciona una solución de administración de claves centralizada que ofrece una solución de administración coherente para muchos servicios basados en la nube e incluso servicios locales que usan cifrado.

- Azure Key Vault admite diversas interfaces integradas para la administración de claves, incluidas PowerShell, CLI, API de REST y Portal de Azure. Se han integrado otros servicios y herramientas con Key Vault, con el fin de ofrecer funcionalidades optimizadas para tareas específicas, como la supervisión. Por ejemplo, puede analizar los registros de uso de claves mediante Log Analytics desde Operations Management Suite, establecer alertas cuando se cumplen los criterios especificados, etc.

- Azure Key Vault proporciona la separación del rol como práctica recomendada de seguridad reconocida. Los administradores de Azure Information Protection pueden centrarse en administrar la protección y la clasificación de datos, mientras que los administradores de Azure Key Vault pueden centrarse en administrar claves de cifrado y las directivas especiales que requieran para la seguridad o el cumplimiento.

- Algunas organizaciones tienen restricciones en lo que respecta al lugar en el que debe residir la clave maestra. Azure Key Vault proporciona un alto nivel de control sobre el lugar en el que se almacenará la clave maestra, ya que el servicio está disponible en muchas regiones de Azure. Actualmente puede elegir entre 28 regiones de Azure, aunque esta cifra probablemente aumente. Para obtener más información, consulte la página [Productos disponibles por región] (https://azure.microsoft.com/regions/services/)) en el sitio de Azure.

Además de la administración de claves, Azure Key Vault ofrece a los administradores de seguridad la misma experiencia de administración para el almacenamiento, el acceso y la administración de certificados y secretos (por ejemplo, contraseñas) para otros servicios y aplicaciones que usan cifrado. 

Para obtener más información sobre Azure Key Vault, consulte [¿Qué es el Almacén de claves de Azure?](/azure/key-vault/key-vault-whatis) y visite el [blog del equipo de Azure Key Vault](https://cloudblogs.microsoft.com/kv/) para obtener la información más reciente y documentarse sobre cómo usan esta tecnología otros servicios.

## <a name="restrictions-when-using-byok"></a>Restricciones en el uso de BYOK

BYOK y el registro de uso funcionan perfectamente con todas las aplicaciones que se integran con el servicio Azure Rights Management usado por Azure Information Protection. Aquí se incluyen servicios en la nube, como SharePoint Online, servidores locales que ejecutan Exchange y SharePoint y que usan el servicio Azure Rights Management a través del conector RMS, y aplicaciones cliente como Office 2013 y Office 2016. Obtiene los registros de uso de claves con independencia de la aplicación que realiza solicitudes al servicio Azure Rigths Management.

Si ya ha habilitado IRM de Exchange Online importando el dominio de publicación de confianza (TPD) de Azure RMS, siga las instrucciones de [Configuración de nuevas capacidades del cifrado de mensajes de Office 365 sobre Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e) (Set up new Office 365 Message Encryption capabilities built on top of Azure Information Protection) para habilitar las nuevas capacidades en Exchange Online que admiten el uso de BYOK para Azure Information Protection.

## <a name="next-steps"></a>Pasos siguientes

Si ha tomado la decisión de administrar su propia clave, vaya a [Implementación de BYOK para la clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

Si ha decidido permanecer con la configuración predeterminada con la que Microsoft administra su clave, consulte la sección [Pasos siguientes](plan-implement-tenant-key.md#next-steps) del artículo Planeamiento e implementación de su clave de inquilino de Azure Information Protection.

