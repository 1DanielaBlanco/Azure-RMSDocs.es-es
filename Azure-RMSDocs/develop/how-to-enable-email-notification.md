---
title: "Habilitar la notificación de correo electrónico | Azure RMS"
description: "Las notificaciones de correo electrónico avisan al propietario de contenido protegido si alguien tiene acceso a su contenido."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5FB975EE-E4E5-4089-B8E1-CAFD5B9B34EC
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 1b9428a79b5c9df76d2b5f7ec1e358be09f0bf7f
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
# <a name="how-to-enable-email-notification"></a>Habilitación de la notificación por correo electrónico

Las notificaciones de correo electrónico avisan al propietario de contenido protegido si alguien tiene acceso a su contenido.

Para configurar las notificaciones de correo electrónico de una licencia determinada, use [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx) con el parámetro de tipo de propiedad, *dwPropID*, como [IPC\_LI\_APP\_SPECIFIC\_DATA](https://msdn.microsoft.com/library/hh535287.aspx) y los campos de datos de la aplicación con formato [IPC\_NAME\_VALUE\_LIST](https://msdn.microsoft.com/library/hh535277.aspx).

    C++

    int numDataPairs = 3;

    IPC_NAME_VALUE propertyValuePairs [numDataPairs];

    // lcid field set to 0 causes the default lcid to be used

    propertyValuePairs[0] = {"MS.Conetent.Name", 0, "FinancialReport.docx"};
    propertyValuePairs[1] = {"MS.Notify.Enabled",0 , "true"};
    propertyValuePairs[2] = {"MS.Notify.Culture",0 , “en-US”};

    IPC_NAME_VALUE_LIST emailNotificationAppData = {numDataPairs, propertyValuePairs};

    result = IpcSetLicenseProperty( licenseHandle, FALSE, IPC_LI_APP_SPECIFIC_DATA, emailNotificationAppData);


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

## <a name="related-topics"></a>Temas relacionados

- [IpcSetLicenseProperty](https://msdn.microsoft.com/library/hh535271.aspx)
- [IPC\_LI\_APP\_SPECIFIC\_DATA](https://msdn.microsoft.com/library/hh535287.aspx)
- [IPC\_NAME\_VALUE\_LIST](https://msdn.microsoft.com/library/hh535277.aspx).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]