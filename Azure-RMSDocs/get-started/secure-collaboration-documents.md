---
title: Protección de la colaboración con documentos mediante Azure Information Protection
description: Flujo de trabajo integral para colaborar con documentos protegidos mediante Azure Information Protection.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/21/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 4895c429-959f-47c7-9007-b8f032f6df6f
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: f6ae088dc551189b264eb3cb5ea1e65b9845e5b8
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39372774"
---
# <a name="secure-document-collaboration-by-using-azure-information-protection"></a>Protección de la colaboración con documentos mediante Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Al utilizar Azure Information Protection, es posible proteger los documentos sin renunciar a la colaboración con usuarios autorizados. La mayoría de los documentos que un usuario crea y, a continuación, comparte con otros usuarios para ver y editar serán documentos de Office de Word, Excel y PowerPoint. Estos documentos admiten la protección nativa, lo que significa que además de las características de autorización y cifrado relativas a la protección, admiten también la restricción de permisos para llevar a cabo un control más minucioso. 

Estos permisos se denominan derechos de uso, e incluyen permisos como ver, editar o imprimir. Puede definir derechos de uso individuales cuando un documento está protegido, o puede definir una agrupación de derechos de uso, lo que se denomina niveles de permisos. Los niveles de permisos facilitan la selección de derechos de uso que normalmente se utilizan en conjunto, como revisor o coautor. Para más información sobre los derechos de uso y los niveles de permiso, consulte [Configuración de los derechos de uso para Azure Rights Management](../deploy-use/configure-usage-rights.md).

Al configurar estos permisos, también puede especificar a qué usuarios están destinados:

- **Para los usuarios de su propia organización o de otra organización que usa Azure Active Directory**: puede especificar cuentas de usuario de Azure AD, grupos de Azure AD o todos los usuarios de esa organización. 

- **Para los usuarios que no tienen una cuenta de Azure Active Directory**: especifique una dirección de correo electrónico que se usará con una cuenta Microsoft. Esta cuenta puede existir ya o bien los usuarios pueden crearla en el momento en que abran el documento protegido. 
    
    Para abrir documentos con una cuenta de Microsoft, los usuarios deben usar Hacer clic y ejecutar de Office 2016. Otras ediciones y versiones de Office todavía no admiten la apertura de documentos protegidos de Office con una cuenta Microsoft.

- **Para cualquier usuario autenticado**: esta opción es adecuada para cuando no es necesario controlar quién tiene acceso al documento protegido, siempre que el usuario se pueda autenticar. La autenticación puede completarse mediante Azure AD, una cuenta Microsoft o un proveedor social federado o un código de acceso de un solo uso cuando el contenido está protegido por las nuevas funcionalidades de Office 365 Message Encryption. 

Como administrador, puede configurar una etiqueta de Azure Information Protection para aplicar los permisos y los usuarios autorizados. Esta configuración facilita en gran medida a los usuarios y otros administradores la aplicación de la configuración de protección adecuada, ya que basta con aplicar la etiqueta sin tener que especificar los detalles. En las secciones siguientes se ofrece un tutorial de ejemplo para proteger un documento que admite la colaboración segura con usuarios internos y externos.


## <a name="example-configuration-for-a-label-to-apply-protection-to-support-internal-and-external-collaboration"></a>Ejemplo de configuración para una etiqueta a fin aplicar una protección que admite la colaboración interna y externa

En este ejemplo se explica cómo configurar una etiqueta existente para aplicar la protección a fin de que los usuarios de su organización puedan colaborar en documentos con todos los usuarios de otra organización que tenga Office 365 o Azure AD, un grupo de otra organización que tenga Office 365 o Azure AD y un usuario que no tenga una cuenta de Azure AD y, en su lugar, utilice su dirección de correo electrónico de Gmail.

Dado que el escenario restringe el acceso a usuarios específicos, no incluye la configuración para todos los usuarios autenticados. Para obtener un ejemplo de cómo configurar una etiqueta con esta configuración, consulte el [Ejemplo 5: Etiqueta que cifra el contenido pero no limita el acceso a este](../deploy-use/configure-policy-protection.md#example-5-label-that-encrypts-content-but-doesnt-restrict-who-can-access-it).  

1. Seleccione una etiqueta que ya esté en la directiva global o una directiva con ámbito. En la hoja **Protección**, asegúrese de que **Azure (clave de nube)** esté seleccionado.
    
2. Asegúrese de que **Establecer permisos** esté seleccionado y seleccione **Agregar permisos**.

3. En la hoja **Agregar permisos**: 
    
    - Para el grupo interno: seleccione **Examinar directorio** para seleccionar el grupo, que debe estar habilitado para correo electrónico.
    
    - Para todos los usuarios de la primera organización : seleccione **Escribir detalles** y escriba el nombre de un dominio en el inquilino de la organización. Por ejemplo, fabrikam.com.
    
    - Para el grupo de la segunda organización externa: aún en la pestaña **Escribir detalles**, escriba la dirección de correo electrónico del grupo en el inquilino de la organización. Por ejemplo, sales@contoso.com.
    
    - Para el usuario que no tiene una cuenta de Azure AD: aún en la pestaña **Escribir detalles**, escriba la dirección de correo electrónico del usuario. Por ejemplo, bengi.turan@gmail.com. 

4. Para conceder los mismos permisos a todos los usuarios: para **Elección de permisos a partir de valores predeterminados**, seleccione **Copropietario**, **Coautor**, **Revisor** o **Personalizado** para seleccionar los permisos que quiera conceder.
    
    Por ejemplo, los permisos configurados podrían ser similares a lo siguiente:
        
    ![Configuración de permisos para colaborar de forma segura](../media/collaboration-permissions.png)

5. Haga clic en **Aceptar** en la hoja **Agregar permisos**.

6. En la hoja **Protección**, haga clic en **Aceptar**.

7. En la hoja **Etiqueta**, seleccione **Guardar**. 

## <a name="applying-the-label-that-supports-secure-collaboration"></a>Aplicación de la etiqueta que admite la colaboración segura

Ahora que se ha configurado esta etiqueta, se puede aplicar a los documentos de varias maneras, como las siguientes:

|Diferentes formas de aplicar la etiqueta|Más información|
|---------------|----------|
|Un usuario selecciona manualmente la etiqueta cuando se crea el documento en su aplicación de Office.|Los usuarios seleccionan la etiqueta del botón **Proteger** en la cinta de Office, o en la barra de Azure Information Protection.|
|Se pedirá a los usuarios que seleccionen una etiqueta cuando se guarde un nuevo documento.|Ha configurado un [valor de directiva](../deploy-use/configure-policy-settings.md) de Azure Information Protection denominado **All documents and emails must have a label** (Todos los documentos y correos electrónicos deben tener una etiqueta).|
|Un usuario comparte el documento por correo electrónico y selecciona manualmente la etiqueta en Outlook.|Los usuarios seleccionan la etiqueta del botón **Proteger** en la cinta de Office, o en la barra de Azure Information Protection, y el documento adjunto se protege automáticamente con la misma configuración.|
|Un administrador aplica la etiqueta al documento mediante el uso de PowerShell.|Use el cmdlet [Set-AIPFileLabel](/powershell/module/azureinformationprotection/set-aipfilelabel) para aplicar la etiqueta a un documento específico o a todos los documentos de una carpeta.|
|Además, ha configurado la etiqueta para aplicar la clasificación automática que ahora se puede aplicar mediante el examen de Azure Information Protection, o mediante PowerShell.|Vea [Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection](../deploy-use/configure-policy-classification.md).|

Para completar este tutorial, aplique manualmente la etiqueta cuando cree el documento en su aplicación de Office: 

1. En un equipo cliente, si ya tiene abierta su aplicación de Office, primero ciérrela y vuelva a abrirla para obtener los últimos cambios de directiva que incluyen la etiqueta recién configurada. 

2. Aplique la etiqueta a un documento y guárdela.

Comparta el documento protegido adjuntándolo a un correo electrónico, y envíelo a las personas que haya autorizado a modificar el documento de envío.

## <a name="opening-and-editing-the-protected-document"></a>Apertura y modificación del documento protegido

Cuando los usuarios a los que haya autorizado abran el documento para su edición, este se abre con un banner informativo que les informa de que los permisos están restringidos. Por ejemplo:

![Banner informativo de ejemplo sobre permisos de Azure Information Protection](../media/example-restricted-access-banner.png)

Si seleccionan el botón **Ver permiso**, verán los permisos que tienen. En el ejemplo siguiente, el usuario puede ver y editar el documento:

![Cuadro de diálogo de ejemplo sobre permisos de Azure Information Protection](../media/example-permisisons-popup.png)

Nota: Si el documento se abre por usuarios externos que también usan Azure Information Protection, la aplicación de Office no muestra la etiqueta de clasificación para el documento, aunque permanecen las marcas visuales de la etiqueta. En su lugar, los usuarios externos pueden aplicar su propia etiqueta en consonancia con la taxonomía de clasificación de su organización. Si estos usuarios externos le devuelven a continuación el documento editado, Office muestra la etiqueta de clasificación original cuando vuelva a abrir el documento.

Antes de que el documento protegido se abra, tiene lugar uno de los siguientes flujos de autenticación:

- En el caso de los usuarios que tienen una cuenta de Azure AD, estos usan sus credenciales de Azure AD para autenticarse mediante Azure AD y el documento se abre. 

- En el caso de los usuarios que no tienen una cuenta de Azure AD, si no han iniciado sesión en Office con una cuenta que tenga permisos para abrir el documento, ven la página **Cuentas**. 
    
   En la página **Cuentas**, seleccione **Agregar cuenta**:
   
    ![Adición de una cuenta Microsoft para abrir el documento protegido](../media/add-account-msa.png)

   En la página **Iniciar sesión**, seleccione **Crear uno** y siga las indicaciones para crear una nueva cuenta Microsoft con la dirección de correo electrónico que se usó para conceder los permisos:
    
    ![Creación de una cuenta Microsoft para abrir el documento protegido](../media/create-account-msa.png)
    
    Cuando se crea la nueva cuenta Microsoft, la cuenta local cambia a esta nueva cuenta de Microsoft y el usuario puede entonces abrir el documento.


### <a name="supported-scenarios-for-opening-protected-documents"></a>Escenarios admitidos para abrir documentos protegidos

En la siguiente tabla se resumen los distintos métodos de autenticación que se admiten para ver y editar documentos protegidos.

Además, los siguientes escenarios admiten la visualización de documentos:

- El visor de Azure Information Protection para Windows, y para iOS y Android, puede abrir archivos mediante una cuenta Microsoft. 

- Un explorador puede abrir archivos adjuntos protegidos cuando se usan proveedores sociales y códigos de acceso de un solo uso para la autenticación con Exchange Online y las nuevas funcionalidades de Office 365 Message Encryption. 

|Plataformas para ver y editar documentos: <br />Word, Excel, PowerPoint|Método de autenticación:<br />Azure AD|Método de autenticación:<br />Cuenta de Microsoft|
|---------------|----------|-----------|-----------|
|Windows|Sí [[1]](#footnote-1)|Sí [[2]](#footnote-2)|
|iOS|Sí [[1]](#footnote-1)|No|
|Android|Sí [[1]](#footnote-1)|No|
|MacOS|Sí [[1]](#footnote-1)|No|

###### <a name="footnote-1"></a>Nota al pie 1
Admite cuentas de usuario, grupos habilitados para correo electrónico, todos los miembros. Las cuentas de usuario y los grupos habilitados para correo electrónico pueden incluir las cuentas de invitado. Todos los miembros excluyen las cuentas de invitado.

###### <a name="footnote-2"></a>Nota al pie 2
Compatible actualmente solo con Hacer clic y ejecutar de Office 2016.




## <a name="next-steps"></a>Pasos siguientes

Consulte otras [configuraciones de ejemplo](../deploy-use/configure-policy-protection.md#example-configurations) de etiquetas para aplicar la protección a los escenarios comunes. Este artículo también contiene información más detallada acerca de la configuración de la protección.

Para obtener más información sobre las otras opciones y parámetros que puede configurar para la etiqueta, vea [Configuración de la directiva de Azure Information Protection](../deploy-use/configure-policy.md). 

La etiqueta que se configuró en este artículo también crea una plantilla de protección con el mismo nombre. Si tiene aplicaciones y servicios que se integran con plantillas de protección de Azure Information Protection, pueden aplicar esta plantilla. Por ejemplo, soluciones de DLP y reglas de flujo de correo electrónico. Outlook en la web muestra automáticamente las plantillas de protección de la directiva global de Azure Information Protection. 




