---
# required metadata

title: Requisitos de Azure RMS&#58; Suscripciones en la nube | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/25/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 6a16e890-3c3e-4f47-80ca-176a34bdf8bc

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Requisitos de Azure RMS: Suscripciones en la nube que son compatibles con Azure RMS

*Se aplica a: Azure Rights Management, Office 365*

Para usar Azure Rights Management (Azure RMS), su organización debe tener al menos una de las siguientes suscripciones con un número suficiente de licencias para usuarios y servicios que protegerán archivos y mensajes de correo electrónico. Si tiene un servicio que aplicará protección para los usuarios (propietarios de los archivos o mensajes de correo electrónico), esos usuarios necesitan una de estas licencias. Los usuarios que solo consumen (por ejemplo, leen y editan) estos datos protegidos no necesita una licencia.

-   Office 365

-   Azure Rights Management Premium (anteriormente Azure RMS Standalone)

-   Enterprise Mobility Suite

-   RMS para usuarios

Use las secciones siguientes para obtener más información y conocer las opciones de registro.

Para ver una comparación de las licencias de las funcionalidades de Azure RMS correspondientes a las suscripciones de pago, consulte [Comparación de las ofertas de Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

¿Tiene preguntas adicionales sobre las licencias de Azure RMS? Descargue **Preguntas más frecuentes sobre licencias para Azure Rights Management** desde la página [Comprar Azure Rights Management](https://www.microsoft.com/en-us/server-cloud/products/azure-rights-management/Purchasing.aspx). 

## Suscripción a Office 365
[Evaluación gratuita de 30 días: Enterprise E3](http://go.microsoft.com/fwlink/p/?LinkID=403802)

Esta suscripción está diseñada para organizaciones que quieran usar los servicios en línea de Office y usar su característica Information Rights Management (IRM), que utiliza Azure RMS. Sin embargo, no todas las suscripciones de Office 365 incluyen Azure RMS.

Suscripción  |Incluye IRM 
------------- | ------------- |
Office 365 Empresa Essentials|No|
Office 365 Empresa Premium|No|
Office 365 Enterprise E1 <br /><br /> Office 365 Educación A1|No <br /><br /> No|
Office 365 Enterprise E3 <br /><br /> Office 365 Educación A3 <br /><br /> Office 365 Administración Pública G3|Sí <br /><br /> Sí <br /><br /> Sí|
Office 365 Enterprise E4 <br /><br /> Office 365 Educación A4 <br /><br /> Office 365 Administración Pública G4|Sí <br /><br /> Sí <br /><br /> Sí|
Office 365 Enterprise E5 <br /><br /> Office 365 Educación A5|Sí <br /><br /> Sí|
Office 365 Enterprise K1|No|
SharePoint plan 1 <br /><br /> SharePoint plan 2|No <br /><br /> No|
Exchange Online Plan 1 <br /><br /> Exchange Online Plan 2|No <br /><br /> No|


## Suscripción a Azure Rights Management Premium
[Prueba gratuita de 30 días](https://portal.microsoftonline.com/Signup/MainSignUp15.aspx?&amp;OfferId=A43415D3-404C-4df3-B31B-AAD28118A778&amp;dl=RIGHTSMANAGEMENT&amp;ali=1)

Esta suscripción antes se denominaba Azure RMS Standalone y está diseñada para organizaciones que desean usar Azure RMS para Office 365, pero la suscripción a Office no incluye Azure RMS. Por ejemplo, si tiene una suscripción para Office 365 Empresa Essentials u Office 365 Enterprise E1, estas suscripciones no incluyen Azure RMS (vea la tabla de la sección anterior). 

Para usar Azure RMS con cualquiera de las suscripciones de Office que no incluyen Azure RMS, podrá adquirir una suscripción a Azure Rights Management Premium. También puede comprar otra suscripción a Office que incluya Azure RMS, como Office 365 Enterprise E4.

> [!NOTE]
> Cuando usa esta suscripción con Office 365 Empresa Premium, hay algunas restricciones de cliente: puede proteger el contenido y consumir contenido protegido con RMS mediante Outlook Web App y la aplicación RMS sharing. Puede consumir contenido protegido, pero no proteger el contenido usando todas las demás aplicaciones de Office, donde se incluyen Office Online y las aplicaciones cliente para Office 365 Empresa Premium.

Para más información sobre la suscripción a Azure Rights Management Premium, consulte [Microsoft Azure Rights Management](http://products.office.com/business/microsoft-azure-rights-management).

Esta suscripción también ofrece un período de evaluación para probar Azure RMS para 25 usuarios, de manera gratuita. 

### ¿Qué ocurre cuando la suscripción de prueba expira?
Si su suscripción de prueba expira, perderá acceso al contenido protegido al usar su suscripción de prueba para Azure RMS. Sin embargo, si después compra una suscripción que admite Azure RMS, el acceso se restaura automáticamente.

Una excepción a la pérdida de acceso tras la expiración es si su organización usó Azure RMS con el RMS para la suscripción de individuos antes de que obtuviera la suscripción de prueba. A continuación, permanece el acceso al contenido anteriormente protegido, incluso después de que expire la suscripción de prueba.

## Suscripción a Enterprise Mobility Suite
[Prueba gratuita de 30 días](http://go.microsoft.com/fwlink/?LinkId=615385)

Esta suscripción está diseñada para organizaciones que quieran usar una combinación de Azure Active Directory Premium, Windows Intune y Azure Rights Management. La compatibilidad para el uso de Azure Rights Management con Office es la misma que al usar la suscripción a Azure Rights Management Premium. Para más información sobre la suscripción a Enterprise Mobility Suite, consulte la [Introducción a la movilidad empresarial Microsoft](http://go.microsoft.com/fwlink/?LinkId=615386).

## Suscripción a RMS para usuarios
Esta suscripción está diseñada para usuarios de una organización que no hayan implementado Azure RMS o AD RMS. Permite que estas personas lean contenido que se ha protegido por una organización que usa Azure RMS, a la vez que pueden proteger su propio contenido.

Es posible que la vea en el portal de administración de Office 365 como **Rights Management Adhoc** y asignada automáticamente a los usuarios. No asigne manualmente esta licencia a los usuarios ni la use para administrar Azure RMS para la organización. 

Para obtener más información, consulte [RMS for individuals and Azure Rights Management](../understand-explore/rms-for-individuals.md) (RMS para usuarios y Azure Rights Management).

## Pasos siguientes
Para buscar otros requisitos, consulte [Requisitos de Azure Rights Management](requirements-azure-rms.md).

<!--HONumber=May16_HO5-->


