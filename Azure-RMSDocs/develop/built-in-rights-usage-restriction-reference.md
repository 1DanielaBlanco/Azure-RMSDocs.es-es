---
title: Cómo usar los derechos integrados | Azure RMS
description: Se describen los derechos integrados que proporciona RMS SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones.
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 0d93f24f74a385613ebb5f3f44eee1951ea00be9
ms.sourcegitcommit: 1cd4edd4ba1eb5e10cb61628029213eda316783a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53266671"
---
# <a name="how-to-use-built-in-rights"></a>Cómo: Usar los derechos integrados

En este tema se describen los derechos integrados que proporciona Microsoft Rights Management SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones. A continuación se muestran los derechos integrados, los derechos comunes, los derechos de documentos editables y los derechos de correo electrónico, seguidos de una descripción y de sus valores por sistema operativo.

**Nota**: En el caso del SDK de Linux, consulte el archivo de origen *rights.h* para obtener más información.

## <a name="common-rights"></a>Derechos comunes

**All**: colección de todos los derechos comunes.
- Android: [CommonRights.All](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS y OS X: [MSCommonRights](https://msdn.microsoft.com/library/dn758314.aspx), propietario del usuario y vista para implementar **All**
- Tienda Windows y Windows Phone: [CommonRights.All</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.all.aspx)
- Linux: [CommonRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**Owner**: El derecho Owner concede control total sobre el contenido protegido.
- Android: [<strong>CommonRights.Owner](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS y OS X: [MSCommonRights owner](https://msdn.microsoft.com/library/dn758314.aspx)
- Tienda Windows y Windows Phone: [CommonRights.Owner](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.owner.aspx)
- Linux: [CommonRights::Owner](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View**: derecho para ver contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario abrir y ver contenido protegido. Sin embargo, se requieren derechos adicionales para modificar, extraer, reenviar o guardar el contenido.

- Android: [CommonRights.View](https://msdn.microsoft.com/library/dn758258.aspx)
- iOS y OS X: [MSCommonRights view](https://msdn.microsoft.com/library/dn758314.aspx)
- Tienda Windows y Windows Phone: [CommonRights.View](https://msdn.microsoft.com/library/microsoft.rightsmanagement.commonrights.view.aspx)
- Linux: [CommonRights::View](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## <a name="editable-document-rights"></a>Derechos de documentos editables
**All**: colección que contiene todos los derechos de documentos editables.
- Android: [EditableDocumentRights.All](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights all](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.all.aspx)
- Linux: [EditableDocumentRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment**: derecho para hacer comentarios en el documento.
- Android: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights comment](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Comment](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.comment.aspx)
- Linux: [EditableDocumentRights::Comment](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit**: derecho para editar contenido protegido y guardarlo en el mismo formato protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario cambiar el contenido protegido y después guardarlo en el mismo archivo.
- Android: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights edit](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Edit](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.edit.aspx)
- Linux: [EditableDocumentRights::Edit](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export**: derecho para extraer contenido de un formato protegido y colocarlo en un formato diferente protegido por AD RMS. Normalmente, cuando se concede este derecho, la aplicación permite al usuario guardar contenido protegido en otros formatos protegidos por AD RMS; por ejemplo, si la aplicación implementa una funcionalidad *Guardar como*.

- Android: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights exportable](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Export](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.export.aspx)
- Linux: [EditableDocumentRights::Export](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract**: derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al usuario copiar y pegar información de contenido protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al usuario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para correo electrónico.

- Android: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights extract](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Extract](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.extract.aspx)
- Linux: [EditableDocumentRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print**: derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario imprimir contenido protegido. Este derecho tiene el mismo valor que el derecho Print para correo electrónico.

- Android: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/dn758284.aspx)
- iOS y OS X: [MSEditableDocumentRights print](https://msdn.microsoft.com/library/dn758318.aspx)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.editabledocumentrights.print.aspx)
- Linux: [EditableDocumentRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## <a name="email-rights"></a>Derechos de correo electrónico

**All**: colección que contiene todos los derechos de correo electrónico.
- Android: [EmailRights.All](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights all](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.All](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.all.aspx)
- Linux: [EmailRights::All](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract**: derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico copiar y pegar información de un mensaje protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al destinatario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para documentos editables.

- Android: [EmailRights.Extract](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights extract](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.Extract</strong>](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.extract.aspx)
- Linux: [EmailRights::Extract](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward**: derecho para reenviar un mensaje protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico reenviar un mensaje protegido.
- Android: [<strong>EmailRights.Forward</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights forward](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.Forward](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.forward.aspx)
- Linux: [EmailRights::Forward](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print**: derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico imprimir un mensaje protegido. Este derecho tiene el mismo valor que el derecho Print para documentos editables.

- Android: [EmailRights.Print](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights print](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.Print](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.print.aspx)
- Linux: [EmailRights::Print](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply**: normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a un mensaje protegido e incluir una copia del mensaje original.

- Android: [EmailRights.Reply](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights reply](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.Reply](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.reply.aspx)
- Linux: [EmailRights::Reply](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll**: normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a todos los destinatarios de un mensaje protegido e incluir una copia del mensaje original.

- Android: [EmailRights.ReplyAll</strong>](https://msdn.microsoft.com/library/dn758285.aspx)
- iOS y OS X: [MSEmailRights replyAll](https://msdn.microsoft.com/library/dn758319.aspx)
- Tienda Windows y Windows Phone: [EmailRights.ReplyAll](https://msdn.microsoft.com/library/microsoft.rightsmanagement.emailrights.replyall.aspx)
- Linux: [EmailRights::ReplyAll](https://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)
