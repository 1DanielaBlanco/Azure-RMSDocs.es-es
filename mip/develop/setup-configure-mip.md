---
title: Instalación y configuración del SDK de Microsoft Information Protection (MIP)
description: Proporciona los requisitos previos de instalación y configuración, para poder usar aplicaciones creadas con el SDK de Microsoft Information Protection.
author: BryanLa
ms.service: information-protection
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.date: 01/30/2019
ms.author: bryanla
ms.openlocfilehash: 13d9d82a402d283c393c90dc52c265a1bf8502d7
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56254278"
---
# <a name="microsoft-information-protection-mip-sdk-setup-and-configuration"></a>Instalación y configuración del SDK de Microsoft Information Protection (MIP) 

La Guía de inicio rápido y los artículos del tutorial se centran en torno a la creación de aplicaciones que usan las API y las bibliotecas del SDK de MIP. Este artículo muestra cómo instalar y configurar la suscripción de Office 365 y la estación de trabajo del cliente, como parte de la preparación para usar el SDK.

## <a name="prerequisites"></a>Requisitos previos

No olvide revisar los siguientes temas antes de comenzar:

- [¿Qué es el Centro de seguridad y cumplimiento de Office 365?](https://docs.microsoft.com/office365/securitycompliance/security-and-compliance)
- [¿Qué es Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection)
- [¿Cómo funciona la protección en Azure Information Protection?](/azure/information-protection/understand-explore/what-is-information-protection#how-data-is-protected)

> [!IMPORTANT]
> **Para mantener la privacidad del usuario, debe pedir al usuario su consentimiento antes de habilitar el registro automático.** El ejemplo siguiente es un mensaje estándar de que Microsoft usa para la notificación de registro:
>
> *Al activar el Registro de errores y rendimiento, acepta enviar datos de errores y rendimiento a Microsoft. Microsoft recopila datos de errores y rendimiento a través de Internet («Datos»). Microsoft usa estos datos para proporcionar y mejorar la calidad, la seguridad y la integridad de los productos y servicios de Microsoft. Por ejemplo, analizamos el rendimiento y la confiabilidad, como qué características usa, la rapidez con que responden las características, el rendimiento del dispositivo, las interacciones con la interfaz de usuario y los problemas que tenga con el producto. Los datos también incluyen información sobre la configuración del software, como el software que ejecuta actualmente y la dirección IP.*

## <a name="sign-up-for-an-office-365-subscription"></a>Registrarse para obtener una suscripción de Office 365

Muchos de los ejemplos del SDK requieren acceso a una suscripción de Office 365. Si no lo ha hecho aún, asegúrese de regístrate en uno de los siguientes tipos de suscripción:

| Nombre | Registrarse |
|------|---------|
| Prueba de Office 365 Enterprise E3 (prueba gratuita de 30 días) | https://go.microsoft.com/fwlink/p/?LinkID=403802 |
| Office 365 Enterprise E3 o E5 | https://products.office.com/business/office-365-enterprise-e3-business-software |
| Blog del equipo de Enterprise Mobility and Security E3 o E5 | https://www.microsoft.com/cloud-platform/enterprise-mobility-security |
| Azure Information Protection Premium P1 o P2 | https://azure.microsoft.com/pricing/details/information-protection/ |
| Microsoft 365 E3, E5 o F1 | https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans | 

## <a name="configure-sensitivity-labels"></a>Configurar etiquetas de confidencialidad

Si actualmente usa Azure Information Protection, debe migrar las etiquetas al centro de cumplimiento y seguridad de Office 365. Para más información sobre el proceso, consulte [Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365](/azure/information-protection/configure-policy-migrate-labels). 

## <a name="configure-your-client-workstation"></a>Configurar la estación de trabajo del cliente

A continuación, complete los siguientes pasos para asegurarse de que su equipo cliente está instalado y configurado correctamente.

1. Si usa una estación de trabajo de Windows 10:

   - Con Windows Update, actualice el equipo a Windows 10 Fall Creators Update (versión 1709) o posterior. Para comprobar su versión actual:
     - Haga clic en el icono de Windows en la parte inferior izquierda.
     - Escriba "Acerca de tu PC" y presione la tecla "Entrar".
     - Desplácese hacia abajo hasta **Especificaciones de Windows** y vea debajo de **Versión**.

   - Asegúrese de que está habilitado el "Modo de programador" en la estación de trabajo:
     - Haga clic en el icono de Windows en la parte inferior izquierda.
     - Escriba "Usar las funciones de desarrollador" y presione la tecla "Entrar" cuando aparezca el elemento **Usar las funciones de desarrollador**.
     - En el cuadro de diálogo **Configuración**, en la pestaña **Para programadores**, en "Usar las funciones de programador", seleccione la opción **Modo de programador**.
     - Cierre el cuadro de diálogo **Configuración**.

2. Instale [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/), con las siguientes cargas de trabajo y estos componentes opcionales:
   - Carga de trabajo de Windows del **desarrollo de la Plataforma universal de Windows**, además de los siguientes componentes opcionales:
     - **Herramientas de la Plataforma universal de Windows de C++**
     - **SDK 10.0.16299.0 de Windows 10** o versiones posteriores, si no se incluye de forma predeterminada
   - Carga de trabajo de Windows del **desarrollo de escritorio con C++**, además de los siguientes componentes opcionales:
     - **SDK 10.0.16299.0 de Windows 10** o versiones posteriores, si no se incluye de forma predeterminada 

     [![Configuración de Visual Studio](media/setup-mip-client/visual-studio-install.png)](media/setup-mip-client/visual-studio-install.png#lightbox)

3. Instalar el [ADAL.PS PowerShell Module](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2): 

   - Dado que se necesitan derechos de administrador para instalar los módulos, primero deberá realizar una de las siguientes acciones:

     - inicie sesión en el equipo con una cuenta que tenga derechos de administrador.
     - ejecutar la sesión de Windows PowerShell con permisos elevados (Ejecutar como administrador).

   - A continuación, ejecute el cmdlet `install-module -name adal.ps`:

     ```powershell
     PS C:\WINDOWS\system32> install-module -name adal.ps

     Untrusted repository
     You are installing the modules from an untrusted repository. If you trust this repository, change its
     InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
     'PSGallery'?
     [Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): A

     PS C:\WINDOWS\system32>
     ```

4. Descargar archivos del SDK:

   El SDK de MIP se admite en las siguientes plataformas, con descargas independientes para cada plataforma o idioma admitido:  

   [!INCLUDE [MIP SDK platform support](../includes/mip-sdk-platform-support.md)]

   **TAR.gz/. Descargas de ZIP**

   TAR.gz y. Descargas de ZIP contienen archivos comprimidos adicionales, uno para cada API. Los archivos comprimidos se denominan como sigue, donde \<API\> = `file`, `protection`, o `upe`, y \<OS\> = la plataforma: `mip_sdk_<API>_<OS>_1.0.0.0.zip (or .tar.gz)`. Por ejemplo, sería el archivo para encabezados y archivos binarios de la API de protección en Debian: `mip_sdk_protection_debian9_1.0.0.0.tar.gz`. Cada.tar.gz/.zip independiente se divide en tres directorios:

   - **Ubicaciones:** Compila los archivos binarios para cada arquitectura de la plataforma, si procede.
   - **Se incluyen:** Archivos de encabezado (C++).
   - **Ejemplos:** Código fuente para aplicaciones de ejemplo.
    
   **Paquetes de NuGet**

   Si va a realizar el desarrollo de Visual Studio, se puede instalar el SDK también a través de la consola de administrador de paquetes de NuGet:

    ```console
    Install-Package Microsoft.InformationProtection.File
    Install-Package Microsoft.InformationProtection.Policy
    Install-Package Microsoft.InformationProtection.Protection
    ```  

5. Si no usa el paquete de NuGet, agregue las rutas de acceso de los archivos binarios del SDK a la variable de entorno PATH. La variable de ruta de acceso permite a los archivos binarios dependientes (DLL) deben encontrarse en tiempo de ejecución, las aplicaciones cliente (opcional):

   Si usa una estación de trabajo de Windows 10:

   - Haga clic en el icono de Windows en la parte inferior izquierda.
   - Escriba "Path" y presione la tecla "Entrar", cuando aparezca el elemento **Editar las variables de entorno del sistema**.
   - En el cuadro de diálogo **Propiedades del sistema**, haga clic en **Variable de entorno**.
   - En el cuadro de diálogo **Variables de entorno**, haz clic en la fila de la variable **Ruta de acceso** debajo de **Variables de usuario para \<usuario\>** y, a continuación, haga clic en **Editar**.
   - En el cuadro de diálogo **Editar variable de entorno**, haga clic en **Nueva** para crear una nueva fila editable. Mediante la ruta de acceso completa a cada uno de los subdirectorios `file\bins\debug\amd64`, `protection\bins\debug\amd64` y `upe\bins\debug\amd64`, agregue una nueva fila para cada uno. Los directorios del SDK se almacenan en un formato `<API>\bins\<target>\<platform>`, donde:
     - \<API\> = `file`, `protection`, `upe`
     - \<destino\> = `debug`, `release`
     - \<plataforma\>  =  `amd64` (x64), `x86`, etcetera.
   
   - Cuando termine de actualizar la variable **Ruta de acceso**, haga clic en **Aceptar**. A continuación, haga clic en **Aceptar** cuando aparezca el cuadro de diálogo **Variables de entorno**.

6. Descargar ejemplos del SDK de GitHub (opcional):

   - Si no tiene uno aún, cree primero un [perfil de GitHub](https://github.com/join).
   - A continuación, instale la versión más reciente de [las herramientas de cliente de Git de Software Freedom Conservancy (Git Bash)](https://git-scm.com/download/)
   - Utilizando Git Bash, descargue los ejemplos de interés:
     - Use la siguiente consulta para ver los repositorios: https://github.com/Azure-Samples?utf8=%E2%9C%93&q=MipSdk. 
     - Utilizando Git Bash, use `git clone https://github.com/azure-samples/<repo-name>` para descargar cada repositorio de ejemplo.

## <a name="register-a-client-application-with-azure-active-directory"></a>Registre una aplicación cliente con Azure Active Directory.

Como parte de la suscripción de Office 365, el proceso de aprovisionamiento, se crea un inquilino de Azure Active Directory (Azure AD) asociado. El inquilino de Azure AD proporciona administración de identidad y acceso para las *cuentas de usuario* y las *cuentas de aplicación* de Office 365. Las aplicaciones que requieren acceso a una API protegida (por ejemplo, API de MIP), requieren una cuenta de la aplicación.

Para la autenticación y autorización en tiempo de ejecución, las cuentas se representan mediante un *entidad de seguridad*, que se deriva de la información de identidad de la cuenta. Las entidades de seguridad que representan una cuenta de la aplicación se conocen como [ *entidad de servicio*](/azure/active-directory/develop/developer-glossary#service-principal-object). 

Para registrar una cuenta de la aplicación en Azure AD para su uso con los ejemplos del SDK de MIP y las guías de inicio rápido:

  > [!IMPORTANT] 
  > Si quiere acceder a la administración de inquilinos de Azure AD para crear cuentas, deberá iniciar sesión en Azure Portal con una cuenta de usuario que sea miembro del [rol "Propietario" en la suscripción](/azure/billing/billing-add-change-azure-subscription-administrator). Según la configuración del inquilino, es posible que deba ser miembro del rol de directorio "Administrador global" para [registrar una aplicación](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps).
  > Se recomienda realizar pruebas con una cuenta restringida. Asegúrese de que la cuenta solo tiene derechos de acceso a los puntos de conexión de SCC necesarios. Las contraseñas de texto no cifrado que se pasan a través de la línea de comandos se pueden recopilar mediante sistemas de registro.

1. Siga los pasos de [registrar una aplicación con Azure AD, registre una nueva aplicación](/azure/active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad#register-a-new-application-using-the-azure-portal) sección. Con fines de prueba, use los siguientes valores para las propiedades a medida que avance en los pasos de la guía: 
    - **Tipo de aplicación**: seleccione "Nativo", ya que las aplicaciones que se muestran en el SDK son aplicaciones de la consola instaladas de forma nativa. OAuth2 considera las aplicaciones nativas como clientes "públicos", ya que son incapaces de almacenar o usar las credenciales de la aplicación de forma segura; a diferencia de una aplicación "confidencial" basada en el servidor, como una aplicación web, que se registra con sus propias credenciales. 
    - **Dirección URI de redireccionamiento**: puesto que el SDK usa aplicaciones cliente de consola sencillas, puede usar un URI con el formato `<app-name>://authorize`.

2. Cuando termine, volverá a la página **Aplicación registrada** para el nuevo registro de aplicación. Copie y guarde el GUID del campo **Id. de aplicación**, ya que lo necesitará para los inicios rápidos. 

3. A continuación, haga clic en **Configuración** para agregar la API y los permisos a los que el cliente debe tener acceso. En la página **Configuración**, haga clic en **Permisos necesarios**.

4. Ahora deberá agregar los permisos y las API de MIP que la aplicación requiere en tiempo de ejecución:
   - En la hoja **Permisos necesarios**, haga clic en **Agregar**. 
   - En la página **Agregar acceso de API**, haga clic en **Seleccionar una API**.
   - En la página **Seleccionar una API**, haga clic en la API "**Microsoft Rights Management Services**" y haga clic en **Seleccionar**.
   - En el **habilitar el acceso** para permisos disponibles de la API de página, haga clic en "**creación y acceso a contenido protegido de los usuarios**", a continuación, **seleccione**, a continuación, **realiza** .

5. Repita el paso 4, pero esta vez cuando llegue a la página **Seleccionar una API**, deberá buscar la API.
   - En la página **Seleccionar una API**, en el cuadro de búsqueda, escriba "**Servicio de sincronización de Microsoft Information Protection**", haga clic en la API y, a continuación, haga clic en **Seleccionar**.
   - En la página **Habilitar acceso** para los permisos disponibles de la API, haga clic en "**Leer todas las directivas unificadas a las que tiene acceso un usuario**", haga clic en **Seleccionar** y, a continuación, en **Listo**.

6. Cuando vuelva a la página **Permisos necesarios**, haga clic en **Conceder permisos** y, a continuación, en **Sí**. Este paso da consentimiento previo a la aplicación con este registro, para tener acceso a las API en los permisos especificados. Si inició sesión como administrador global, el consentimiento se registra para todos los usuarios en el inquilino que ejecuta la aplicación. En caso contrario, se aplica solo a su cuenta de usuario. 

Cuando termine, el registro de aplicación y los permisos de API deberían ser similares al ejemplo siguiente:

   [![Registro de aplicación de Azure AD](media/setup-mip-client/aad-app-registration.png)](media/setup-mip-client/aad-app-registration.png#lightbox)


Para obtener más información sobre cómo agregar las API y los permisos a un registro, consulte [configurar una aplicación cliente para tener acceso a las API web](/azure/active-directory/develop/quickstart-v1-update-azure-ad-app#configure-a-client-application-to-access-web-apis). Aquí encontrará información sobre cómo agregar las API y los permisos necesarios para una aplicación cliente.  

## <a name="request-an-information-protection-integration-agreement-ipia"></a>Solicitud de un Contrato de integración de Information Protection (IPIA)

Antes de publicar una aplicación desarrollada con MIP, debe solicitar y rellenar un contrato formal con Microsoft.

1. Obtenga su IPIA enviando un correo electrónico a [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Requesting%20IPIA%20for%20<company-name>) con la siguiente información:

   **Asunto:** Solicitud de IPIA para *nombre de la compañía*

   En el cuerpo del correo electrónico, incluya:
   - Nombre de la aplicación y del producto
   - Nombre y apellidos del solicitante
   - Dirección de correo electrónico del solicitante

2. Tras la recepción de la solicitud de IPIA, le enviaremos un formulario (como un documento de Word). Revise los términos y las condiciones del IPIA y devuelva el formulario a [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=IPIA%20Response%20for%20<company-name>) con la siguiente información:

   - Nombre legal de la empresa
   - Estado o provincia (Estados Unidos y Canadá) o el país de incorporación
   - Dirección URL de la empresa
   - Dirección de correo electrónico de la persona de contacto
   - Direcciones adicionales de la empresa (opcional)
   - Nombre de la aplicación de la empresa
   - Breve descripción de la aplicación
   - *Identificador del inquilino de Azure*
   - *Identificador de aplicación* de la aplicación
   - Contactos de la compañía, correo electrónico y teléfono para la correspondencia en caso de situaciones críticas

3. Cuando recibamos su formulario, le enviaremos el vínculo IPIA final para firmar digitalmente. Después de la firma, lo firmará el representante de Microsoft adecuado, con lo que el contrato quedará completado.

### <a name="already-have-a-signed-ipia"></a>¿Ya tiene un IPIA firmado?

Si ya tiene un IPIA firmado y desea agregar un nuevo *identificador de aplicación* para una aplicación que se esté lanzando, envíe un correo electrónico a [IPIA@microsoft.com](mailto:IPIA@microsoft.com?subject=Updating%20IPIA%20for%20<company-name>) y proporciónenos la siguiente información:

- Nombre de la aplicación de la empresa
- Breve descripción de la aplicación
- Identificador de inquilino de Azure (incluso si el mismo que antes)
- Identificador de aplicación de la aplicación
- Contactos de la compañía, correo electrónico y teléfono para la correspondencia en caso de situaciones críticas

Tras el envío del correo electrónico, permiten una confirmación del recibo hasta 72 horas.

## <a name="next-steps"></a>Pasos siguientes

- Si es un desarrollador de C++
  - No olvide leer [conceptos observadores](concept-async-observers.md) antes de iniciar la sección de inicio rápido para obtener información sobre la naturaleza asincrónica de las APIs de C++.
  - Cuando esté listo para obtener algo de experiencia con el SDK, comience con [inicio rápido: Inicialización de la aplicación cliente (C++)](quick-app-initialization-cpp.md).
- Si eres un C# para desarrolladores, cuando esté listo para obtener algo de experiencia con el SDK, comience con [inicio rápido: Inicialización de la aplicación cliente (C#)](quick-app-initialization-csharp.md).


