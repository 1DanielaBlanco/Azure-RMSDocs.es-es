---
# required metadata

title: Habilitar la notificación de correo electrónico | Azure RMS
description: Las notificaciones de correo electrónico avisan al propietario de contenido protegido si alguien tiene acceso a su contenido.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---
** El contenido de este SDK no es actual. Durante un breve periodo podrá encontrar la [versión actual](https://msdn.microsoft.com/library/windows/desktop/hh535290(v=vs.85).aspx) de la documentación en MSDN. **
# Habilitar la notificación de correo electrónico

Las notificaciones de correo electrónico avisan al propietario de contenido protegido si alguien tiene acceso a su contenido.

Para configurar las notificaciones de correo electrónico de una licencia determinada, use [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty) con el parámetro de tipo de propiedad, *dwPropID*, como [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA) y los campos de datos de la aplicación con formato [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list).

## C++

    ...
    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {&quot;MS.Conetent.Name&quot;, 0, &quot;FinancialReport.docx&quot;};
    propertyValuePairs[1] = {&quot;MS.Notify.Enabled&quot;,0 , &quot;true&quot;};
    propertyValuePairs[2] = {&quot;MS.Notify.Culture&quot;,0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);
    ...    

La siguiente tabla contiene los campos de datos de la aplicación y los pares de nombre y valor de propiedad correspondientes a la notificación de correo electrónico de RMS.


|Nombre de la propiedad | Tipo de datos | Valor de ejemplo | Notas |
|--------------|-----------|---------------|-------|
|MS.Content.Name|cadena|“FinancialReport.docx”|Se trata de un identificador asociado con el contenido protegido.<br><br> Para archivos protegidos, este valor debe ser el nombre del archivo sin información de ruta de acceso.<br><br> Para otros tipos de contenido, como un mensaje de correo electrónico, podría ser el asunto del correo electrónico o podría estar vacío.|
|MS.Notify.Enabled|cadena|“true” &#124; “false”|Si este valor se establece en “true”, el propietario de la licencia de publicación recibirá una notificación de correo electrónico cuando un usuario intente usarla para obtener una licencia de usuario final.|
|MS.Notify.Culture|cadena|“en-US”| **Origen:** System.Globalization.CultureInfo.CurrentUICulture.Name <br><br>Este valor se usa para determinar el idioma del correo electrónico de notificación, así como el formato de fecha, hora y número que debe usarse en el mensaje de correo electrónico.<br><br>Debe establecerse en función de la configuración establecida por el usuario de la máquina en la que se crea la licencia de publicación o en función de la referencia cultural preferida del propietario de la licencia de publicación.|
|MS.Notify.TZID|cadena|“Pacific Standard Time”|**Origen:** TimeZoneInfo.Local.Id - Identificador de zona horaria de Windows.<br><br>Este valor es el identificador de zona horaria del sistema operativo Microsoft Windows que describe una zona horaria determinada y sus características.|
|MS.Notify.TZO|cadena|“-480”|Se trata del desplazamiento de zona horaria del propietario de la licencia de publicación expresado minutos y con respecto a la hora UTC.<br><br>Si se proporciona un valor válido de TZID, se usará el desplazamiento de la zona horaria especificada por él y se omitirá este valor.<br><br>Este valor será el que con toda probabilidad usen aquellas plataformas de publicación que no estén basadas en Windows y que, por tanto, no tengan acceso a la lista de valores de identificador de zona horaria del sistema operativo Windows.<br><br>Si no se proporciona un valor TZID, se usará este valor para calcular el desplazamiento horario de los mensajes de notificación, mientras que el TZSN se usará (independientemente del valor de zona horaria) para indicar el nombre de la zona horaria. Esto provocará que la zona horaria sea fija y no se actualice con el horario de verano.<br><br>Por ejemplo:<br><br>Si TXID está en blanco, TZ0 se configura en “-420” y el valor de TZSN se establece en “Pacific Daylight Time”, entonces todos los valores mostrados en el correo electrónico de notificación se ajustarán a esa zona horaria y se mostrarán aunque el horario de verano ya no esté en vigor.<br><br>Por otra parte, si se proporciona un valor de TZID junto con TZSN y TZDN, las horas especificadas en el correo electrónico de notificación se ajustarán y se mostrarán en función de si la fecha y hora deben mostrarse en modo de verano o en modo estándar.|
|MS.Notify.TZSN|cadena|“Pacific Standard Time”|**Origen:** TimeZoneInfo.Local.StandardName - Nombre de la zona horaria estándar.<br><br>Este debe el nombre localizado de la zona horaria estándar.|
|MS.Notify.TZDN|cadena|“Pacific Daylight Time”|**Origen:** TimeZoneInfo.Local.DaylightName - Nombre de la zona horaria del horario de verano.<br><br>Este debe ser el nombre localizado del horario de verano de la zona horaria. Puede ser el mismo que el nombre estándar si la zona horaria no admite horario de verano.|

## Temas relacionados

* [**IpcSetLicenseProperty**](/rights-management/sdk/2.1/api/win/functions#msipc_ipcsetlicenseproperty)
* [**IPC\_LI\_APP\_SPECIFIC\_DATA**](/rights-management/sdk/2.1/api/win/License%20property%20types#msipc_license_property_types_IPC_LI_APP_SPECIFIC_DATA)
* [**IPC\_NAME\_VALUE\_LIST**](/rights-management/sdk/2.1/api/win/structures#msipc_ipc_name_value_list)
 

 


<!--HONumber=Jun16_HO1-->


