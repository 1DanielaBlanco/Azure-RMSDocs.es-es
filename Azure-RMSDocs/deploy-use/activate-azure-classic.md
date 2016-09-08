---
title: "Activación de Azure Rights Management desde el Portal de Azure clásico | Azure RMS"
description: "Si tiene acceso al Portal de Azure, siga estas instrucciones. Por ejemplo, tiene una suscripción para Enterprise Mobility Suite o tiene la suscripción de Azure Rights Management Premium."
author: cabailey
manager: mbaldwin
ms.date: 06/27/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 9b0a0227-88ce-44b8-ba3f-31eeaab27ff7
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: 573aa437d8449212bd2f22b532342e4c7e3a1be6


---

# Activación de Azure Rights Management desde el Portal de Azure clásico

>*Se aplica a: Azure Rights Management*


Si tiene acceso al Portal de Azure, siga estas instrucciones. Por ejemplo, tiene una suscripción para Enterprise Mobility Suite o tiene la suscripción de Azure Rights Management Premium.

> [!TIP]
> Consulte un vídeo de 2 minutos: [Activación de Azure RMS](https://channel9.msdn.com/series/pit-stop-enterprise-mobility-suite/activate-azure-rms)

1.  Después de registrarse para obtener la cuenta de Azure, [inicie sesión en el Portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=275081). Use una cuenta de administrador global, como la cuenta que ha usado para obtener la suscripción que incluye Azure Rights Management.

2.  En el panel izquierdo, haga clic en **ACTIVE DIRECTORY**.

3.  En la página **Active Directory** , haga clic en **RIGHTS MANAGEMENT**.

4.  Seleccione el directorio que administrará para [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)], haga clic en **ACTIVAR** y confirme la acción.

    > [!NOTE]
    >Si ve un error de activación, puede que el plan de servicio o la versión del producto no incluyan [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)].
    >
    >Utilice la información de [Suscripciones en la nube que admiten Azure RMS](../get-started/requirements-subscriptions.md) para confirmar la compatibilidad con RMS. Para obtener ayuda con este problema, envíe un mensaje de correo electrónico a [askipteam](mailto:askipteam?subject=I%20cannot%20activate%20RMS).


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


<!--HONumber=Aug16_HO4-->


