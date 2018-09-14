---
title: Descarga e instalación del cliente de Azure Information Protection
description: Instrucciones para que los usuarios instalen el cliente de Azure Information Protection para Windows de forma que puedan clasificar y proteger sus documentos y correos electrónicos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/31/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: be7ae3dd29034813e9b0b4475407f68c8685c167
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44147937"
---
# <a name="user-guide-download-and-install-the-azure-information-protection-client"></a>Guía del administrador: Descarga e instalación del cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8 y Windows 7 con SP1*

Si el administrador no instala el cliente de Azure Information Protection para los usuarios, estos pueden hacerlo por su cuenta. Debe ser un administrador local para que el equipo instale este cliente para que pueda etiquetar y proteger sus documentos y correos electrónicos.

Además:

- El cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo.

- Si tiene Windows 7 SP1, el cliente de Azure Information Protection necesita una actualización específica: KB 2533623. Si su equipo necesita esta actualización pero no está instalada, la instalación se completa con un mensaje que indica que el cliente de Azure Information Protection requiere esta actualización. No podrá usar todas las características del cliente de Azure Information Protection hasta que instale la actualización. 

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Para descargar e instalar el cliente de Azure Information Protection    

1.  Vaya a la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.

    Esta página tiene vínculos para todos los dispositivos conocidos que puede utilizar, por lo que puede descargar fácilmente una aplicación de visor si fuera necesaria para abrir archivos protegidos. Si no es un administrador local de su PC, puede instalar la aplicación del visor para Windows. No obstante, estas instrucciones van a instalar el cliente completo, lo que permite etiquetar y proteger los archivos. 

2. Busque la sección **Cliente de Azure Information Protection** y haga clic en el icono de Windows. Haga clic en **Descargar** y guarde el archivo **AzInfoProtection.exe**.     

3. Ejecute el archivo ejecutable que se ha descargado. Si el sistema le pregunta si desea continuar, haga clic en **Sí**.    

4. En la página **Instalar el cliente de Azure Information Protection**:     
    - Si no puede conectarse a la nube, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.    

    - Cuando haya leído los términos de licencia y las condiciones, haga clic en **Acepto**.    

5. Si se le pregunta si desea continuar, haga clic en **Sí** y espere a que finalice la instalación.    

6. Haga clic en **Cerrar**. Antes de empezar a usar el cliente de Azure Information Protection, siga estas recomendaciones:    

    - Si su equipo ejecuta Office 2010, reinicie el equipo y, a continuación, vaya a la sección siguiente para proceder con el paso final.    
        
    - Para otras versiones de Office, reinicie todas las aplicaciones de Office y todas las instancias del Explorador de archivos. La instalación está completa y ahora puede usar el cliente para etiquetar y proteger sus documentos y correos electrónicos.    

### <a name="installing-the-azure-information-protection-client-with-office-2010"></a>Instalación del cliente de Azure Information Protection con Office 2010    
Una vez instalado el cliente de Azure Information Protection siguiendo las instrucciones anteriores:    

1. Abra Microsoft Word. Si es la primera vez que ejecuta una aplicación de Office 2010 después de haber instalado el cliente de Azure Information Protection, verá un cuadro de diálogo de **Microsoft Azure Information Protection**. En este cuadro de diálogo se indica que se necesitan las credenciales de administrador para completar el proceso de inicio de sesión.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Aceptar**.

3. Si ve un cuadro de diálogo **Control de acceso de usuarios**, haga clic en **Sí** para que el cliente de Azure Information Protection pueda actualizar el Registro.

La instalación está completa y puede utilizar Azure Information Protection para etiquetar y proteger sus documentos y correos electrónicos.

## <a name="other-instructions"></a>Otras instrucciones    
Puede encontrar más instrucciones sobre procedimientos en la guía del usuario de Azure Information Protection:

- [¿Qué desea hacer?](client-user-guide.md#what-do-you-want-to-do)

## <a name="additional-information-for-administrators"></a>Información adicional para los administradores    
Consulte [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide-install.md) en la [guía del administrador](client-admin-guide.md).
 
  
