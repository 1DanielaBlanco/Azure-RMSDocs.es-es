---
title: Tipos de archivos compatibles con Azure Information Protection
description: "Detalles técnicos sobre tipos de archivos, extensiones de nombres de archivos y niveles de protección compatibles para administradores responsables del cliente de Azure Information Protection para Windows."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/06/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4f187b3fa991fb4ed3a11ded34fa663dc6b4bafc
ms.sourcegitcommit: 04eb4990e2bf0004684221592cb93df35e6acebe
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/30/2017
---
<a id="file-types-supported-by-the-azure-information-protection-client" class="xliff"></a>

# Tipos de archivos compatibles con el cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012*

El cliente de protección de Azure Information Protection puede aplicar los siguientes documentos y correos electrónicos:

- Solo confirmación

- Clasificación y protección

- Solo protección

Utilice la siguiente información para comprobar los tipos de archivos compatibles, los diferentes niveles de protección y cómo cambiar el nivel de protección predeterminado y qué archivos se excluyen automáticamente (omiten) de la clasificación y la protección.

<a id="file-types-supported-for-classification-only" class="xliff"></a>

## Tipos de archivos compatibles solo para clasificación

Solo se admite la clasificación para los siguientes tipos de archivo. Hay otros tipos de archivo que admiten la clasificación cuando también están protegidos. Para obtener más información, consulte la sección [Tipos de archivos compatibles para protección y clasificación](#supported-file-types-for-classification-and-protection).

- **Formato de documento portátil de Adobe**: .pdf

- **Microsoft Visio**: .vsdx, .vsdm, .vssx, .vssm, .vsd, .vdw, .vst

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft Office 97, Office 2010, Office 2003**: .xls, .xlt, .doc, .dot, .ppt, .pps, .pot
- **Microsoft XPS**: .xps .oxps

- **Imágenes**: .jpg, .jpe, .jpeg, .jif, .jfif,. jfi.png, .tif, .tiff

- **SolidWorks**: .sldprt, .slddrw, .sldasm

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

<a id="file-types-supported-for-protection" class="xliff"></a>

## Tipos de archivo compatibles para protección

El cliente de Azure Information Protection admite la protección en dos niveles distintos, como se describe en la tabla siguiente.

|Tipo de protección|Nativa|Genérico|
|----------------------|----------|-----------|
|Descripción|Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones compatibles con el servicio de Rights Management, la protección nativa ofrece un fuerte nivel de protección que incluye tanto cifrado como aplicación de derechos (permisos).|Para todas las demás aplicaciones y tipos de archivo, la protección genérica proporciona un nivel de protección que incluye encapsulación de archivos mediante el tipo de archivo .pfile, y autenticación para comprobar si un usuario está autorizado para abrir el archivo.|
|Protección|La protección de los archivos se aplica de las siguientes formas:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que reciben el archivo por correo electrónico o a las que se les concede acceso a él mediante permisos de archivo o recurso compartido.<br /><br />- Además, cuando el contenido se presenta en el visor de Azure Information Protection (en el caso de archivos de texto e imagen protegidos) o en la aplicación asociada (en el caso de todos los demás tipos de archivos admitidos), se aplican completamente los derechos de uso y la directiva definida por el propietario del contenido cuando se protegen los archivos.|La protección de los archivos se aplica de las siguientes formas:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que están autorizadas para abrir el archivo o a las que se les proporciona acceso a él. Si la autorización da error, el archivo no se abre.<br /><br />- Se muestran los derechos de uso y la directiva establecida por el propietario del contenido para informar a los usuarios autorizados de la directiva de uso previsto.<br /><br />- Se genera el registro de auditoría de los usuarios autorizados que abren los archivos y acceden a ellos. Sin embargo, no se aplican derechos de uso.|
|Valor predeterminado para tipos de archivo|Es el nivel predeterminado de protección para los siguientes tipos de archivo:<br /><br />- Archivos de texto e imagen<br /><br />- Archivos de Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato de documento portátil (.pdf)<br /><br />Para obtener más información, consulte la sección siguiente, [Tipos de archivos compatibles para protección y clasificación](#supported-file-types-for-classification-and-protection).|Se trata de la protección predeterminada para todos los demás tipos de archivo (por ejemplo, .vsdx, .rtf, etc.) que no son compatibles con la protección nativa.|

Puede cambiar el nivel de protección predeterminado que el cliente de Azure Information Protection aplica. Puede cambiar el nivel predeterminado de nativo a genérico, de genérico a nativo, e incluso impedir que el cliente de Azure Information Protection aplique protección. Para más información, consulte la sección [Cambio del nivel de protección predeterminado de los archivos](#changing-the-default-protection-level-of-files) de este artículo.

La protección de los datos se puede aplicar automáticamente cuando un usuario selecciona una etiqueta que el administrador ha configurado, o los usuarios pueden especificar su propia configuración personalizada de protección mediante [niveles de permiso](../deploy-use/configure-usage-rights.md#rights-included-in-permissions-levels). 

<a id="file-sizes-supported-for-protection" class="xliff"></a>

### Tamaños de archivo compatibles para protección

Hay tamaños de archivo máximos que el cliente de Azure Information Protection admite para protección.

- **Para archivos de Office:**
    
    |Aplicación de Office|Tamaño de archivo máximo admitido|
    |--------------------------------|-------------------------------------|
    |Word 2007 (solo compatible con AD RMS)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016|32 bits: 512 MB<br /><br />64 bits: 512 MB
    |Excel 2007 (solo compatible con AD RMS)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016|32 bits: 2 GB<br /><br />64 bits: solo limitado por el espacio disponible en disco y la memoria|
    |PowerPoint 2007 (solo compatible con AD RMS)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016|32 bits: solo limitado por el espacio disponible en disco y la memoria<br /><br />64 bits: solo limitado por el espacio disponible en disco y la memoria

- **Para todos los demás archivos**: 1 GB

<a id="supported-file-types-for-classification-and-protection" class="xliff"></a>

### Tipos de archivos compatibles para protección y clasificación

En la tabla siguiente se enumera un subconjunto de tipos de archivos que el cliente de Azure Information Protection admite de forma nativa y que se pueden clasificar. 

Estos tipos de archivo se identifican por separado porque, cuando se protegen de forma nativa, se cambia la extensión del nombre del archivo original y pasan a ser de solo lectura. Tenga en cuenta que, cuando los archivos se protegen de manera genérica, la extensión del nombre de archivo original siempre se cambia a .pfile.

> [!WARNING]
> Si dispone de firewalls, servidores proxy web o software de seguridad que inspeccionan o realizan acciones en función de las extensiones de nombre de archivo, puede que tenga que volver a configurar estos para admitir las nuevas extensiones de nombre de archivo.

|Extensión de nombre de archivo original|Extensión de nombre de archivo con protección|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

En la tabla siguiente se enumeran los tipos de archivos restantes que el cliente de Azure Information Protection admite de forma nativa y que se pueden clasificar. Los reconocerá, ya que se trata de tipos de archivos de las aplicaciones de Microsoft Office. 

En estos archivos, la extensión de nombre de archivo permanece igual después de que el archivo se ha protegido con el servicio de Rights Management.

|Tipos de archivo admitidos por Office|Tipos de archivo admitidos por Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

<a id="changing-the-default-protection-level-of-files" class="xliff"></a>

### Cambio del nivel de protección predeterminado de los archivos
Puede cambiar la manera en que el cliente de Azure Information Protection protege los archivos mediante la modificación del Registro. Por ejemplo, puede forzar que los archivos que admiten la protección nativa estén protegidos de forma genérica por el cliente de Azure Information Protection.

Puede que quiera hacer esto por los siguientes motivos:

- Para asegurarse de que todos los usuarios pueden abrir el archivo si no tienen una aplicación que admite la protección nativa.

- Para tener en cuenta sistemas de seguridad que realizan acciones sobre los archivos por su extensión de nombre de archivo y que se pueden reconfigurar para que tengan en cuenta la extensión de nombre de archivo .pfile pero no para admitir varias extensiones de nombre de archivo para la protección nativa.

De modo similar, puede forzar que el cliente de Azure Information Protection aplique protección nativa a archivos a los que, de forma predeterminada, se les aplicaría protección genérica. Esto podría resultar adecuados si tiene una aplicación que admite las API de RMS, por ejemplo, una aplicación de línea de negocio que han escrito sus desarrolladores internos o una aplicación adquirida a un fabricante de software independiente (ISV).

También puede forzar a que el cliente de Azure Information Protection boquee la protección de los archivos, es decir, que no aplique protección nativa ni protección genérica. Por ejemplo, esto podría ser necesario si tiene una aplicación o un servicio automatizados que deben poder abrir un archivo específico para procesar su contenido. Cuando se bloquea la protección para un tipo de archivo, los usuarios no pueden usar el cliente de Azure Information Protection para proteger un archivo con ese tipo de archivo. Cuando lo intentan, verán un mensaje que dice que el administrador ha impedido la protección y deben cancelar su acción para proteger el archivo.

Para configurar el cliente de Azure Information Protection para aplicar protección genérica a todos los archivos a los que, de forma predeterminada, se les aplicaría protección nativa, realice las siguientes modificaciones en el Registro. Tenga en cuenta que si la clave FileProtection no existe, debe crearla manualmente.

1. Cree una clave con el nombre * para la ruta de registro siguiente, de modo que se muestren archivos con cualquier extensión de nombre de archivo:
    
    - Para la versión de 32 bits de Windows: **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection**
    
    - Para la versión de 64 bits de Windows: **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection**

2. En la clave recién agregada (por ejemplo, HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\\\*), cree un valor de cadena (REG_SZ) con el nombre **Encryption** que tenga el valor de datos de **Pfile**.

    Esta configuración permite que el cliente de Azure Information Protection aplique protección genérica.

Estas dos configuraciones permiten que el cliente de Azure Information Protection aplique protección genérica a todos los archivos que tiene una extensión de nombre de archivo. Si éste es su objetivo, no es necesario configurar nada más. Sin embargo, puede definir excepciones para tipos de archivo específicos para que sigan estando protegidos de forma nativa. Para ello, debe realizar tres modificaciones adicionales en el Registro para cada tipo de archivo:

1. Para **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection** (versión de 32 bits de Windows) o **HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\MSIPC\FileProtection** (versión de 64 bits de Windows): agregue una clave nueva con el nombre de la extensión de nombre de archivo (sin el punto anterior).

    Por ejemplo, para los archivos que tienen una extensión .docx, cree una clave denominada **DOCX**.

2. En la clave de tipo de archivo recién creada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), cree un nuevo valor DWORD denominado **AllowPFILEEncryption** que tenga un valor de **0**.

3. En la clave de tipo de archivo recién agregada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\FileProtection\DOCX**), cree un nuevo valor de cadena denominado **Encryption** que tenga un valor de **Native**.

Como resultado de esta configuración, todos los archivos están protegidos genéricamente, excepto los archivos que tienen una extensión de nombre de archivo .docx, que están protegidos de forma nativa por el cliente de Azure Information Protection.

Repita estos tres pasos con otros tipos de archivos que quiera definir como excepciones porque admiten la protección nativa y no quiere que el cliente de Azure Information Protection los proteja de forma genérica.

Puede realizar modificaciones parecidas en el Registro para otras situaciones cambiando el valor de la cadena **Encryption** que admite los siguientes valores:

- **Pfile**: Protección genérica

- **Native**: Protección nativa

- **Off**: Bloquear protección

Para más información, vea [Configuración de la API de archivo](../develop/file-api-configuration.md) en la guía del desarrollador. En esta documentación para desarrolladores, se hace referencia a la protección genérica como "PFile". 

<a id="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-client" class="xliff"></a>

## Tipos de archivos que están excluidos de la clasificación y la protección con el cliente de Azure Information Protection

Para ayudar a impedir que los usuarios modifiquen los archivos que son fundamentales para las operaciones del equipo, se excluyen automáticamente algunos tipos de archivos y carpetas de la clasificación y la protección. Si los usuarios intentan clasificar o proteger estos archivos, aparecerá un mensaje para indicar que están excluidos.

- **Tipos de archivos excluidos**: .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb y .jar

- **Carpetas excluidas**: 
    - Windows
    - Archivos de programa (\Archivos de programa y \Archivos de programa (x86))
    - \ProgramData 
    - \AppData (de todos los usuarios)


<a id="next-steps" class="xliff"></a>

## Pasos siguientes
Ahora que ha identificado los tipos de archivos compatibles con el cliente de Azure Information Protection, vea la siguiente información adicional que puede necesitar para la compatibilidad con este cliente:

- [Customizations](client-admin-guide-customizations.md) (Personalizaciones)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
