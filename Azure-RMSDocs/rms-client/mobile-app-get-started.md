---
title: 'Introducción: aplicación AIP para iOS y Android'
description: ''
keywords: Cómo ver correos electrónicos o archivos con la aplicación de Azure Information Protection para iOS y Android
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/05/2017
ms.topic: article
ms.prod: azure
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3d5d18d8-7b2e-456c-bb45-48da4eb55544
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ccee69ba4f0b17440e9748787502a480e692de7c
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="get-started-with-the-microsoft-azure-information-protection-app-for-ios-and-android"></a>Introducción a la aplicación de Microsoft Azure Information Protection para iOS y Android

*Se aplica a: Active Directory Rights Management Services y [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Antes de seguir las instrucciones de esta página, asegúrese de que ha leído las [Preguntas más frecuentes sobre la aplicación de Azure Information Protection para iOS y Android](mobile-app-faq.md). En esa página se explica para qué sirve la aplicación, qué dispositivos son compatibles e información básica sobre cómo usar la aplicación.

Normalmente, la mayoría de los usuarios usarán la aplicación de Azure Information Protection cuando abran un archivo o un correo electrónico protegido. Pero si es administrador y quiere probar la aplicación para los usuarios, o simplemente quiere probarla antes de necesitarla, puede usar las instrucciones siguientes.

> [!NOTE]
> En este caso, no debe abrir primero la aplicación para seleccionar los documentos y correos electrónicos que quiera ver. En su lugar, abra el documento o correo electrónico y, a continuación, seleccione esta aplicación para ver el documento o correo electrónico.
>
> De forma similar, no intente iniciar sesión en la aplicación hasta que se le pida.

Para acceder al visor y ver cómo funciona, abra en el dispositivo móvil uno de los archivos compatibles con la aplicación. Por ejemplo:

- **Un archivo .rpmsg**: se trata de un mensaje de correo electrónico protegido por derechos que se muestra como un archivo adjunto en un mensaje de correo electrónico cuando la aplicación de correo electrónico de su dispositivo móvil no admite de forma nativa la protección de datos de Rights Management. 
    
    Use otro dispositivo para enviarse a usted mismo un mensaje de correo electrónico protegido por derechos al que pueda acceder desde su dispositivo móvil. Por ejemplo, use Outlook en un equipo Windows. Para ver una lista de clientes de correo electrónico que admiten de forma nativa Rights Management, vea la columna CORREO ELECTRÓNICO de la página [Aplicaciones compatibles con la protección de datos de Azure Rights Management](../get-started/requirements-applications.md).

- **Un archivo PDF protegido por derechos**: desde un equipo con Windows, utilice el cliente de Azure Information Protection para [proteger un archivo PDF](client-classify-protect.md) y, después, envíe manualmente este archivo PDF protegido por derechos como datos adjuntos de correo electrónico. También puede cargar un archivo PDF en una biblioteca protegida de SharePoint y, después, compartirlo mediante su dirección de correo electrónico.

- **Un .ptxt, .pjpg o .ppng**: desde un equipo con Windows, use el cliente de Azure Information Protection para proteger un archivo de texto o imagen y envíe manualmente este archivo protegido como datos adjuntos de correo electrónico. Para obtener la lista completa de tipos de archivo que puede utilizar para realizar pruebas, consulte la primera tabla de la sección [Tipos de archivos compatibles para protección y clasificación](client-admin-guide-file-types.md#supported-file-types-for-classification-and-protection) de la Guía para administradores del cliente de Azure Information Protection. 

Para ver estos archivos en la aplicación de visor de Azure Information Protection, pulse el vínculo o el archivo adjunto del correo electrónico. Cuando se le pida que seleccione una aplicación para abrirlo, seleccione la aplicación **Visor AIP**. A continuación se le solicitará que inicie sesión con su cuenta profesional o educativa, o que seleccione un certificado. Una vez que las credenciales se hayan autenticado, la aplicación de Azure Information Protection mostrará el correo electrónico o el archivo para que lo lea.

## <a name="next-steps"></a>Pasos siguientes

Si tiene preguntas o comentarios sobre esta aplicación que no se tratan en las [Preguntas más frecuentes](mobile-app-faq.md), visite nuestro [sitio de Yammer](https://www.yammer.com/AskIPTeam).

Si la aplicación no funciona como se describe, consulte los recursos enumerados en nuestra página [Reglas internas](../house-rules.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]