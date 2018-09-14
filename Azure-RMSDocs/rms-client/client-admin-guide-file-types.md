---
title: Tipos de archivos compatibles con Azure Information Protection
description: Detalles técnicos sobre tipos de archivos, extensiones de nombres de archivos y niveles de protección compatibles para administradores responsables del cliente de Azure Information Protection para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/28/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ''
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 2f96a9c395b2a5df11a05acb4ce7dac0da516164
ms.sourcegitcommit: 26a2c1becdf3e3145dc1168f5ea8492f2e1ff2f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/07/2018
ms.locfileid: "44151833"
---
# <a name="admin-guide-file-types-supported-by-the-azure-information-protection-client"></a>Guía del administrador: Tipos de archivos compatibles con el cliente de Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 8.1, Windows 8, Windows 7 con SP1, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 y Windows Server 2008 R2*

El cliente de protección de Azure Information Protection puede aplicar los siguientes documentos y correos electrónicos:

- Solo confirmación

- Clasificación y protección

- Solo protección

Use la siguiente información para comprobar los tipos de archivos compatibles con Azure Information Protection, los diferentes niveles de protección, cómo cambiar el nivel de protección predeterminado e identificar los archivos que se excluyen (omiten) automáticamente de la clasificación y la protección.

No se admiten ubicaciones de WebDav para los tipos de archivo de la lista.

## <a name="file-types-supported-for-classification-only"></a>Tipos de archivos compatibles solo para clasificación

Los siguientes tipos de archivo se pueden clasificar aunque no estén protegidos.

- **Formato de documento portátil de Adobe**: .pdf

- **Microsoft Project**: .mpp, .mpt

- **Microsoft Publisher**: .pub

- **Microsoft XPS**: .xps .oxps

- **Imágenes**: .jpg, .jpe, .jpeg, .jif, .jfif, .jfi., .png, .tif y .tiff

- **Autodesk Design Review 2013**: .dwfx

- **Adobe Photoshop**: .psd

- **Digital Negative**: .dng

- **Microsoft Office**: tipos de archivo en la tabla siguiente.
    
    Los formatos de archivo compatibles para estos tipos de archivo son los formatos 97-2003 y los formatos Open XML de los siguientes programas de Office: Word, Excel y PowerPoint. A menos que tenga la versión preliminar del cliente de Azure Information Protection, no se admite el formato Documento Open XML estricto.
    
    |Tipo de archivo de Office|Tipo de archivo de Office|
    |----------------------------------|----------------------------------|
    |.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vdw<br /><br />.vsd|.vsdm<br /><br /> .vsdx<br /><br />.vss<br /><br />.vssm<br /><br />.vst<br /><br />.vstm<br /><br />.vssx<br /><br />.vstx<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx|

Otros tipos de archivo admiten la clasificación cuando también están protegidos. Para conocer estos tipos de archivo, vea la sección [Tipos de archivos compatibles para protección y clasificación](#supported-file-types-for-classification-and-protection).

Por ejemplo, en la actual [directiva predeterminada](../configure-policy-default.md), la etiqueta **General** aplica la clasificación pero no la protección. Podría aplicar la etiqueta **General** a un archivo denominado ventas.pdf, pero no a un archivo denominado ventas.txt. 

Además, en la directiva predeterminada actual, **Confidencial\Todos los empleados** aplica la clasificación y la protección. Podría aplicar esta etiqueta a un archivo denominado ventas.pdf y a un archivo denominado ventas.txt. También podría aplicar solamente protección a estos archivos, sin clasificación.

## <a name="file-types-supported-for-protection"></a>Tipos de archivo compatibles para protección

El cliente de Azure Information Protection admite la protección en dos niveles distintos, como se describe en la tabla siguiente.

|Tipo de protección|Nativa|Genérico|
|----------------------|----------|-----------|
|Descripción|Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones compatibles con el servicio de Rights Management, la protección nativa ofrece un fuerte nivel de protección que incluye tanto cifrado como aplicación de derechos (permisos).|Para todas las demás aplicaciones y tipos de archivo, la protección genérica proporciona un nivel de protección que incluye encapsulación de archivos mediante el tipo de archivo .pfile, y autenticación para comprobar si un usuario está autorizado para abrir el archivo.|
|Protección|La protección de los archivos se aplica de las siguientes formas:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que reciben el archivo por correo electrónico o a las que se les concede acceso a él mediante permisos de archivo o recurso compartido.<br /><br />- Además, los derechos de uso y la directiva establecidos por el propietario del contenido cuando se protegieron los archivos se aplican cuando se presenta el contenido en el visor de Azure Information Protection (en el caso de los archivos de texto e imagen protegidos) o en la aplicación asociada (en el caso de los demás tipos de archivo admitidos).|La protección de los archivos se aplica de las siguientes formas:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que están autorizadas a abrir el archivo o a las que se les proporciona acceso a él. Si la autorización da error, el archivo no se abre.<br /><br />- Se muestran los derechos de uso y la directiva establecida por el propietario del contenido para informar a los usuarios autorizados de la directiva de uso previsto.<br /><br />- Se genera el registro de auditoría de los usuarios autorizados que abren los archivos y acceden a ellos. Sin embargo, no se aplican derechos de uso.|
|Valor predeterminado para tipos de archivo|Es el nivel predeterminado de protección para los siguientes tipos de archivo:<br /><br />- Archivos de texto e imagen<br /><br />- Archivos de Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato de documento portátil (.pdf)<br /><br />Para obtener más información, consulte la sección siguiente, [Tipos de archivos compatibles para protección y clasificación](#supported-file-types-for-classification-and-protection).|Se trata de la protección predeterminada para todos los demás tipos de archivo (por ejemplo, .vsdx, .rtf, etc.) que no son compatibles con la protección nativa.|

Puede cambiar el nivel de protección predeterminado que el cliente de Azure Information Protection aplica. Puede cambiar el nivel predeterminado de nativo a genérico, de genérico a nativo, e incluso impedir que el cliente de Azure Information Protection aplique protección. Para más información, consulte la sección [Cambio del nivel de protección predeterminado de los archivos](#changing-the-default-protection-level-of-files) de este artículo.

La protección de los datos se puede aplicar automáticamente cuando un usuario selecciona una etiqueta que el administrador ha configurado, o los usuarios pueden especificar su propia configuración personalizada de protección mediante [niveles de permiso](../configure-usage-rights.md#rights-included-in-permissions-levels). 

### <a name="file-sizes-supported-for-protection"></a>Tamaños de archivo compatibles para protección

Hay tamaños de archivo máximos que el cliente de Azure Information Protection admite para protección.

- **Para archivos de Office:**
    
    |Aplicación de Office|Tamaño de archivo máximo admitido|
    |--------------------------------|-------------------------------------|
    |Word 2007 (solo compatible con AD RMS)<br /><br />Word 2010<br /><br />Word 2013<br /><br />Word 2016|32 bits: 512 MB<br /><br />64 bits: 512 MB
    |Excel 2007 (solo compatible con AD RMS)<br /><br />Excel 2010<br /><br />Excel 2013<br /><br />Excel 2016|32 bits: 2 GB<br /><br />64 bits: solo limitado por el espacio disponible en disco y la memoria|
    |PowerPoint 2007 (solo compatible con AD RMS)<br /><br />PowerPoint 2010<br /><br />PowerPoint 2013<br /><br />PowerPoint 2016|32 bits: solo limitado por el espacio disponible en disco y la memoria<br /><br />64 bits: solo limitado por el espacio disponible en disco y la memoria

- **Para todos los demás archivos**: 
    
    - Para proteger otros tipos de archivo y abrirlos en el visor de Azure Information Protection, el tamaño de archivo máximo está limitado solo por la memoria y el espacio disponible en disco.
    
    - Para desproteger los archivos con el cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile), el tamaño de archivo máximo compatible para los archivos .pst es 5 GB. Los otros tipos de archivo están limitados solo por la memoria y el espacio disponible en disco.

### <a name="supported-file-types-for-classification-and-protection"></a>Tipos de archivos compatibles para protección y clasificación

En la tabla siguiente se enumera un subconjunto de tipos de archivos que el cliente de Azure Information Protection admite de forma nativa y que se pueden clasificar. 

Estos tipos de archivo se identifican por separado porque, cuando se protegen de forma nativa, se cambia la extensión del nombre del archivo original y pasan a ser de solo lectura. Tenga en cuenta que, cuando los archivos se protegen de manera genérica, la extensión del nombre de archivo original siempre se cambia a .pfile.

> [!WARNING]
> Si dispone de firewalls, servidores proxy web o software de seguridad que inspeccionan o realizan acciones en función de las extensiones de nombre de archivo, puede que tenga que volver a configurar estos dispositivos de red y softwares para admitir las nuevas extensiones de nombre de archivo.

|Extensión de nombre de archivo original|Extensión de nombre de archivo con protección|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjpeg|
|.pdf|.ppdf [[1]](#footnote-1)|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|

###### <a name="footnote-1"></a>Nota al pie 1
Si usa la versión preliminar del cliente de Azure Information Protection, [de manera predeterminada](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), la extensión de nombre de archivo del documento PDF protegido sigue siendo .pdf.

En la tabla siguiente se enumeran los tipos de archivos restantes que el cliente de Azure Information Protection admite de forma nativa y que se pueden clasificar. Los reconocerá, ya que se trata de tipos de archivos de las aplicaciones de Microsoft Office. Los formatos de archivo compatibles para estos tipos de archivo son los formatos 97-2003 y los formatos Open XML de los siguientes programas de Office: Word, Excel y PowerPoint. A menos que tenga la versión preliminar del cliente de Azure Information Protection, no se admite el formato Documento Open XML estricto.

En estos archivos, la extensión de nombre de archivo permanece igual después de que el archivo se ha protegido con el servicio de Rights Management.

|Tipos de archivo admitidos por Office|Tipos de archivo admitidos por Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm<br /><br />.pptx<br /><br />.vsdm|.vsdx<br /><br />.vssm<br /><br />.vssx<br /><br />.vstm<br /><br />.vstx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Cambio del nivel de protección predeterminado de los archivos
Puede cambiar la manera en que el cliente de Azure Information Protection protege los archivos mediante la modificación del Registro. Por ejemplo, puede forzar que los archivos que admiten la protección nativa estén protegidos de forma genérica por el cliente de Azure Information Protection.

Puede que quiera hacer esto por los siguientes motivos:

- Para asegurarse de que todos los usuarios pueden abrir el archivo si no tienen una aplicación que admite la protección nativa.

- Para tener en cuenta sistemas de seguridad que realizan acciones sobre los archivos por su extensión de nombre de archivo y que se pueden reconfigurar para que tengan en cuenta la extensión de nombre de archivo .pfile pero no para admitir varias extensiones de nombre de archivo para la protección nativa.

De modo similar, puede forzar que el cliente de Azure Information Protection aplique protección nativa a archivos a los que, de forma predeterminada, se les aplicaría protección genérica. Esta acción podría ser adecuada si dispone de una aplicación que admite las API de RMS. Por ejemplo, una aplicación de línea de negocio que han escrito sus desarrolladores internos o una aplicación adquirida a un fabricante de software independiente (ISV).

También puede forzar a que el cliente de Azure Information Protection boquee la protección de los archivos, es decir, que no aplique protección nativa ni protección genérica. Por ejemplo, esta acción podría ser necesaria si tiene una aplicación o un servicio automatizados que deben poder abrir un archivo específico para procesar su contenido. Cuando se bloquea la protección para un tipo de archivo, los usuarios no pueden usar el cliente de Azure Information Protection para proteger un archivo con ese tipo de archivo. Cuando lo intentan, verán un mensaje que dice que el administrador ha impedido la protección y deben cancelar su acción para proteger el archivo.

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

Como resultado de esta configuración, todos los archivos están protegidos genéricamente, excepto los que tienen una extensión de nombre de archivo .docx. Estos archivos están protegidos de forma nativa mediante el cliente de Azure Information Protection.

Repita estos tres pasos con otros tipos de archivos que quiera definir como excepciones porque admiten la protección nativa y no quiere que el cliente de Azure Information Protection los proteja de forma genérica.

Puede realizar modificaciones parecidas en el Registro para otras situaciones cambiando el valor de la cadena **Encryption** que admite los siguientes valores:

- **Pfile**: Protección genérica

- **Native**: Protección nativa

- **Off**: Bloquear protección

Para más información, vea [Configuración de la API de archivo](../develop/file-api-configuration.md) en la guía del desarrollador. En esta documentación para desarrolladores, se hace referencia a la protección genérica como "PFile". 

## <a name="file-types-that-are-excluded-from-classification-and-protection"></a>Tipos de archivos excluidos de la clasificación y la protección

Para ayudar a impedir que los usuarios modifiquen los archivos que son fundamentales para las operaciones del equipo, se excluyen automáticamente algunos tipos de archivos y carpetas de la clasificación y la protección. Si los usuarios intentan clasificar o proteger estos archivos mediante el cliente de Azure Information Protection, recibirán un mensaje para indicar que están excluidos.

- **Tipos de archivos excluidos**: .lnk, .exe, .com, .cmd, .bat, .dll, .ini, .pst, .sca, .drm, .sys, .cpl, .inf, .drv, .dat, .tmp, .msp, .msi, .pdb y .jar

- **Carpetas excluidas**: 
    - Windows
    - Archivos de programa (\Archivos de programa y \Archivos de programa (x86))
    - \ProgramData 
    - \AppData (de todos los usuarios)

### <a name="file-types-that-are-excluded-from-classification-and-protection-by-the-azure-information-protection-scanner"></a>Tipos de archivos excluidos de la clasificación y la protección mediante el analizar de Azure Information Protection

De manera predeterminada, el analizador también excluye los mismos tipos de archivo que el cliente de Azure Information Protection con las siguientes excepciones para la versión preliminar del analizador: .rar, .rtf, .msg y .zip. 

Puede cambiar los tipos de archivo incluidos o excluidos de la inspección de archivos mediante el analizador con los cmdlets de PowerShell siguientes:

- [Set-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Set-AIPScannerScannedFileTypes)

- [Add-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Add-AIPScannerScannedFileTypes)

- [Remove-AIPScannerScannedFileTypes](/powershell/module/azureinformationprotection/Remove-AIPScannerScannedFileTypes)

> [!NOTE]
> Si incluye los archivos .rtf en la exploración, debe supervisar atentamente el analizador. Algunos archivos .rtf no se pueden inspeccionar correctamente mediante el analizador. La inspección de estos archivos no se completa y hay que reiniciar el servicio. 

De forma predeterminada, el analizador solo protege los tipos de archivos de Office. Para cambiar este comportamiento del analizador, edite el Registro y especifique el resto de tipos de archivo que quiera proteger. Para obtener instrucciones, vea [Configuración de la API de archivo](../develop/file-api-configuration.md) en la guía del desarrollador.

### <a name="files-that-cannot-be-protected-by-default"></a>Archivos que no se puede proteger de forma predeterminada

Ningún archivo protegido con contraseña se puede proteger de forma nativa con el cliente de Azure Information Protection a menos que esté abierto en la aplicación que aplica la protección. Los archivos protegidos con contraseña más frecuentes son PDF, pero hay otras aplicaciones, como las de Office, que también ofrecen esta funcionalidad.

Además, la versión de disponibilidad general (GA) del cliente de Azure Information Protection para Windows puede ver los siguientes archivos pero no proteger de forma nativa ni desproteger archivos PDF en ninguna de las circunstancias siguientes:

- Un archivo PDF basado en formulario. 

- Un archivo PDF protegido con una extensión de nombre de archivo .pdf.
    
    El cliente de Azure Information Protection puede proteger un archivo PDF desprotegido y puede desproteger y volver a proteger un archivo PDF protegido si tiene la extensión de nombre de archivo .ppdf.

Como solución alternativa para proteger estos archivos, puede protegerlos de forma genérica siguiendo las instrucciones de la sección [Cambio del nivel de protección predeterminado de los archivos](#changing-the-default-protection-level-of-files). Con todo, este método cambia el nivel de protección de todos los archivos con una extensión de nombre de archivo .pdf en el nivel del equipo. No puede definir una protección genérica únicamente para los archivos que coincidan con los criterios mostrados.

Si la protección de estos archivos es importante, podría copiarlos temporalmente en otro equipo para protegerlos de forma genérica y, después, copiarlos de nuevo. También puede utilizar la versión preliminar del cliente de Azure Information Protection.

Cuando usa la versión preliminar actual del cliente de Azure Information Protection, [de manera predeterminada](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), puede proteger y desproteger de manera nativa los archivos PDF en cualquiera de estas dos circunstancias:

- Un archivo PDF basado en formulario.

- Un archivo PDF protegido con una extensión de nombre de archivo .pdf. 

### <a name="limitations-for-container-files-such-as-zip-files"></a>Limitaciones en los archivos de contenedor, como los archivos .zip

Los archivos de contenedor son archivos que incluyen otros archivos, y un ejemplo típico son los archivos .zip que contienen archivos comprimidos. Otros ejemplos son los archivos .rar, .7z y .msg.

Puede clasificar y proteger estos archivos de contenedor, pero la clasificación y la protección no se aplican a los archivos incluidos dentro del contenedor.

Si tiene un archivo de contenedor que incluye archivos clasificados y protegidos, primero debe extraer los archivos para cambiar su configuración de clasificación o protección. Sin embargo, puede quitar la protección de todos los archivos incluidos en archivos de contenedor compatibles mediante el cmdlet [Unprotect-RMSFile](/powershell/module/azureinformationprotection/unprotect-rmsfile).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha identificado los tipos de archivos compatibles con el cliente de Azure Information Protection, vea los siguientes recursos para obtener más información que puede necesitar para la compatibilidad con este cliente:

- [Personalizaciones](client-admin-guide-customizations.md)

- [Archivos de cliente y registro de uso](client-admin-guide-files-and-logging.md)

- [Seguimiento de documentos](client-admin-guide-document-tracking.md)

- [Comandos de PowerShell](client-admin-guide-powershell.md)

