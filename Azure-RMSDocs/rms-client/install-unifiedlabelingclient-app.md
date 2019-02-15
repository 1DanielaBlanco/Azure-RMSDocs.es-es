---
title: Descarga e instalación del cliente de etiquetado unificado de Azure Information Protection (versión preliminar)
description: Instrucciones para que los usuarios instalen la versión preliminar del cliente de etiquetado unificado de Azure Information Protection para Windows a fin de clasificar y proteger los documentos y correos electrónicos.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 10/17/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 2bf09690-9dba-43b7-9e0a-0110915d4081
ms.reviewer: eymanor
ms.suite: ems
ms.openlocfilehash: 6ee27b9aedd35ae135fc7150a3211be43ca2f092
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56250901"
---
# <a name="download-and-install-the-azure-information-protection-unified-labeling-client-preview"></a>Descarga e instalación del cliente de etiquetado unificado de Azure Information Protection (versión preliminar)

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1*

> [!NOTE]
> Este cliente está en versión preliminar y sujeto a cambios. Usa el almacén de etiquetado unificado y descarga la directiva con etiquetas de confidencialidad del Centro de seguridad y cumplimiento de Office 365. Para usar estas etiquetas, primero deben publicarse desde el Centro de seguridad y cumplimiento. [Más información](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492)

Debe ser administrador local del equipo para instalar este cliente de versión preliminar para que pueda etiquetar y proteger los documentos y correos electrónicos.

Además:

- El cliente de etiquetado unificado de Azure Information Protection requiere una versión mínima de Microsoft .NET Framework 4.6.2 y, en su defecto, el instalador intenta descargar e instalar este requisito previo. Cuando este requisito previo se instala como parte de la instalación de cliente, es necesario reiniciar el equipo.

- Si tiene Windows 7 SP1, el cliente de etiquetado unificado de Azure Information Protection necesita una actualización específica: KB 2533623. Si el equipo necesita esta actualización pero no está instalada, la instalación finaliza con un mensaje que indica que el cliente de etiquetado unificado de Azure Information Protection requiere esta actualización. Hasta que la actualización no se instala, no se pueden usar todas las características del cliente de etiquetado unificado de Azure Information Protection. 

## <a name="to-download-and-install-the-azure-information-protection-unified-labeling-client"></a>Para descargar e instalar el cliente de etiquetado unificado de Azure Information Protection

Antes de instalar el cliente de etiquetado unificado de Azure Information Protection, confirme que tenga etiquetas de confidencialidad del Centro de seguridad y cumplimiento de Office 365 publicadas para los usuarios. 

Si tiene etiquetas publicadas de Azure Portal para Azure Information Protection, puede [migrar dichas etiquetas](../configure-policy-migrate-labels.md) al Centro de seguridad y cumplimiento.

1. Descargue el cliente de versión preliminar desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=57440).

2. Ejecute el archivo ejecutable que se ha descargado, **AzInfoProtection_For_Unified_Labeling.exe**. Si el sistema le pregunta si desea continuar, haga clic en **Sí**.    

3. En la página **Instalar el cliente de Azure Information Protection**:     
    - Si no puede conectarse a la nube, pero desea ver y experimentar el lado cliente de Azure Information Protection mediante una directiva local con fines de demostración, seleccione la opción para instalar una directiva de demostración. Cuando el cliente se conecte al Centro de seguridad y cumplimiento de Office 365, esta directiva de demostración se sustituirá por la directiva de etiquetas de la organización.

    - Cuando haya leído los términos de licencia y las condiciones, haga clic en **Acepto**.    

4. Si se le pregunta si desea continuar, haga clic en **Sí** y espere a que finalice la instalación.    

6. Haga clic en **Cerrar**. Antes de empezar a usar el cliente de etiquetado unificado de Azure Information Protection:    

    - Si su equipo ejecuta Office 2010, reinicie el equipo y, a continuación, vaya a la sección siguiente para proceder con el paso final.    
        
    - Para otras versiones de Office, reinicie todas las aplicaciones de Office y todas las instancias del Explorador de archivos. La instalación está completa y ahora puede usar el cliente para etiquetar y proteger sus documentos y correos electrónicos.    

### <a name="installing-the-azure-information-protection-unified-labeling-client-with-office-2010"></a>Instalación del cliente de etiquetado unificado de Azure Information Protection con Office 2010

Una vez instalado el cliente de etiquetado unificado de Azure Information Protection con las instrucciones anteriores:

1. Abra Microsoft Word. Si es la primera vez que ejecuta una aplicación de Office 2010 después de haber instalado el cliente de Azure Information Protection, verá un cuadro de diálogo de **Microsoft Azure Information Protection**. En este cuadro de diálogo se indica que se necesitan las credenciales de administrador para completar el proceso de inicio de sesión.

2. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Aceptar**.

3. Si ve un cuadro de diálogo **Control de acceso de usuarios**, haga clic en **Sí** para que el cliente de Azure Information Protection pueda actualizar el Registro.

La instalación ya ha finalizado y puede usar el cliente de etiquetado unificado de Azure Information Protection para etiquetar y proteger los documentos y correos electrónicos.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre el almacén de etiquetado unificado que el Centro de seguridad y cumplimiento de Office 365 usa ahora, lea la entrada de blog siguiente: [Announcing the availability of unified labeling management in the Security & Compliance Center](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Announcing-the-availability-of-unified-labeling-management-in/ba-p/262492) (Anuncio de la disponibilidad de la administración de etiquetado unificado en el Centro de seguridad y cumplimiento).

