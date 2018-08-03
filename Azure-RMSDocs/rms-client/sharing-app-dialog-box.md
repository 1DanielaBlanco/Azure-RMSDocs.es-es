---
title: Opciones del cuadro de diálogo para la aplicación RMS sharing - AIP
description: Información útil para especificar las opciones en el cuadro de diálogo Agregar protección o en el cuadro de diálogo Uso compartido seguro de la aplicación RMS sharing. Verá este cuadro de diálogo cuando proteja un archivo para compartirlo o cuando proteja un archivo en contexto y elija permisos personalizados.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 7b91ab30-6363-4929-bcbd-4dfbd05f644a
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8fc94edec250fd0cef1be5f3030e19ce8628cc92
ms.sourcegitcommit: 44ff610dec678604c449d42cc0b0863ca8224009
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39370166"
---
# <a name="dialog-box-options-for-the-rights-management-sharing-application"></a>Opciones del cuadro de diálogo para la aplicación de uso compartido Rights Management

>*Se aplica a: Active Directory Rights Management Services, [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection), Windows 10, Windows 7 con SP1, Windows 8 y Windows 8.1*

Use esta información para especificar las opciones en el cuadro de diálogo **Agregar protección** o en el cuadro de diálogo **Uso compartido seguro** de la aplicación de uso compartido de RMS. Verá este cuadro de diálogo cuando [proteja un archivo para compartirlo](sharing-app-protect-by-email.md) o cuando [proteja un archivo en contexto](sharing-app-protect-in-place.md) y elija permisos personalizados.

> [!IMPORTANT]
> Si las opciones que ve son diferentes de las mostradas aquí, probablemente no tiene instalada la versión más reciente de la aplicación. Puede descargar la versión más reciente en la página [Microsoft Rights Management](http://go.microsoft.com/fwlink/?LinkId=303970) .
> 
> ¿Cómo puede saber si tiene la versión más reciente? Busque **Aplicación para uso compartido de Microsoft Rights Management** en Programas y características y compruebe el número de versión. Para poder ver y usar las opciones de la tabla, la versión debe ser al menos **1.0.1770.0**. Puede comprobar el número de versión más reciente en la página de descarga.

Además de las opciones que puede elegir, es posible que también se pregunte lo siguiente:

-   [¿Qué es ese archivo .ppdf que se crea automáticamente?](#whats-the-ppdf-file-thats-automatically-created)

-   [¿Cuál es la diferencia entre la protección genérica y la protección incorporada (nativa)?](#whats-the-difference-between-generic-protection-and-built-in-native-protection)

|Opción|Descripción|
|----------|---------------|
|**USUARIOS**|Si todavía no especificó una dirección de correo electrónico de Outlook, escriba las direcciones de correo electrónico de las personas que desea que puedan abrir el archivo.<br /><br />Tenga en cuenta que la aplicación RMS sharing no admite todas las direcciones de correo electrónico.<br /><br />Si su organización usa la versión local de Rights Management (AD RMS), las direcciones de correo electrónico que puede especificar se limitan a personas de su organización. En este caso, cuando intente especificar direcciones de correo electrónico externas, verá un mensaje que indica que la configuración de la empresa permite el uso compartido de contenido protegido únicamente dentro de la empresa. <br /><br /> Si la organización usa Azure RMS, estas direcciones de correo electrónico pueden ser de personas de la organización o de personas de otra organización.<br /><br />Por ejemplo: **janetm@contoso.com; p.dover@fabrikam.com**<br /><br />La aplicación RMS sharing no admite actualmente direcciones de correo electrónico personal|
|**Protección genérica**|Si está seleccionada esta opción, significa que el archivo seleccionado no se puede proteger de forma nativa. Para obtener más información, vea. [¿Cuál es la diferencia entre la protección genérica y la protección integrada (nativa)?](#whats-the-difference-between-generic-protection-and-built-in-native-protection) en esta página.|
|**Visor – Solo ver**<br /><br />**Revisor – Ver y editar**<br /><br />**Coautor – Ver, editar, copiar e imprimir**<br /><br />**Copropietario – Todos los permisos**<br /><br />Nota: Todas estas opciones tienen un icono redondo antes del nombre, que representa un globo terráqueo. Se usa este icono porque, normalmente, se selecciona una de estas opciones cuando se envía un archivo adjunto a una persona de otra organización.|Seleccione una de estas opciones si desea definir los derechos del documento protegido. Haga clic en cada opción para ver una descripción.<br /><br />Cuando elija una de estas opciones, solo las personas que indique en **USUARIOS** tienen los derechos que especifique para abrir y usar el documento. Por ejemplo, si reenvían el documento a otra persona, no se abrirá.|
|Plantillas de directiva que configura el administrador.<br /><br />Por ejemplo, si el nombre de la organización es Contoso, Ltd: **Contoso, Ltd - Solo vista confidencial**.<br /><br />Todas estas opciones tienen un icono cuadrado antes del nombre, que representa un edificio de oficinas. Se usa este icono porque, normalmente, se selecciona una de estas opciones cuando se envía un archivo adjunto a una persona de la misma organización.|Al compartir un documento con personas que trabajan en su organización, verá las plantillas de directiva disponibles que configura el administrador. Elija una de estas plantillas cuando no se deba compartir el documento fuera de su organización.<br /><br />Cuando se elija una de estas opciones, el administrador definirá los derechos del documento y quién puede abrirlo.|
|**Estos documentos expiran el**|Seleccione esta opción solo para los archivos sujetos a limitación temporal que los usuarios seleccionados no deben poder abrir después de la fecha que especifique. Usted seguirá pudiendo abrir el archivo original, pero después de la medianoche (de su zona horaria actual) del día que especifique, nadie más podrá abrir el archivo.<br /><br />Esta opción no está disponible si selecciona una plantilla de directiva configurada por el administrador.|
|**Enviarme un correo electrónico cuando alguien trate de abrir estos documentos**|Nota: Esta opción está disponible actualmente en versión preliminar.<br /><br />Seleccione esta opción si desea recibir notificaciones por correo electrónico cuando alguien intente abrir el documento que está protegiendo. El mensaje de correo electrónico dirá quién intentó abrirlo, cuándo y si lo consiguió.<br /><br />Esta opción solo está disponible si su organización usa Azure Information Protection. Si su organización usa la versión local de Rights Management (AD RMS), no verá esta opción.|
|**Permitirme revocar el acceso a estos documentos de forma instantánea**|Elija esta opción si necesita revocar el acceso a los documentos más adelante a través del sitio de seguimiento de documentos y si la revocación debe surtir efecto de inmediato. Sin embargo, si establece esta opción, mientras el documento no se revoque, los usuarios siempre necesitarán una conexión a Internet para leer el documento cada vez que accedan a él. Pueden darse casos en los que los usuarios no puedan conectar su dispositivo a Internet y no puedan leer el documento tal como se pretende.<br /><br />Si no elige esta opción, todavía puede revocar los documentos más adelante, a través del sitio de seguimiento de documentos. Sin embargo, dado que los usuarios no siempre necesitan una conexión a Internet para leer el documento, no sabrán inmediatamente que el documento está revocado y podrán seguir leyéndolo hasta que vuelvan a autenticarse con Azure RMS. De forma predeterminada, el número máximo de días que alguien puede seguir leyendo un documento protegido revocado es 30 días, pero un administrador puede cambiar este valor para que sea mayor o menor que 30 días.<br /><br />Esta opción solo está disponible si su organización usa Azure Information Protection. Si su organización usa la versión local de Rights Management (AD RMS), no verá esta opción.|

## <a name="whats-the-difference-between-generic-protection-and-built-in-native-protection"></a>¿Cuál es la diferencia entre la protección genérica y la protección incorporada (nativa)?

-   Cuando se **protege genéricamente un archivo**, las personas no autorizadas no pueden abrir el archivo. Sin embargo, cuando una persona autorizada abre el archivo, puede reenviarlo desprotegido a otras personas o guardarlo en una ubicación a la que podrían acceder otros usuarios. A pesar de ello, verán un mensaje que les informa de los permisos que tienen para el archivo y se les solicitará que los respeten, aunque no es posible obligar al cumplimiento de esta protección. Además, al proteger un archivo de forma genérica, no es posible restringir los permisos más allá de la autorización. Por ejemplo, no se puede restringir el contenido a Solo ver, o a No imprimir.

    > [!NOTE]
    > Un archivo protegido genéricamente siempre tiene la extensión de nombre de archivo **.pfile**.

-   En cambio, cuando se usa la **protección integrada (nativa)** de Rights Management con aplicaciones que la admiten (por ejemplo, archivos de Office), la protección se aplica al archivo aunque este se envíe a otra persona o se guarde en otra ubicación. Además, al proteger estos archivos, puede usar permisos restrictivos, como el permiso de solo lectura o el permiso para editar pero no imprimir ni copiar. Por ejemplo, puede seleccionar **Visor – Solo ver**, de modo que el contenido no se pueda editar, imprimir ni copiar.

Para obtener información técnica adicional, consulte la sección [Niveles de protección: nativa y genérica](sharing-app-admin-guide-technical.md#levels-of-protection--native-and-generic) de la [Guía del administrador de la aplicación Microsoft Rights Management sharing](sharing-app-admin-guide.md).

## <a name="whats-the-ppdf-file-thats-automatically-created"></a>¿Qué es ese archivo .ppdf que se crea automáticamente?

-   Cuando se comparte un archivo protegido por correo electrónico (uso compartido seguro), la aplicación de uso compartido de RMS crea automáticamente una versión **.ppdf** del archivo de Word, Excel, PowerPoint o PDF. Se trata de una versión protegida de solo lectura del archivo que únicamente pueden abrir las personas autorizadas, y garantiza que los destinatarios siempre puedan leer los archivos adjuntos, incluso si usan un dispositivo móvil que no tiene una aplicación que admita Rights Management de forma nativa. Estas personas podrán leer los datos adjuntos siempre y cuando tengan instalada la aplicación de uso compartido de RMS.

    En este escenario, a diferencia de lo que sucede en el caso de un archivo protegido de forma genérica, se aplica la restricción de uso. El destinatario no podrá guardar esta versión del archivo y, si reenvía el archivo adjunto a otra persona, las restricciones originales seguirán en vigor en el documento. Solo los usuarios que recibieron una autorización para el documento protegido podrán abrirlo.

    > [!NOTE]
    > Se crea automáticamente un archivo .ppdf cuando se hace un uso compartido seguro (compartir por correo electrónico), pero no se crea cuando se protege en contexto.

## <a name="examples-and-other-instructions"></a>Ejemplos y otras instrucciones
Para obtener ejemplos de cómo puede usar la aplicación para uso compartido de Rights Management e instrucciones de procedimientos, consulte las siguientes secciones de la guía de usuario de la aplicación para uso compartido de Rights Management:

-   [Ejemplos de uso de la aplicación RMS sharing](sharing-app-user-guide.md#examples-for-using-the-rms-sharing-application)

-   [¿Qué desea hacer?](sharing-app-user-guide.md#what-do-you-want-to-do)

## <a name="see-also"></a>Consulte también
[Guía de usuario de la aplicación Rights Management sharing](sharing-app-user-guide.md)

