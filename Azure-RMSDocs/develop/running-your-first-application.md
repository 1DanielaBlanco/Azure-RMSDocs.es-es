---
# required metadata

title: Probar la aplicación con derechos habilitados | Azure RMS
description: Se describen los pasos necesarios para probar la aplicación con derechos habilitados de RMS SDK 2.1.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 834B7242-31D3-4275-A892-CFE95A61E29E
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
# Prueba de la aplicación con derechos habilitados

En este tema se describen los pasos necesarios para probar la aplicación con derechos habilitados de Rights Management Services SDK 2.1.

Para publicar y consumir contenido protegido, una aplicación de Rights Management Services (RMS) usa distintos tipos de certificados y licencias, cada uno de los cuales consta de una cadena de certificados que lleva en última instancia a una entidad de certificación de Microsoft. Microsoft proporciona las siguientes jerarquías:

-   La jerarquía de preproducción se puede usar para desarrollar y probar aplicaciones.
-   La jerarquía de producción se debe usar en aplicaciones publicadas.

Se recomienda usar la jerarquía de preproducción al desarrollar una aplicación. Al hacerlo, podrá trabajar sin tener que firmar un contrato de licencia de producción con Microsoft.

> [!IMPORTANT]
> Este es un procedimiento recomendado para probar primero la aplicación de RMS SDK 2.1 en el entorno de preproducción de RMS, en un servidor RMS. Luego, si quiere que su cliente tenga la posibilidad de usar la aplicación con el servicio de Azure RMS, pase a las pruebas con ese entorno. Para más información, consulte [Enable your service application to work with cloud based RMS](how-to-use-file-api-with-aadrm-cloud.md) (Permitir que la aplicación de servicio funcione con RMS en la nube).

 

### Requisitos previos

-   Una configuración de entorno de desarrollo de RMS SDK 2.1. Para más información, vea [Setting up the pre-production development environment](how-to-set-up-the-pre-production-development-environment.md) (Configuración del entorno de desarrollo de preproducción).
-   Para ver una aplicación de ejemplo, vea [IPCHelloWorld - an example application](how-to-build-your-first-application.md) (IPCHelloWorld: una aplicación de ejemplo).

Instrucciones

### Paso 1:

Cree y compile una aplicación con derechos habilitados. Consulte la sección de requisitos previos anterior para conocer las opciones.

### Paso 2: Generar un manifiesto de aplicación mediante la cadena de certificados de preproducción

Para poder ejecutar la aplicación, debe generar un manifiesto de aplicación.

**Nota:** Si la aplicación usa el modo de API de servidor (**IPC\_API\_MODE\_SERVER**), el manifiesto de aplicación no será necesario. Podrá probar la aplicación en un servidor de AD RMS de producción y no será necesario obtener una licencia de producción cuando pase al entorno de producción. Para más información sobre las aplicaciones de modo de servidor, vea [Application types](application-types.md) (Tipos de aplicación).

 

Este proceso también se conoce como firmar la aplicación. Puede generar el manifiesto mediante una cadena de certificados de producción o con la cadena de certificados de preproducción que se instala con el SDK. Se recomienda usar la cadena de certificados de preproducción durante el desarrollo.

Para más información sobre las claves y las cadenas de certificados, vea [Understanding certificate chains](understanding-certificate-chains.md) (Descripción de cadenas de certificados).

Para más información sobre cómo firmar una aplicación con una cadena de certificados de producción, vea [Switching to the production environment](switching-to-the-production-environment.md) (Cambiar al entorno de producción).

Para generar el manifiesto de aplicación con la cadena de certificados de preproducción, haga lo siguiente en el equipo de desarrollo:

1.  Copie los siguientes archivos desde sus directorios de instalación a la misma carpeta que la aplicación.

    %MSIPCSdkDir%\\Tools\\Genmanifest.exe

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningprivkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsigningpubkey.dat

    %MSIPCSdkDir%\\bin\\Isvtier5appsignsdk\_client.xml

    %MSIPCSdkDir%\\bin\\YourAppName.isv.mcf

2.  En la carpeta de la aplicación, cambie el nombre del archivo de configuración del manifiesto (YourAppName.isv.mcf) por el nombre de la aplicación con la extensión de nombre de archivo .mcf anexada. Por ejemplo, si la aplicación se llama MyApp.exe, cambie el nombre YourAppName.isv.mcf por MyApp.exe.mcf.

3.  Use un editor de texto para agregar la aplicación al archivo de configuración del manifiesto. Para ello, reemplace el texto de marcador &lt;nombreDeLaAplicación&gt;.exe en la lista de módulos del archivo .mcf por el nombre de la aplicación (por ejemplo, MyApp.exe).

    El proceso de firma generará un error si el archivo .mcf se usa sin modificarlo.

4.  Ejecute Genmanifest.exe para generar el manifiesto de aplicación. Esto también se conoce como firmar la aplicación. El resultado de esta operación debe ser un archivo .man. Por ejemplo, si la aplicación se denomina MyApp.exe y el archivo de configuración del manifiesto se denomina MyApp.exe.mcf, ejecute el siguiente comando:

    **genmanifest.exe -chain isvtier5appsignsdk\_client.xml MyApp.exe.mcf MyApp.exe.man**

### Paso 3: Ejecutar la aplicación

Puede ejecutar la aplicación desde cualquier directorio, pero el manifiesto de aplicación (MyApp.exe.man) debe estar en el mismo directorio que el archivo ejecutable (MyApp.exe).

-   **Uso del entorno de 1 cuadro de RMS**

    Si usa el entorno de 1 cuadro de RMS para probar la aplicación, copie el archivo ejecutable de la aplicación y el manifiesto de aplicación en cualquier directorio del entorno de 1 cuadro y, acto seguido, ejecute la aplicación.

    Para más información sobre el entorno de 1 cuadro de RMS, vea [Set up the test environment](how-to-set-up-your-test-environment.md) (Configurar el entorno de prueba).

-   **Uso de una configuración de servidor de preproducción**

    Si va a probar la aplicación en un servidor de RMS configurado para preproducción, asegúrese de que ha configurado Active Directory Rights Management Services Client 2.1 en el equipo donde se ejecutará la aplicación (por ejemplo, en el equipo de desarrollo). Procure también que el archivo ejecutable de la aplicación y el manifiesto de aplicación se encuentren en el mismo directorio en ese equipo y, luego, ejecute la aplicación.

    Para más información sobre cómo configurar el cliente en el equipo, vea [Configure the client](how-to-configure-the-ad-rms-client-2-0.md) (Configurar el cliente). Para más información sobre cómo instalar un servidor RMS, vea [Install and configure the server](how-to-install-and-configure-an-rms-server.md) (Instalar y configurar el servidor).

## Temas relacionados

* [How-to use (Procedimientos)](how-to-use-msipc.md)
* [Configure the client (Configurar el cliente)](how-to-configure-the-ad-rms-client-2-0.md)
* [Install and configure the server (Instalar y configurar el servidor)](how-to-install-and-configure-an-rms-server.md)
* [IPCHelloWorld - an example application (IPCHelloWorld: una aplicación de ejemplo)](how-to-build-your-first-application.md)
* [Setting up the pre-production development environment (Configuración del entorno de desarrollo de preproducción)](how-to-set-up-the-pre-production-development-environment.md)
* [Switching to the production environment (Cambiar al entorno de producción)](switching-to-the-production-environment.md)
* [Set up the test environment (Configurar el entorno de prueba)](how-to-set-up-your-test-environment.md)
* [Understanding certificate chains (Descripción de cadenas de certificados)](understanding-certificate-chains.md)
 

 





<!--HONumber=Jun16_HO1-->


