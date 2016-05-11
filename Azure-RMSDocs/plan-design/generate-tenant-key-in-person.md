---
# required metadata

title: Generar y transferir su clave de inquilino en persona | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3281e45e-cf69-4dc5-946b-3029851d3152

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Generar y transferir su clave de inquilino en persona

Use los procedimientos siguientes si ha decidido [administrar su propia clave de inquilino](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) y no quiere transferirla a través de Internet, sino que prefiere transferirla en persona.

## Generar su clave de inquilino
Para generar su propia clave de inquilino, siga estos 3 pasos:

-   [Paso 1: Preparar una estación de trabajo con HSM de Thales](#step-1-prepare-a-workstation-with-thales-hsm)

-   [Paso 2: Crear un mundo de seguridad](#step-2-create-a-security-world)

-   [Paso 3: Crear una clave nueva](#step-3-create-a-new-key)

### Paso 1: Preparar una estación de trabajo con HSM de Thales
Instale el software de soporte nCipher (Thales) en un equipo con Windows. Conecte un HSM de Thales a ese equipo. Asegúrese de que las herramientas de Thales se encuentran en su ruta de acceso. Para obtener más información, consulte la guía de usuario incluida en el HSM de Thales o visite el sitio web de Thales para Azure RMS en [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Paso 2: Crear un mundo de seguridad
Inicie un símbolo de comando y ejecute el programa del nuevo mundo de Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa crea un archivo de **mundo de seguridad** en %NFAST_KMDATA%\local\world, que corresponde a la carpeta C:\ProgramData\nCipher\Key Management Data\local. Puede usar valores diferentes para el quórum, pero en nuestro ejemplo, recibe el aviso de que tiene que escribir tres tarjetas en blanco y anclar todas ellas. A continuación, dos tarjetas cualquiera le proporcionarán acceso completo al mundo de seguridad.  Estas tarjetas convierten el **Conjunto de tarjetas del administrador** para el nuevo mundo de seguridad.

A continuación, haga lo siguiente:

1.  Instale el proveedor de CNG de Thales como se describe en la documentación de Thales y configúrelo para usar el nuevo mundo de seguridad.

2.  Haga una copia de seguridad del archivo del mundo. Asegure y proteja el archivo del mundo, las tarjetas del administrador y sus anclajes, y asegúrese de que ninguna persona tiene acceso a más de una tarjeta.

Ahora está listo para crear una clave nueva que será su clave de inquilino de RMS.

### Paso 3: Crear una clave nueva
Genere una clave de CNG mediante los programas **generatekey** y **cngimport** de Thales.

Ejecute el comando siguiente para generar la clave:

```
generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=
```
Cuando ejecute este comando, siga estas instrucciones:

-   El parámetro **protect** debe establecerse en el valor **module**, tal y como se muestra. Así se crea una clave protegida por el módulo. El conjunto de herramientas BYOK no es compatible con claves protegidas por OCS.

-   Para el tamaño de la clave, recomendamos 2048 bits, pero también admite claves RSA de 1024 bits para clientes de AD RMS existentes que tienen dichas claves y van a migrar a Azure RMS.

-   Reemplace el valor de *contosokey* para el **ident** y **plainname** con cualquier valor de cadena. Para minimizar sobrecargas administrativas y reducir el riesgo de errores, recomendamos que use el mismo valor para ambos, y que escriba todos los caracteres en minúsculas.

-   El pubexp se deja en blanco (predeterminado) en este ejemplo, pero puede determinar valores concretos. Para obtener más información, vea la documentación de Thales.

A continuación, ejecute el comando siguiente para importar la clave a CNG:

```
cngimport --import –M --key=contosokey --appname=simple contosokey
```
Cuando ejecute este comando, siga estas instrucciones:

-   Remplace *contosokey* por el mismo valor que especificó en el Paso 1.

-   Utilice la opción **-M** para que la clave sea adecuada para este escenario. Sin esto, la clave resultante será una clave específica de usuario para el usuario actual.

Este comando crea un archivo de clave acortada en la carpeta %NFAST_KMDATA%\local con un nombre que comienza con **key_caping`_`** seguido por un SID. Por ejemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este archivo contiene una clave cifrada.

Haga una copia de seguridad de este archivo de clave acortado en una ubicación segura.

> [!IMPORTANT]
> Cuando posteriormente transfiera su clave a Azure RMS, Microsoft tendrá una copia no recuperable de su clave. De este modo, nadie puede recuperar su clave de los HSM en Microsoft. Así, le permite conservar el control exclusivo sobre su clave de inquilino. Por tanto, pasa a tener mucha importancia que haga la copia de seguridad de su clave y del mundo de seguridad de forma segura. Póngase en contacto con Thales para averiguar más detalles sobre las instrucciones y las buenas prácticas a la hora de hacer una copia de seguridad de tu clave.

Ahora está listo para transferir su clave de inquilino a Azure RMS.

## Transferir su clave de inquilino a Azure RMS
Después de que haya generado su propia clave, debe transferirla a Azure RMS antes de usarla. Para el nivel más alto de seguridad, esta transferencia es un proceso manual que le obliga a volar a la oficina de Microsoft en Redmond, Washington, Estados Unidos de América. Para completar este proceso, siga estos 3 pasos:

-   [Paso 1: Aportar su clave a Microsoft](#step-1-bring-your-key-to-microsoft)

-   [Paso 2: Transferir su clave al mundo de seguridad de Azure RMS](#step-2-transfer-your-key-to-the-azure-rms-security-world)

-   [Paso 3: Procedimientos de cierre](#step-3-closing-procedures)

### Paso 1: Aportar su clave a Microsoft

-   Póngase en contacto con los Servicios de soporte al cliente de Microsoft (CSS) para programar una cita a fin de transferir la clave para Azure RMS. Debe presentar a Microsoft en Redmond los siguientes requisitos:

    -   Un quórum de sus tarjetas administrativas. Si ha seguido las instrucciones anteriores en [Paso 2: Crear un mundo de seguridad](#step-2-create-a-security-world), estas serán dos de sus tres tarjetas.

    -   Personal autorizado para transportar tus tarjetas administrativas y anclajes, habitualmente dos (uno para cada tarjeta).

    -   Su archivo de mundo de seguridad (%NFAST_KMDATA%\local\world) en una unidad USB.

    -   Su archivo de clave acortado en una unidad USB.

### Paso 2: Transferir su clave al mundo de seguridad de Azure RMS

1.  Cuando llega a Microsoft para transferir su clave, puede pasar lo siguiente:

    -   Microsoft le proporciona una estación de trabajo fuera de línea que tiene un HSM de Thales adjunto, el software de Thales instalado y un archivo de mundo de seguridad Azure RMS cargado previamente en la carpeta C:\Temp\Destination.

    -   En esta estación de trabajo, cargue su archivo de mundo de seguridad y el archivo de clave acortado desde su unidad USB en la carpeta C:\Temp\Source.

    -   Los operadores de Azure RMS transfieren de forma segura tu clave al mundo de seguridad de Azure RMS mediante las utilidades de Thales.

    Este proceso será parecido a lo siguiente, donde el último parámetro de key-xfer-im en este ejemplo se reemplaza por su nombre de archivo de clave acortado:

    **C:\&gt; mk-reprogram.exe --owner c:\Temp\Destination add c:\Temp\Source**

    **C:\&gt; key-xfer-im.exe c:\Temp\Source c:\Temp\Destination --module c:\Temp\Source\key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**

2.  Mk-reprogram le pedirá a usted y a los operadores de Azure RMS conectar sus tarjetas de administrador y sus anclajes respectivos. Estos comandos generan un archivo de clave acortado en C:\Temp\Destination que contiene su clave protegida por el mundo de seguridad Azure RMS.

### Paso 3: Procedimientos de cierre

-   En su presencia, los operadores de Azure RMS hacen lo siguiente:

    -   Ejecutar una herramienta que Microsoft ha desarrollado en colaboración con Thales, que elimina dos permisos: El permiso para recuperar la clave y el permiso para cambiar otros permisos. Después de que se haga esto, esta copia de tu clave está bloqueada para el mundo de seguridad de Azure RMS. Los HSM de Thales no permitirán a los operadores de Azure RMS con sus tarjetas de administrador para recuperar la copia en texto simple de su clave.

    -   Copiar el archivo de la clave resultante a una unidad USB para cargar posteriormente al servicio Azure RMS.

    -   Restablece la configuración predeterminada de fábrica del HSM y barre la estación de trabajo hasta que quede limpia.

Ahora ha completado las instrucciones obligatorias para aportar su propia clave en persona y puede volver a su organización para llevar a cabo los pasos siguientes para planificar e implementar la clave de inquilino.

> [!div class="button"]
[Pasos siguientes >>](plan-implement-tenant-key.md#next-steps)





<!--HONumber=Apr16_HO3-->


