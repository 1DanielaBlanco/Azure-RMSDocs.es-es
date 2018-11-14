---
title: 'Preguntas frecuentes y problemas conocidos: SDK de Microsoft Information Protection.'
description: Preguntas frecuentes sobre el SDK de Microsoft Information Protection (MIP) y guía para la solución de problemas y errores.
author: BryanLa
ms.service: information-protection
ms.topic: troubleshooting
ms.date: 10/19/2018
ms.author: bryanla
ms.openlocfilehash: f213b31d9b0e41ea9c1e076055a90e9f62b31b3a
ms.sourcegitcommit: fa0be701b85b1fba5e75428714bb4525dd739a93
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51223932"
---
# <a name="microsoft-information-protection-mip-sdk-faqs-and-issues"></a>Preguntas frecuentes y problemas del SDK de Microsoft Information Protection (MIP)

En este artículo se ofrecen respuestas a las preguntas frecuentes y una guía para la solución de problemas conocidos y errores comunes.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes 

### <a name="question-which-platforms-are-supported-by-the-mip-sdk"></a>Pregunta: ¿Qué plataformas son compatibles con el SDK de MIP?

El SDK de MIP es compatible en las siguientes plataformas:

[!INCLUDE [MIP SDK platform support](../include/mip-sdk-platform-support.md)]

### <a name="question-how-does-the-sdk-handle-strings-and-what-string-type-should-i-be-using-in-my-code"></a>Pregunta: ¿Cómo trata el SDK las cadenas y qué tipo de cadena se debe usar en mi código?

El SDK está pensado para un uso multiplataforma y utiliza [UTF-8 (Unicode Transformation Format - 8 bits)](https://wikipedia.org/wiki/UTF-8) para el tratamiento de cadenas. Las instrucciones específicas dependen de la plataforma que se esté usando:

| Plataforma | Instrucciones |
|-|-|
| Nativo de Windows | Para los clientes del SDK de C++, el tipo de biblioteca estándar de C++ [`std::string`](https://wikipedia.org/wiki/C%2B%2B_string_handling) se utiliza para pasar cadenas a o desde funciones de API. La conversión a o desde UTF-8 se administra internamente con el SDK de MIP. Cuando se devuelve un `std::string` desde una API, debe esperar la codificación UTF-8 y administrarla en consecuencia si se convierte la cadena. En algunos casos, una cadena se devuelve como parte de un vector `uint8_t` (como una licencia de publicación (PL)), pero debe tratarse como un blob opaco.<br><br>Para más información y ejemplos, consulte:<ul><li>[Función WideCharToMultiByte](/windows/desktop/api/stringapiset/nf-stringapiset-widechartomultibyte) para ayudarle a convertir cadenas de caracteres anchos a cadenas de varios bytes, como UTF-8.<li>Los siguientes archivos de ejemplo se incluyen en la [descarga del SDK](setup-configure-mip.md#configure-your-client-workstation):<ul><li>Ejemplo de funciones de utilidad de cadenas en `file\samples\common\string_utils.cpp`, para convertir a cadenas anchas UTF-8 o desde ellas.<li>Una implementación de `wmain(int argc, wchar_t *argv[])` en `file\samples\file\main.cpp`, que utiliza las funciones de conversión de cadena anterior.</li></ul></ul>|
| .NET | Para los clientes del SDK de .NET, todas las cadenas utilizan la codificación UTF-16 predeterminada y no se necesita ninguna conversión especial. La conversión a o desde UTF-16 se administra internamente con el SDK de MIP. |
| Otras plataformas | Todas las demás plataformas que admite el SDK de MIP tienen compatibilidad nativa para UTF-8. |

## <a name="issues-and-errors-reference"></a>Referencia sobre errores y problemas

### <a name="error-file-format-not-supported"></a>Error: "Formato de archivo no admitido"  

| Error | Solución |
|-|-|
|*Formato de archivo no admitido*| Esta excepción se produce al intentar proteger o etiquetar un archivo PDF que se ha firmado digitalmente o se ha protegido con contraseña. Consulte [New support for PDF encryption with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/New-support-for-PDF-encryption-with-Microsoft-Information/ba-p/262757) (Nueva compatibilidad con el cifrado de archivos PDF con Microsoft Information Protection) para obtener más información sobre el cifrado y el etiquetado de archivos PDF.|

### <a name="error-failed-to-parse-the-acquired-compliance-policy"></a>Error: "Failed to parse the acquired Compliance Policy" (No se pudo analizar la directiva de cumplimiento adquirida)  

Ha descargado el SDK de MIP y ha ejecutado las aplicaciones de ejemplo. Utiliza el ejemplo de archivo para enumerar todas las etiquetas, pero obtiene el siguiente error:

| Error | Solución |
|-|-|
|*Something bad happened: Failed to parse the acquired Compliance Policy. Failed with: [class mip::CompliancePolicyParserException] Tag not found: policy, NodeType: 15, Name: No Name Found, Value: , Ancestors: <SyncFile><Content>, correlationId:[34668a40-blll-4ef8-b2af-00005aa674z9]*| Esto indica que no ha migrado la etiquetas de Azure Information Protection a la experiencia de etiquetado unificado. Consulte [Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365](/azure/information-protection/configure-policy-migrate-labels) para migrar las etiquetas, y luego cree una directiva de etiquetas en el Centro de seguridad y cumplimiento de Office 365. Cuando haya terminado, el ejemplo se ejecutará correctamente.|
