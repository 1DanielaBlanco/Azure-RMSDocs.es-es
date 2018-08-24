---
title: Información general técnica para la aplicación RMS sharing - AIP
description: Detalles técnicos para administradores en redes empresariales que son responsables de implementar la aplicación RMS sharing para Windows.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 06/02/2017
ms.topic: article
ms.service: information-protection
ms.assetid: f7b13fa4-4f8e-489a-ba46-713d7a79f901
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 4a04af78d1327fa9810325d799336c98f12b5163
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42804496"
---
# <a name="technical-overview-and-protection-details-for-the-microsoft-rights-management-sharing-application"></a>Información general técnica de la aplicación Microsoft Rights Management sharing

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*


La aplicación Microsoft Rights Management sharing es una aplicación opcional descargable para Microsoft Windows y otras plataformas, que ofrece lo siguiente:

-   Protección de un solo archivo o protección masiva de varios archivos y de todos los archivos de una carpeta seleccionada.

-   Funcionalidad completa para proteger cualquier tipo de archivo y un visor integrado para los tipos de archivo de texto y de imagen más comunes.

-   Protección genérica para los archivos que no admiten la protección de RMS.

-   Interoperabilidad completa con los archivos protegidos mediante Office Information Rights Management (IRM).

-   Interoperabilidad completa con archivos PDF protegidos con la infraestructura de clasificación de archivos (FCI) y herramientas de creación de PDF admitidas.

La aplicación Microsoft Rights Management sharing usa el [tiempo de ejecución del cliente de AD RMS 2.1](http://www.microsoft.com/download/details.aspx?id=38396). Mediante el uso de la funcionalidad de AD RMS 2.1, la aplicación Microsoft Rights Management sharing proporciona a los usuarios finales una experiencia sencilla de protección y el consumo.

Con la versión de RMS de octubre de 2013, puede proteger documentos de forma nativa mediante Office 2010 y enviarlos a personas de otra compañía, quienes pueden consumirlos entonces con el servicio Azure Rights Management de Azure Information Protection. Además, con esta versión, si usa AD RMS en modo criptográfico 2, puede usar RMS para individuos y consumir contenido de personas de otra compañía que use el servicio Azure Rights Management. Para obtener más información sobre el Modo criptográfico 2, consulte [Modos criptográficos de AD RMS](http://technet.microsoft.com/library/hh867439%28v=ws.10%29.aspx).

Para obtener información de implementación, consulte [Implementación automática de la aplicación Microsoft Rights Management sharing](sharing-app-admin-guide.md#automatic-deployment-for-the-microsoft-rights-management-sharing-application)

## <a name="levels-of-protection--native-and-generic"></a>Niveles de protección: nativo y genérico
La aplicación Microsoft Rights Management sharing admite la protección en dos niveles distintos, como se describe en la tabla siguiente.

|Tipo de protección|Nativa|Genérico|
|----------------------|----------|-----------|
|Descripción|Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones compatibles con el servicio de Rights Management, la protección nativa ofrece un fuerte nivel de protección que incluye tanto cifrado como aplicación de derechos (permisos).|Para todas las demás aplicaciones y tipos de archivo, la protección genérica proporciona un nivel de protección que incluye encapsulación de archivos mediante el tipo de archivo .pfile, y autenticación para comprobar si un usuario está autorizado para abrir el archivo.|
|Protección|Los archivos están completamente cifrados y la protección se aplica de las siguientes maneras:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que reciben el archivo por correo electrónico o a las que se les concede acceso a él mediante permisos de archivo o recurso compartido.<br /><br />- Además, cuando el contenido se presenta en el Visor de IP (en el caso de archivos de texto e imagen protegidos) o en la aplicación asociada (en el caso de todos los demás tipos de archivo admitidos), se aplican completamente los derechos de uso y la directiva definida por el propietario del contenido cuando se protegen los archivos.|La protección de los archivos se aplica de las siguientes formas:<br /><br />- Antes de presentar el contenido protegido, se debe autenticar correctamente a aquellas personas que están autorizadas para abrir el archivo o a las que se les proporciona acceso a él. Si la autorización da error, el archivo no se abre.<br /><br />- Se muestran los derechos de uso y la directiva establecida por el propietario del contenido para informar a los usuarios autorizados de la directiva de uso previsto.<br /><br />- Se produce el registro de auditoría de los usuarios autorizados a abrir y obtener acceso a los archivos, pero no se aplican derechos de uso por parte de las aplicaciones no admitidas.|
|Valor predeterminado para tipos de archivo|Es el nivel predeterminado de protección para los siguientes tipos de archivo:<br /><br />- Archivos de texto e imagen<br /><br />- Archivos de Microsoft Office (Word, Excel, PowerPoint)<br /><br />- Formato de documento portátil (.pdf)<br /><br />Para más información, consulte la sección siguiente, [Tipos de archivo y extensiones de nombre de archivo admitidos](#supported-file-types-and-file-name-extensions).|Se trata de la protección predeterminada para todos los demás tipos de archivo (por ejemplo, .vsdx, .rtf, etc.) que no son compatibles con la protección completa.|
Puede cambiar el nivel de protección predeterminado que aplica la aplicación RMS sharing. Puede cambiar el nivel predeterminado de nativo a genérico, de genérico a nativo, e incluso impedir que la aplicación RMS sharing aplique protección. Para más información, consulte la sección [Cambio del nivel de protección predeterminado de los archivos](#changing-the-default-protection-level-of-files) de este artículo.

## <a name="supported-file-types-and-file-name-extensions"></a>Tipos de archivo y extensiones de nombre de archivo admitidos
En la tabla siguiente se enumeran los tipos de archivo que admite de forma nativa la aplicación Microsoft Rights Management sharing. En estos tipos de archivo, la extensión de nombre de archivo original se cambia cuando se aplica el archivo nativo protegido, y estos archivos se vuelven de solo lectura.

Además, cuando la aplicación RMS sharing protege de forma nativa un archivo de Word, Excel o PowerPoint que protegen los usuarios mediante uso compartido, esta acción crea automáticamente un segundo archivo que es una copia del original con el mismo nombre pero con una extensión **.ppdf** ¹. Esta versión del archivo garantiza que los destinatarios que instalan la aplicación RMS sharing siempre pueden abrir el archivo al que se le ha aplicado protección nativa.

En el caso de los archivos que están protegidos de manera genérica, la extensión del nombre de archivo original siempre se cambia a .pfile.

> [!WARNING]
> Si dispone de firewalls, servidores proxy web o software de seguridad que inspeccionan o realizan acciones en función de las extensiones de nombre de archivo, puede que tenga que volver a configurar estos para admitir las nuevas extensiones de nombre de archivo.

|Extensión de nombre de archivo original|Extensión de nombre de archivo con protección de RMS|
|--------------------------------|-------------------------------------|
|.txt|.ptxt|
|.xml|.pxml|
|.jpg|.pjpg|
|.jpeg|.pjeg|
|.pdf|.ppdf|
|.png|.ppng|
|.tif|.ptif|
|.tiff|.ptiff|
|.bmp|.pbmp|
|.gif|.pgif|
|.jpe|.pjpe|
|.jfif|.pjfif|
|.jt|.pjt|
¹ Representación de PDF con tecnología Foxit. Copyright © 2003–2014 by Foxit Corporation.

En la tabla siguiente se enumeran los tipos de archivo que admite de forma nativa la aplicación Microsoft Rights Management sharing en Microsoft Office 2016, Office 2013 y Office 2010. En estos archivos, la extensión de nombre de archivo permanece igual después de que el archivo se ha protegido con el servicio de Rights Management.

|Tipos de archivo admitidos por Office|Tipos de archivo admitidos por Office|
|----------------------------------|----------------------------------|
|.doc<br /><br />.docm<br /><br />.docx<br /><br />.dot<br /><br />.dotm<br /><br />.dotx<br /><br />.potm<br /><br />.potx<br /><br />.pps<br /><br />.ppsm<br /><br />.ppsx<br /><br />.ppt<br /><br />.pptm|.pptx<br /><br />.thmx<br /><br />.xla<br /><br />.xlam<br /><br />.xls<br /><br />.xlsb<br /><br />.xlt<br /><br />.xlsm<br /><br />.xlsx<br /><br />.xltm<br /><br />.xltx<br /><br />.xps|

### <a name="changing-the-default-protection-level-of-files"></a>Cambio del nivel de protección predeterminado de los archivos
Puede cambiar la manera en que la aplicación RMS sharing protege los archivos mediante la modificación del Registro. Por ejemplo, puede forzar que los archivos que admiten la protección nativa estén protegidos de forma genérica por la aplicación RMS sharing.

Puede que quiera hacer esto por los siguientes motivos:

-   Para asegurarse de que todos los usuarios pueden abrir el archivo desde sus dispositivos móviles.

-   Para asegurarse de que todos los usuarios pueden abrir el archivo si no tienen una aplicación que admite la protección nativa.

-   Para tener en cuenta sistemas de seguridad que realizan acciones sobre los archivos por su extensión de nombre de archivo y que se pueden reconfigurar para que tengan en cuenta la extensión de nombre de archivo .pfile pero no para admitir varias extensiones de nombre de archivo para la protección nativa.

De igual forma, puede forzar que la aplicación RMS sharing aplique protección nativa a archivos a los que, de forma predeterminada, se les aplicaría protección genérica. Esto podría resultar adecuados si tiene una aplicación que admite las API de RMS, por ejemplo, una aplicación de línea de negocio que han escrito sus desarrolladores internos o una aplicación adquirida a un fabricante de software independiente (ISV).

También puede forzar que la aplicación RMS sharing boquee la protección de los archivos, es decir, que no aplique protección nativa ni protección genérica. Por ejemplo, esto podría ser necesario si tiene una aplicación o un servicio automatizados que deben poder abrir un archivo específico para procesar su contenido. Cuando se bloquea la protección para un tipo de archivo, los usuarios no pueden usar la aplicación RMS sharing para proteger un archivo con ese tipo de archivo. Cuando lo intentan, verán un mensaje que dice que el administrador ha impedido la protección y deben cancelar su acción para proteger el archivo.

Para configurar la aplicación RMS sharing para aplicar protección genérica a todos los archivos a los que, de forma predeterminada, se les aplicaría protección nativa, realice las siguientes modificaciones en el Registro. Tenga en cuenta que si las claves RmsSharingApp o FileProtection no existen, debe crearlas manualmente.

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**: cree una nueva clave denominada *.

    Este valor indica archivos con cualquier extensión de nombre de archivo.

2.  En la clave recién agregada de HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\\\*, cree un nuevo valor de cadena (REG_SZ) denominado **Encryption** que tenga el valor de datos de **Pfile**.

    Este valor da como resultado la aplicación de protección genérica por parte de la aplicación RMS sharing.

Estos dos valores provocarán que la aplicación RMS sharing aplique protección genérica a todos los archivos que tiene una extensión de nombre de archivo. Si éste es su objetivo, no es necesario configurar nada más. Sin embargo, puede definir excepciones para tipos de archivo específicos para que sigan estando protegidos de forma nativa. Para ello, debe realizar tres modificaciones adicionales en el Registro para cada tipo de archivo:

1.  **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection**: agregue una nueva clave con el nombre de la extensión de nombre de archivo (sin el punto anterior).

    Por ejemplo, para los archivos que tienen una extensión .docx, cree una clave denominada **DOCX**.

2.  En la clave de tipo de archivo recién creada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**), cree un nuevo valor DWORD denominado **AllowPFILEEncryption** que tenga un valor de **0**.

3.  En la clave de tipo de archivo recién agregada (por ejemplo, **HKEY_LOCAL_MACHINE\Software\Microsoft\MSIPC\RmsSharingApp\FileProtection\DOCX**), cree un nuevo valor de cadena denominado **Encryption** que tenga un valor de **Native**.

Como resultado de esta configuración, todos los archivos están protegidos genéricamente, excepto los archivos que tienen una extensión de nombre de archivo .docx, que están protegidos de forma nativa por la aplicación RMS sharing.

Repita estos tres pasos con otros tipos de archivo que quiera definir como excepciones porque admiten la protección nativa y no quiere que la aplicación RMS sharing los proteja de forma genérica.

Puede realizar modificaciones parecidas en el Registro para otras situaciones cambiando el valor de la cadena **Encryption** que admite los siguientes valores:

-   **Pfile**: Protección genérica

-   **Native**: Protección nativa

-   **Off**: Bloquear protección

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)

