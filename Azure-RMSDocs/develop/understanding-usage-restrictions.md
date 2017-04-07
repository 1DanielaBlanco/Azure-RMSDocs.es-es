---
title: "Descripción de las restricciones de uso | Azure RMS"
description: Todas las aplicaciones habilitadas para RMS deben aplicar restricciones de uso.
keywords: 
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: E388B16C-ECDA-4696-A040-D457D3C96766
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 8ed5897accf7bf4db08a5fc699af3f0f850740a2
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="understanding-usage-restrictions"></a>Descripción de las restricciones de uso

Todas las aplicaciones habilitadas para RMS deben aplicar restricciones de uso. Una restricción de uso es una condición que se produce cuando un usuario intenta realizar una acción (p. ej. imprimir un documento), pero la directiva de RMS para ese documento no le concede el permiso o el derecho a realizar esa acción (p. ej. el derecho PRINT).

Los permisos de un usuario en relación con un documento se pueden consultar mediante la función [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx).

## <a name="designing-with-usage-restrictions"></a>Diseño con restricciones de uso

-   Familiarícese con derechos estándar de RMS

    Para obtener el conjunto completo de derechos de RMS que puede exigir la aplicación, consulte [Usage restriction reference](#usage-restriction-reference) (Referencia de restricción de uso).

    Tenga en cuenta es posible crear derechos definidos para la aplicación que sean específicos para su situación y que vayan más allá de los derechos de RMS.

-   Identificación de los puntos de cumplimiento de restricción de uso

    Un *punto de cumplimiento de restricción de uso* es un lugar en el flujo de control de la aplicación donde es necesario aplicar una restricción de uso. El tema [Usage restriction reference](#usage-restriction-reference) (Referencia de restricción de uso) proporciona varios ejemplos de puntos de cumplimiento comunes.

    Evalúe su propia aplicación para determinar los puntos de cumplimiento de restricción pertinentes.

    Es posible que la aplicación no necesite todos los puntos de cumplimiento que se describen en [Usage restriction reference](#usage-restriction-reference) (Referencia de restricción de uso). Por ejemplo, si la aplicación no permite a los usuarios imprimir contenido, no es necesario comprobar el derecho **IPC\_GENERIC\_PRINT**.

-   Actualización del código para realizar una comprobación de acceso en cada punto de cumplimiento

    Para obtener instrucciones acerca de cómo aplicar derechos específicos, consulte [Usage restriction reference](#usage-restriction-reference) (Referencia de restricción de uso).

## <a name="usage-restriction-reference"></a>Usage restriction reference (Referencia de restricción de uso).

Las restricciones de uso se definen mediante las siguientes constantes.

Cada derecho de usuario, que aparece en la columna de derechos de AD RMS, tiene una descripción, un punto de cumplimiento y métodos de cumplimiento sugeridos.

| Derecho de AD RMS/descripción | Cómo aplicar el cumplimiento |
|--------------------------|----------------|
|**IPC_GENERIC_ALL** <br><br> Concede todos los derechos al usuario. <br><br> **Puntos de cumplimiento comunes**: ninguno |El sistema usa este derecho y por lo general no se debe comprobar directamente. <br><br> [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx) usa este derecho para determinar si se deben conceder otros derechos al usuario como en este ejemplo.<br><br> `/* fAccessGranted is set to TRUE if either the IPC_GENERIC_WRITE or the IPC_GENERIC_ALL right is granted */` <br><br> `IpcAccessCheck(hKey, IPC_GENERIC_WRITE, &fAccessGranted);`|
|**IPC_GENERIC_READ** <br><br> Derecho para leer el contenido del documento. <br><br> **Puntos de cumplimiento comunes**: carga del documento|No cargue ni presente el contenido del documento.|
|**IPC_GENERIC_WRITE** <br><br> Derecho para editar el contenido del documento. <br><br> **Puntos de cumplimiento comunes**: modificación del documento|Haga que los controles de interfaz de usuario que se pueden usar para modificar el contenido del documento no se puedan editar. <br><br> Deshabilite los elementos del menú que desencadenan cambios en el documento. **Editar** > **Cortar**, **Editar** > **Pegar** e **Insertar** son ejemplos típicos. <br><br>Deshabilite los elementos del menú contextual que desencadenan cambios en el documento.|
|Ningún derecho de AD RMS <br><br> Ninguna descripción <br><br> **Puntos de cumplimiento comunes**: guardar | Deshabilite el menú **Archivo** > **Guardar**. <br><br> **Nota** Este derecho no controla **Archivo** > **Guardar como** porque ese derecho no representa un cambio en el documento original.<br><br> Deshabilite cualquier método abreviado de teclado que se pueda usar para desencadenar un proceso de guardar (por ejemplo, Ctrl+S).<br><br> **Sugerencia** Un procedimiento recomendado consiste en actualizar el código principal de **Archivo** > **Guardar** para que produzca un error si el usuario no tiene este derecho. Esto actúa como red de seguridad si se salta algún mecanismo de experiencia de usuario que se pueda usar para desencadenar un proceso de guardar. |
|**IPC_GENERIC_EXTRACT** <br><br> Derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. <br><br> **Puntos de cumplimiento comunes**: copiar al Portapapeles | Deshabilite el menú **Editar** > **Copiar**. Deshabilite el menú **Editar** > **Cortar**. <br><br>Deshabilite **Copiar** y **Cortar** en los menús contextuales.<br><br>Deshabilite cualquier método abreviado de teclado que se pueda usar para desencadenar un proceso de copiar (por ejemplo, Ctrl+C o Ctrl+X).<br><br>Actualice los controladores de mensajes de ventana para que [**WM_CUT**](https://msdn.microsoft.com/library/ms649023) rechace la copia de datos si el usuario no tiene este derecho. Si la ventana usa el controlador de mensajes predeterminado que proporciona Windows, cree una subclase para esta ventana y proporcione sus propios controladores para **WM_COPY** y **WM_CUT**. |
|Ningún derecho de AD RMS <br><br> Ninguna descripción <br><br> **Puntos de cumplimiento comunes**: guardar como |En su cuadro de diálogo **Guardar como**, deshabilite todos los formatos de archivo que hagan que el documento se guarde sin protección de RMS.|
|Ningún derecho de AD RMS <br><br> Ninguna descripción <br><br> **Puntos de cumplimiento comunes**: Alt+Impr Pant|Llame a [IpcProtectWindow](https://msdn.microsoft.com/library/hh535268.aspx) en todas las ventanas que representan el contenido del documento.|
|**IPC_GENERIC_EXPORT** <br><br> Derecho para extraer contenido de un formato protegido y colocarlo en un formato diferente protegido por AD RMS. <br><br> **Puntos de cumplimiento comunes**: guardar como|En su cuadro de diálogo **Guardar como**, deshabilite la capacidad de guardar en otros formatos de archivo.<br><br>**Sugerencia** Un procedimiento recomendado consiste en actualizar el código principal de **Archivo** > **Guardar como** para que produzca un error si el usuario intenta guardar este archivo en un formato diferente y no tiene este derecho. Esto actúa como red de seguridad si se salta algún mecanismo de experiencia de usuario que se pueda usar para desencadenar un proceso de guardar como.|
|**IPC_GENERIC_PRINT** <br><br> Derecho para imprimir el contenido del documento. <br><br> **Puntos de cumplimiento comunes**: imprimir|Deshabilite el menú **Archivo** > **Imprimir**.<br><br>Deshabilite cualquier método abreviado de teclado que se pueda usar para desencadenar un proceso de impresión (por ejemplo, Ctrl+P).<br><br>Deshabilite los elementos del menú contextual que se puedan usar para desencadenar una impresión.<br><br>**Sugerencia** Un procedimiento recomendado consiste en actualizar el código principal de **Archivo** > **Imprimir** para que produzca un error si el usuario no tiene este derecho. Esto actúa como red de seguridad si se salta algún mecanismo de experiencia de usuario que se pueda usar para desencadenar un proceso de impresión.|
|**IPC_GENERIC_COMMENT** <br><br> Algunas aplicaciones admiten la capacidad de agregar comentarios y anotaciones al documento sin actualizar el contenido principal del documento.<br><br>Este derecho concede al usuario acceso a esta funcionalidad. <br><br> **Puntos de cumplimiento comunes**: <br><br> Revisar > Insertar comentario <br><br> Revisar > Eliminar comentario | Deshabilite los elementos del menú que se puedan usar para modificar los comentarios o las anotaciones del documento. Por ejemplo, **Revisar** > **Insertar comentario** y **Revisar** > **Eliminar comentario**. <br><br>Deshabilite cualquier método abreviado de teclado que pueda desencadenar la modificación de los comentarios del documento.<br><br>**Nota** Una implementación predeterminada necesita **IPC_GENERIC_COMMENT** y **IPC_GENERIC_WRITE** para conservar los comentarios nuevos de un archivo. Las aplicaciones pueden optar por agregar compatibilidad en caso de que se conceda el derecho **IPC_GENERIC_COMMENT** y no se conceda el derecho **IPC_GENERIC_WRITE**. En este caso se permite para posibilitar el proceso de guardar, siempre y cuando las modificaciones del documento se restrinjan a los comentarios.|
|**IPC_VIEW_RIGHTS** <br><br> Ninguna descripción <br><br> **Puntos de cumplimiento comunes**: N/D|Aplicado por el sistema. El sistema no permitirá que el desarrollador consulte la [**lista de derechos de usuario**](https://msdn.microsoft.com/library/hh535286.aspx) de una licencia a menos que se conceda este derecho.
|**IPC_EDIT_RIGHTS** <br><br> Algunas aplicaciones permiten que los usuarios modifiquen el conjunto de usuarios y derechos del contenido protegido por AD RMS.<br><br>Este derecho concede al usuario acceso a esta funcionalidad. <br><br> **Puntos de cumplimiento comunes**: control de la interfaz de usuario de edición de derechos de la aplicación|Deshabilite el acceso del usuario a cualquier interfaz de usuario que se pueda usar para editar la directiva de RMS de un documento.|


## <a name="related-topics"></a>Temas relacionados

* [IpcAccessCheck](https://msdn.microsoft.com/library/hh535253.aspx)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]