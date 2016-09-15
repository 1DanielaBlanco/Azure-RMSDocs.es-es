---
title: Precio y restricciones de BYOK | Azure RMS
description: "Conozca las restricciones de uso de claves administradas por el cliente, conocidas como “Bring your own key” (BYOK, Traiga su propia clave) con Azure RMS."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f5930ed3-a6cf-4eac-b2ec-fcf63aa4e809
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: ada00b6f6298e7d359c73eb38dfdac169eacb708
ms.openlocfilehash: d704f3d9357993bdb01a38cda6f434ab1583b627


---

# Precio y restricciones de BYOK

>*Se aplica a: Azure Rights Management, Office 365*


Las organizaciones que tienen una suscripción con Azure Rights Management pueden usar claves administradas por el cliente (BYOK) en el Almacén de claves de Azure y registrar su uso sin costo adicional. Sin embargo, para usar el Almacén de claves de Azure, es necesario tener una suscripción de Azure compatible con los almacenes de claves con claves protegidas por HSM. El uso de las claves en el Almacén de claves de Azure conlleva un cargo mensual. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/).

Si tiene usuarios que se han registrado para obtener una cuenta gratuita de RMS de uso personal, no podrá usar BYOK ni los registros de uso, ya que esta configuración no tiene un administrador de inquilinos para configurar estas características.


> [!NOTE]
> Para más información sobre RMS para usuarios, consulte [RMS para usuarios y Azure Rights Management](../understand-explore/rms-for-individuals.md).

![BYOK no es compatible con Exchange Online.](../media/RMS_BYOK_noExchange.png)

BYOK y los registros de uso funcionan sin ningún problema con todas las aplicaciones que se integran con Azure RMS. Aquí se incluyen servicios en la nube, como SharePoint Online, servidores locales que ejecutan Exchange y SharePoint y que funcionan con Azure RMS a través del conector RMS y de aplicaciones cliente como Office 2013 y Office 2016. Obtendrá los registros de uso de claves independientemente de la aplicación que realiza solicitudes de Azure RMS.

Existe una sola excepción: Actualmente, **BYOK de Azure RMS no es compatible con Exchange Online**. Si usa Exchange Online, se recomienda implementar ahora Azure RMS en el modo de administración de claves predeterminado, donde Microsoft genera y administra su clave. Tiene la opción de pasar a BYOK más adelante, por ejemplo, cuando Exchange Online no sea compatible con BYOK de Azure RMS. Sin embargo, si no puede esperar, otra opción es implementar Azure RMS con BYOK ahora, con funcionalidad reducida de RMS para Exchange Online (los correos electrónicos y datos adjuntos desprotegidos permanecen completamente funcionales):

-   No se pueden mostrar los mensajes de correo electrónico o los datos adjuntos protegidos en Outlook Web Access.

-   No se pueden mostrar los mensajes de correo electrónico en dispositivos móviles que usan Exchange ActiveSync IRM.

-   El descifrado de transporte (por ejemplo, para explorar el malware) y el descifrado de diario no son posibles, de modo que los mensajes de correo electrónico y los datos adjuntos protegidos se omitirán.

-   Las reglas de protección de transporte y la prevención de pérdida de datos (DLP) que aplican directivas de IRM no son posibles, de modo que no se puede aplicar protección de RMS mediante estos métodos.

-   La búsqueda basada en servidor para los mensajes de correo electrónico protegidos no es posible, de modo que estos se omitirán.

Cuando usa BYOK de Azure RMS con funcionalidad reducida de RMS para Exchange Online, RMS funcionará con los clientes de correo electrónico de Outlook en Windows y Mac y en otros clientes de correo electrónico que no usan Exchange ActiveSync IRM.

Si realiza la migración a Azure RMS desde AD RMS, puede que haya importado la clave como un dominio de publicación de confianza (TPD) en Exchange Online (también denominado BYOK en la terminología de Exchange, que es independiente de BYOK del Almacén de claves de Azure). En este escenario, debe quitar el TDP de Exchange Online para evitar conflictos de plantillas y directivas. Para más información, consulte [Remove-RMSTrustedPublishingDomain](https://technet.microsoft.com/library/jj200720%28v=exchg.150%29.aspx) en la biblioteca de cmdlets de Exchange Online.

A veces, la excepción de BYOK de Azure RMS para Exchange Online no es un problema en la práctica. Por ejemplo, las organizaciones que necesitan que BYOK y el registro ejecuten sus aplicaciones de datos (Exchange, SharePoint, Office) localmente y usan Azure RMS para funcionalidades que no son compatibles fácilmente con AD RMS local (por ejemplo, colaboración con otras compañías y acceso desde clientes móviles). BYOK y el registro funcionan bien en este escenario y permiten a la organización tomar el control completo sobre su suscripción de Azure RMS.

## Pasos siguientes

Si ha tomado la decisión de administrar su propia clave, vaya a [Implementing your Azure Rights Management tenant key](plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) (Implementación de su clave de inquilino de Azure Rights Management).

Si ha decidido permanecer con la configuración predeterminada con la que Microsoft administra su clave, consulte la sección [Pasos siguientes](plan-implement-tenant-key.md#next-steps) del artículo Planeamiento e implementación de la clave de inquilino de Azure Rights Management




<!--HONumber=Aug16_HO4-->


