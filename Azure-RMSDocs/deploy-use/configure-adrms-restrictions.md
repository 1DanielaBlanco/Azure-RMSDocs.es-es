---
title: Protección HYOK para Azure Information Protection
description: Identifique las limitaciones, los requisitos previos y las recomendaciones si selecciona la protección de HYOK (AD RMS) con Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/24/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
ms.openlocfilehash: 8e9a29f01c3fe22a2eb30380510a3c532780fdf2
ms.sourcegitcommit: 5892db302bdf96538ecb3af8e3c2f678f5d1ebe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="hold-your-own-key-hyok-requirements-and-restrictions-for-ad-rms-protection"></a>Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

La protección de los documentos y correos electrónicos más confidenciales normalmente se lleva a cabo mediante la aplicación de protección de Azure Rights Management (Azure RMS) para beneficiarse de las siguientes características:

- No se requiere ninguna infraestructura de servidor, lo que hace que la solución sea más rápida y más rentable de implementar y mantener que una solución local.

- Uso compartido más fácil con asociados y usuarios de otras organizaciones mediante la autenticación basada en la nube.

- Estrecha integración con servicios de Office 365, como la búsqueda, visores web, vistas dinamizadas, antimalware, eDiscovery y Delve.

- Seguimiento de documentos, revocación y notificación por correo electrónico para los documentos confidenciales que ha compartido.

Azure RMS protege los documentos y correos electrónicos de la organización mediante una clave privada de la organización que administra Microsoft (valor predeterminado), o el usuario (escenario "traiga su propia clave" o BYOK). La información que proteja con Azure RMS nunca se envía a la nube. Los documentos y correos electrónicos protegidos no se almacenan en Azure a menos que los almacene explícitamente ahí o use otro servicio en la nube que los almacene en Azure. Para obtener más información sobre las opciones de clave de inquilino, vea [Planeamiento e implementación de la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

En cambio, algunas organizaciones podrían requerir la protección de un pequeño subconjunto de documentos y correos electrónicos con una clave que esté almacenada de forma local. Por ejemplo, esto puede ser necesario por motivos normativos o de cumplimiento.  

Esta configuración se conoce a veces como "mantenga su propia clave" (HYOK) y es compatible con Azure Information Protection si tiene una implementación en funcionamiento de Active Directory Rights Management Services (AD RMS) con los requisitos que se documentan en la sección siguiente.

En este escenario HYOK, las directivas de permisos y la clave privada de la organización que protege estas directivas se administran y mantienen de forma local, mientras que Azure sigue administrando la directiva de Azure Information Protection para etiquetado y clasificación, que se almacena en Azure. Al igual que con la protección de Azure RMS, la información que protege con AD RMS nunca se envía a la nube.

> [!NOTE]
> Use esta configuración solo cuando tenga que hacerlo y solo en documentos y correos electrónicos que lo requieran. La protección de AD RMS no ofrece las ventajas enumeradas que obtiene al usar la protección de Azure RMS y su finalidad es "opacidad de datos a toda costa".
>
> Incluso en el caso de las organizaciones que utilizan esta configuración, esta opción normalmente está indicada para menos del 10 % de todo el contenido que requiere protección. A efectos orientativos, utilícela solo para documentos o mensajes de correo electrónico que cumplan los siguientes criterios:
> 
> **El contenido tiene la clasificación de confidencialidad más alta de la organización ("ultrasecreto") y son muy pocas las personas que tienen acceso a él.**
> 
> **El contenido no se comparte nunca fuera de la organización.**
> 
> **El contenido solo se usa en la red interna.**
> 
> **El contenido no necesita usarse en equipos Mac o dispositivos móviles.**

Los usuarios no saben si una etiqueta usa la protección de AD RMS en lugar de la protección de Azure RMS. Debido a las restricciones y limitaciones de la protección de AD RMS, asegúrese de proporcionar instrucciones claras sobre las excepciones relativas a cuándo deben seleccionar los usuarios las etiquetas que aplican la protección de AD RMS. 

[Las directivas de ámbito](configure-policy-scope.md) son muy útiles para asegurarse de que los usuarios que tienen que aplicar la protección de AD RMS sean los únicos que ven las etiquetas configuradas para la protección de AD RMS. 

## <a name="additional-limitations-when-using-hyok"></a>Limitaciones adicionales de uso de Hold your own key (HYOK, Mantenga su propia clave)

Además de no poder gozar de los beneficios que se obtienen al utilizar la protección de Azure RMS, el uso de la protección de AD RMS con Azure Information Protection tiene las limitaciones siguientes:

- No es compatible con Office 2010 ni Office 2007.

- Indique a los usuarios que no seleccionen **No reenviar** en Outlook, o proporcióneles instrucciones específicas. 

    Aunque puede configurar una etiqueta para **No reenviar** para usar HYOK o el servicio Azure Rights Management, los usuarios también pueden seleccionar por sí mismos No reenviar. Pueden seleccionar esta opción mediante el botón **No reenviar** situado en la pestaña **Mensaje** de la cinta de opciones de Office, o mediante las opciones de menú de Outlook. Las opciones de menú **No reenviar** se encuentran en **Archivo** > **Permisos**, y en el botón **Permisos** en la pestaña **Opciones** de la cinta de opciones. 
    
    El cliente de Azure Information Protection siempre usa Azure RMS cuando los usuarios seleccionan el botón **No reenviar** de Outlook. Si no quiere este comportamiento, puede ocultar este botón estableciendo la [configuración de directiva](../deploy-use/configure-policy-settings.md) **Agregar el botón No reenviar a la cinta de Outlook** en **Desactivado**. 
    
    Cuando los usuarios seleccionan **No reenviar** desde una opción de menú de Outlook, pueden elegir Azure RMS o AD RMS, pero es posible que no sepan qué opción deben seleccionar para el mensaje de correo electrónico. Si se usa AD RMS cuando se debería usar Azure RMS, los usuarios con los que se comparta de forma externa no podrán abrir estos mensajes de correo electrónico.

- Si los usuarios eligen una etiqueta en Outlook que aplica la protección de AD RMS y, antes de enviar el correo electrónico, cambian de opinión y seleccionan una etiqueta que aplica la protección de Azure RMS, no se podrá aplicar la etiqueta recién seleccionada. Aparece el siguiente mensaje de error: **Azure Information Protection no puede aplicar esta etiqueta. No tiene permiso para realizar esta acción.**
    
    La única solución es cerrar el mensaje de correo electrónico y volver a iniciarlo. Existe la misma limitación si, de forma similar, los usuarios primero eligen una etiqueta que aplica la protección de Azure RMS y, a continuación, cambian la etiqueta a otra que aplica la protección de AD RMS.

## <a name="requirements-for-hyok"></a>Requisitos para HYOK

Compruebe que la implementación de AD RMS cumple los siguientes requisitos para proporcionar protección de AD RMS para Azure Information Protection.

- Configuración de AD RMS:
    
    - Versión mínima de Windows Server 2012 R2: necesaria para entornos de producción, pero para fines de pruebas o evaluación se puede usar una versión mínima de Windows Server 2008 R2 con Service Pack 1.
    
    - Una de las topologías siguientes:
        
        - Un bosque individual con un clúster raíz de AD RMS único. 
        
        - Varios bosques con clústeres de raíz de AD RMS independientes y usuarios sin acceso al contenido protegido por los usuarios en los otros bosques.
        
        - Varios bosques con clústeres de AD RMS en cada uno. Cada clúster de AD RMS comparte una dirección URL de licencia que apunta al mismo clúster de AD RMS. En este clúster de AD RMS, debe importar todos los certificados de dominio de usuario de confianza (TUD) de todos los otros clústeres de AD RMS. Para obtener más información acerca de esta topología, consulte [Dominio de usuario de confianza] (https://technet.microsoft.com/library/dd983944(v=ws.10\).aspx).
        
    Cuando haya varios clústeres de AD RMS en bosques diferentes, elimine las etiquetas en la directiva global que aplica la protección de HYOK (AD RMS) y configure una [directiva con ámbito](configure-policy-scope.md) para cada clúster. A continuación, asigne los usuarios de cada clúster a su directiva con ámbito, asegurándose de que no se usen grupos que puedan causar que un usuario quede asignado a más de una directiva con ámbito. El resultado debería ser que cada usuario tenga etiquetas para un único clúster de AD RMS. 
    
    - [Modo criptográfico 2](https://technet.microsoft.com/library/hh867439.aspx): puede confirmar el modo comprobando las propiedades de clúster de AD RMS en la pestaña **General**.
    
    - Cada servidor de AD RMS está configurado para la dirección URL de certificación. [Instrucciones](#configuring-ad-rms-servers-to-locate-the-certification-url) 
    
    - Punto de conexión de servicio (SCP) no registrado en Active Directory: cuando se usa la protección de AD RMS con Azure Information Protection, no se utiliza ningún SCP. 
    
        - Si tiene registrado un SCP para la implementación de AD RMS, debe quitarlo para que la [detección de servicios](../rms-client/client-deployment-notes.md#rms-service-discovery) se realice correctamente para la protección de Azure Rights Management. 
        
        - Si está instalando un nuevo clúster de AD RMS para HYOK, omita el paso para registrar el SCP durante la configuración del primer nodo. Para cada nodo adicional, asegúrese de que el servidor está configurado para la dirección URL de certificación antes de agregar el rol de AD RMS y unirse al clúster existente.
    
    - Los servidores de AD RMS están configurados para usar SSL/TLS con un certificado X.509 válido que sea de confianza para los clientes que se conecten a este: es necesario para entornos de producción, pero no es obligatorio para fines de pruebas o evaluación.
    
    - Plantillas de permisos configuradas.

- La sincronización de directorios se configura entre su Active Directory local y Azure Active Directory y los usuarios que usarán la protección de AD RMS están configurados para el inicio de sesión único.

- Si comparte documentos o correos electrónicos que están protegidas por AD RMS con otros usuarios fuera de la organización: AD RMS está configurado para confianzas definidas explícitamente en una relación directa punto a punto con el resto de las organizaciones mediante el uso de dominios de usuario de confianza (TUD) o confianzas federadas que se crean mediante los servicios de federación de Active Directory (AD FS).

- Los usuarios tienen una versión de Office que es Office 2016 Professional Plus u Office 2013 Professional Plus con Service Pack 1, que se ejecuta en Windows 7 Service Pack 1 o una versión posterior. Tenga en cuenta que Office 2010 y Office 2007 no son compatibles con este escenario.
    
    
    - Para Office 2016, edición basada en Microsoft Installer (.msi): ha instalado la [actualización 4018295 para Microsoft Office 2016 que se publicó en 6 de marzo de 2018](https://support.microsoft.com/en-us/help/4018295/march-6-2018-update-for-office-2016-kb4018295).

> [!IMPORTANT]
> Para cumplir con la seguridad alta que ofrece este escenario, se recomienda que los servidores de AD RMS no se encuentren en la red perimetral y que solo los usen los equipos bien administrados (por ejemplo, los que no son dispositivos móviles ni equipos de grupo de trabajo). 
> 
> También recomendamos que en el clúster de AD RMS se use un módulo de seguridad de hardware (HSM) para que la clave privada del certificado de emisor de licencias de servidor (SLC) no quede expuesta o se pueda robar en caso de que se produzca alguna infracción de seguridad en la implementación de AD RMS o esta pierda su carácter confidencial. 

Para obtener información e instrucciones sobre la implementación de AD RMS, consulte [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) en la biblioteca de Windows Server. 


## <a name="configuring-ad-rms-servers-to-locate-the-certification-url"></a>Configuración de servidores de AD RMS para buscar la dirección URL de certificación

1. En cada servidor de AD RMS del clúster, cree la entrada del Registro siguiente:

    `Computer\HKEY_LOCAL_MACHINE\Software\Microsoft\DRMS\GICURL = "<string>"`
    
    Para el \<valor de cadena>, especifique uno de los siguientes:
    
    - Para clústeres de AD RMS que usan SSL/TLS:

            https://<cluster_name>/_wmcs/certification/certification.asmx
    
    - Para clústeres de AD RMS que no usan SSL/TLS (solo redes de prueba):
        
            http://<cluster_name>/_wmcs/certification/certification.asmx

2. Reinicie IIS.

## <a name="locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label"></a>Buscar la información para especificar la protección de AD RMS con una etiqueta de Azure Information Protection

Al configurar una etiqueta para la protección de **HYOK (AD RMS)**, debe especificar la dirección URL de administración de licencias del clúster de AD RMS. Además, debe especificar una plantilla que haya configurado para los permisos que se conceden a los usuarios, o bien dejar que los usuarios definan los permisos y los usuarios. 

Encontrará los valores del GUID de plantilla y de la dirección URL de administración de licencias en la consola de Active Directory Rights Management Services:

- Para buscar un GUID de plantilla: expanda el clúster y haga clic en **Plantillas de directiva de derechos**. En la información **Plantillas de directiva de permisos distribuidas**, puede copiar el GUID de la plantilla que quiera usar. Por ejemplo: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Para buscar la URL de administración de licencias: haga clic en el nombre del clúster. En la información **Detalles del clúster**, copie el valor **Licencias** menos la cadena **/_wmcs/licensing**. Por ejemplo: https://rmscluster.contoso.com 
    
    Si tiene un valor de administración de licencias de extranet, así como un valor de administración de licencias de intranet, y estas son diferentes, especifique el valor de extranet solo si va a compartir documentos o correos electrónicos protegidos con asociados que haya definido con confianzas explícitas punto a punto. De lo contrario, use el valor de intranet y asegúrese de que todos los equipos cliente que usan la protección de AD RMS con Azure Information Protection se conectan mediante una conexión de intranet (por ejemplo, los equipos remotos usan una conexión VPN).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre esta característica y orientaciones para cuándo usarla, vea el anuncio de entrada de blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://cloudblogs.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) (Azure Information Protection con HYOK [Mantenga su propia clave]).

Para configurar una etiqueta para la protección de AD RMS, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](../deploy-use/configure-policy-protection.md). 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]