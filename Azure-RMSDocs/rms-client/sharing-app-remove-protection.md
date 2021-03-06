---
title: Retirada de protección mediante la aplicación RMS sharing - AIP
description: Instrucciones para quitar la protección (es decir, desproteger) de un archivo protegido anteriormente con la aplicación RMS sharing.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: da95b938-eaad-4c83-a21e-ff1d4872aae4
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 871a9c34e3b02fcf1e7295228d1c79f9840f719b
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151601"
---
# <a name="remove-protection-from-a-file-by-using-the-rights-management-sharing-application"></a>Quitar la protección de un archivo mediante la aplicación Rights Management sharing

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

Para quitar la protección (es decir, desproteger) de un archivo protegido anteriormente con la aplicación de RMS sharing, use la opción **Quitar protección** en el Explorador de archivos.

> [!IMPORTANT]
> Debe ser propietario del archivo para quitar la protección.

## <a name="to-remove-protection-from-a-file"></a>Para quitar la protección de un archivo

1.  En el Explorador de archivos, haga clic con el botón derecho en el archivo (por ejemplo, Sample.ptxt), seleccione **Proteger con RMS**, haga clic en **Proteger en contexto** y, luego, en **Quitar protección**:

    ![Opción de menú Quitar protección para la aplicación RMS sharing](../media/ADRMS_MSRMSApp_RemoveProtection.png)

    Puede que se le soliciten las credenciales.

Nota: Si no ve estas opciones, es probable que la aplicación RMS sharing no esté instalada en el equipo, que no esté instalada la última versión o que el equipo deba reiniciarse para completar la instalación. Para más información sobre cómo instalar la aplicación de uso compartido, consulte [Descarga e instalación de la aplicación Rights Management sharing](install-sharing-app.md).

El archivo protegido original se elimina (por ejemplo, Sample.ptxt) y se reemplaza con un archivo que tiene el mismo nombre pero la extensión de nombre de archivo desprotegido (por ejemplo, Sample.txt).

## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)
