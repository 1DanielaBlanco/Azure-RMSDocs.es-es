---
title: Procedimiento para&#58; habilitar el registro de rendimiento y errores | Azure RMS
description: El SDK 4.2 de Microsoft Rights Management administra la carga de registro de rendimiento y diagnóstico mediante una única propiedad de dispositivo.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 906746990fd08a749d2879fbc04b054e49e65f01
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
ms.locfileid: "27764495"
---
# <a name="how-to-enable-error-and-performance-logging"></a>Procedimiento para habilitar el registro de rendimiento y errores
El SDK 4.2 de Microsoft Rights Management administra la carga de registro de rendimiento y diagnóstico mediante una única propiedad de dispositivo.

## <a name="overview"></a>Introducción ##
Puede mejorar la experiencia de los usuarios y la solución de problemas mediante la habilitación de la carga automática de datos de registro de diagnóstico, rendimiento y telemetría en Microsoft. 

> [!IMPORTANT] 
> Para mantener la privacidad de los usuarios, los desarrolladores de aplicaciones deben pedir al usuario que den su consentimiento antes de habilitar el registro automático.

> [!NOTE]
> Como ejemplo, se muestra a continuación un mensaje estándar de Microsoft que se utiliza para la notificación de registro: 
>
> *Al activar el Registro de errores y rendimiento, acepta enviar datos de errores y rendimiento a Microsoft.  Microsoft recopila datos de errores y rendimiento a través de Internet («Datos»).  Microsoft usa estos datos para proporcionar y mejorar la calidad, la seguridad y la integridad de los productos y servicios de Microsoft.  Por ejemplo, analizamos el rendimiento y la confiabilidad, como qué características usa, la rapidez con que responden las características, el rendimiento del dispositivo, las interacciones con la interfaz de usuario y los problemas que tenga con el producto.  Los datos también incluyen información sobre la configuración del software, como el software que ejecuta actualmente y la dirección IP.*  

Administrará el control de diagnóstico mediante dos propiedades:

-   Habilite el registro mediante la propiedad **IpcCustomerExperienceDataCollectionEnabled**. El valor se mantiene entre reinicios del dispositivo.
-   Controle el nivel de registro mediante la propiedad **IpcLogLevel** usando los siguientes valores:

    * 1: Detallado
    * 2: Informativo
    * 3: Advertencia
    * 4: Error
    * 5: Crítico

En cada uno de los fragmentos de código de ejemplo siguientes, la aplicación de llamada puede establecer o consultar la propiedad.

### <a name="android"></a>Android ###
Habilitar el registro automático

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obtener el valor de marca de control del registro actual

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## <a name="ios"></a>iOS ##
Habilitar el registro automático

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
        [prefs setBool:FALSE forKey:@&quot;IpcCustomerExperienceDataCollectionEnabled”];
        [[NSUserDefaults standardUserDefaults] synchronize];

Obtener el valor de marca de control del registro actual

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcCustomerExperienceDataCollectionEnabled&quot;];

Establecer el control de nivel de registro

    NSUserDefaults \*prefs = [NSUserDefaults standardUserDefaults];
      [prefs setInteger:1 forKey:@&quot;IpcLogLevel”];
      [[NSUserDefaults standardUserDefaults] synchronize];

Obtener el valor de control de nivel de registro

    [[NSUserDefaults standardUserDefaults] boolForKey:@&quot;IpcLogLevel&quot;];
 

## <a name="windows"></a>Windows ##
Habilitar el registro automático

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Para obtener más información sobre los valores de configuración opcionales, consulte [CustomerExperienceOptions](https://msdn.microsoft.com/library/microsoft.rightsmanagement.customerexperienceoptions.aspx).

Obtener el valor de marca de control del registro actual

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Nota**: Los fragmentos de código de Windows anteriores están en C++. Para C\#, actualice la sintaxis con ‘.’ en lugar de ‘::’.

**Linux/C++**: este SDK tiene algún registro básico que no es tan extensivo como el de otras plataformas. Para más información, consulte la sección de **solución de problemas** del archivo "README.md" en el [SDK de RMS para C++ Portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]