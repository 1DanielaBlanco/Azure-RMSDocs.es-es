---
title: "Descarga e instalación del cliente de Azure Information Protection | Azure Information Protection"
description: "Instrucciones para que los usuarios instalen el cliente de Azure Information Protection para Windows de forma que puedan clasificar y proteger sus documentos y correos electrónicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 633f3dfe12828a21943bb5faf6ad9f69b98fc70b
ms.openlocfilehash: 303ca72fa8753e417b4a06b4cad475559295eb2a


---

# <a name="download-and-install-the-azure-information-protection-client"></a>Descarga e instalación del cliente de Azure Information Protection

Si el administrador no instala el cliente de Azure Information Protection para los usuarios, estos pueden hacerlo por su cuenta. Debe ser administrador local del equipo para instalar este cliente. 

Además:

- El cliente de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo.

- Si tiene Windows 7 SP1, el cliente de Azure Information Protection necesita una actualización específica: [KB 2533623](https://support.microsoft.com/kb/2533623). Si su equipo necesita esta actualización pero no está instalada, la instalación se completa, pero aparece un mensaje en el que se indica que debe instalar esta actualización para poder usar todas las características del cliente de Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-client"></a>Para descargar e instalar el cliente de Azure Information Protection    

1.  Vaya a la página [Microsoft Azure Information Protection](https://go.microsoft.com/fwlink/?LinkId=303970) en el sitio web de Microsoft.    
2. Haga clic en el icono de Windows para el **cliente de Azure Information Protection** y guarde el archivo **AzInfoProtection.exe** para instalar el cliente de Azure Information Protection.     

2. Haga doble clic en el archivo ejecutable que se ha descargado. Si el sistema le pregunta si desea continuar, haga clic en **Sí**.    

3. En la página **Instalar el cliente de Azure Information Protection**:     
    - Si no puede conectarse a la nube, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecta a un servicio de Azure Information Protection, esta directiva de demostración se reemplaza por la directiva de Azure Information Protection de su organización.    

    - Cuando haya leído los términos de licencia y las condiciones, haga clic en **Acepto**.    

4. Si se le pregunta si desea continuar, haga clic en **Sí** y espere a que finalice la instalación.    

3. Haga clic en **Cerrar**. Antes de empezar a usar el cliente de Azure Information Protection, siga estas recomendaciones:    

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
Vea [Instalación del cliente de Azure Information Protection para los usuarios](client-admin-guide.md#how-to-install-the-azure-information-protection-client-for-users) en la guía del administrador.
 

[!INCLUDE[Commenting house rules](../includes/houserules.md)]  



<!--HONumber=Feb17_HO2-->


