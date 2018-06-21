---
title: Tipos de aplicación | Azure RMS
description: En este tema se cubren los tipos de aplicaciones que puede elegir crear como aplicaciones con derechos habilitados.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 97169FC3-1395-4433-A632-7B0F020FABFE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: d25f377f8a3d592ef8af414ab275783c6c614ede
ms.sourcegitcommit: 93124ef58e471277c7793130f1a82af33dabcea9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/11/2018
ms.locfileid: "27765292"
---
# <a name="application-types"></a>Tipos de aplicación


En este tema se cubren los tipos de aplicaciones que puede elegir crear como aplicaciones con derechos habilitados.

Los siguientes tipos de aplicación son compatibles actualmente con Rights Management Services SDK 2.1

## <a name="simple-applications"></a>Aplicaciones sencillas

Una aplicación sencilla podría ser una herramienta de línea de comandos creada para cifrar un archivo proporcionado. Para ver un ejemplo de una aplicación sencilla habilitada para derechos, consulte nuestra implementación de *IPCHelloWorld*, que se describe en [Desarrollo de la aplicación](developing-your-application.md).

### <a name="server-mode-applications"></a>Aplicaciones en modo servidor

El *modo servidor* está pensado para aplicaciones no interactivas que consumen, protegen o procesan contenido con protección de RMS. Un ejemplo sería una aplicación de *prevención de pérdida de datos* que se ejecute como servicio en un servidor de archivos y proteja documentos confidenciales. Consulte [IpcDlp sample](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/IpcDlpApp) (ejemplo IpcDlp) para ver un ejemplo de este tipo de aplicación.

Si su aplicación usa el *modo servidor*, debe autenticarse en el servidor RMS de forma silenciosa. A diferencia del *modo cliente*, RMS SDK 2.1 no abrirá una petición de credenciales si no se autentica de forma silenciosa. Además, al ejecutarse en *modo servidor*, no es necesario ningún manifiesto de aplicación.

Para más información sobre cómo establecer el modo de seguridad de API, consulte [Establecimiento del modo de seguridad de API](setting-the-api-security-mode-api-mode.md).

### <a name="rich-client-applications"></a>Aplicaciones cliente enriquecidas

Una aplicación cliente enriquecida permite a los usuarios ver y manipular datos a través de una interfaz gráfica de usuario (GUI). A menudo, los datos presentados en esta GUI son de gran valor y sensibles al robo o a la exposición accidental. La compatibilidad con la protección de la información suele mejorar los escenarios existentes, pero no es la principal motivación para desarrollar la aplicación.

Usar RMS SDK 2.1 con aplicaciones cliente enriquecidas le ayuda a:

-   Garantizar que estos datos siempre estén cifrados.

-   Impedir que los usuarios extraigan datos a un formato sin protección (por ejemplo, impedir el uso del portapapeles para copiar y pegar).

Microsoft Notepad es una aplicación cliente enriquecida sencilla. Microsoft Office es una aplicación cliente enriquecida más compleja.

Para más información sobre la protección de su aplicación, consulte [Understanding usage restrictions](understanding-usage-restrictions.md) (Descripción de las restricciones de uso).

## <a name="related-topics"></a>Temas relacionados

- [Ejemplo IpcDlp](https://Code.MSDN.Microsoft.Com/IpcDlp-Sample-Application-d30bb99d)
- [Desarrollo de la aplicación](developing-your-application.md)
- [Establecimiento del modo de seguridad de API](setting-the-api-security-mode-api-mode.md)
- [Descripción de las restricciones de uso](understanding-usage-restrictions.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]