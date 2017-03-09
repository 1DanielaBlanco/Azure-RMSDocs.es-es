---
title: Precio y restricciones de Bring your own key (BYOK, Traiga su propia clave) - Azure Information Protection
description: "Conozca las restricciones de uso de claves administradas por el cliente, conocidas como “Bring your own key” (BYOK, Traiga su propia clave) con Azure RMS."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: c05521faed2cd8a7f9d32d81cd6899161e858153
ms.lasthandoff: 02/24/2017


---

# <a name="byok-pricing-and-restrictions"></a>Precio y restricciones de BYOK

>*Se aplica a: Azure Information Protection, Office 365*


Las organizaciones que tienen una suscripción con Azure Information Protection pueden configurar su inquilino de Azure Information Protection para usar una clave administrada por el cliente (BYOK) y [registrar su uso](../deploy-use/log-analyze-usage.md) sin costo adicional. 

La clave debe almacenarse en Azure Key Vault, que requiere una suscripción de Azure de pago (o de prueba), y debe usar el nivel de servicio Premium de Azure Key Vault para admitir claves protegidas con HSM. El uso de las claves protegidas con HSM en Azure Key Vault conlleva un cargo mensual. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Si usa Azure Key Vault para la clave de inquilino de Azure Information Protection, se recomienda que use un almacén de claves dedicado para esta clave con una suscripción dedicada, para asegurarse de que solo la use el servicio Azure Rights Management. 

## <a name="benefits-of-using-azure-key-vault"></a>Ventajas de usar Azure Key Vault

Además de emplear el registro de uso de Azure Information Protection, para una mayor seguridad, puede hacer referencias cruzadas con el [registro de Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-logging/) para supervisar de manera independiente que solo el servicio Azure Rights Management use esta clave. Si es necesario, puede revocar de inmediato el acceso a la clave eliminando los permisos en el almacén de claves.

Otras ventajas de usar Azure Key Vault para la clave de inquilino de Azure Information Protection:

- Azure Key Vault proporciona una solución de administración de claves centralizada que ofrece una solución de administración coherente para muchos servicios basados en la nube e incluso servicios locales que usan cifrado.

- Azure Key Vault admite diversas interfaces integradas para la administración de claves, incluidas PowerShell, CLI, API de REST y Portal de Azure. Se han integrado otros servicios y herramientas con Key Vault, con el fin de ofrecer funcionalidades optimizadas para tareas específicas, como la supervisión. Por ejemplo, puede analizar los registros de uso de claves mediante Log Analytics desde Operations Management Suite, establecer alertas cuando se cumplen los criterios especificados, etc.

- Azure Key Vault proporciona la separación del rol como práctica recomendada de seguridad reconocida. Los administradores de Azure Information Protection pueden centrarse en administrar la protección y la clasificación de datos, mientras que los administradores de Azure Key Vault pueden centrarse en administrar claves de cifrado y las directivas especiales que requieran para la seguridad o el cumplimiento.

- Algunas organizaciones tienen restricciones en lo que respecta al lugar en el que debe residir la clave maestra. Azure Key Vault proporciona un alto nivel de control sobre el lugar en el que se almacenará la clave maestra, ya que el servicio está disponible en muchas regiones de Azure. Actualmente puede elegir entre 28 regiones de Azure, aunque esta cifra probablemente aumentará. Para obtener más información, consulte la página [Productos disponibles por región] (https://azure.microsoft.com/regions/services/) en el sitio de Azure.

Además de la administración de claves, Azure Key Vault ofrece a los administradores de seguridad la misma experiencia de administración para el almacenamiento, el acceso y la administración de certificados y secretos (por ejemplo, contraseñas) para otros servicios y aplicaciones que usan cifrado. 

Para obtener más información sobre Azure Key Vault, consulte [¿Qué es el Almacén de claves de Azure?](https://azure.microsoft.com/documentation/articles/key-vault-whatis/) y visite el [blog del equipo de Azure Key Vault](https://blogs.technet.microsoft.com/kv/) para obtener la información más reciente y documentarse sobre cómo usan esta tecnología otros servicios.


## <a name="restrictions-when-using-byok"></a>Restricciones en el uso de BYOK

Si tiene usuarios que se han registrado para obtener una cuenta gratuita de RMS para usuarios, no podrá usar BYOK ni los registros de uso, ya que esta configuración no tiene un administrador de inquilinos para configurar estas características.


> [!NOTE]
> Para más información sobre RMS para usuarios, consulte [RMS para usuarios y Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK no es compatible con Exchange Online.](../media/RMS_BYOK_noExchange.png)

BYOK y el registro de uso funcionan perfectamente con todas las aplicaciones que se integran con el servicio Azure Rights Management (Azure RMS) usado por Azure Information Protection. Aquí se incluyen servicios en la nube, como SharePoint Online, servidores locales que ejecutan Exchange y SharePoint y que funcionan con Azure RMS a través del conector RMS y de aplicaciones cliente como Office 2013 y Office 2016. Obtendrá los registros de uso de claves independientemente de la aplicación que realiza solicitudes de Azure RMS.

Existe una sola excepción: Actualmente, **BYOK de Azure RMS no es compatible con Exchange Online**. Si usa Exchange Online, se recomienda implementar ahora Azure RMS en el modo de administración de claves predeterminado, donde Microsoft genera y administra su clave. Tiene la opción de pasar a BYOK más adelante, por ejemplo, cuando Exchange Online no sea compatible con BYOK de Azure RMS. Sin embargo, si no puede esperar, otra opción es implementar Azure RMS con BYOK ahora, con funcionalidad reducida de RMS para Exchange Online (los correos electrónicos y datos adjuntos desprotegidos permanecen completamente funcionales):

-   No se pueden mostrar los mensajes de correo electrónico o los datos adjuntos protegidos en Outlook Web Access.

-   No se pueden mostrar los mensajes de correo electrónico en dispositivos móviles que usan Exchange ActiveSync IRM.

-   El descifrado de transporte (por ejemplo, para explorar el malware) y el descifrado de diario no son posibles, de modo que los mensajes de correo electrónico y los datos adjuntos protegidos se omitirán.

-   Las reglas de protección de transporte y la prevención de pérdida de datos (DLP) que aplican directivas de IRM no son posibles, de modo que no se puede aplicar protección de RMS mediante estos métodos.

-   La búsqueda basada en servidor para los mensajes de correo electrónico protegidos no es posible, de modo que estos se omitirán.

Cuando usa BYOK de Azure RMS con funcionalidad reducida de RMS para Exchange Online, RMS funcionará con los clientes de correo electrónico de Outlook en Windows y Mac y en otros clientes de correo electrónico que no usan Exchange ActiveSync IRM.

Si realiza la migración a Azure RMS desde AD RMS, puede que haya importado la clave como un dominio de publicación de confianza (TPD) en Exchange Online (también denominado BYOK en la terminología de Exchange, que es independiente de BYOK del Almacén de claves de Azure). En este escenario, debe quitar el TDP de Exchange Online para evitar conflictos de plantillas y directivas. Para más información, consulte [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) en la biblioteca de cmdlets de Exchange Online.

A veces, la excepción de BYOK de Azure RMS para Exchange Online no es un problema en la práctica. Por ejemplo, las organizaciones que necesitan que BYOK y el registro ejecuten sus aplicaciones de datos (Exchange, SharePoint, Office) localmente y usan Azure RMS para funcionalidades que no son compatibles fácilmente con AD RMS local (por ejemplo, colaboración con otras compañías y acceso desde clientes móviles). BYOK y el registro funcionan bien en este escenario y permiten a la organización tomar el control completo sobre su suscripción de Azure RMS.

## <a name="next-steps"></a>Pasos siguientes

Si ha tomado la decisión de administrar su propia clave, vaya a [Implementing your Azure Rights Management tenant key](plan-implement-tenant-key.md#implementing-your-azure-information-protection-tenant-key) (Implementación de su clave de inquilino de Azure Rights Management).

Si ha decidido permanecer con la configuración predeterminada con la que Microsoft administra su clave, consulte la sección [Pasos siguientes](plan-implement-tenant-key.md#next-steps) del artículo Planeamiento e implementación de la clave de inquilino de Azure Rights Management

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

