---
title: Problemas resueltos por Azure Rights Management - AIP
description: Identifique problemas o requisitos que puede tener su organización y obtenga información sobre cómo la tecnología de Azure RMS puede abordarlos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/21/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8f57c33f023cd45fd2538244520b77a89f944db1
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474732"
---
# <a name="what-problems-does-azure-rms-solve"></a>¿Qué problemas resuelve Azure RMS?

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la tabla siguiente para identificar problemas o requisitos empresariales que puede tener su organización para proteger documentos y correos electrónicos y de qué manera puede tratarlos la tecnología de Azure Rights Management (Azure RMS).

Azure RMS es la tecnología de protección que usa [Azure Information Protection](what-is-information-protection.md).

|Requisito o problema|Resuelto por Azure RMS|
|--------------------------|-----------------------|
|Proteger varios tipos de archivo|√ En implementaciones anteriores de Rights Management, solo se podían proteger los archivos de Office, con la protección nativa de Rights Management. Ahora, la **protección genérica** que ofreció por primera vez la aplicación Rights Management sharing y que ahora ofrece Azure Information Protection amplía la compatibilidad a más [tipos de archivo](./rms-client/client-admin-guide-file-types.md).|
|Proteger los archivos en cualquier lugar|√ Si un archivo está [protegido](./rms-client/client-classify-protect.md), la protección permanece con el archivo, aunque se guarde o copie en almacenamiento que no se encuentra bajo el control de TI, como un servicio de almacenamiento en la nube.|
|Compartir información de forma segura|√ Si un archivo [protegido](./rms-client/client-classify-protect.md), se puede compartir con otros de forma segura. Por ejemplo, un archivo adjunto a un correo electrónico o un vínculo a un sitio de SharePoint. Si un correo electrónico contiene información confidencial, puede proteger el correo electrónico o utilizar solo la opción No reenviar de Outlook. <br /><br />La ventaja de adjuntar un archivo protegido con respecto a la protección del mensaje de correo electrónico completo es que el texto de correo electrónico no está cifrado, por lo que puede incluir instrucciones sobre el primer uso si el correo se va a enviar fuera de la organización. Todo el mundo puede leer las instrucciones pero, como el documento adjunto está protegido, solo podrán abrirlo los usuarios autorizados, aunque el correo electrónico o el documento se reenvíen a otras personas.|
|Auditoría y supervisión|√ Puede [auditar y supervisar el uso](./deploy-use/log-analyze-usage.md) de sus archivos protegidos, incluso después de que estos archivos salgan de los límites de su organización.<br /><br />Por ejemplo, puede trabajar para Contoso, Ltd. Está trabajando en un proyecto conjunto con tres empleados de Fabrikam, Inc. Envía por correo electrónico a estos tres empleados un documento que protege y restringe a solo lectura. La auditoría de Azure Rights Management puede proporcionar la siguiente información:<br /><br />- Si las personas que ha especificado en Fabrikam han abierto el documento y cuándo.<br /><br />- Si otras personas que no ha especificado han intentado (sin éxito) abrir el documento, quizá porque se reenvió o se guardó en una ubicación compartida a la que otros usuarios podían acceder.<br /><br />- Si cualquiera de las personas especificadas ha intentado (y no ha logrado) imprimir o cambiar el documento.<br /><br />Además, el [sitio de seguimiento de documentos](./rms-client/client-track-revoke.md) permite a los usuarios y a los administradores realizar un seguimiento y, si es necesario, revocar el acceso a documentos protegidos.|
|Soporte para dispositivos de uso común, no solo equipos Windows|√ Entre los [dispositivos compatibles](./requirements-client-devices.md) se incluyen:<br /><br />- Equipos y teléfonos con Windows<br /><br />- Equipos Mac<br /><br />- Tabletas y teléfonos iOS<br /><br />- Tabletas y teléfonos Android|
|Soporte para colaboración de negocio a negocio|√ Debido a que Azure Rights Management es un servicio en la nube, no hay que configurar de manera explícita las confianzas con otras organizaciones para poder compartir contenido protegido con ellas. Si ya tiene un directorio de Office 365 o Azure AD, la colaboración entre organizaciones se admite automáticamente. Si no es así, los usuarios pueden suscribirse para disfrutar de una suscripción gratuita de [RMS para usuarios](rms-for-individuals.md), o usar la cuenta Microsoft para [las aplicaciones que admiten esta autenticación para Azure Information Protection](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).|
|Compatibilidad con los servicios locales, así como con Office 365|√  Además de funcionar [sin problemas con Office 365](office-apps-services-support.md), también puede usar Azure Rights Management con los siguientes servicios locales al implementar el [conector RMS](./deploy-use/deploy-rms-connector.md):<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- Windows Server que ejecuta la infraestructura de clasificación de archivos|
|Activación sencilla|√ Para las suscripciones nuevas, la activación es automática. En cuanto a las suscripciones existentes, para [activar el servicio de Rights Management](./deploy-use/activate-service.md) solo hacen falta un par de clics en el portal de administración. O bien, si prefiere el control de la línea de comandos, solo se deben usar dos comandos de PowerShell.|
|Capacidad de escalar en la organización, según sea necesario|√ Dado que Azure Rights Management se ejecuta como servicio en la nube con la elasticidad de Azure para escalar verticalmente y horizontalmente, no tiene que aprovisionar o implementar servidores locales adicionales.|
|Capacidad para crear directivas simples y flexibles|√ Las [plantillas de protección personalizadas](./deploy-use/configure-policy-templates.md) proporcionan una solución rápida y sencilla para que los administradores apliquen las directivas y para que los usuarios apliquen el nivel correcto de protección para cada documento y restrinjan el acceso a las personas dentro de la organización.<br /><br />Por ejemplo, para que se comparta un documento estratégico de toda la compañía con todos los empleados, podría aplicar una directiva de solo lectura a todos los empleados internos. A continuación, para un documento más confidencial, como un informe financiero, podría restringir el acceso solo a ejecutivos.|
|Amplia compatibilidad de aplicaciones|√ Azure Rights Management tiene una integración estrecha con aplicaciones y servicios de Microsoft Office, y amplía la compatibilidad con otras aplicaciones mediante el [cliente de Azure Information Protection](./rms-client/aip-client.md ).<br /><br />√ Los [SDK de Azure Information Protection](./develop/developers-guide.md) proporcionan a sus desarrolladores internos y proveedores de software API para escribir aplicaciones personalizadas que admiten Azure Information Protection.<br /><br />Para más información, vea [Otras aplicaciones compatibles con las API de Rights Management](api-support.md).|
|TI debe mantener el control de los datos|√ Las organizaciones pueden elegir administrar su propia clave de inquilino y usar su solución "[Aportar tu propia clave](./plan-design/plan-implement-tenant-key.md)" (BYOK) y almacenar su clave de inquilino en los módulos de seguridad de hardware (HSM).<br /><br />√ Compatibilidad con la auditoría y el [registro de uso](./deploy-use/log-analyze-usage.md) para que pueda analizar información empresarial, supervisar el abuso y (si tiene una pérdida de información) realizar análisis forenses.<br /><br />√ El acceso delegado mediante la [característica de superusuario](./deploy-use/configure-super-users.md) garantiza que TI siempre pueda tener acceso al contenido protegido, aunque un documento estuviera protegido por un empleado que haya dejado la organización. En comparación, las soluciones de cifrado punto a punto se arriesgan a perder acceso a los datos de la compañía.<br /><br />√ Sincronice [solo los atributos de directorio que Azure RMS necesita](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) para admitir una identidad común para sus cuentas de Active Directory locales, mediante una [herramienta de sincronización de directorios](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), como Azure AD Connect.<br /><br />√ Habilite el inicio de sesión único sin replicar contraseñas a la nube, mediante AD FS.<br /><br />√ Las organizaciones siempre tienen la opción de dejar de usar el servicio Azure Rights Management sin perder el acceso a contenido anteriormente protegido por Azure Rights Management. Para obtener información sobre las opciones de retirada, consulte [Retirada y desactivación de Azure Rights Management](./deploy-use/decommission-deactivate.md). Además, las organizaciones que hayan implementado Active Directory Rights Management Services (AD RMS) pueden [migrar al servicio Azure Rights Management](./plan-design/migrate-from-ad-rms-to-azure-rms.md) sin perder el acceso a los datos protegidos anteriormente por AD RMS.|
> [!TIP]
> Si está familiarizado con la versión local de Rights Management, Active Directory Rights Management Services (AD RMS), puede que esté interesado en la tabla de comparación de [Comparación entre Azure Rights Management y AD RMS](compare-on-premise.md).

## <a name="security-compliance-and-regulatory-requirements"></a>Requisitos de seguridad, normativos y regulatorios
Azure Rights Management admite los siguientes requisitos de seguridad, reglamentarios y de cumplimiento:

√ Uso de criptografía estándar del sector y admite FIPS 140-2. Para más información, consulte [Controles criptográficos usados por Azure RMS: Longitudes de clave y algoritmos](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Soporte para que los módulos de seguridad de hardware (HSM) de Thales almacenen su clave de inquilino en centros de datos de Microsoft Azure. Azure Rights Management usa espacios de seguridad independientes para los centros de datos de Estados Unidos, EMEA (Europa, Oriente Medio y África) y Asia, para que las claves solo se puedan usar en su región.

√ Certificado para lo siguiente:

-   ISO/IEC 27001:2013 (incluye [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Atestaciones de SOC 2 SSAE 16/ISAE 3402

-   HIPAA BAA

-   Cláusula del modelo de la UE

-   FedRAMP como parte de Azure Active Directory en la certificación de Office 365, FedRAMP Agency Authority to Operate emitido por HHS

-   PCI DSS nivel 1

Para obtener más información sobre estas certificaciones externas, consulte el [Centro de confianza de Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## <a name="next-steps"></a>Pasos siguientes

Para obtener información más técnica sobre el funcionamiento del servicio Azure Rights Management, vea [¿Cómo funciona Azure RMS?](how-does-it-work.md)
