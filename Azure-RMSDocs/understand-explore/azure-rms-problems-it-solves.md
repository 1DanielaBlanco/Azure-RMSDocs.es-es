---
title: "¿Qué problemas resuelve Azure RMS? | Azure RMS"
description: "Identifique problemas o requisitos empresariales que puede tener su organización y obtenga información sobre cómo Azure RMS puede abordarlos."
author: cabailey
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: b551c62d-5ac6-4359-85b3-90693e77b37f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 43429b44c019144744f39a1f92f144d315c2024c
ms.openlocfilehash: bc25d2ee7224983d70a23177666c1a72b3db1a17


---


# ¿Qué problemas resuelve Azure RMS?

>*Se aplica a: Azure Rights Management, Office 365*

Use la tabla siguiente para identificar problemas o requisitos empresariales que puede tener su organización y de qué manera puede tratarlos Azure RMS.

|Requisito o problema|Resuelto por Azure RMS|
|--------------------------|-----------------------|
|Proteger todos los tipos de archivos|√ En la implementación anterior de Rights Management, solo se podían proteger los archivos de Office, con la protección nativa. Ahora, la [protección genérica](../rms-client/sharing-app-dialog-box.md#what-s-the-difference-between-generic-protection-and-built-in-native-protection) significa que se admiten todos los tipos de archivos.|
|Proteger los archivos en cualquier lugar|√ Cuando un archivo se guarda en una ubicación ([proteger en contexto](../rms-client/sharing-app-protect-in-place.md)), la protección permanece con el archivo, aunque se copia en almacenamiento que no se encuentra bajo el control de TI, como un servicio de almacenamiento en la nube.|
|Compartir archivos de manera segura por correo electrónico|√ Cuando un archivo se comparte por correo electrónico ([uso compartido protegido](../rms-client/sharing-app-protect-by-email.md)), el archivo se protege como datos adjuntos de un mensaje de correo electrónico, con instrucciones sobre cómo abrir los datos adjuntos protegidos. El texto del mensaje de correo electrónico no está cifrado, por lo que el destinatario siempre puede leer estas instrucciones. Sin embargo, dado que el documento adjunto está protegido, solo podrán abrirlo los usuarios autorizados, aunque se reenvíe el documento o mensaje de correo electrónico a otras personas.|
|Auditoría y supervisión|√ Puede [auditar y supervisar el uso](../deploy-use/log-analyze-usage.md) de sus archivos protegidos, incluso después de que estos archivos salgan de los límites de su organización.<br /><br />Por ejemplo, puede trabajar para Contoso, Ltd. Está trabajando en un proyecto conjunto con 3 empleados de Fabrikam, Inc. Envía por correo electrónico a estos 3 empleados un documento que protege y restringe a solo lectura. La auditoría de Azure RMS puede proporcionar la siguiente información:<br /><br />- Si las personas que ha especificado en Fabrikam han abierto el documento y cuándo.<br /><br />- Si otras personas que no ha especificado han intentado (sin éxito) abrir el documento, quizá porque se reenvió o se guardó en una ubicación compartida a la que otros usuarios podían acceder.<br /><br />- Si cualquiera de las personas especificadas ha intentado (y no ha logrado) imprimir o cambiar el documento.|
|Soporte para todos los dispositivos usados comúnmente, no solo equipos Windows|√ Entre los [dispositivos compatibles](../get-started/requirements-client-devices.md) se incluyen:<br /><br />- Equipos y teléfonos con Windows<br /><br />- Equipos Mac<br /><br />- Tabletas y teléfonos iOS<br /><br />- Tabletas y teléfonos Android|
|Soporte para colaboración de negocio a negocio|√ Debido a que Azure RMS es un servicio en la nube, no hay que configurar de manera explícita las confianzas con otras organizaciones para poder compartir contenido protegido con ellas. Si ya tiene un directorio de Office 365 o Azure AD, la colaboración entre organizaciones se admite automáticamente. Si no lo hace, los usuarios podrán registrarse para la suscripción a [RMS para usuarios](rms-for-individuals.md) gratuita.|
|Compatibilidad con los servicios locales, así como con Office 365|√  Además de funcionar [sin problemas con Office 365](office-apps-services-support.md), también puede usar Azure RMS con los siguientes servicios locales al implementar el [conector RMS](../deploy-use/deploy-rms-connector.md):<br /><br />- Exchange Server<br /><br />- SharePoint Server<br /><br />- Windows Server que ejecuta la infraestructura de clasificación de archivos|
|Activación sencilla|√ La [activación del servicio de Rights Management](../deploy-use/activate-service.md) para los usuarios solo requiere que hagan un par de veces clic en el Portal de Azure clásico.|
|Capacidad de escalar en la organización, según sea necesario|√ Dado que Azure RMS se ejecuta como servicio en la nube con la elasticidad de Azure para escalar verticalmente y horizontalmente, no tiene que aprovisionar o implementar servidores locales adicionales.|
|Capacidad para crear directivas simples y flexibles|√ Las [plantillas de directivas de derechos personalizadas](../deploy-use/configure-custom-templates.md) proporcionan una solución rápida y sencilla para que los administradores apliquen las directivas y para que los usuarios apliquen el nivel correcto de protección para cada documento y restrinjan el acceso a las personas dentro de la organización.<br /><br />Por ejemplo, para que se comparta un documento estratégico de toda la compañía con todos los empleados, podría aplicar una directiva de solo lectura a todos los empleados internos. A continuación, para un documento más confidencial, como un informe financiero, podría restringir el acceso solo a ejecutivos.|
|Amplia compatibilidad de aplicaciones|√ Azure RMS tiene una integración estrecha con aplicaciones y servicios de Microsoft Office, y amplía la compatibilidad con otras aplicaciones mediante la aplicación de RMS sharing.<br /><br />√ [Microsoft Rights Management SDK](../develop/developers-guide.md#software-development-kits) proporciona a los desarrolladores internos y a los proveedores de software las API para escribir aplicaciones personalizadas que admiten Azure RMS.<br /><br />Para más información, consulte [Otras aplicaciones compatibles con las API de RMS](api-support.md).|
|TI debe mantener el control de los datos|√ Las organizaciones pueden elegir administrar su propia clave de inquilino y usar su solución "[Aportar tu propia clave](../plan-design/plan-implement-tenant-key.md)" (BYOK) y almacenar su clave de inquilino en los módulos de seguridad de hardware (HSM).<br /><br />√ Compatibilidad con la auditoría y el [registro de uso](../deploy-use/log-analyze-usage.md) para que pueda analizar información empresarial, supervisar el abuso y (si tiene una pérdida de información) realizar análisis forenses.<br /><br />√ El acceso delegado mediante la [característica de superusuario](../deploy-use/configure-super-users.md) garantiza que TI siempre pueda tener acceso al contenido protegido, aunque un documento estuviera protegido por un empleado que haya dejado la organización. En comparación, las soluciones de cifrado punto a punto se arriesgan a perder acceso a los datos de la compañía.<br /><br />√ Sincronice [solo los atributos de directorio que Azure RMS necesita](/active-directory/active-directory-aadconnectsync-attributes-synchronized#azure-rms) para admitir una identidad común para sus cuentas de Active Directory locales, mediante una [herramienta de sincronización de directorios](/active-directory/active-directory-hybrid-identity-design-considerations-tools-comparison), como Azure AD Connect.<br /><br />√ Habilite el inicio de sesión único sin replicar contraseñas a la nube, mediante AD FS.<br /><br />√ Las organizaciones siempre tienen la opción de dejar de usar Azure RMS sin perder el acceso a contenido anteriormente protegido por Azure RMS. Para obtener información sobre las opciones de retirada, consulte [Retirada y desactivación de Azure Rights Management](../deploy-use/decommission-deactivate.md). Además, las organizaciones que hayan implementado Active Directory Rights Management Services (AD RMS) pueden [migrar a Azure RMS](../plan-design/migrate-from-ad-rms-to-azure-rms.md) sin perder el acceso a los datos protegidos anteriormente por AD RMS.|
> [!TIP]
> Si está familiarizado con la versión local de Rights Management, Active Directory Rights Management Services (AD RMS), puede que esté interesado en la tabla de comparación de [Comparación entre Azure Rights Management y AD RMS](compare-azure-rms-ad-rms.md).

## Requisitos de seguridad, normativos y regulatorios
Azure RMS admite los siguientes requisitos de seguridad, normativos y regulatorios:

√ Uso de criptografía estándar del sector y admite FIPS 140-2. Para más información, consulte [Controles criptográficos usados por Azure RMS: Longitudes de clave y algoritmos](how-does-it-work.md#cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths).

√ Soporte para que los módulos de seguridad de hardware (HSM) de Thales almacenen su clave de inquilino en centros de datos de Microsoft Azure. Azure RMS utiliza espacios de seguridad independientes para sus centros de datos en América del Norte, EMEA (Europa, Oriente Medio y África) y Asia, para que sus claves solo se puedan usar en su región.

√ Certificado para lo siguiente:

-   ISO/IEC 27001:2013 (incluye [ISO/IEC 27018](http://azure.microsoft.com/blog/2015/02/16/azure-first-cloud-computing-platform-to-conform-to-isoiec-27018-only-international-set-of-privacy-controls-in-the-cloud/))

-   Atestaciones de SOC 2 SSAE 16/ISAE 3402

-   HIPAA BAA

-   Cláusula del modelo de la UE

-   FedRAMP como parte de Azure Active Directory en la certificación de Office 365, FedRAMP Agency Authority to Operate emitido por HHS

-   PCI DSS nivel 1

Para obtener más información sobre estas certificaciones externas, consulte el [Centro de confianza de Azure](http://azure.microsoft.com/support/trust-center/compliance/).

## Pasos siguientes

Para ver el aspecto de Azure RMS para los administradores y usuarios, consulte [Azure RMS en acción](what-admins-users-see.md).

Si le interesa información más técnica sobre el funcionamiento de Azure RMS, consulte [¿Cómo funciona Azure RMS?](how-does-it-work.md) 


<!--HONumber=Aug16_HO4-->


