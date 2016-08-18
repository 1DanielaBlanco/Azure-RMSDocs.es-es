---
title: Directiva predeterminada de Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 08/08/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 0e02a3f78f1c5986d61f73e57265b944e9d03552
ms.openlocfilehash: 4abce96c4e1215f92211a231a187bd2de4ad3845


---

# Directiva predeterminada de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Utilice la siguiente información para comprender cómo está configurada la directiva predeterminada de Azure Information Protection. Si modifica la directiva predeterminada, puede tomar estos valores como referencia para devolver la directiva a la configuración predeterminada.

## Barra de Information Protection

|Configuración|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidad|
|Información sobre herramientas|Information Sensitivity consta de cuatro niveles distintos (Público, Interno, Confidencial y Secreto), que permiten al usuario identificar el riesgo de exposición de la información a usuarios no autorizados dentro o fuera de la empresa.|

## Etiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo para uso personal. Estos datos no se supervisan en la organización. La información personal no debe incluir datos relacionados con el negocio.|**Habilitada**: activada <br /><br />**Color**: verde claro<br /><br />**Marcas visuales**: desactivadas <br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|
|Público|Esta información es interna y todo el mundo puede usarla, tanto dentro como fuera de la empresa.|**Habilitada**: activada <br /><br />**Color**: verde<br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|
|Interno|Esta información incluye una amplia variedad de datos empresariales internos que todos los empleados pueden usar y que se pueden compartir con clientes y asociados comerciales autorizados. Ejemplos de información interna son las directivas de empresa y la mayoría de las comunicaciones internas.|**Habilitada**: activada <br /><br />**Color**: azul <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|
|Confidencial|Estos datos incluyen información empresarial confidencial. Exponer estos datos a usuarios no autorizados puede provocar daños para la organización. Ejemplos de información confidencial son información de los empleados, proyectos o contratos de clientes individuales y datos de cuentas de ventas.|**Habilitada**: activada <br /><br />**Color**: naranja<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|
|Secreto|Estos datos incluyen información confidencial de la empresa que se debe proteger. Exponer datos secretos a usuarios no autorizados puede provocar daños graves para la organización. Ejemplos de información secreta son información de identificación personal, registros de cliente, código fuente e informes financieros previamente anunciados.|**Habilitada**: activada <br /><br />**Color**: rojo<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|

## Etiquetas secundarias

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|*Secreto* > All Company (Toda la compañía)|Estos datos incluyen información empresarial confidencial, permitida para todos los empleados de la empresa.|**Habilitada**: activada <br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|
|*Secreto* > My Group (Mi grupo)|Estos datos incluyen información empresarial confidencial, permitida solo para grupos de empleados.|**Habilitada**: activada <br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: no|

## Configuración global

|Configuración|Valor|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) [Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios)]|Desactivado|
|Select the default label (Seleccionar la etiqueta predeterminada)|Ninguno|
|Users must provide justification when lowering the sensitivity level (for example, from Confidential to Public) [Los usuarios deben proporcionar justificación al bajar el nivel de confidencialidad (por ejemplo, de Confidencial a Público)]|Desactivado|


## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización). 



<!--HONumber=Aug16_HO2-->


