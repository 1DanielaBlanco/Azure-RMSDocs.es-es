---
title: Restricciones de HYOK | Azure Information Protection
description: Identify the limitations, prerequisites, and recommendations if you select AD RMS protection with Azure Information Protection. This solution is sometimes referred to as "hold your own key" (HYOK).
manager: mbaldwin
ms.date: 08/25/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 7667b5b0-c2e9-4fcf-970f-05577ba51126
translationtype: Human Translation
ms.sourcegitcommit: 6bbac611f9c8bba96fbbba69e8044e494134d792
ms.openlocfilehash: fe0f492b94cbcc437c722daae9c3c56820593566


---

# Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Al proteger los documentos y correos electrónicos más confidenciales, normalmente lo hace mediante la aplicación de protección de Azure Rights Management para beneficiarse de las siguientes características:

- No se requiere ninguna infraestructura de servidor, lo que hace que la solución sea más rápida y más rentable de implementar y mantener que una solución local.

- Uso compartido más fácil con asociados y usuarios de otras organizaciones mediante la autenticación basada en la nube.

- Estrecha integración con servicios de Office 365, como la búsqueda, visores web, vistas dinamizadas, antimalware, eDiscovery y Delve.

- Seguimiento de documentos, revocación y notificación por correo electrónico para los documentos confidenciales que ha compartido.

Azure RMS protege los documentos y correos electrónicos de la organización mediante una clave privada de la organización que administra Microsoft (valor predeterminado), o el usuario (escenario "traiga su propia clave" o BYOK). La información que proteja con Azure RMS nunca se envía a la nube. Los documentos y correos electrónicos protegidos no se almacenan en Azure a menos que los almacene explícitamente ahí o use otro servicio en la nube que los almacene en Azure. Para obtener más información sobre las opciones de clave de inquilino, vea [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md). 

En cambio, algunos clientes podrían necesitar proteger documentos y correos electrónicos seleccionados con una clave que esté almacenada de forma local. Por ejemplo, esto puede ser necesario por motivos normativos o de cumplimiento. 

Esta configuración se conoce a veces como "mantenga su propia clave" (HYOK) y es compatible con Azure Information Protection si tiene una implementación en funcionamiento de Active Directory Rights Management Services (AD RMS) con los requisitos que se documentan en la sección siguiente. 

En este escenario HYOK, las directivas de permisos y la clave privada de la organización que protege estas directivas se administran y mantienen de forma local, mientras que Azure sigue administrando la directiva de Azure Information Protection para etiquetado y clasificación, que se almacena en Azure. Al igual que con la protección de Azure RMS, la información que protege con AD RMS nunca se envía a la nube.

> [!NOTE]
> Use esta configuración solo cuando tenga que hacerlo y solo en documentos y correos electrónicos que lo requieran. La protección de AD RMS no ofrece las ventajas enumeradas que obtiene al usar la protección de Azure RMS y su finalidad es "opacidad de datos a toda costa".

Los usuarios no sabrán si una etiqueta usa la protección de AD RMS en lugar de la protección de Azure RMS. Debido a las restricciones de la protección de AD RMS, asegúrese de que proporciona instrucciones claras sobre cuándo deben seleccionar los usuarios las etiquetas que aplican la protección de AD RMS.

## Requisitos para HYOK

Compruebe que la implementación de AD RMS cumple los siguientes requisitos para proporcionar protección de AD RMS para Azure Information Protection.

- Configuración de AD RMS:
    
    - Versión mínima de Windows Server 2012 R2: necesaria para entornos de producción, pero para fines de pruebas o evaluación se puede usar una versión mínima de Windows Server 2008 R2 con Service Pack 1.
    
    - Un único clúster raíz de AD RMS.
    
    - [Modo criptográfico 2](https://technet.microsoft.com/library/hh867439.aspx): puede confirmar la versión del modo criptográfico del clúster de AD RMS y su estado general con la [herramienta RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437).   
    
    - Los servidores de AD RMS están configurados para usar SSL/TLS con un certificado X.509 válido que sea de confianza para los clientes que se conecten a este: es necesario para entornos de producción, pero no es obligatorio para fines de pruebas o evaluación.
    
    - Plantillas de permisos configuradas.

- La sincronización de directorios se configura entre su Active Directory local y Azure Active Directory y los usuarios que usarán la protección de AD RMS están configurados para el inicio de sesión único.

- Si va a compartir documentos o correos electrónicos que están protegidas por AD RMS con otros usuarios fuera de la organización: AD RMS está configurado para confianzas definidas explícitamente en una relación directa punto a punto con el resto de las organizaciones mediante el uso de dominios de usuario de confianza (TUD) o confianzas federadas que se crean mediante los servicios de federación de Active Directory (AD FS).

- Los usuarios tienen una versión de Office que es Office 2013 Pro Plus con Service 1 u Office 2016 Pro Plus, que se ejecuta en Windows 7 Service Pack 1 o una versión posterior. Tenga en cuenta que Office 2010 y Office 2007 no son compatibles con este escenario.

- La versión del cliente de [Azure Information Protection](info-protect-client.md) es **1.0.233.0** o una versión posterior.

> [!IMPORTANT]
> Para cumplir con la seguridad alta que ofrece este escenario, se recomienda que los servidores de AD RMS no se encuentren en la red perimetral y que solo los usen los equipos bien administrados (por ejemplo, los que no son dispositivos móviles ni equipos de grupo de trabajo). 
> 
> También recomendamos que en el clúster de AD RMS se use un módulo de seguridad de hardware (HSM) para que la clave privada del certificado de emisor de licencias de servidor (SLC) no quede expuesta o se pueda robar en caso de que se produzca alguna infracción de seguridad en la implementación de AD RMS o esta pierda su carácter confidencial. 

Para obtener información e instrucciones sobre la implementación de AD RMS, consulte [Active Directory Rights Management Services](https://technet.microsoft.com/library/hh831364.aspx) en la biblioteca de Windows Server. 


## Buscar la información para especificar la protección de AD RMS con una etiqueta de Azure Information Protection

Al configurar una etiqueta para la protección de AD RMS, debe especificar el GUID de la plantilla y la dirección URL de administración de licencias del clúster de AD RMS. Puede encontrar estos valores en la consola de Active Directory Rights Management Services:

- Para buscar el GUID de la plantilla: expanda el clúster y haga clic en **Plantillas de directiva de permisos**. En la información **Plantillas de directiva de permisos distribuidas**, puede copiar el GUID de la plantilla que quiera usar. Por ejemplo: 82bf3474-6efe-4fa1-8827-d1bd93339119

- Para buscar la URL de administración de licencias: haga clic en el nombre del clúster. En la información **Detalles del clúster**, copie el valor **Licencias** menos la cadena **/_wmcs/licensing**. Por ejemplo: https://rmscluster.contoso.com 
    
    Si tiene un valor de administración de licencias de extranet, así como un valor de administración de licencias de intranet y son diferentes: especifique el valor de extranet solo si va a compartir documentos o correos electrónicos protegidos con asociados que ha definido con confianzas explícitas punto a punto. De lo contrario, use el valor de intranet y asegúrese de que todos los equipos cliente que usan la protección de AD RMS con Azure Information Protection se conectan mediante una conexión de intranet (por ejemplo, los equipos remotos usan una conexión VPN).

## Pasos siguientes

Para obtener más información sobre esta característica en vista previa, consulte el anuncio de entrada de blog [Azure Information Protection with HYOK (Hold Your Own Key)](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/10/azure-information-protection-with-hyok-hold-your-own-key/) [Azure Information Protection con HYOK (Mantenga su propia clave)].

Para configurar una etiqueta para la protección de AD RMS, consulte [Configuración de una etiqueta para aplicar protección de Rights Management](configure-policy-protection.md). 



<!--HONumber=Sep16_HO1-->


