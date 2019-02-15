---
title: Configuración de la API de archivo | Azure RMS
description: El comportamiento de la API de archivo puede configurarse a través de los valores del Registro.
keywords: ''
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 10/11/2017
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 930878C2-D2B4-45F1-885F-64927CEBAC1D
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: a46a270780fe6245adf14b950833d6f6277f1b35
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253032"
---
# <a name="file-api-configuration"></a>Configuración de la API de archivo


El comportamiento de la API de archivo puede configurarse a través de los valores del Registro.

La API de archivo proporciona dos tipos de protección: protección nativa y protección PFile.

-   **Protección nativa**: el archivo está protegido en un formato de AD RMS según su tipo MIME (extensión de nombre de archivo).
-   **Protección PFile**: el archivo está protegido en el formato de archivo protegido (PFile) de AD RMS.

Para obtener más información sobre los formatos de archivo compatibles, consulte **API de archivo: detalles sobre la compatibilidad de archivos** en este artículo.

## <a name="keykey-value-types-and-descriptions"></a>Tipos y descripciones de las claves y los valores de clave

En las secciones siguientes se describen las claves y los valores de clave que controlan el cifrado.

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection`

**Tipo**: Key

**Descripción**: contiene la configuración general de la API de archivo.

### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>`

**Tipo**: Key

**Descripción**: especifica la información de configuración de una extensión de archivo específica, como TXT, JPG, etc.

- Se permite el carácter comodín "*", pero la configuración de una extensión específica tiene prioridad sobre la configuración del comodín. El carácter comodín no afecta a la configuración de los archivos de Microsoft Office. Dichos archivos deben deshabilitarse explícitamente por tipo de archivo.
- Para especificar archivos que no tienen extensión, use ".".
- No especifique el carácter "." al especificar la clave de una extensión de archivo concreta. Por ejemplo, use `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\TXT` para especificar la configuración de los archivos .txt. (No use `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\.TXT`).

Para especificar el comportamiento de protección, establezca el valor **Encryption** en la clave. Si no se establece el valor **Encryption**, se observa el comportamiento predeterminado del tipo de archivo.


### `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\<EXT>\Encryption*`

**Tipo**: REG_SZ

**Descripción**: contiene uno de estos tres valores:

- **Desactivada**: el cifrado está deshabilitado.

> [!Note]
> Esta configuración no afecta al descifrado. Es posible descifrar cualquier archivo cifrado con la protección nativa o con la protección PFile, siempre y cuando el usuario tenga el derecho **EXTRACT**.

- **Nativa**:  se usa el cifrado nativo. En el caso de los archivos de Office, el archivo cifrado tendrá la misma extensión que el archivo original. Por ejemplo, un archivo con la extensión .docx se cifrará en un archivo con la extensión .docx. En el caso de otros archivos que puedan tener aplicada la protección nativa, se cifrarán en un archivo con una extensión del formato p*zzz*, donde *zzz* es la extensión de archivo original. Por ejemplo, los archivos .txt se cifrarán en un archivo con una extensión .ptxt. A continuación se incluye una lista de extensiones de archivo que pueden tener aplicada la protección nativa.

- **Pfile**: se usa el cifrado PFile. El archivo cifrado tendrá anexado .pfile a la extensión original. Por ejemplo, después del cifrado, un archivo .txt tendrá una extensión .txt.pfile.


> [!Note]
> Esta configuración no afecta a los formatos de archivo de Office. Por ejemplo, si el valor `HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX\Encryption` se establece en &quot;Pfile", los archivos .docx seguirán cifrándose con la protección nativa y el archivo cifrado seguirá teniendo una extensión .docx.

Si se establece otro valor o si no se establece ningún valor, el resultado será el comportamiento predeterminado.

## <a name="default-behavior-for-different-file-formats"></a>Comportamiento predeterminado de los diferentes formatos de archivo

-   **Archivos de Office** Está habilitado el cifrado nativo.
-   **Archivos txt, xml, jpg, jpeg, pdf, png, tiff, bmp, gif, giff, jpe, jfif, jif** Está habilitado el cifrado nativo (xxx se convierte en pxxx).
-   **Todos los demás archivos** Está habilitado el cifrado de archivo protegido (pfile) (xxx se convierte en xxx.pfile).

Si se intenta cifrar un tipo de archivo que está bloqueado, se produce el error [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx).

### <a name="file-api---file-support-details"></a>API de archivo: detalles sobre la compatibilidad de archivos

Puede agregarse compatibilidad nativa para cualquier tipo de archivo (extensión). Por ejemplo, en el caso de cualquier extensión &lt;ext&gt; (que no es de Office), se usará \*.p&lt;ext&gt; si la configuración de administración de esa extensión es "NATIVE".

**Archivos de Office**

-   Extensiones de archivo: doc, dot, xla, xls, xlt, pps, ppt, docm, docx, dotm, dotx, xlam, xlsb, xlsm, xlsx, xltm, xltx, xps, potm, potx, ppsx, ppsm, pptm, pptx, thmx, vsdx, vsdm, vssx, vssm, vstx y vstm. 
-   Tipo de protección = nativa (valor predeterminado): sample.docx se cifra en sample.docx.
-   Tipo de protección = Pfile: en el caso de los archivos de Office, tiene el mismo efecto que la protección nativa.
-   Desactivado: deshabilita el cifrado.

**Archivos PDF**

-   Tipo de protección = nativa: sample.pdf se cifra y se denomina sample.ppdf.
-   Tipo de protección = PFile: sample.pdf se cifra y se denomina sample.pdf.pfile.
-   Desactivado: deshabilita el cifrado.

**Todos los demás formatos de archivo**

-   Tipo de protección = PFile: sample.*zzz* se cifra y se denomina sample.*zzz*.pfile, donde *zzz* es la extensión de archivo original.
-   Desactivado: deshabilita el cifrado.

### <a name="examples"></a>Ejemplos

Las opciones siguientes permiten el cifrado PFile de archivos txt. A los archivos de Office se les aplicará la protección nativa (de forma predeterminada), a los archivos txt se les aplicará la protección PFile y a los demás archivos se les bloqueará la protección (de forma predeterminada).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               txt
                  Encryption = Pfile
```

Las opciones siguientes permiten el cifrado PFile de todos los archivos que no sean de Office, excepto los archivos txt. A los archivos de Office se les aplicará la protección nativa (de forma predeterminada), a los archivos txt se les bloqueará la protección y a los demás archivos se les aplicará la protección PFile.

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               *
                  Encryption = Pfile
               txt
                  Encryption = Off
```

Las opciones siguientes deshabilitan el cifrado nativo de archivos docx. A los archivos de Office, excepto los archivos docx, se les aplicará la protección nativa (de forma predeterminada) y a los demás archivos se les bloqueará la protección (de forma predeterminada).

```
HKEY_LOCAL_MACHINE
   Software
      Microsoft
         MSIPC
            FileProtection
               docx
                  Encryption = Off
```

## <a name="related-articles"></a>Artículos relacionados

- [Notas para el desarrollador](developer-notes.md)
- [IPCERROR\_FILE\_ENCRYPT\_BLOCKED](https://msdn.microsoft.com/library/hh535248.aspx)
