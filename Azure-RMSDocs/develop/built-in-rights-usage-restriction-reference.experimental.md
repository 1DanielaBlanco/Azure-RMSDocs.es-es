---
title: "Cómo usar los derechos integrados | Azure RMS"
description: "Se describen los derechos integrados que proporciona RMS SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones."
keywords: 
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9142dd29-f1f4-4c2f-82ac-534f14b8bba1
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
experiment_id: priyamo-TableVsFlatList-20160805
translationtype: Human Translation
ms.sourcegitcommit: ac7f8296149b93be803165ebde5144b0f78fa0c8
ms.openlocfilehash: 25bfc768aba30be7f81ce659ca90e71266c599ba


---

# Cómo usar los derechos integrados

En este tema se describen los derechos integrados que proporciona Microsoft Rights Management SDK 4.2 y las restricciones de uso que una aplicación debe exigir para cumplir con esas restricciones. En la siguiente tabla se muestran los derechos integrados, los derechos comunes, los derechos de documentos editables y los derechos de correo electrónico, seguidos de una descripción y de sus valores por sistema operativo.

**Nota**: En el caso del SDK de Linux, consulte el archivo de origen *rights.h* para obtener más información.

## Derechos comunes ##

| Right | Descripción | Android | iOS y OSX | Tienda Windows y Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** | Una colección de todos los derechos comunes. | [CommonRights.All](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_ALL) | [MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)| [CommonRights.All</strong>](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights)| [CommonRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Propietario**| Concede control total sobre el contenido protegido |  [CommonRights.Owner](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_Owner) |[MSCommonRights owner](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_) |[CommonRights.Owner](/rights-management/sdk/4.2/api/winrt/commonrights#msipcthin2_commonrights_owner) |  [CommonRights::Owner](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html)|
| **Vista** | El derecho para ver contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario abrir y ver contenido protegido. Sin embargo, se requieren derechos adicionales para modificar, extraer, reenviar o guardar el contenido. |  [CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [MSCommonRights view](/rights-management/sdk/4.2/api/iOS/mscommonrights#msipcthin2_mscommonrights_interface_objc___NSString__owner_)|[CommonRights.View](/rights-management/sdk/4.2/api/android/commonrights#msipcthin2_commonrights_class_java_View) | [CommonRights::View](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1CommonRights.html) |


## Derechos de documentos editables ##

| Right | Descripción | Android | iOS y OSX | Tienda Windows y Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** | Una colección que contiene todos los derechos de documentos editables.| [EditableDocumentRights.All](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_ALL) | [MSEditableDocumentRights all](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.All](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_all) |[EditableDocumentRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Comentario** | El derecho para hacer comentarios en el documento. | [EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Comment)|[MSEditableDocumentRights comment](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Comment](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights__comment)| [EditableDocumentRights::Comment](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Editar** | El derecho para editar contenido protegido y guardarlo en el mismo formato protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario cambiar el contenido protegido y después guardarlo en el mismo archivo. | [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Edit) | [MSEditableDocumentRights edit](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Edit](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_edit) | [EditableDocumentRights::Edit](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html) |
| **Exportar** | Derecho para extraer contenido de un formato protegido y colocarlo en un formato diferente protegido por AD RMS. Normalmente, cuando se concede este derecho, la aplicación permite al usuario guardar contenido protegido en otros formatos protegidos por AD RMS; por ejemplo, si la aplicación implementa una funcionalidad *Guardar como*. | [EditableDocumentRights.Export](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Export) | [MSEditableDocumentRights exportable](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) |[EditableDocumentRights.Export](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_export) | [EditableDocumentRights::Export](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Extracción** | Derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al usuario copiar y pegar información de contenido protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al usuario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para correo electrónico. |  [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Extract) |[MSEditableDocumentRights extract](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc) | [EditableDocumentRights.Extract](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_extract) |  [EditableDocumentRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
| **Imprimir** | El derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al usuario imprimir contenido protegido. Este derecho tiene el mismo valor que el derecho Print para correo electrónico. | [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/android/editabledocumentrights#msipcthin2_editabledocumentrights_class_java_Print) |  [MSEditableDocumentRights print](/rights-management/sdk/4.2/api/iOS/mseditabledocumentrights#msipcthin2_mseditabledocumentrights_interface_objc)| [EditableDocumentRights.Print](/rights-management/sdk/4.2/api/winrt/editabledocumentrights#msipcthin2_editabledocumentrights_print) | [EditableDocumentRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EditableDocumentRights.html)|
 

## Derechos de correo electrónico ##

| Right | Descripción | Android | iOS y OSX | Tienda Windows y Windows Phone | Linux |
|-------|-------------|---------|-------------|---------------------------------|-------|
| **Todos** |Una colección que contiene todos los derechos de correo electrónico. |  [EmailRights.All](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ALL) | [MSEmailRights all](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.All](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_all)|[EmailRights::All](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Extracción** | Derecho para extraer contenido de un formato protegido y colocarlo en un formato sin protección. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico copiar y pegar información de un mensaje protegido. Si la aplicación implementa una funcionalidad <em>Guardar como</em>, la aplicación también podría permitir al destinatario guardar contenido protegido en formatos no protegidos y otros formatos protegidos. Este derecho tiene el mismo valor que el derecho Extract para documentos editables. | [EmailRights.Extract](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Extract) | [MSEmailRights extract](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Extract</strong>](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_extract) | [EmailRights::Extract](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Reenviar**| El derecho para reenviar un mensaje protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico reenviar un mensaje protegido.| [<strong>EmailRights.Forward</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Forward) | [MSEmailRights forward](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Forward](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_forward) | [EmailRights::Forward](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html) |
|**Imprimir** | El derecho para imprimir contenido protegido. Normalmente, cuando se concede este derecho, la aplicación permite al destinatario de correo electrónico imprimir un mensaje protegido. Este derecho tiene el mismo valor que el derecho Print para documentos editables. | [EmailRights.Print](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Print) |[MSEmailRights print](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Print](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_print) | [EmailRights::Print](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Responder** | Normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a un mensaje protegido e incluir una copia del mensaje original. | [EmailRights.Reply](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_Reply) | [MSEmailRights reply](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.Reply](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_reply) | [EmailRights::Reply](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|
| **Responder a todos** | Normalmente, cuando se concede este derecho, la aplicación permite a un destinatario de correo electrónico responder a todos los destinatarios de un mensaje protegido e incluir una copia del mensaje original. | [EmailRights.ReplyAll</strong>](/rights-management/sdk/4.2/api/android/emailrights#msipcthin2_emailrights_class_java_ReplyAll) | [MSEmailRights replyAll](/rights-management/sdk/4.2/api/iOS/msemailrights#msipcthin2_msemailrights_interface_objc) | [EmailRights.ReplyAll](/rights-management/sdk/4.2/api/winrt/emailrights#msipcthin2_emailrights_replyall) | [EmailRights::ReplyAll](http://azuread.github.io/rms-sdk-for-cpp/classrmscore_1_1modernapi_1_1EmailRights.html)|



<!--HONumber=Aug16_HO2-->


