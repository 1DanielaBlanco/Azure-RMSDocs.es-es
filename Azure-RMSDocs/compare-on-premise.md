---
title: 'Comparación de Azure Information Protection y AD RMS: AIP'
description: Si conoce o ha implementado con anterioridad Active Directory Rights Management Services (AD RMS), es posible que se pregunte cuáles son las diferencias de Azure Information Protection en términos de funcionalidad y requisitos.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 8123bd62-1814-4d79-b306-e20c1a00e264
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 3e1de24471b89ac0081f5f5e93a25baf1d798e34
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56260041"
---
# <a name="comparing-azure-information-protection-and-ad-rms"></a>Comparación de Azure Information Protection y AD RMS

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si conoce o ha implementado con anterioridad Active Directory Rights Management Services (AD RMS), es posible que se pregunte cuáles son las diferencias de Azure Information Protection en términos de funcionalidad y requisitos como solución de protección de la información.

Estas son algunas de las principales diferencias de Azure Information Protection:

- **No se necesita ninguna infraestructura de servidor**: Azure Information Protection no necesita los servidores y certificados PKI adicionales que necesita AD RMS, ya que Microsoft Azure se encarga de ellos. En consecuencia, esta solución en la nube es más rápida de implementar y fácil de mantener.

- **Autenticación basada en la nube**: Azure Information Protection usa Azure AD para la autenticación, tanto para los usuarios internos como para los usuarios de otras organizaciones. Esto significa que los usuarios móviles se pueden autenticar incluso cuando no están conectados a la red interna y es más fácil compartir contenido protegido con usuarios de otras organizaciones. Muchas organizaciones ya tienen cuentas de usuario en Azure AD porque ejecutan servicios de Azure o disponen de Office 365. Pero si no es así, RMS para usuarios permite a los usuarios crear una cuenta gratuita, o puede utilizarse una cuenta Microsoft para [las aplicaciones que admiten la autenticación de Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents). Para compartir contenido protegido por AD RMS con otra organización debe configurar relaciones de confianza explícitas con cada organización.

- **Compatibilidad integrada con dispositivos móviles**: no se necesita ningún cambio de implementación para que Azure RMS admita dispositivos móviles y equipos Mac. Para admitir estos dispositivos con AD RMS, debe instalar la extensión para dispositivos móviles, configurar AD FS para la federación y crear registros adicionales para el servicio DNS público.

- **Plantillas predeterminadas**: Azure Information Protection crea plantillas predeterminadas en cuanto se activa el servicio de protección, lo que facilita empezar a proteger datos importantes de inmediato. No hay plantillas predeterminadas para AD RMS.

- **Plantillas de departamento**: También se conoce como plantillas con ámbito. Azure Information Protection admite plantillas de departamento para las plantillas adicionales que cree. Esta configuración permite especificar un subconjunto de usuarios para que vean plantillas específicas en sus aplicaciones cliente. La limitación del número de plantillas que ven los usuarios les facilita la selección de la directiva correcta definida para los diferentes grupos de usuarios. AD RMS no es compatible con las plantillas de departamento.

- **Seguimiento y revocación de documentos**: Azure Information Protection admite estas características con el cliente de Azure Information Protection, mientras que AD RMS no las admite.

- **Clasificación y etiquetado**: Azure Information Protection admite estas características con el cliente de Azure Information Protection que se integra en las aplicaciones de Office y en el Explorador de archivos, mientras que AD RMS no lo hace. 


Además, dado que Azure Information Protection es un servicio en la nube, puede entregar correcciones y características nuevas más rápidamente que una solución local basada en servidor. No hay características nuevas planeadas para AD RMS en Windows Server.

Para obtener más información y conocer otras diferencias, vea en la tabla siguiente una comparación en paralelo de las características y las ventajas de Azure Information Protection y AD RMS. Si tiene preguntas acerca de una comparación específica de la seguridad, consulte la sección [Controles criptográficos para firmas y cifrado](#cryptographic-controls-for-signing-and-encryption) en este artículo.

> [!NOTE]
> Para facilitar esta comparación, parte de la información que se encuentra aquí se repite de [Requisitos de Azure Information Protection](requirements.md). Use este artículo para obtener soporte más específico e información de la versión para Azure Rights Management.

|Azure Information Protection|AD RMS|
|-----------------------------------------------------------------------------------------|--------------------------------------------------------|
|Admite capacidades de Information Rights Management (IRM) en servicios de Microsoft Online, como Exchange Online y SharePoint Online, así como Office 365.<br /><br />También admite productos de servidor de Microsoft locales, como Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server e Infraestructura de clasificación de archivos (FCI).|Admite productos de servidor de Microsoft locales, como Exchange Server, SharePoint Server y servidores de archivos que ejecutan Windows Server e Infraestructura de clasificación de archivos (FCI).|
|Permite colaborar automáticamente de forma segura en los documentos con cualquier organización que también use Azure AD para la autenticación. Esto significa que las organizaciones pueden proteger los documentos que comparten internamente o con otras organizaciones.|Colaborar de forma segura en documentos de fuera de la organización requiere la definición explícita de confianzas de autenticación en una relación directa de punto a punto entre dos organizaciones. Debe configurar dominios de usuario de confianza (TUD) o confianzas federadas que cree mediante Servicios de federación de Active Directory (AD FS).|
|Envíe un correo electrónico protegido (opcionalmente, con datos adjuntos a documentos de Office que estén protegidos automáticamente) a los usuarios cuando no exista ninguna relación de confianza de autenticación. Este escenario se consigue mediante el uso de la federación con proveedores de redes sociales o un código de acceso de un solo uso y un explorador web para la visualización.|No admite el envío de correo electrónico protegido cuando no existe ninguna relación de confianza de autenticación.|
|Proporciona plantillas de protección predeterminadas que restringen el acceso al contenido a su propia organización; una que proporciona vista de solo lectura de contenido protegido, y la otra que permite escribir o modificar permisos para el contenido protegido.<br /><br />También puede crear sus propias plantillas personalizadas, incluidas plantillas de departamento, visibles solo para un subconjunto de usuarios. Para obtener más información, vea [Configuración y administración de plantillas para Azure Information Protection](configure-policy-templates.md).<br /><br />Además, los usuarios pueden definir su propio conjunto de permisos si las plantillas no son suficientes.|No hay plantillas predeterminadas; debe crearlas y luego distribuirlas. Para obtener más información, consulte [Consideraciones de la plantilla de directivas para AD RMS](https://go.microsoft.com/fwlink/?LinkId=154765).<br /><br />Además, los usuarios pueden definir su propio conjunto de permisos si las plantillas no son suficientes.|
|La versión mínima compatible de Microsoft Office es Office 2010, que requiere el [cliente de Azure Information Protection](./rms-client/aip-client.md).|La versión mínima compatible de Microsoft Office es Office 2010.|
|Admite el [cliente de Azure Information Protection](./rms-client/aip-client.md) para Windows, iOS y Android. La aplicación RMS sharing continúa admitiendo equipos Mac.<br /><br />Además, el cliente de Azure Information Protection admite lo siguiente:<br /><br />- Uso compartido con personas de otra organización.<br /><br />- Un sitio de seguimiento de documentos para los usuarios, que incluye la capacidad de revocar un documento.|Admite el [cliente de Azure Information Protection](./rms-client/aip-client.md) para Windows, iOS y Android. La aplicación RMS sharing continúa admitiendo equipos Mac. Sin embargo, el uso compartido no es compatible con compartir con personas de otra organización o el sitio de Seguimiento de documentos y la capacidad de los usuarios de revocar documentos.|
|La mayoría de los [tipos de archivo](./rms-client/client-admin-guide-file-types.md) se pueden clasificar y proteger con el cliente de Azure Information Protection.<br /><br />Para otras aplicaciones, compruebe la tabla de [Requisitos de Azure RMS: aplicaciones](./requirements-applications.md).|La mayoría de los [tipos de archivo](./rms-client/client-admin-guide-file-types.md) se pueden proteger con el cliente de Azure Information Protection.<br /><br />Para otras aplicaciones, compruebe la tabla de [Requisitos de Azure RMS: aplicaciones](./requirements-applications.md).|
|La versión mínima compatible del cliente Windows es Windows 7 SP1.|La versión mínima compatible del cliente Windows es Windows 7 SP1.|
|La compatibilidad con dispositivos móviles incluye Windows 10 Mobile, iOS y Android.<br /><br />El soporte del correo electrónico mediante Exchange ActiveSync IRM también es compatible en todas las plataformas de dispositivos móviles que admiten este protocolo.|La compatibilidad de dispositivos móviles incluye Windows 10 Mobile, Android y iOS, y requiere la [extensión de Active Directory Rights Management Services para dispositivos móviles](https://technet.microsoft.com/library/dn673574.aspx).<br /><br />El soporte del correo electrónico mediante Exchange ActiveSync IRM es compatible en todas las plataformas de dispositivos móviles que admiten este protocolo.|
|Admite Multi-Factor Authentication (MFA) para equipos y dispositivos móviles.<br /><br />Para más información, vea [Multi-Factor Authentication (MFA) y Azure Information Protection](./requirements-azure-ad.md#multi-factor-authentication-mfa-and-azure-information-protection).|Admite la autenticación de tarjeta inteligente si IIS está configurado para solicitar certificados.|
|Es compatible con el Modo criptográfico 2 sin otra configuración adicional, lo que proporciona una mayor seguridad para longitudes de clave y algoritmos de cifrado.<br /><br />Para más información, consulte la sección [Controles criptográficos para firmas y cifrado](#cryptographic-controls-for-signing-and-encryption) de este artículo y [Modos criptográficos de AD RMS](https://go.microsoft.com/fwlink/?LinkId=266659).|Es compatible con el Modo criptográfico 1 de forma predeterminada y precisa configuración adicional para admitir el Modo criptográfico 2 para obtener una mayor seguridad.<br /><br />Para más información, consulte la sección [Controles criptográficos para firmas y cifrado](#cryptographic-controls-for-signing-and-encryption) de este artículo y [Modos criptográficos de AD RMS](https://go.microsoft.com/fwlink/?LinkId=266659).|
|Admite la migración desde AD RMS e incluso, si se requiere, a AD RMS:<br /><br />- [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)<br /><br />- [Retirada y desactivación de Azure Information Protection](decommission-deactivate.md)|Admite la migración desde Azure Information Protection y a Azure Information Protection:<br /><br />- [Retirada y desactivación de Azure Rights Management](decommission-deactivate.md)<br /><br />- [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md)|
|Se requiere una licencia de Azure Information Protection o una licencia de Azure Rights Management con Office 365 para proteger contenido. No se requieren licencias para consumir el contenido que ha protegido con Azure Information Protection (incluye usuarios de otra organización).<br /><br />Para obtener más información, consulte la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection.|Requiere una licencia de RMS para proteger el contenido y para consumir el contenido que ha protegido AD RMS.<br /><br />Para obtener más información acerca de licencias de AD RMS, consulte [Licencias de acceso de cliente y licencias de administración](https://www.microsoft.com/en-us/Licensing/product-licensing/client-access-license.aspx) , donde encontrará información general, pero si desea información más específica, póngase en contacto con un partner o representante de Microsoft.|

## <a name="cryptographic-controls-for-signing-and-encryption"></a>Controles criptográficos para firmas y cifrado
De manera predeterminada, Azure Information Protection usa RSA 2048 para toda la criptografía de claves públicas y SHA 256 para operaciones de firma. En comparación, AD RMS admite RSA 1024 y RSA 2048, y SHA 1 o SHA 256 para operaciones de firma.

Tanto Azure Information Protection como AD RMS usan AES 128 para el cifrado simétrico.

Azure Information Protection cumple con la normativa FIPS 140-2 cuando el tamaño de la clave de inquilino es de 2048 bits, el valor predeterminado cuando está activo el servicio Azure Rights Management. 

Para más información sobre los controles criptográficos, vea [Controles criptográficos usados por Azure RMS: Longitudes de clave y algoritmos](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).


## <a name="next-steps"></a>Pasos siguientes
Si está buscando migrar desde AD RMS a Azure Information Protection, vea [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


