---
title: Formatos de archivo compatibles | Azure RMS
description: La versión actual de la API de archivo admite protección nativa para archivos de MS Office, PDF y protección PFile para los demás formatos de archivo.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.service: information-protection
ms.assetid: EC831494-7F2C-4C70-9063-B02CDDEA14EE
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: c429d7fc92916f5fcdd1756774fa981055157151
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42808194"
---
# <a name="supported-file-formats"></a>Formatos de archivo compatibles

La API de archivo admite formatos nativo y Pfile.

## <a name="supported-file-formats"></a>Formatos de archivo compatibles

La versión actual de la API de archivo admite protección nativa para archivos de Microsoft Office, archivos PDF (Portable Document Format) y protección PFile para los demás formatos de archivo. Los archivos PDF pueden tener opcionalmente aplicada protección PFile.

-   **Protección nativa** En la protección nativa, el archivo se cifra en un formato de archivo de AD RMS que se basa en su tipo MIME (extensión de nombre de archivo). Los archivos protegidos de forma nativa con la API de archivo son coherentes con el formato esperado por aplicaciones habilitadas para AD RMS que usen protección nativa; por ejemplo, Office 2013, Office 2010 y FoxIt/PDF Reader. La protección nativa solo se admite en archivos de Office, archivos PDF y un número selecto de otros tipos de archivos. Para más información sobre los tipos de archivo en los que se admite protección nativa, consulte [File API configuration](file-api-configuration.md) (Configuración de la API de archivo).
-   **Protección PFile**. En la protección PFile, los archivos se cifran con formato de archivo de protegido de AD RMS (PFile). El archivo se cifra en un archivo con una extensión de .pfile. La protección PFile se admite para todos los formatos de archivo, excepto archivos de Office.

Los administradores pueden establecer claves del Registro para configurar si los archivos deben protegerse y cómo en función de su extensión de nombre de archivo. Para más información sobre cómo configurar la protección de archivos cuando se utiliza la API de archivos, consulte [File API configuration](file-api-configuration.md) (Configuración de la API de archivo).

## <a name="related-topics"></a>Temas relacionados

* [Notas para el desarrollador](developer-notes.md)
* [File API configuration](file-api-configuration.md) (Configuración de la API de archivo)
 