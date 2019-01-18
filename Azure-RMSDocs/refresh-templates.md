---
title: Actualización de plantillas de Azure RMS - AIP
description: Cuando usa el servicio Azure Rights Management, se descargan de forma automática plantillas a los ordenadores cliente para que los usuarios puedan seleccionarlas desde sus aplicaciones. Sin embargo, es posible que tengas que tomar medidas adicionales si quieres efectuar cambios en las plantillas.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/12/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 8c2064f0-dd71-4ca5-9040-1740ab8876fb
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 178e191a4099e0e077a45892b3b72310a995a528
ms.sourcegitcommit: 9dc6da0fb7f96b37ed8eadd43bacd1c8a1a55af8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2019
ms.locfileid: "54394004"
---
# <a name="refreshing-templates-for-users-and-services"></a>Actualización de plantillas para usuarios y servicios

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Cuando usa el servicio Azure Rights Management de Azure Information Protection, se descargan de forma automática plantillas a los ordenadores cliente para que los usuarios puedan seleccionarlas desde sus aplicaciones. Sin embargo, es posible que tengas que tomar medidas adicionales si quieres efectuar cambios en las plantillas:

|Aplicación o servicio|Cómo se actualizan las plantillas tras los cambios|
|--------------------------|---------------------------------------------|
|Exchange Online<br /><br />Se aplica a reglas de transporte y Outlook Web App |Se actualiza automáticamente en una hora, no hay que seguir más pasos.<br /><br />Este es el caso si usa el [cifrado de mensajes de Office 365 con nuevas capacidades](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Si previamente ha configurado Exchange Online para que use el servicio Azure Rights Management y, para ello, ha importado su dominio de publicación de confianza (TPD), use el mismo conjunto de instrucciones para habilitar las nuevas capacidades de Exchange Online.|
|Cliente de Azure Information Protection|Se actualiza automáticamente cada vez que la directiva de Azure Information Protection se actualiza en el cliente:<br /><br /> - Cuando se abre una aplicación de Office que admite la barra de Azure Information Protection. <br /><br /> - Cuando hace clic con el botón derecho para clasificar y proteger un archivo o carpeta. <br /><br /> - Cuando ejecuta cmdlets de PowerShell para etiquetado y protección (Get-AIPFileStatus y Set-AIPFileLabel).<br /><br /> - Cuando se inicia el servicio del analizador de Azure Information Protection y la directiva local es anterior a una hora. Además, el servicio del analizador comprueba los cambios cada hora y los utiliza para el próximo ciclo de examen.<br /><br /> - Cada 24 horas.<br /><br /> Además, dado que este cliente está estrechamente integrado con Office, cualquier plantillas actualizada para Office 2016 u Office 2013 también se actualizará para el cliente de Azure Information Protection.|
|Cliente de etiquetado unificado de Azure Information Protection (versión preliminar)|Se actualiza automáticamente cada cuatro horas, por aplicación de Office.<br /><br /> Además, dado que el cliente de Azure Information Protection está estrechamente integrado con Office, cualquier plantillas actualizada para Office 2016 u Office 2013 también se actualizará para el cliente de etiquetado unificado de Azure Information Protection.|
|Office 2016 y Office 2013<br /><br />Aplicaciones de uso compartido de RMS para Windows|Actualización automática: programada:<br /><br />- Para estas versiones posteriores de Office: el intervalo de actualización predeterminado es cada 7 días.<br /><br />- Para la aplicación de uso compartido de RMS para Windows: a partir de la versión 1.0.1784.0, el intervalo de actualización predeterminado es cada día. Las versiones anteriores tienen un intervalo de actualización predeterminado de 7 días.<br /><br />Para exigir una actualización antes de esta programación, vea la sección [Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado](#office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template).|
|Office 2010|Se actualiza automáticamente cuando los usuarios cierran la sesión de Windows, vuelven a iniciarla y esperan hasta 1 hora.|
|Exchange local con el conector Rights Management<br /><br />Se aplica a reglas de transporte y Outlook Web App|Actualización automática: no se requieren pasos adicionales. Pero Outlook Web App almacena en caché la interfaz de usuario durante un día.|
|Office 2016 para Mac|Actualización automática: no se requieren pasos adicionales.|
|Aplicación RMS sharing para equipos Mac|Actualización automática: no se requieren pasos adicionales.|
|Aplicaciones de Office que [admiten la característica de sensibilidad](https://support.office.com/article/apply-sensitivity-labels-to-your-documents-and-email-within-office-2f96e7cd-d5a4-403b-8bd7-4cc636bae0f9?ad=US&ui=en-US&rs=en-US#bkmk_whereavailable)|Estos clientes no descargan plantillas, sino que acceden a ellas en línea. No se requieren pasos adicionales.|

Cuando las aplicaciones cliente deben descargar plantillas (inicialmente o con actualización para los cambios), prepárese para esperar hasta 15 minutos antes de que se complete la descarga y que las plantillas nuevas o actualizadas estén completamente operativas. El tiempo real dependerá de factores como el tamaño y la complejidad de la configuración de la plantilla y la conectividad de red. 

## <a name="office-2016--office-2013-and-rms-sharing-application-for-windows-how-to-force-a-refresh-for-a-changed-custom-template"></a>Office 2016, Office 2013 y la aplicación RMS sharing para Windows: Cómo forzar una actualización de una plantilla personalizada que se ha cambiado
Si modifica el Registro de los equipos que ejecutan Office 2016, Office 2013 o la aplicación Rights Management (RMS) sharing, puede cambiar la programación automática para que las plantillas cambiadas se actualicen en los equipos con más frecuencia que la indicada en sus valores predeterminados. También puede forzar una actualización inmediata eliminando los datos existentes en un valor del Registro.

> [!WARNING]
> Si usas el Editor del Registro de forma incorrecta, es posible que ocasiones problemas serios que puedan hacer preciso que reinstales el sistema operativo. Microsoft no puede garantizar que pueda resolver problemas ocasionados por un uso incorrecto del Editor del Registro. Usa el Editor del Registro bajo tu propia responsabilidad.

### <a name="to-change-the-automatic-schedule"></a>Para cambiar la programación automática

1.  Con un editor del Registro, cree y establezca uno de los valores del Registro siguientes:

    - Para establecer una frecuencia de actualización en días (mínimo de 1 día):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequency** y defina un valor entero para los datos, que especificará la frecuencia en días para descargar los cambios en una plantilla descargada. Use la información siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        **Ruta de acceso del Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valor:** TemplateUpdateFrequency

    - Para establecer una frecuencia de actualización en segundos (mínimo de 1 segundo):  cree un nuevo valor del Registro denominado **TemplateUpdateFrequencyInSeconds** y defina un valor entero para los datos, que especificará la frecuencia en segundos para descargar los cambios en una plantilla descargada. Use la información siguiente para localizar la ruta de acceso del Registro y crear este nuevo valor del Registro.

        **Ruta de acceso del Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC

        **Tipo:** REG_DWORD

        **Valor:** TemplateUpdateFrequencyInSeconds

    Asegúrese de crear y establecer uno de estos valores del Registro, no ambos. Si ambos están presentes, **TemplateUpdateFrequency** se omite.

2.  Si desea forzar una actualización inmediata de las plantillas, vaya al procedimiento siguiente. En caso contrario, reinicie ahora las aplicaciones de Office y las instancias del Explorador de archivos.

### <a name="to-force-an-immediate-refresh"></a>Para forzar una actualización inmediata

1. Con un editor del Registro, elimine los datos del valor **LastUpdatedTime** . Por ejemplo, en los datos puede aparecer **2015-04-20T15:52**. Elimine 2015-04-20T15:52 para que no se muestre ningún dato. Use la información siguiente para localizar la ruta de acceso del Registro y eliminar estos datos del valor del Registro.

   **Ruta de acceso del Registro:** HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\\<*MicrosoftRMS_FQDN*>\Template\\<*user_alias*>

   **Tipo:** REG_SZ

   **Valor:** LastUpdatedTime

   > [!TIP]
   > En la ruta de acceso del Registro, <*MicrosoftRMS_FQDN*> hace referencia al FQDN de servicio de Microsoft RMS. Si desea comprobar este valor:
   > 
   > Ejecute el cmdlet [Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) para Azure RMS. Si aún no ha instalado el módulo de Windows PowerShell para Azure RMS, vea [Instalación del módulo de PowerShell para AADRM](install-powershell.md).
   > 
   > En la salida, identifique el valor **LicensingIntranetDistributionPointUrl** .
   > 
   > Por ejemplo: **LicensingIntranetDistributionPointUrl   : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing**
   > 
   > En el valor, quite **https://** y **/_wmcs/licensing** de esta cadena. El valor restante es el FQDN de servicio de Microsoft RMS. En nuestro ejemplo, el FQDN de servicio de Microsoft RMS sería el valor siguiente:
   > 
   > **5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com**

2. Elimine la carpeta siguiente y todos los archivos que contenga: **%localappdata%\Microsoft\MSIPC\Templates**

3. Reinicie las aplicaciones de Office y las instancias del Explorador de archivos.


## <a name="see-also"></a>Consulte también
[Configuración y administración de plantillas en la directiva de Azure Information Protection](configure-policy-templates.md)

