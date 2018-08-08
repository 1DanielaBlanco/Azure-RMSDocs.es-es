---
title: Protección HYOK para Azure Information Protection
description: Información general sobre la protección HYOK (AD RMS) con Azure Information Protection, los escenarios compatibles, las limitaciones, los requisitos previos y las recomendaciones.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/01/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: 5c8e918bd467d1d7540a129bca266c0f0c077a56
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39474263"
---
# <a name="hold-your-own-key-hyok-protection-for-azure-information-protection"></a>Protección HYOK (hold your own key) para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Use la siguiente información para comprender qué es la protección HYOK (hold your own key) para Azure Information Protection y en qué se diferencia de la protección predeterminada basada en la nube. Antes de usar la protección HYOK, asegúrese de que comprende cuándo es adecuada, los escenarios admitidos, las limitaciones y los requisitos. 

## <a name="cloud-based-protection-vs-hyok"></a>Protección basada en la nube frente a HYOK

Cuando se protegen los documentos y los mensajes de correo electrónico más confidenciales con Azure Information Protection, normalmente se hace mediante la aplicación de una clave basada en la nube que usa la protección de Azure Rights Management (Azure RMS) para beneficiarse de lo siguiente:

- No se requiere ninguna infraestructura de servidor, lo que hace que la solución sea más rápida y más rentable de implementar y mantener que una solución local.

- Uso compartido más fácil con asociados y usuarios de otras organizaciones mediante la autenticación basada en la nube.

- Estrecha integración con servicios de Azure y Office 365, como búsqueda, visores web, vistas dinamizadas, antimalware, eDiscovery y Delve.

- Seguimiento de documentos, revocación y notificación por correo electrónico para los documentos confidenciales que ha compartido.

Una clave basada en la nube protege los documentos y los mensajes de correo electrónico de la organización mediante una clave privada de la organización que administra Microsoft (valor predeterminado) o el usuario (escenario "Bring Your Own Key" o BYOK). Para obtener más información sobre las opciones de clave de inquilino, vea [Planeamiento e implementación de la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

Los documentos y los mensajes de correo electrónico que protege se pueden almacenar en la nube o en local. Para obtener más información sobre cómo funciona el proceso de protección de esta clave basada en la nube, vea [¿Qué es Azure Rights Management?](../what-is-azure-rms.md )

Los servicios de Office 365 y las aplicaciones basadas en la nube del inquilino se pueden integrar con Azure Information Protection para que las funciones empresariales importantes, como los servicios de búsqueda, indización, archivado y antimalware, continúen funcionando sin problemas para el contenido protegido con Azure Information Protection. Esta capacidad de leer el contenido cifrado de estos escenarios se suele denominar "reasoning over data" (razonamiento a través de datos). Por ejemplo, es la capacidad que permite a Exchange Online descifrar los mensajes de correo electrónico para la exploración de malware y ejecutar reglas de 
prevención de pérdida de datos (DLP) en mensajes cifrados.

Pero, para los requisitos normativos, algunas organizaciones podrían exigir el cifrado del contenido con una clave aislada de la nube. Este aislamiento significa que solo las aplicaciones locales y los servicios locales pueden leer el contenido cifrado. Esta opción de administración de claves es compatible con Azure Information Protection y se conoce como "hold your own key" o HYOK. Cuando se usa Azure Information Protection con HYOK, el inquilino tiene una clave basada en la nube y una clave local.

## <a name="hyok-guidance-and-best-practices"></a>Instrucciones y procedimientos recomendados de HYOK

Use la protección HYOK solo para los documentos y los mensajes de correo electrónico que exijan que la clave de cifrado esté aislada de la nube. La protección HYOK no ofrece las ventajas mencionadas que se obtienen al usar la protección de claves basada en la nube y suele tener la desventaja de la "opacidad de datos". Esta frase significa que solo las aplicaciones y los servicios locales pueden abrir datos protegidos con HYOK; las aplicaciones y los servicios basados en la nube no pueden razonar a través de datos protegidos con HYOK.

Incluso en las organizaciones que usan la protección HYOK, normalmente es adecuada para un número pequeño de documentos que se deben proteger. A efectos orientativos, úsela solo para documentos que cumplan todos los criterios siguientes:

- El contenido tiene la clasificación de confidencialidad más alta de la organización ("ultrasecreto") y son muy pocas las personas que tienen acceso a él

- El contenido no se comparte fuera de la organización

- El contenido solo se usa en la red interna

Dado que la protección HYOK es una opción de configuración de administrador para una etiqueta, los flujos de trabajo de usuario siguen igual, independientemente de si la protección usa una clave basada en la nube o HYOK.

Las [directivas con ámbito](configure-policy-scope.md) son muy útiles para asegurarse de que los usuarios que tienen que aplicar la protección HYOK sean los únicos que ven las etiquetas configuradas para la protección HYOK. 

## <a name="supported-scenarios-for-hyok"></a>Escenarios admitidos para HYOK

Para aplicar la protección HYOK, use etiquetas de Azure Information Protection. 

En la tabla siguiente se enumeran los escenarios admitidos para proteger el contenido mediante etiquetas configuradas para HYOK y para abrir (usar) el contenido protegido por HYOK.

|Plataforma|Aplicación|Compatible.|
|----------------------|----------|-----------|
|Windows|Cliente de Azure Information Protection con Office 2016 y Office 2013 <br /><br />- Word, Excel, PowerPoint|Protección: sí<br /><br />Uso: sí|
|Windows|Cliente de Azure Information Protection con Office 2016 y Office 2013 <br /><br />- Outlook|Protección: sí<br /><br />Uso: sí|
|Windows|Cliente de Azure Information Protection con el Explorador de archivos|Protección: sí <br /><br />Uso: sí|
|Windows|Visor de Azure Information Protection|Protección: no aplicable<br /><br />Uso: sí|
|Windows|Cliente de Azure Information Protection con cmdlets de etiquetado de PowerShell|Protección: sí<br /><br />Uso: sí|
|Windows|Analizador de Azure Information Protection|Protección: sí<br /><br />Uso: sí|
|Windows|Aplicación de uso compartido Rights Management|Protección: no<br /><br />Uso: sí|
|MacOS|Office para Mac <br /><br /> - Word, Excel, PowerPoint|Protección: no<br /><br />Uso: sí|
|MacOS|Office para Mac<br /><br />- Outlook|Protección: no<br /><br />Uso: sí|
|MacOS|Aplicación de uso compartido Rights Management|Protección: no<br /><br />Uso: sí|
|iOS|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protección: no<br /><br />Uso: sí|
|iOS|Office Mobile <br /><br />-Outlook|Protección: no<br /><br />Uso: no|
|iOS|Visor de Azure Information Protection|Protección: no aplicable<br /><br />Uso: sí|
|Android|Office Mobile <br /><br />- Word, Excel, PowerPoint|Protección: no<br /><br />Uso: sí|
|Android|Office Mobile <br /><br />- Outlook|Protección: no<br /><br />Uso: no|
|Android|Visor de Azure Information Protection|Protección: no aplicable<br /><br />Uso: sí|
|Web|Outlook en la web|Protección: no<br /><br />Uso: no|
|Web|Office Online<br /><br />- Word, Excel, PowerPoint|Protección: no<br /><br />Uso: no|
|Universal|Aplicaciones universales de Office<br /><br />- Word, Excel, PowerPoint|Protección: no<br /><br />Uso: no|


## <a name="additional-limitations-when-using-hyok"></a>Limitaciones adicionales de uso de Hold your own key (HYOK, Mantenga su propia clave)

Además, el uso de la protección HYOK con las etiquetas de Azure Information Protection tiene las siguientes limitaciones:

- No es compatible con Office 2010 ni Office 2007.

- Los servicios de Office 365 y otros servicios en línea no pueden descifrar documentos y mensajes de correo electrónico protegidos con HYOK para inspeccionar el contenido y tomar medidas en ellos. Esta limitación se extiende a los documentos y los mensajes de correo electrónico protegidos con HYOK que han sido protegidos con el conector de Rights Management. 
    
    Esta pérdida de funcionalidad del correo electrónico protegido con HYOK incluye detectores de malware, soluciones de prevención de pérdida de datos (DLP), reglas de enrutamiento de correo electrónico, registro en diario, eDiscovery, soluciones de archivado y Exchange ActiveSync. Además, los usuarios no entenderán por qué algunos dispositivos no pueden abrir sus mensajes de correo electrónico protegidos con HYOK, y esto puede dar lugar a llamadas al departamento de soporte técnico. Debido a la cantidad de limitaciones, no se recomienda usar la protección HYOK para los mensajes de correo electrónico.

## <a name="implementing-hyok"></a>Implementación de HYOK

HYOK es compatible con Azure Information Protection si tiene una implementación en funcionamiento de Active Directory Rights Management Services (AD RMS) con los requisitos que se documentan en la sección siguiente. En este escenario, las directivas de derechos de uso y la clave privada de la organización que protege estas directivas se administran y mantienen de forma local, mientras que Azure sigue administrando la directiva de Azure Information Protection para etiquetado y clasificación, que se almacena en Azure. 

No confunda HYOK y Azure Information Protection con el uso de una implementación completa de AD RMS y Azure Information Protection, ni lo considere una alternativa a la migración de AD RMS a Azure Information Protection. HYOK solo se admite mediante la aplicación de etiquetas, no ofrece paridad de características con AD RMS y no admite todas las configuraciones de implementación de AD RMS:

- Para obtener más información sobre los escenarios admitidos por HYOK para proteger el contenido y usar contenido protegido, vea la sección [Escenarios admitidos para HYOK](#supported-scenarios-for-hyok).

- Para obtener instrucciones de migración desde AD RMS, vea [Migración desde AD RMS a Azure Information Protection](../plan-design/migrate-from-ad-rms-to-azure-rms.md).

- Para obtener más información sobre los requisitos de implementación de AD RMS, vea la siguiente sección.

### <a name="requirements-for-ad-rms-to-support-hyok"></a>Requisitos de AD RMS para admitir HYOK

Una implementación de AD RMS debe cumplir los siguientes requisitos para proporcionar protección HYOK para etiquetas de Azure Information Protection.

- Configuración de AD RMS:
    
    - Versión mínima de Windows Server 2012 R2: necesaria para entornos de producción, pero para fines de pruebas o evaluación se puede usar una versión mínima de Windows Server 2008 R2 con Service Pack 1.
    
    - Una de las topologías siguientes:
        
        - Un bosque individual con un clúster raíz de AD RMS único. 
        
        - Varios bosques con clústeres de raíz de AD RMS independientes y usuarios sin acceso al contenido protegido por los usuarios en los otros bosques.
        
        - Varios bosques con clústeres de AD RMS en cada uno. Cada clúster de AD RMS comparte una dirección URL de licencia que apunta al mismo clúster de AD RMS. En este clúster de AD RMS, debe importar todos los certificados de dominio de usuario de confianza (TUD) de todos los otros clústeres de AD RMS. Para obtener más información sobre esta topología, vea [Dominio de usuario de confianza](https://technet.microsoft.com/library/dd983944(v=ws.10\).aspx).
        
    Cuando haya varios clústeres de AD RMS en bosques diferentes, elimine las etiquetas en la directiva global que aplica la protección de HYOK (AD RMS) y configure una [directiva con ámbito](configure-policy-scope.md) para cada clúster. A continuación, asigne los usuarios de cada clúster a su directiva con ámbito, asegurándose de que no se usen grupos que puedan causar que un usuario quede asignado a más de una directiva con ámbito. El resultado debería ser que cada usuario tenga etiquetas para un único clúster de AD RMS. 
    
    - [Modo criptográfico 2](https://technet.microsoft.com/library/hh867439.aspx): puede confirmar el modo comprobando las propiedades de clúster de AD RMS en la pestaña **General**.
    
    - Cada servidor de AD RMS está configurado para la dirección URL de certificación. [Instrucciones](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
    - Punto de conexión de servicio (SCP) no registrado en Active Directory: cuando se usa la protección de AD RMS con Azure Information Protection, no se utiliza ningún SCP. 
    
        - Si tiene registrado un SCP para la implementación de AD RMS, debe quitarlo para que la [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se realice correctamente para la protección de Azure Rights Management. 
        
        - Si está instalando un nuevo clúster de AD RMS para HYOK, omita el paso para registrar el SCP durante la configuración del primer nodo. Para cada nodo adicional, asegúrese de que el servidor está configurado para la dirección URL de certificación antes de agregar el rol de AD RMS y unirse al clúster existente.
    
    - Los servidores de AD RMS están configurados para usar SSL/TLS con un certificado X.509 válido que sea de confianza para los clientes que se conecten a este: es necesario para entornos de producción, pero no es obligatorio para fines de pruebas o evaluación.
    
    - Plantillas de permisos configuradas.
    
    - No haber establecido la configuración para IRM para Exchange.
    
    - En dispositivos móviles y equipos Mac: [Extensión de Active Directory Rights Management Services para dispositivos móviles](https://technet.microsoft.com/library/dn673574.aspx) instalada y configurada.

- La sincronización de directorios se configura entre Active Directory local y Azure Active Directory, y los usuarios que van a usar la protección HYOK se configuran para el inicio de sesión único.

- Si comparte documentos o mensajes de correo electrónico protegidos con HYOK con otros usuarios fuera de la organización: AD RMS está configurado para confianzas definidas explícitamente en una relación directa punto a punto con el resto de las organizaciones mediante el uso de dominios de usuario de confianza (TUD) o confianzas federadas que se crean mediante los Servicios de federación de Active Directory (AD FS).

- Los usuarios tienen una versión de Office que es Office 2016 Professional Plus u Office 2013 Professional Plus con Service Pack 1, que se ejecuta en Windows 7 Service Pack 1 o una versión posterior. Tenga en cuenta que Office 2010 y Office 2007 no son compatibles con este escenario.
    
    - Para Office 2016, edición basada en Microsoft Installer (.msi): ha instalado la [actualización 4018295 para Microsoft Office 2016 que se publicó en 6 de marzo de 2018](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295).

> [!IMPORTANT]
> Para alcanzar la seguridad alta que ofrece la protección HYOK, se recomienda que los servidores de AD RMS no se encuentren en la red perimetral y que solo los usen los equipos administrados. 
> 
> También recomendamos que en el clúster de AD RMS se use un módulo de seguridad de hardware (HSM) para que la clave privada del certificado de emisor de licencias de servidor (SLC) no quede expuesta o se pueda robar en caso de que se produzca alguna infracción de seguridad en la implementación de AD RMS o esta pierda su carácter confidencial. 

Para obtener información e instrucciones sobre la implementación de AD RMS, consulte [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) en la biblioteca de Windows Server. 


### <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configuración de servidores de AD RMS para buscar la dirección URL de certificación

1. En cada servidor de AD RMS del clúster, cree la entrada del Registro siguiente:

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    Para el \<valor de cadena>, especifique uno de los siguientes:
    
    - Para clústeres de AD RMS que usan SSL/TLS:

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - Para clústeres de AD RMS que no usan SSL/TLS (solo redes de prueba):
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. Reinicie IIS.

### <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Buscar la información para especificar la protección de AD RMS con una etiqueta de Azure Information Protection

Al configurar una etiqueta para la protección de **HYOK (AD RMS)**, debe especificar la dirección URL de administración de licencias del clúster de AD RMS. Además, debe especificar una plantilla que haya configurado para los permisos que se conceden a los usuarios, o bien dejar que los usuarios definan los permisos y los usuarios. 

Encontrará los valores del GUID de plantilla y de la dirección URL de administración de licencias en la consola de Active Directory Rights Management Services:

- Para buscar un GUID de plantilla: expanda el clúster y haga clic en **Plantillas de directiva de derechos**. En la información **Plantillas de directiva de permisos distribuidas**, puede copiar el GUID de la plantilla que quiera usar. Por ejemplo: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Para buscar la URL de administración de licencias: haga clic en el nombre del clúster. En la información **Detalles del clúster**, copie el valor **Licencias** menos la cadena **/_wmcs/licensing**. Por ejemplo: https://rmscluster.contoso.com 
    
    Si tiene un valor de administración de licencias de extranet, así como un valor de administración de licencias de intranet, y estas son diferentes, especifique el valor de extranet solo si va a compartir documentos o correos electrónicos protegidos con asociados que haya definido con confianzas explícitas punto a punto. De lo contrario, use el valor de intranet y asegúrese de que todos los equipos cliente que usan la protección de AD RMS con Azure Information Protection se conectan mediante una conexión de intranet (por ejemplo, los equipos remotos usan una conexión VPN).


## <a name="next-steps"></a>Pasos siguientes

Para configurar una etiqueta para la protección HYOK, vea [Configuración de una etiqueta para la protección de Rights Management](../deploy-use/configure-policy-protection.md). 
