---
title: Lectores PDF protegidos para Microsoft Information Protection
description: Obtenga más información sobre los documentos PDF etiquetados para clasificación y protección y sobre cómo visualizarlos.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2018
ms.topic: article
ms.service: information-protection
ms.assetid: aab59e02-930b-4a17-8442-2d5d081fe1a6
ms.reviewer: kartikka
ms.suite: ems
ms.openlocfilehash: c6d02b5b7f82acc8b540fca57c2a7e8ab56f76fb
ms.sourcegitcommit: 2c90f5bf11ec34ab94824a39ccab75bde71fc3aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314822"
---
# <a name="supported-pdf-readers-for-microsoft-information-protection"></a>Lectores PDF compatibles con Microsoft Information Protection

Use la siguiente información para obtener más datos sobre los documentos PDF etiquetados para clasificación y protección y sobre cómo visualizarlos.

La colaboración entre Microsoft y Adobe ofrece una experiencia más simplificada y coherente para los documentos PDF que se han clasificado y, opcionalmente, protegido. Esta colaboración proporciona compatibilidad de la integración nativa de Acrobat con las soluciones de Microsoft Information Protection, como [Azure Information Protection](../what-is-information-protection.md). 

Esta integración nativa tiene las siguientes ventajas:

- Permite ver documentos PDF que se han protegido porque contienen información confidencial.

- Permite ver el valor de clasificación de la etiqueta de la organización que se ha aplicado al documento.

- Compatibilidad con el estándar ISO para cifrado de archivos PDF.
    
    A menos que esta funcionalidad se haya [deshabilitado por un administrador](client-admin-guide-customizations.md#dont-protect-pdf-files-by-using-the-iso-standard-for-pdf-encryption), este formato de archivo PDF protegido ahora está habilitado de forma predeterminada en la versión más reciente del cliente de Azure Information Protection.

Para más información, vea la siguiente entrada de blog: [Starting October, use Adobe Acrobat Reader for PDFs protected by Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Starting-October-use-Adobe-Acrobat-Reader-for-PDFs-protected-by/ba-p/262738) (A partir de octubre, use Adobe Acrobat Reader para los archivos PDF protegidos mediante Microsoft Information Protection)

## <a name="supported-pdf-readers"></a>Lectores PDF compatibles

Los lectores PDF siguientes pueden abrir archivos PDF protegidos que cumplen el estándar ISO para cifrado de archivos PDF:

|Sistema operativo|Lectores compatibles y vínculo de descarga|
|----------------|-----------------------------------|
|De Windows 10 y versiones anteriores<br />a Windows 7 Service Pack 1|Adobe Acrobat Reader (preferido):<br />-  1. Leer los [Términos de uso generales de Adobe](https://www.adobe.com/legal/terms.html) <br />- 2. Instalar Adobe Reader desde el [sitio de Adobe](https://www.adobe.com/)<br />- 3. Instalar el [complemento Adobe](https://go.microsoft.com/fwlink/?linkid=2050049)<br />- 4. Si se le solicita, pídale al administrador que [autorice el complemento](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/General-Availability-of-Adobe-Acrobat-Reader-integration-with/ba-p/298396) <br /><br /> Visor de Azure Information Protection: [Descargar](https://go.microsoft.com/fwlink/?linkid=838993)<br /><br />Foxit Reader: [Descargar](https://www.foxitsoftware.com/pdf-reader/)|
|Android|Aplicación Azure Information Protection: [Descargar](https://go.microsoft.com/fwlink/?LinkId=325340)|
|iOS|Aplicación Azure Information Protection: [Descargar](https://go.microsoft.com/fwlink/?LinkId=325338)|

### <a name="support-for-previous-formats"></a>Compatibilidad con formatos anteriores

Los lectores PDF de la siguiente tabla admiten documentos PDF protegidos con una extensión de nombre de archivo .ppdf y formatos más antiguos con una extensión de nombre de archivo .pdf.

Actualmente, SharePoint Online y SharePoint local usan un formato más antiguo para los documentos PDF de las bibliotecas protegidas por IRM.


|Sistema operativo|Lectores compatibles|
|----------------|-----------------------------------|
|De Windows 10 y versiones anteriores<br />a Windows 7 Service Pack 1|Visor de Azure Information Protection<br /><br />Gaaiho Doc<br /><br />GigaTrust Desktop PDF Client for Adobe<br /><br />Foxit Reader<br /><br />Nitro PDF Reader<br /><br /> Nuance Power PDF<br /><br />Aplicación RMS sharing|
|Android|Aplicación Azure Information Protection<br /><br />Foxit MobilePDF con RMS<br /><br />GigaTrust App para Android|
|iOS|Aplicación Azure Information Protection<br /><br />Foxit MobilePDF con RMS<br /><br />Documentos TITUS|
