---
title: "Tutorial de inicio rápido de Azure Information Protection | Azure Rights Management"
description: "Un tutorial introductorio rápido para probar Microsoft Azure Information Protection para su organización en solo 4 pasos que deberían tardar menos de 15 minutos."
author: cabailey
manager: mbaldwin
ms.date: 07/16/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1260b9e5-dba1-41de-84fd-609076587842
translationtype: Human Translation
ms.sourcegitcommit: cac95dec84f99d2e6caa3458dc8284defe2324bc
ms.openlocfilehash: 7dc988365c1fa86827d1a7edc33c0a2eb6180f0e


---

# Tutorial de inicio rápido de Azure Information Protection 

*Se aplica a: Azure Information Protection (versión preliminar)*

Use este tutorial rápido para probar Azure Information Protection (versión preliminar) para su organización; son solo 4 pasos que deberían tardar menos de 15 minutos. Si quiere, puede activar el servicio de Azure Rights Management. Consulte y modifique la directiva predeterminada de Azure Information Protection, instale el cliente de Azure Information Protection y use un documento de Word para ver la clasificación, el etiquetado y la protección en acción.

Este tutorial está destinado a los administradores y consultores de TI a fin de ayudarles a evaluar Azure Information Protection como una solución de protección de la información para una organización. En un entorno de producción, el encargado de seguir las instrucciones para activar el servicio, configurar la directiva de Information Protection e instalar el cliente para los usuarios es el administrador, mientras que los encargados de seguir las instrucciones para etiquetar el documento son los usuarios finales. En este tutorial se incluyen los dos tipos de instrucciones para mostrar el escenario de extremo a extremo consistente en clasificar, etiquetar y proteger los datos de su organización. 

Si tiene algún problema para seguir este tutorial, para usar la versión preliminar de Azure Information Protection o si quiere ver lo que comentan otros usuarios, diríjase al [sitio de Yammer de Azure Information Protection](https://www.yammer.com/askipteam/#/threads/inGroup?type=in_group&feedId=8652489&view=all).

## Requisitos previos 
Para completar este tutorial, necesitará lo siguiente:

- Cualquier suscripción que incluya Azure Rights Management, que le dará acceso a la versión preliminar de Azure Information Protection. Azure Information Protection está disponible en todas las regiones en las que se admite Azure Rights Management. Para obtener más información sobre las suscripciones y los vínculos disponibles para las pruebas gratuitas, vea [Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md).

- Una suscripción a Azure, para que pueda obtener acceso al portal de Azure para configurar la directiva de Azure Information Protection. Si todavía no dispone de una suscripción a Azure para su organización, puede obtener una registrándose a una prueba gratuita: vaya a la página [Introducción a Azure](https://account.windowsazure.com/organization) y siga las instrucciones.

  > [!TIP] 
  > Si necesita obtener una o ambas suscripciones, hágalo con anticipación porque el proceso puede durar varios minutos.

- Una cuenta de administrador global para iniciar sesión en el centro de administración de Office 365 o en el Portal de Azure clásico si tiene que activar el servicio de Rights Management. Esta cuenta también debe tener una dirección de correo electrónico y un servicio de correo electrónico de trabajo (por ejemplo, Exchange Online o Exchange Server).

- Un equipo que ejecute Windows (a partir de Windows 7 con el Service Pack 1) y que tenga instalado Office 2016, Office 2013 con el Service Pack 1 u Office 2010. 

- Si tiene implementado Active Directory Rights Management Services (AD RMS) en su organización: el equipo debe ser un equipo de grupo de trabajo que no haya usado antes AD RMS. Este requisito es obligatorio si quiere proteger los documentos; además, garantiza que el equipo descargue plantillas únicamente de Azure Rights Management. No es válido si quiere conectar un equipo a AD RMS y Azure RMS al mismo tiempo. Si quiere obtener información sobre la migración, vea [Migración desde AD RMS a Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md).   

Comencemos.

>[!div class="step-by-step"]
[&#187; Paso 1](infoprotect-tutorial-step1.md)





<!--HONumber=Jul16_HO3-->


