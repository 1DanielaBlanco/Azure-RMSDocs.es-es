---
# required metadata

title: Firma de la aplicación para producción | Azure RMS
description: Este tema le guiará por el proceso de firma de la aplicación para el modo de producción.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 09BA148C-7D1E-43C8-92EA-24BBB6EFDB19
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
# Firma de la aplicación para producción

Este tema le guiará por el proceso de firma de la aplicación para el modo de producción.

## Firma de la aplicación con derechos habilitados

En este procedimiento se supone que ya firmó la aplicación para una jerarquía de preproducción. Si aún no lo ha hecho, repase el proceso descrito en [Pruebas de la aplicación con derechos habilitados](running-your-first-application.md).

Cuando haya recibido el certificado de producción de Microsoft, tendrá los siguientes archivos:

-   YourPrivateKey.dat
-   YourPublicKey.dat
-   ProductionCertificate.xml

Colóquelos en el mismo directorio con *GenManifest.exe* y el archivo binario de la aplicación (.exe).

-   El proceso siguiente le muestra cómo crear un archivo MCF con certificado de producción:

    -   Cree un directorio y coloque archivos en el nuevo directorio. Use Notepad.exe para crear un archivo MCF para la aplicación. El archivo debe tener el siguiente contenido.

        ``` syntax
        AUTO-GUID
        .\\YourPrivateKey.dat
        modulelist
        req     .\\<yourappname>.exe
        POLICYLIST
        INCLUSION
        PUBLICKEY .\\YourPublicKey.dat
        EXCLUSION
        ```

    -   Ejecute el comando siguiente para firmar la aplicación:

        **genmanifest.exe -chain ProductionCertificate.xml** *YourAppName***.mcf** *YourAppName***.exe.man**

        Si Genmanifest se ejecutó correctamente, solo verá el texto siguiente:

        Si Genmanifest no se ejecutó, verá un mensaje de error.

    -   *YourAppName*. exe.man siempre se debe colocar en el mismo directorio que *YourAppName*.exe.

## Temas relacionados

* [Procedimiento](how-to-use-msipc.md)
* [Prueba de la aplicación con derechos habilitados](running-your-first-application.md)
 

 





<!--HONumber=Jun16_HO1-->


