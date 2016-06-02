---
# required metadata

title: Cómo usar los derechos integrados | Azure RMS
description: Se describen los derechos integrados que proporciona RMS SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones.
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Cómo usar los derechos integrados

En este tema se describen los derechos integrados que proporciona Microsoft Rights Management SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones. A continuación se muestran los derechos integrados, los derechos comunes, los derechos de documentos editables y los derechos de correo electrónico, seguidos de una descripción y de sus valores por sistema operativo.

**Nota**: En el caso del SDK de Linux, consulte el archivo de origen *rights.h* para obtener más información.

## Derechos comunes ##

**All**: colección de todos los derechos comunes.
- Android: [CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL)
- iOS y OS X: [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Tienda Windows y Windows Phone: [CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)
- Linux: [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

** Owner**: el derecho Owner concede control total sobre el contenido protegido.
- Android: [<strong>CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner)
- iOS y OS X: [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Tienda Windows y Windows Phone: [CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner)
- Linux: [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)

**View**: derecho para ver contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario abrir y ver contenido protegido. Sin embargo, se requieren derechos adicionales para modificar, extraer, reenviar o guardar el contenido.

- Android: [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- iOS y OS X: [MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)
- Tienda Windows y Windows Phone: [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View)
- Linux: [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)</li>

 

## Derechos de documentos editables ##
**All**: colección que contiene todos los derechos de documentos editables.
- Android: [EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL)
- iOS y OS X: [MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all)
- Linux: [EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Comment**: derecho para hacer comentarios en el documento.
- Android: [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)
- iOS y OS X: [MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)
- Linux: [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Edit**: derecho para editar contenido protegido y guardarlo en el mismo formato protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario cambiar el contenido protegido y después guardarlo en el mismo archivo.
- Android: [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit)
- iOS y OS X: [MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit)
- Linux: [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Export**: derecho para extraer contenido de un formato protegido y colocarlo en un formato diferente protegido por AD RMS. Normalmente, cuando se concede este derecho, la aplicación permite al usuario guardar contenido protegido en otros formatos protegidos por AD RMS; por ejemplo, si la aplicación implementa una funcionalidad *Guardar como*.

- Android: [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export)
- iOS y OS X: [MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export)
- Linux: [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Extract**: derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al usuario copiar y pegar información de contenido protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al usuario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para correo electrónico.

- Android: [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract)
- iOS y OS X: [MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract)
- Linux: [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

**Print**: derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario imprimir contenido protegido. Este derecho tiene el mismo valor que el derecho Print para correo electrónico.

- Android: [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print)
- iOS y OS X: [MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)
- Tienda Windows y Windows Phone: [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print)
- Linux: [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)

 

## Derechos de correo electrónico ##

**All**: colección que contiene todos los derechos de correo electrónico.
- Android: [EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL)
- iOS y OS X: [MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)
- Linux: [EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Extract**: derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico copiar y pegar información de un mensaje protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al destinatario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para documentos editables.

- Android: [EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract)
- iOS y OS X: [MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract)
- Linux: [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Forward**: derecho para reenviar un mensaje protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico reenviar un mensaje protegido.
- Android: [<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward)
- iOS y OS X: [MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward)
- Linux: [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Print**: derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico imprimir un mensaje protegido. Este derecho tiene el mismo valor que el derecho Print para documentos editables.

- Android: [EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print)
- iOS y OS X: [MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print)
- Linux: [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**Reply**: normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a un mensaje protegido e incluir una copia del mensaje original.

- Android: [EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply)
- iOS y OS X: [MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply)
- Linux: [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

**ReplyAll**: normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a todos los destinatarios de un mensaje protegido e incluir una copia del mensaje original.

- Android: [EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll)
- iOS y OS X: [MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc)
- Tienda Windows y Windows Phone: [EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall)
- Linux: [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)

 

 

 


<!--HONumber=Apr16_HO4-->


