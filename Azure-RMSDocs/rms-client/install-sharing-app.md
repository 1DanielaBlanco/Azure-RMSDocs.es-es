---
title: Descarga e instalación de la aplicación RMS sharing - AIP
description: Instrucciones para instalar interactivamente la aplicación RMS sharing para Windows, por lo que se pueden compartir documentos con otros de manera segura.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 139198780f5a83b1336715dccf8540c2962cda00
ms.sourcegitcommit: d06594550e7ff94b4098a2aa379ef2b19bc6123d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2018
ms.locfileid: "53023332"
---
# <a name="download-and-install-the-rights-management-sharing-application"></a>Descargar e instalar la aplicación de uso compartido de Rights Management

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

> [!IMPORTANT]
> **Finalización de notificación de compatibilidad**: la aplicación Rights Management sharing para Windows se va a sustituir por el [cliente de Azure Information Protection](aip-client.md). La aplicación anterior dejará de ser compatible el 31 de enero de 2019.

No hace falta que sea un administrador local para instalar la aplicación RMS sharing. Sin embargo, si no lo es y usa Office 2010, hay algunas limitaciones. Para más información, consulte la sección [Si no es un administrador local y usa Office 2010](#if-you-are-not-a-local-administrator-and-use-office-2010) de esta página.

## <a name="to-download-and-install-the-rights-management-sharing-application"></a>Para descargar e instalar la aplicación Rights Management sharing

1.  Vaya a la página de [Microsoft Rights Management](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

2.  En la sección **Equipos** , haga clic en el icono de la **aplicación RMS para Windows** y guarde el archivo **Setup.exe** para instalar la aplicación Microsoft Rights Management sharing.

3.  Haga doble clic en el archivo Setup.exe que se descargó. Si el sistema le pregunta si desea continuar, haga clic en **Sí**.

4.  En la página **Instalar Microsoft RMS** , haga clic en **Siguiente**y espere a que finalice la instalación.

    > [!NOTE]
    > La aplicación RMS sharing requiere Microsoft .NET Framework, versión mínima 4.0. El programa de instalación comprueba si está instalado y, si no es así, verá un mensaje con un vínculo para instalarlo.

5.  Cuando finalice la instalación, haga clic en **Reiniciar** para reiniciar el equipo y completar la instalación. O bien, haga clic en **Cerrar** y reinicie el equipo más tarde para completar la instalación.

Ahora ya puede empezar a proteger sus archivos o a leer los archivos protegidos por otros usuarios.

## <a name="if-you-are-not-a-local-administrator-and-use-office-2010"></a>Si no es un administrador local y usa Office 2010
Si inicia sesión en el equipo y no tiene derechos administrativos locales y el programa de instalación detecta que tiene instalado Office 2010, verá un mensaje de advertencia en el que se le indicará que algunos escenarios no funcionarán con tal configuración. Los escenarios son los siguientes:

-   Si su organización usa el servicio Azure Rights Management de Azure Information Protection en lugar de la versión local de Rights Management:

    -   Las características de Information Rights Management (IRM) de Office no estarán disponibles. Por ejemplo, la opción **No reenviar** de los mensajes de correo electrónico y los permisos **Restringir acceso** que puede establecer desde el menú **Archivo** de Word y Excel. Puede usar la opción Uso compartido protegido de la cinta y las opciones del botón derecho del Explorador de archivos.

-   Si su organización usa una versión local de Rights Management en lugar del servicio Azure Rights Management de Azure Information Protection:

    -   No podrá leer un documento protegido que le envíe alguien de otra organización que use el servicio Azure Rights Management.

Si no es un administrador local y usa Office 365 u Office 2013, no verá este mensaje y se admitirán estos escenarios.

Puede continuar la instalación con estas limitaciones conocidas. Asimismo, puede detener la instalación y volver a ejecutarla con la opción **Ejecutar como administrador** al ejecutar Setup.exe en el paso 3, o bien pedirle a un administrador que se lo instale. Los administradores pueden [crear un script para esta instalación](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application) para que se instale automáticamente.

## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)

