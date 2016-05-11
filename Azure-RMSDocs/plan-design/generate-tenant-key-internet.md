---
# required metadata

title: Generar y transferir su clave de inquilino a través de Internet | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1bff9b06-8c5a-4b1d-9962-6668219210e6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Generar y transferir su clave de inquilino a través de Internet
Use los procedimientos siguientes si ha decidido [administrar su propia clave de inquilino](plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok-) y quiere transferirla a través de Internet en lugar de viajar a una oficina de Microsoft para transferirla en persona:


## Prepare su estación de trabajo conectada a Internet.
Para preparar su estación de trabajo conectada a Internet, siga estos 3 pasos:

-   [Paso 1: Instale Windows PowerShell para Azure Rights Management.](#step-1-install-windows-powershell-for-azure-rights-management)

-   [Paso 2: Obtén tu id. de inquilino de Azure Active Directory.](#step-2-get-your-azure-active-directory-tenant-id)

-   [Paso 3: Descargue el conjunto de herramientas de BYOK.](#step-3-download-the-byok-toolset)

### Paso 1: Instale Windows PowerShell para Azure Rights Management.
En la estación de trabajo conectada a Internet, descargue e instale el módulo Windows PowerShell para Azure Rights Management.

> [!NOTE]
> Si ha descargado anteriormente este módulo de Windows PowerShell, ejecute el siguiente comando para comprobar que su número de versión es 2.1.0.0 como mínimo: `(Get-Module aadrm -ListAvailable).Version`

Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

### Paso 2: Obtén tu id. de inquilino de Azure Active Directory.
Inicie Windows PowerShell con la opción **Ejecutar como administrador** y, a continuación, ejecute los comandos siguientes:

-   Use el cmdlet [Connect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629415.aspx) para conectarse al servicio Azure RMS:

    ```
    Connect-AadrmService
    ```
    Cuando se le pida, escriba las credenciales de administrador de inquilinos de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (normalmente, usará una cuenta de administrador global de Office 365 o Azure Active Directory).

-   Use el cmdlet [Get-AadrmConfiguration](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) para mostrar la configuración de su inquilino:

    ```
    Get-AadrmConfiguration
    ```
    Desde la salida, guarde el GUID desde la primera línea (BPOSId). Este es tu id. de inquilino de Azure Active Directory, que necesitará posteriormente cuando prepare su clave de inquilino para cargarla.

-   Use el cmdlet [Disconnect-AadrmService](http://msdn.microsoft.com/library/windowsazure/dn629416.aspx) para desconectarse del servicio de Azure RMS hasta que esté listo para cargar la clave:

    ```
    Disconnect-AadrmService
    ```

No cierre la ventana de Windows PowerShell.

### Paso 3: Descargue el conjunto de herramientas de BYOK.
Vaya al Centro de descarga de Microsoft y [descargue el conjunto de herramientas de BYOK](http://go.microsoft.com/fwlink/?LinkId=335781) para su región:

|Región|Nombre del paquete|
|----------|----------------|
|América del Norte|AzureRMS-BYOK-tools-UnitedStates.zip|
|Europa|AzureRMS-BYOK-tools-Europe.zip|
|Asia|AzureRMS-BYOK-tools-AsiaPacific.zip|
El conjunto de herramientas incluye los siguientes elementos:

-   Un paquete de clave de intercambio de claves (KEK) cuyo nombre comienza por **BYOK-KEK-pkg-**.

-   Un paquete de mundo de seguridad cuyo nombre comienza por **BYOK-SecurityWorld-pkg-**.

-   Un script Python llamado **verifykeypackage.py**.

-   Un archivo ejecutable de la línea de comandos llamado **KeyTransferRemote.exe**, un archivo de metadatos llamado **KeyTransferRemote.exe.config** y archivos DLL asociados.

-   Un paquete Visual C++ Redistributable, llamado **vcredist_x64.exe**.

Copia el paquete a la unidad de USB o a otro almacenamiento portátil.

## Prepare su estación de trabajo desconectada.
Para preparar su estación de trabajo que no esté conectada a una red (ya sea a Internet o a la red interna), siga estos 2 pasos:

-   [Paso 1: Preparar la estación de trabajo desconectada con HSM de Thales](#step-1-prepare-the-disconnected-workstation-with-thales-hsm)

-   [Paso 2: Instalar el conjunto de herramientas BYOK en la estación de trabajo desconectada](#step-2-install-the-byok-toolset-on-the-disconnected-workstation)

### Paso 1: Preparar la estación de trabajo desconectada con HSM de Thales
En la estación de trabajo desconectada, instale el software de soporte nCipher (Thales) en un equipo de Windows y, a continuación, adjunte un HSM de Thales a ese equipo.

Asegúrese de que las herramientas de Thales se encuentran en la ruta de acceso **(%nfast_home%\bin** y **%nfast_home%\python\bin**). Por ejemplo, escriba lo siguiente:

```
set PATH=%PATH%;”%nfast_home%\bin”;”%nfast_home%\python\bin”
```
Para obtener más información, consulte la guía de usuario incluida en el HSM de Thales o visite el sitio web de Thales para Azure RMS en [http://www.thales-esecurity.com/msrms/cloud](http://www.thales-esecurity.com/msrms/cloud).

### Paso 2: Instalar el conjunto de herramientas BYOK en la estación de trabajo desconectada
Copie el paquete del conjunto de herramientas de BYOK de la unidad USB o de otra unidad de almacenamiento portátil y, a continuación, haga lo siguiente:

1.  Extraiga los archivos del paquete descargado en cualquier carpeta.

2.  Desde esa carpeta, ejecute vcredist_x64.exe.

3.  Siga las instrucciones para instalar los componentes de tiempo de ejecución de Visual C++ para Visual Studio 2012.

## Generar su clave de inquilino
En la estación de trabajo desconectada, siga estos 3 pasos para generar tus propias claves de inquilino:

-   [Paso 1: Crear un mundo de seguridad](#step-1-create-a-security-world)

-   [Paso 2: Validar el paquete descargado](#step-2-validate-the-downloaded-package)

-   [Paso 3: Crear una clave nueva](#step-3-create-a-new-key)

### Paso 1: Crear un mundo de seguridad
Inicie un símbolo de comando y ejecute el programa del nuevo mundo de Thales.

```
new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3
```
Este programa crea un archivo de **mundo de seguridad** en %NFAST_KMDATA%\local\world, que corresponde a la carpeta C:\ProgramData\nCipher\Key Management Data\local. Puede usar valores diferentes para el quórum, pero en nuestro ejemplo, recibe el aviso de que tiene que escribir tres tarjetas en blanco y anclar todas ellas. A continuación, se solicitará que dos tarjetas cualesquiera tengan acceso administrativo al mundo de seguridad (el cuórum que ha especificado).  Estas tarjetas convierten el **Conjunto de tarjetas del administrador** para el nuevo mundo de seguridad. En esta fase, puede especificar la contraseña o el PIN de cada tarjeta de ACS, o bien agregarlo más adelante con un comando.

> [!TIP]
> Puede comprobar el estado actual de la configuración de los HSM mediante el comando `nkminfo` .

A continuación, haga lo siguiente:

1.  Instale el proveedor de CNG de Thales como se describe en la documentación de Thales y configúrelo para usar el nuevo mundo de seguridad.

2.  Realice una copia de seguridad del archivo del mundo en **%nfast_kmdata%\local**. Asegure y proteja el archivo del mundo, las tarjetas del administrador y sus anclajes, y asegúrese de que ninguna persona tiene acceso a más de una tarjeta.

### Paso 2: Validar el paquete descargado
Este paso es opcional, pero es recomendable para que pueda validar estas características:

-   La Clave de intercambio de claves que se incluye en el grupo de herramientas se ha generado en un HSM de Thales genuino.

-   El hash del Mundo de seguridad de Azure RMS que se incluye en el conjunto de herramientas se ha generado desde un HSM de Thales genuino.

-   La Clave de intercambio de claves no es exportable.

> [!NOTE]
> Para validar el paquete descargado, el HSM debe conectarse, encenderse, y tener un mundo de seguridad en él (igual que el acaba de crear).

#### Para validar el paquete descargado

1.  Ejecute el script verifykeypackage.py escribiendo uno de los siguientes, en función de su región:

    -   Para América del Norte:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Para Europa:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Para Asia:

        ```
        python verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
        ```

    > [!TIP]
    > El software de Thales incluye un intérprete Python en %NFAST_HOME%\python\bin

2.  Confirme que ve lo que se indica a continuación, lo cual significa que la validación es correcta: **Resultado:  CORRECTO**

Este script valida la cadena del firmante hasta la clave de la raíz de Thales. El hash de esta clave de la raíz está incrustada en el script y su valor debe ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**. También puede confirmar este valor de forma independiente visitando el [sitio web de Thales](http://www.thalesesec.com/).

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
cngimport --import -M --key=contosokey --appname=simple contosokey
```
Cuando ejecute este comando, siga estas instrucciones:

-   Reemplace *contosokey* por el mismo valor que especificó en [Paso 1: Crear un mundo de seguridad](#step-1-create-a-security-world) en la sección *Generar su clave de inquilino*.

-   Utilice la opción **-M** para que la clave sea adecuada para este escenario. Sin esto, la clave resultante será una clave específica de usuario para el usuario actual.

-   La opción **appname** corresponde al nombre de la aplicación que aparece en el archivo de clave. Si siguió estas instrucciones para crear una clave, se usará el valor de simple, tal y como se muestra en el comando. Pero, si va a migrar una clave existente protegida por HSM para realizar una migración de AD RMS a Azure RMS, especifique el nombre existente en este comando y los comandos que siguen si también usan la opción appname.

Este comando crea un archivo de clave acortada en la carpeta %NFAST_KMDATA%\local con un nombre que comienza con **key_caping`_`** seguido por un SID. Por ejemplo: **key_caping_machine--801c1a878c925fd9df4d62ba001b94701c039e2fb**. Este archivo contiene una clave cifrada.

> [!TIP]
> Puede consultar el estado actual de la configuración de las claves mediante el comando `nkminfo –k` .

Haga una copia de seguridad de este archivo de clave acortado en una ubicación segura.

> [!IMPORTANT]
> Cuando posteriormente transfiera su clave a Azure RMS, Microsoft no le puede volver a exportar esta clave, así que tiene mucha importancia que haga la copia de seguridad de su clave y del mundo de seguridad de forma segura. Póngase en contacto con Thales para averiguar más detalles sobre las instrucciones y las buenas prácticas a la hora de hacer una copia de seguridad de tu clave.

Ahora está listo para transferir su clave de inquilino a Azure RMS.

## Preparar su clave de inquilino para transferirla
En la estación de trabajo desconectada, siga estos 4 pasos para preparar su propia clave de inquilino:

-   [Paso 1: Crear una copia de su clave con permisos restringidos](#step-1-create-a-copy-of-your-key-with-reduced-permissions)

-   [Paso 2: Inspeccionar la nueva copia de la clave](#step-2-inspect-the-new-copy-of-the-key)

-   [Paso 3: Cifrar su clave mediante la Clave de intercambio de claves de Microsoft](#step-3-encrypt-your-key-by-using-microsoft-s-key-exchange-key)

-   [Paso 4: Copiar su paquete de transferencia de claves a la estación de trabajo conectada a Internet](#step-4-copy-your-key-transfer-package-to-the-internet-connected-workstation)

### Paso 1: Crear una copia de su clave con permisos restringidos
Para reducir los permisos en su clave de inquilino, haga lo siguiente:

-   En el símbolo del sistema, ejecute uno de los siguientes, en función de su región:

    -   Para América del Norte:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
        ```

    -   Para Europa:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
        ```

    -   Para Asia:

        ```
        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
        ```

Cuando ejecute este comando, reemplace *contosokey* por el mismo valor que especificó en [Paso 1: Crear un mundo de seguridad](##step-1-create-a-security-world) en la sección *Generar su clave de inquilino*.

Se le pedirá que conecte sus tarjetas de ACS del mundo de seguridad y, si se especifica, su contraseña o PIN.

Cuando el comando finalice, verá **Resultado: CORRECTO** y la copia de su clave de inquilino con permisos reducidos estará en el archivo llamado key_xferacId_*&lt;contosokey&gt;*.

### Paso 2: Inspeccionar la nueva copia de la clave
De forma opcional, ejecute las utilidades de Thales para confirmar los permisos mínimos en la nueva clave de inquilino:

-   aclprint.py:

    ```
    "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
    ```

-   kmfile-dump.exe:

    ```
    "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
    ```

Cuando ejecute estos comandos, reemplace *contosokey* por el mismo valor que especificó en [Paso 1: Crear un mundo de seguridad](##step-1-create-a-security-world) en la sección *Generar su clave de inquilino*.

### Paso 3: Cifrar su clave mediante la Clave de intercambio de claves de Microsoft
Ejecute uno de los siguientes comandos, en función de su región:

-   Para América del Norte:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Para Europa:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

-   Para Asia:

    ```
    KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -TenantBposId GUID -KeyFriendlyName ContosoFirstkey
    ```

Cuando ejecute este comando, siga estas instrucciones:

-   Reemplace *contosokey* por el identificador que usó para generar la clave en [Paso 1: Crear un mundo de seguridad](##step-1-create-a-security-world) en la sección *Generar su clave de inquilino*.

-   Reemplace *GUID* por el identificador de inquilino de Azure Active Directory que recuperó en [Paso 2: Obtener el identificador de inquilino de Azure Active Directory](#step-2-get-your-azure-active-directory-tenant-id) en la sección *Preparar la estación de trabajo conectada a Internet*.

-   Reemplace *ContosoFirstKey* por una etiqueta que se usará para el nombre de su archivo de salida.

Cuando finalice de forma correcta, mostrará **Resultado: CORRECTO** y habrá un nuevo archivo en la carpeta actual cuyo nombre es el siguiente: TransferPackage-*ContosoFirstkey*.byok.

### Paso 4: Copiar su paquete de transferencia de claves a la estación de trabajo conectada a Internet
Use una unidad USB u otra unidad de almacenamiento portátil para copiar el archivo de salida del paso anterior (KeyTransferPackage-*ContosoFirstkey*.byok) a la estación de trabajo conectada a Internet.

> [!NOTE]
> Utilice prácticas de seguridad para proteger el archivo, ya que incluye su clave privada.

## Transferir su clave de inquilino a Azure RMS
En la estación de trabajo conectada a Internet, siga estos 3 pasos para transferir su nueva clave de inquilino a Azure RMS:

-   [Paso 1: Conectarse a Azure RMS](#step-1-connect-to-azure-rms)

-   [Paso 2: Cargar el paquete de la clave](#step-2-upload-the-key-package)

-   [Paso 3: Enumerar tus claves de inquilino, según sea necesario](#step-3-enumerate-your-tenant-keys-as-needed)

### Paso 1: Conectarse a Azure RMS
Vuelva a la ventana de Windows PowerShell y escriba lo siguiente:

1.  Vuelva a conectarte al servicio [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)]:

    ```
    Connect-AadrmService
    ```

2.  Use el cmdlet [Get-AadrmKeys](http://msdn.microsoft.com/library/windowsazure/dn629420.aspx) para ver la configuración actual de tu clave de inquilino:

    ```
    Get-AadrmKeys
    ```

### Paso 2: Cargar el paquete de la clave
Use el cmdlet [Add-AadrmKey](http://msdn.microsoft.com/library/windowsazure/dn629418.aspx) para cargar el paquete de transferencia de claves que ha copiado en la estación de trabajo desconectada:

```
Add-AadrmKey –KeyFile <PathToPackageFile> -Verbose
```
> [!WARNING]
> Se le pedirá que confirme esta acción. Es importante que entienda que esta acción no se puede deshacer. Cuando carga una clave de inquilino, automáticamente se convierte en la clave de inquilino principal de su organización y los usuarios comenzarán a usar esta clave de inquilino cuando protegen documentos y archivos.

Si la carga es correcta, verá el mensaje siguiente: **El servicio de Rights Management ha agregado de forma correcta la clave.**

Espere un retardo de replicación para el cambio a fin de propagar todos los centros de datos de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

### Paso 3: Enumerar tus claves de inquilino, según sea necesario
Use el cmdlet Get-AadrmKeys de nuevo para ver el cambio de tu clave de inquilino, y siempre que quiera ver una lista de sus claves de inquilino. Las claves de inquilino que se muestran incluyen la clave de inquilino inicial que Microsoft había generado para usted, y cualquier clave de inquilino que haya agregado:

```
Get-AadrmKeys
```
La clave de inquilino que esté marcada como **Activa** es la única de su organización que se usa actualmente para proteger documentos y archivos.

Ahora ha completado todos los pasos obligatorios para aportar su propia clave a través de Internet y puede llevar a cabo los pasos siguientes para planificar e implementar la clave de inquilino.


> [!div class="button"]
[Pasos siguientes >>](plan-implement-tenant-key.md#next-steps)




<!--HONumber=Apr16_HO3-->


