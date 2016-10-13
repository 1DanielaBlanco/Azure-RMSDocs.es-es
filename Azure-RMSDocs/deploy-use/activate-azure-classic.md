---
title: "Cómo activar Azure Rights Management desde el Portal de Azure clásico | Azure Information Protection"
description: "Instrucciones de activación del servicio Azure Rights Management cuando tiene acceso a Azure Portal. Por ejemplo, tiene una suscripción para Enterprise Mobility Suite o tiene la suscripción de Azure Information Protection Premium."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 805644a7c6dacc00519ad9ac07f39367d0784745
ms.openlocfilehash: a553ea57bd4b396b7629dc24aea9f76b4a2a5e5a


---

# Activación de Azure Rights Management desde el Portal de Azure clásico

>*Se aplica a: Azure Information Protection*


Si tiene acceso al Portal de Azure, siga estas instrucciones. Por ejemplo, tiene una suscripción para Enterprise Mobility Suite o tiene la suscripción de Azure Information Protection Premium.

> [!TIP]
> Consulte un vídeo de 2 minutos: [Activación de Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Después de registrarse para obtener la cuenta de Azure, [inicie sesión en el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081). Use una cuenta de administrador global, como la cuenta que ha usado para obtener la suscripción que incluye Azure Rights Management.

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que administrará para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], haga clic en **ACTIVAR** y confirme la acción.

    > [!NOTE]
    >Si ve un error de activación, quizá sea porque su plan de servicio o la versión del producto no incluyen el servicio Azure Rights Management para Azure Information Protection.
    >
    >Use la [información de suscripción](https://go.microsoft.com/fwlink/?LinkId=827589) para confirmar que su suscripción incluye Azure Rights Management. Para obtener ayuda con este problema, envíe un mensaje de correo electrónico a [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


El **ESTADO DE RIGHTS MANAGEMENT** debe indicar ahora **Activo** y la opción **ACTIVAR** debe aparecer reemplazada por **DESACTIVAR**.

## Descripciones y valores de estado de Rights Management en el Portal de Azure clásico.
Además del estado **Activo** , que indica que el servicio de Rights Management está habilitado y listo para usarse, es posible que también vea **Inactivo**, **No disponible**o **No autorizado**.

|Valor de estado|Descripción|
|----------------|---------------|
|**Activo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está habilitado y listo para usarse.|
|**Inactivo**|[!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está deshabilitado y se debe activar antes de que la organización pueda proteger archivos.|
|**No disponible**|El servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] está inactivo. Inténtelo de nuevo más tarde.|
|**No autorizado**|No tiene permisos para ver el estado del servicio [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)]. Por ejemplo, su cuenta está bloqueada o no es el administrador global del inquilino seleccionado.|

## Pasos siguientes
Vuelva a [Activación de Rights Management de Azure](activate-service.md).


<!--HONumber=Sep16_HO4-->


