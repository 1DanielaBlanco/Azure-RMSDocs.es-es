---
title: "Desarrollo de la aplicación - AIP"
description: "Una guía que le lleva por la implementación básica de consola de la protección de documentos con AIP."
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 1854329b9cb949a6b4318d00f981f0be9065a33e
ms.sourcegitcommit: 1b6af3c85ed32e8d80ed10cb6ba86fc61026eaa4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2017
---
# <a name="developing-your-application"></a>Desarrollo de la aplicación

En este ejemplo, va a crear una aplicación de consola sencilla que interactúa con el servicio Azure Information Protection (AIP).  Se tomará como entrada la ruta de acceso del documento que se va a proteger y luego se protegerá con una directiva ad-hoc o una plantilla de Azure. A continuación, la aplicación aplicará las directivas correctas de acuerdo con las entradas y se creará un documento con información protegida. El código de ejemplo que se usará es la [aplicación Azure IP Test](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test), que se encuentra en Github.

## <a name="sample-app-prerequisites"></a>Requisitos previos de la aplicación de ejemplo
- **Sistema operativo**: Windows 10, Windows 8, Windows 7, Windows Server 2008, Windows Server 2008 R2 o Windows Server 2012.
- **Lenguaje de programación**: C# (.NET Framework 3.0 y versiones posteriores).
- **Entorno de desarrollo**: Visual Studio 2015 (y versiones posteriores).

## <a name="setting-up-your-azure-configuration"></a>Establecimiento de la configuración de Azure

Para configurar Azure para esta aplicación, es necesario crear un identificador del inquilino, una clave simétrica y un id. de entidad de aplicación.

### <a name="azure-ad-tenant-configuration"></a>Configuración del inquilino de Azure AD

Para configurar el entorno de Azure AD para Azure Information Protection, siga las instrucciones que se indican en [Activar Azure Rights Management](https://docs.microsoft.com/information-protection/deploy-use/activate-service).

Una vez activado el servicio, necesitará componentes de PowerShell para los siguientes pasos. Para ello, siga los pasos que se describen en [Administración del servicio Azure Rights Management mediante Windows PowerShell](https://docs.microsoft.com/information-protection/deploy-use/administer-powershell).

### <a name="getting-your-tenant-id"></a>Obtención del identificador de inquilino

- Abra PowerShell como administrador.
- Importe el módulo de RMS: `Import-Module AADRM`
- Conéctese al servicio con las credenciales de usuario asignadas: `Connect-AadrmService –Verbose`
- Asegúrese de que RMS está habilitado: `Enable-AADRM`
- Para obtener su identificador de inquilino, ejecute: `Get-AadrmConfiguration`

>Registre el valor de BPOSId (identificador de inquilino). Lo necesitará en próximos pasos.

*Salida de ejemplo*
![salida de cmdlet](../media/develop/output-of-Get-AadrmConfiguration.png)

- Desconéctese del servicio: `Disconnect-AadrmService`

### <a name="create-a-service-principal"></a>Creación de una entidad de servicio
Siga estos pasos para crear a una entidad de servicio:
> Una entidad de servicio son credenciales configuradas globalmente para el control de acceso que permiten a los servicios autenticarse en Microsoft Azure AD y proteger la información mediante Microsoft Azure AD Rights Management.

- Abra PowerShell como administrador.
- Importe el módulo Microsoft Azure AD mediante: `Import-Module MSOnline`
- Conéctese al servicio en línea con las credenciales de usuario asignadas: `Connect-MsolService`
- Cree a una nueva entidad de servicio mediante la ejecución de: `New-MsolServicePrincipal`
- Proporcione un nombre para la entidad de servicio
> Registre la clave simétrica y el id. de entidad de la aplicación para usarlos más adelante.

*Salida de ejemplo*
![salida de cmdlet](../media/develop/output-of-NewMsolServicePrincipal.png)

- Agregue el id. de entidad de la aplicación, la clave simétrica y el identificador de inquilino al archivo App.config de la aplicación.

*Archivo App.config de ejemplo*
![salida de cmdlet](../media/develop/example-App.config-file.png)

- Los valores de *ClientID* y *RedirectUri* estarán disponibles desde el momento en que registre su aplicación en Azure. Para más información sobre cómo registrar su aplicación en Azure y adquirir los elementos *ClientID* y *RedirectUri*, consulte [Configuración de Azure RMS para la autenticación de ADAL authentication](adal-auth.md).


## <a name="design-summary"></a>Resumen de diseño
El siguiente diagrama muestra un flujo de proceso y arquitectura de la aplicación que se va a crear. Los pasos se describen a continuación.
![resumen de diseño](../media/develop/design-summary.png)

1. El usuario:
  - Especifica la ruta de acceso del archivo que se va a proteger.
  - Selecciona una plantilla o crea una directiva ad-hoc.
2. La aplicación solicita la autenticación con AIP.
3. AIP confirma la autenticación.
4. La aplicación solicita plantillas a AIP.
5. AIP devuelve plantillas predefinidas.
6. La aplicación busca el archivo especificado con la ubicación indicada.
7. La aplicación aplica la directiva de protección de AIP al archivo.

## <a name="how-the-code-works"></a>Funcionamiento del código

En el ejemplo, Azure IP Test, la solución comienza con el archivo Iprotect.cs. Se trata de una aplicación de consola en C# y, al igual que con cualquier otra aplicación habilitada para AIP, se carga *MSIPC.dll* para comenzar, como se muestra en el método `main()`.

    //Loads MSIPC.dll
    SafeNativeMethods.IpcInitialize();
    SafeNativeMethods.IpcSetAPIMode(APIMode.Server);

Cargue los parámetros necesarios para conectarse a Azure:

    //Loads credentials for the service principal from App.Config
    SymmetricKeyCredential symmetricKeyCred = new SymmetricKeyCredential();
    symmetricKeyCred.AppPrincipalId = ConfigurationManager.AppSettings["AppPrincipalId"];
    symmetricKeyCred.Base64Key = ConfigurationManager.AppSettings["Base64Key"];
    symmetricKeyCred.BposTenantId = ConfigurationManager.AppSettings["BposTenantId"];

Cuando proporcione la ruta de acceso del archivo en la aplicación de consola, la aplicación comprueba si el documento ya está cifrado. El método es de la clase **SafeFileApiNativeMethods**.

    var checkEncryptionStatus = SafeFileApiNativeMethods.IpcfIsFileEncrypted(filePath);

Si el documento no está cifrado, se procede a cifrar el documento con la selección proporcionada en el símbolo del sistema.

    if (!checkEncryptionStatus.ToString().ToLower().Contains(alreadyEncrypted))
    {
      if (method == EncryptionMethod1)
      {
        //Encrypt a file via AIP template
        ProtectWithTemplate(symmetricKeyCred, filePath);

      }
      else if (method == EncryptionMethod2)
      {
        //Encrypt a file using ad-hoc policy
        ProtectWithAdHocPolicy(symmetricKeyCred, filePath);
      }

La opción de protección con plantilla pasa a obtener la lista de plantillas del servidor y proporciona al usuario la opción que se seleccionará.
>Si no modifica las plantillas obtendrá plantillas predeterminadas de AIP.

     public static void ProtectWithTemplate(SymmetricKeyCredential symmetricKeyCredential, string filePath)
     {
       // Gets the available templates for this tenant             
       Collection<TemplateInfo> templates = SafeNativeMethods.IpcGetTemplateList(null, false, true,
           false, true, null, null, symmetricKeyCredential);

       //Requests tenant template to use for encryption
       Console.WriteLine("Please select the template you would like to use to encrypt the file.");

       //Outputs templates available for selection
       int counter = 0;
       for (int i = 0; i < templates.Count; i++)
       {
         counter++;
         Console.WriteLine(counter + ". " + templates.ElementAt(i).Name + "\n" +
             templates.ElementAt(i).Description);
       }

       //Parses template selection
       string input = Console.ReadLine();
       int templateSelection;
       bool parseResult = Int32.TryParse(input, out templateSelection);

       //Returns error if no template selection is entered
       if (parseResult)
       {
         //Ensures template value entered is valid
         if (0 < templateSelection && templateSelection <= counter)
         {
           templateSelection -= templateSelection;

           // Encrypts the file using the selected template             
           TemplateInfo selectedTemplateInfo = templates.ElementAt(templateSelection);

           string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(filePath,
               selectedTemplateInfo.TemplateId,
               SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST, true, false, true, null,
               symmetricKeyCredential);
          }
        }
      }

Si selecciona la directiva ad-hoc, el usuario de la aplicación tiene que proporcionar las direcciones de correo electrónico de las personas que tendrán derechos. En esta sección, la licencia se crea mediante el método **IpcCreateLicenseFromScratch()** y con la aplicación de la nueva directiva en la plantilla.

    if (issuerDisplayName.Trim() != "")
    {
      // Gets the available issuers of rights policy templates.              
      // The available issuers is a list of RMS servers that this user has already contacted.
      try
      {
        Collection<TemplateIssuer> templateIssuers = SafeNativeMethods.IpcGetTemplateIssuerList(
                                                        null,
                                                        true,
                                                        false,
                                                        false, true, null, symmetricKeyCredential);

        // Creates the policy and associates the chosen user rights with it             
        SafeInformationProtectionLicenseHandle handle = SafeNativeMethods.IpcCreateLicenseFromScratch(
                                                            templateIssuers.ElementAt(0));
        SafeNativeMethods.IpcSetLicenseOwner(handle, owner);
        SafeNativeMethods.IpcSetLicenseUserRightsList(handle, userRights);
        SafeNativeMethods.IpcSetLicenseDescriptor(handle, new TemplateInfo(null, CultureInfo.CurrentCulture,
                                                                policyName,
                                                                policyDescription,
                                                                issuerDisplayName,
                                                                false));

        //Encrypts the file using the ad hoc policy             
        string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(
                                       filePath,
                                       handle,
                                       SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST,
                                       true,
                                       false,
                                       true,
                                       null,
                                       symmetricKeyCredential);
       }
    }

## <a name="user-interaction-example"></a>Ejemplo de interacción del usuario

Después de que todo se ha creado y está en ejecución, las salidas de la aplicación se parecerán a estas:

1.Se le pide que seleccione un método de cifrado.
![aplicación de salida - paso 1](../media/develop/app-output-1.png)

2. Se le pide que proporcione la ruta de acceso al archivo que se va a proteger.
![salida de aplicación - paso 2](../media/develop/app-output-2.png)

3. Se le pide que escriba la dirección de correo electrónico del propietario de la licencia (dicho propietario debe tener privilegios de administrador global en el inquilino de Azure AD).
![salida de aplicación - paso 3](../media/develop/app-output-3.png)

4. Escriba las direcciones de correo electrónico de los usuarios que tendrán derechos de acceso al archivo (deben ir separadas por un espacio).
![salida de aplicación - paso 4](../media/develop/app-output-4.png)

5. En la lista, seleccione los derechos que se concederán a los usuarios autorizados.
![salida de aplicación - paso 5](../media/develop/app-output-5.png)

6. Por último, especifique algunos metadatos de directiva: nombre de la directiva, descripción y nombre para mostrar del emisor (identificador de inquilino de Azure AD). ![salida de aplicación - paso 6](../media/develop/app-output-6.png)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
