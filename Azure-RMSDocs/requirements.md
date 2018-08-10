---
title: Requirements for Azure Information Protection (Requisitos de Azure Information Protection)
description: Identifique los requisitos previos para implementar Azure Information Protection en su organización.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/27/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: dc78321d-d759-4653-8818-80da74b6cdeb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 98c4f32e0964b736c16d28ada37a1d59ee565d41
ms.sourcegitcommit: 5fdf013fe05b65517b56245e1807875d80be6e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2018
ms.locfileid: "39489372"
---
# <a name="requirements-for-azure-information-protection"></a>Requirements for Azure Information Protection (Requisitos de Azure Information Protection)

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Antes de implementar Azure Information Protection para su organización, asegúrese de que tiene los siguientes requisitos previos. 

## <a name="subscription-for-azure-information-protection"></a>Suscripción a Azure Information Protection

**Para clasificación, etiquetado y protección**: debe tener un [plan de Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection/). 

**Solo para protección**: debe tener un [plan de Office 365 que incluya Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

Para asegurarse de que la suscripción de la organización incluya las características de Azure Information Protection que quiera usar, revise la lista de características en la página [Precios de Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection).

> [!TIP]
> ¿Quiere saber si su plan de Office 365 o su plan independiente de Exchange Online son compatibles con las [nuevas funcionalidades del cifrado de mensajes de Office 365](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) que permiten enviar correos electrónicos protegidos a direcciones de correo electrónico personales? Por ejemplo, Gmail, Yahoo y Microsoft. Consulte los siguientes recursos:
>
> [Exchange Online Service Description](https://technet.microsoft.com/library/exchange-online-service-description.aspx) (Descripción del servicio Exchange Online)
>
> [Office 365 Educación](https://technet.microsoft.com/library/mt844095.aspx)
>
> [Office 365 Gobierno de EE. UU.](https://technet.microsoft.com/library/mt774581.aspx)

Si tiene alguna pregunta sobre las suscripciones o licencias, no las publique en esta página. En su lugar, póngase en contacto con el administrador de cuentas de Microsoft o con [Soporte técnico de Microsoft](information-support.md#to-contact-microsoft-support).

## <a name="azure-active-directory"></a>Azure Active Directory

Su organización debe tener un directorio de Azure Active Directory (Azure AD) para admitir la autenticación y autorización de usuario para Azure Information Protection. Además, si desea usar sus cuentas de usuario desde su directorio local (AD DS), también deberá configurar la integración de directorios.

Como Azure Information Protection admite el inicio de sesión único (SSO), ya no se solicita repetidamente a los usuarios sus credenciales. Si utiliza otra solución de proveedor para la federación, consulte con ese proveedor cómo configurarlo para Azure AD. WS-Trust es un requisito común para que estas soluciones admitan el inicio de sesión único. 

Multi-Factor Authentication (MFA) es compatible con Azure Information Protection si tiene el software cliente necesario y la infraestructura de MFA configurada correctamente.

El acceso condicional es compatible con la vista previa de documentos protegidos con Azure Information Protection. Para obtener más información, consulte este artículo de preguntas más frecuentes: [Veo que Azure Information Protection aparece como una aplicación en la nube disponible para el acceso condicional. ¿Cómo funciona?](faqs.md#i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work).

Para obtener más información sobre los requisitos de autenticación, consulte [Requisitos de Azure Active Directory para Azure Information Protection](requirements-azure-ad.md). 

Para más información acerca de los requisitos de usuario y cuentas de grupo para la autorización, consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

## <a name="client-devices"></a>Dispositivos cliente

Los usuarios deben tener dispositivos cliente (equipo o dispositivo móvil) que ejecuten un sistema operativo compatible con Azure Information Protection.

Los siguientes dispositivos admiten el cliente de Azure Information Protection, que permite a los usuarios clasificar y etiquetar correos electrónicos y documentos:

- Windows 10 (x86 y x64)
    
    - No hay compatibilidad para la escritura a mano en la versión de Windows 10 RS4 para Insiders. 

- Windows 8.1 (x86 y x64)

- Windows 8 (x86 y x64)

- Windows 7 Service Pack 1 (x86 y x64)

- Windows Server 2016 

- Windows Server 2012 R2 y Windows Server 2012

- Windows Server 2008 R2 

En estas versiones de servidor, el cliente de Azure Information Protection es compatible con los Servicios de Escritorio remoto. Si elimina perfiles de usuario al utilizar el cliente de Azure Information Protection con los Servicios de Escritorio remoto, no elimine la carpeta **%Appdata%\Microsoft\Protect**.

Cuando el cliente de Azure Information Protection protege los datos mediante el servicio Azure Rights Management, pueden consumirlos los [mismos dispositivos](requirements-client-devices.md) que son compatibles con el servicio Azure Rights Management.

El cliente de Azure Information Protection tiene [requisitos previos adicionales](./rms-client/client-admin-guide-install.md#additional-prerequisites-for-the-azure-information-protection-client) que figuran en la guía del administrador.

## <a name="applications"></a>Aplicaciones

El cliente de Azure Information Protection puede etiquetar y proteger documentos y correos electrónicos mediante las aplicaciones de Office **Word**, **Excel**, **PowerPoint** y **Outlook** de cualquiera de las siguientes ediciones de Office:

- Office 365 ProPlus con aplicaciones de 2016 o 2013 (hacer clic y ejecutar o instalación basada en Windows Installer)
    
    Estas ediciones de Office se incluyen con la mayoría (aunque no todas) de las suscripciones de Office 365 que incluyen la protección de datos de Azure Information Protection. Consulte la información de su suscripción para comprobar si se incluye Office 365 ProPlus. También encontrará esta información en la [hoja de datos de Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf).

- Office Professional Plus 2016

- Office Professional Plus 2013 con Service Pack 1

- Office Professional Plus 2010 con Service Pack 2

Las demás ediciones de Office no pueden proteger los documentos y correos electrónicos mediante un servicio de Rights Management. En estas ediciones, Azure Information Protection solo admite la clasificación. Por lo tanto, las etiquetas que aplican la protección no se muestran a los usuarios en la barra de Azure Information Protection o en el botón **Proteger** de la cinta de opciones de Office. 

El cliente de Azure Information Protection no admite varias versiones de Office en el mismo equipo. Asimismo, el cliente tampoco permite cambiar cuentas de usuario en Office.

Para obtener información sobre las ediciones de Office que son compatibles con el servicio de protección de datos, vea [Aplicaciones compatibles con la protección de datos de Azure Rights Management](requirements-applications.md).

## <a name="firewalls-and-network-infrastructure"></a>Firewalls e infraestructura de red

Si tiene un firewall o dispositivos de red de intervención similares que estén configurados para permitir conexiones específicas, vea la información de **Azure Rights Management (RMS)** en la sección [Portal de Office 365 e infraestructura compartida](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US#bkmk_portal-identity) del siguiente artículo de Office: [URL de Office 365 e intervalos de direcciones IP](https://support.office.com/en-US/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Siga las instrucciones de este artículo de Office para suscribirse a una fuente RSS y mantenerse así al día de los cambios que se hagan en esta información.

Además de la información del artículo de Office específica de Azure Information Protection:

- Permita tráfico HTTPS en TCP 443 a **api.informationprotection.azure.com**.

- Permitir tráfico HTTPS en TCP 443 a **mobile.pipe.aria.microsoft.com**.

- Si usa un proxy web que precisa de autenticación, debe configurarlo para usar la autenticación integrada de Windows con las credenciales de inicio de sesión de Active Directory del usuario.

- No termine las conexiones TLS de cliente a servicio (por ejemplo, para realizar una inspección de los paquetes) establecidas con el servicio Azure Rights Management. Al hacerlo, se interrumpe la asignación de certificados que los clientes de RMS utilizan con las entidades de certificación administradas por Microsoft para ayudar a proteger su comunicación con el servicio Azure Rights Management.
    
    - Sugerencia: Debido a cómo Chrome muestra las conexiones seguras en la barra de direcciones, puede utilizar este explorador para comprobar rápidamente si la conexión de cliente se ha cancelado antes de que llegue al servicio Azure Rights Management. Escriba la dirección URL siguiente en la barra de direcciones del explorador: `https://admin.na.aadrm.com/admin/admin.svc` 
    
        No se preocupe por lo que muestra la ventana del explorador. En su lugar, haga clic en el candado de la barra de direcciones para ver la información del sitio. La información del sitio le permite ver la entidad de certificación emisora. Si el certificado no lo emite una entidad de certificación de Microsoft, es muy probable que la conexión segura de cliente a servicio finalice y tenga que volver a configurarla en el firewall. La imagen siguiente muestra un ejemplo de una entidad de certificación emisora de Microsoft. Si ve que una entidad de certificación interna ha emitido el certificado, esta configuración no es compatible con Azure Information Protection.
        
        ![Comprobación del certificado emitido para las conexiones de Azure Information Protection](./media/certificate-checking.png)

### <a name="on-premises-servers"></a>Servidores locales

Si quiere usar el servicio Azure Rights Management de Azure Information Protection con servidores locales, los siguientes productos son compatibles:

- Exchange Server

- Servidor de SharePoint

- Servidores de archivos de Windows Server que son compatibles con la Infraestructura de la clasificación de archivos

Para más información sobre los requisitos adicionales para este escenario, vea [Requisitos de Azure RMS: Servidores locales que son compatibles con Azure RMS](requirements-servers.md).

### <a name="coexistence-of-ad-rms-with-azure-rms"></a>Coexistencia de AD RMS y Azure RMS

El siguiente escenario de implementación no se admite a no ser que esté usando AD RMS para la [protección HYOK](configure-adrms-restrictions.md) con Azure Information Protection (la configuración "conserve su propia clave"):

- Ejecución de AD RMS y Azure RMS en paralelo en la misma organización, salvo durante la migración, tal como se describe en [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).

Existe una ruta de acceso de migración que se admite [desde AD RMS a Azure Information Protection](http://technet.microsoft.com/library/Dn858447.aspx) y desde [Azure Information Protection a AD RMS](/powershell/module/aadrm/Set-AadrmMigrationUrl). Si implementa Azure Information Protection y después decide que ya no quiere usar este servicio en la nube, vea [Retirada y desactivación de Azure Information Protection](decommission-deactivate.md).




