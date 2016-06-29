---
# required metadata

title: Procedimiento para&#58; habilitar el registro de rendimiento y errores | Azure RMS
description: El SDK 4.2 de Microsoft Rights Management administra la carga de registro de rendimiento y diagnóstico mediante una única propiedad de dispositivo.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: F5AD3826-2292-4A25-AF5C-D17D083F5742
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Procedimiento para habilitar el registro de rendimiento y errores
El SDK 4.2 de Microsoft Rights Management administra la carga de registro de rendimiento y diagnóstico mediante una única propiedad de dispositivo.

## Información general ##
Puede mejorar la experiencia de los usuarios y la solución de problemas mediante la habilitación de la carga de registro de rendimiento y diagnóstico en Microsoft. Para mantener la privacidad de los usuarios, los desarrolladores de aplicaciones deben pedir al usuario que den su consentimiento antes de habilitar el registro automático.

Administrará el control de diagnóstico mediante dos propiedades:

-   Habilite el registro mediante la propiedad **IpcCustomerExperienceDataCollectionEnabled**. El valor se mantiene entre reinicios del dispositivo.
-   Controle el nivel de registro mediante la propiedad **IpcLogLevel** usando los siguientes valores:

    * 1: Detallado
    * 2: Informativo
    * 3: Advertencia
    * 4: Error
    * 5: Crítico

En cada uno de los fragmentos de código de ejemplo siguientes, la aplicación de llamada puede establecer o consultar la propiedad.

### Android ###
Habilitar el registro automático

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    SharedPreferences.Editor editor = preferences.edit();
    editor.putBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, true);
    editor.commit();

Obtener el valor de marca de control del registro actual

    SharedPreferences preferences = PreferenceManager.getDefaultSharedPreferences(context);
    Boolean isLogUploadEnabled = preferences.getBoolean(&quot;IpcCustomerExperienceDataCollectionEnabled&quot;, false);

## iOS ##
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
 

## Windows ##
Habilitar el registro automático

    CustomerExperienceConfiguration::Option = CustomerExperienceOptions::LoggingEnabledNow;

Para obtener más información sobre los valores de configuración opcionales, consulte [CustomerExperienceOptions](/rights-management/sdk/4.2/api/winrt/Microsoft.RightsManagement#msipcthin2_customerexperienceoptions).

Obtener el valor de marca de control del registro actual

    CustomerExperienceOptions loggingOption = CustomerExperienceConfiguration::Option;


**Nota**: Los fragmentos de código de Windows anteriores están en C++. Para C\#, actualice la sintaxis con ‘.’ en lugar de ‘::’.

**Linux/C++**: este SDK tiene algún registro básico que no es tan extensivo como el de otras plataformas. Para más información, consulte la sección de **solución de problemas** del archivo "README.md" en el [SDK de RMS para C++ Portable](https://github.com/AzureAD/rms-sdk-for-cpp#troubleshooting).

 

 


<!--HONumber=Apr16_HO4-->


