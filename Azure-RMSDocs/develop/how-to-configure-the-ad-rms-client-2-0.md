---
# required metadata

title: Configurar el cliente | Azure RMS
description: Instrucciones sobre cómo configurar Active Directory Rights Management Services Client 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 74C342BF-0F79-486D-AED7-C53230DE5FA7
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
# Configuración del cliente

Este tema contiene instrucciones sobre cómo configurar Active Directory Rights Management Services Client 2.1.

**Importante**  Si va a probar la aplicación en el entorno 1-box RMS ISV, no necesitará configurar AD RMS Client 2.1. Para más información, vea [Probar aplicaciones con derechos habilitados](running-your-first-application.md).

 

### Requisitos previos

-   Debe tener AD RMS Client 2.1 instalado en el equipo en el que va a probar la aplicación.

    -   Si va a probar la aplicación en el equipo de desarrollo, necesita tener instalado Rights Management Services SDK 2.1. A estas alturas, AD RMS Client 2.1 ya se habrá instalado en modo silencioso.

        Para más información sobre cómo instalar RMS SDK 2.1, vea [Instalar el SDK](create-your-first-rights-aware-application.md).

    -   Si va a probar la aplicación en un equipo que no sea el equipo de desarrollo, puede instalar AD RMS Client 2.1 en ese equipo desde la [página de descarga de AD RMS Client 2.1](http://www.microsoft.com/en-us/download/details.aspx?id=38396).
        **Nota:** Si la aplicación usa el modo de API de servidor (**IPC\_API\_MODE\_SERVER**), el manifiesto de aplicación no será necesario. Podrá probar la aplicación en un servidor RMS de producción y no será necesario obtener una licencia de producción cuando pase al entorno de producción. Para más información sobre las aplicaciones de modo de servidor, vea [Application types](application-types.md) (Tipos de aplicación).

         

-   Para poder trabajar en el entorno de producción, es necesario tener instalado y configurado un servidor RMS. Para más información, vea [Instalar y configurar el servidor](how-to-install-and-configure-an-rms-server.md).

Instrucciones

### Paso 1: Cómo configurar RMS Client 2.1 para la jerarquía de certificados de preproducción

Los pasos siguientes explica cómo instalar el runtime del desarrollador, cómo configurar el cliente para usar la jerarquía de certificados (preproducción) de ISV y cómo configurar la detección de servicios en el cliente.

1.  Copie Developer Runtime, Ipcsecproc\_isv.dll, desde %MSIPCSDKDIR%\\bin\\x86 (para versiones de Windows de 32 bits) o %MSIPCSDKDIR\\bin\\x64 (para versiones de Windows de 64 bits) en C:\\Archivos de programa\\Active Directory Rights Management Services Client 2.1.

    **Importante**: Si ejecuta una aplicación de 32 bits en una versión de Windows de 64 bits, deberá copiar Ipcsecproc\_isv.dll desde %MSIPCSDKDIR%\\bin\\x86 en C:\\Archivos de programa(x86)\\Active Directory Rights Management Services Client 2.1.

     

2.  Configure AD RMS Client 2.1 para que use la jerarquía de certificados (preproducción) de ISV. Para ello, establezca en 1 el valor de clave del registro **Hierarchy**.

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **Nota**  No tener el valor **Hierarchy** presente en el registro es, desde el punto de vista funcional, lo mismo que tener su valor establecido en 0 (cero), lo que significa que RMS SDK 2.1 funcionará en modo de producción. Para más información sobre las claves y las cadenas de certificados, vea [Descripción de cadenas de certificados](understanding-certificate-chains.md).

    **Importante**  
    Si está ejecutando una aplicación de 32 bits en una versión de Windows de 64 bits, establezca el valor de **Hierarchy** en la ubicación de claves siguiente:

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  Configurar la detección del lado servidor o del lado cliente para permitir que AD RMS Client 2.1 pueda detectar y establecer comunicación con el servidor RMS de preproducción.

    -   En la detección del lado servidor, un administrador registra un punto de conexión de servicio (SCP) para el clúster raíz de RMS de preproducción con Active Directory, y el cliente consulta a Active Directory para descubrir el SCP y establecer una conexión con el servidor.
    -   En la detección del lado cliente, la detección de servicios de RMS se configura en el registro del equipo donde se ejecuta AD RMS Client 2.1. En esta configuración, AD RMS Client 2.1 apunta al servidor RMS que se va a usar. Cuando están presentes, no se realiza la detección del lado servidor.

    Para configurar la detección del lado cliente, se pueden establecer las siguientes claves del registro de modo que apunten al servidor RMS de preproducción. Para más información sobre cómo configurar la detección del lado cliente, vea [RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx) (Notas de implementación de RMS Client 2.0).

|Key|Valor|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|(Predeterminado):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|(Predeterminado):<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Licensing**|


**Nota**   De forma predeterminada, estas claves no existen en el registro y necesitan ser creadas.
     
**Importante**  
    Si está ejecutando una aplicación de 32 bits en una versión de Windows de 64 bits, establezca estas claves en la ubicación de claves siguiente:


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### Comentarios

Las instrucciones de este tema no son exhaustivas. Para información detallada sobre cómo configurar AD RMS Client 2.1, vea [RMS Client 2.0 Deployment Notes](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx) (Notas de implementación de RMS Client 2.0).

## Temas relacionados


* [Procedimientos](how-to-use-msipc.md)
* [Notas de implementación de RMS Client 2.0](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [Instalar el SDK](create-your-first-rights-aware-application.md)
* [Instalar y configurar el servidor](how-to-install-and-configure-an-rms-server.md)
* [Probar aplicaciones con derechos habilitados](running-your-first-application.md)
* [Descripción de cadenas de certificados](understanding-certificate-chains.md)
 

 


<!--HONumber=Jun16_HO1-->


