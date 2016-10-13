---
title: La directiva predeterminada | Azure Information Protection
description: "Obtenga información sobre cómo está configurada la directiva predeterminada de Azure Information Protection. Si modifica la directiva predeterminada, puede tomar estos valores como referencia para devolver la directiva a la configuración predeterminada."
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 2fd29eb6dec94535d0358fe0a2d9c9285fcd7cd1
ms.openlocfilehash: 531d7a474daeea752fc8cd63b8b39e9fec373a24


---

# Directiva predeterminada de Azure Information Protection

>*Se aplica a: Azure Information Protection*

Utilice la siguiente información para comprender cómo está configurada la directiva predeterminada de Azure Information Protection. Si modifica la directiva predeterminada, puede tomar estos valores como referencia para devolver la directiva a la configuración predeterminada.

## Barra de Information Protection

|Configuración|Valor|
|-------------------------------|---------------------------|
|Título|Sensibilidad|
|Información sobre herramientas|Information Sensitivity consta de cuatro niveles distintos (Público, Interno, Confidencial y Secreto), que permiten al usuario identificar el riesgo de exposición de la información a usuarios no autorizados dentro o fuera de la empresa.|

## Etiquetas

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Personal|Solo para uso personal. Estos datos no se supervisan en la organización. La información personal no debe incluir datos relacionados con el negocio.|**Habilitada**: activada <br /><br />**Color**: verde claro<br /><br />**Marcas visuales**: desactivadas <br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|
|Público|Esta información es interna y todo el mundo puede usarla, tanto dentro como fuera de la empresa.|**Habilitada**: activada <br /><br />**Color**: verde<br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|
|Interno|Esta información incluye una amplia variedad de datos empresariales internos que todos los empleados pueden usar y que se pueden compartir con clientes y asociados comerciales autorizados. Ejemplos de información interna son las directivas de empresa y la mayoría de las comunicaciones internas.|**Habilitada**: activada <br /><br />**Color**: azul <br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|
|Confidencial|Estos datos incluyen información empresarial confidencial. Exponer estos datos a usuarios no autorizados puede provocar daños para la organización. Ejemplos de información confidencial son información de los empleados, proyectos o contratos de clientes individuales y datos de cuentas de ventas.|**Habilitada**: activada <br /><br />**Color**: naranja<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|
|Secreto|Estos datos incluyen información confidencial de la empresa que se debe proteger. Exponer datos secretos a usuarios no autorizados puede provocar daños graves para la organización. Ejemplos de información secreta son información de identificación personal, registros de cliente, código fuente e informes financieros previamente anunciados.|**Habilitada**: activada <br /><br />**Color**: rojo<br /><br />**Marcas visuales**: pie de página (documentos y correo electrónico)<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|

## Etiquetas secundarias

|Etiqueta|Información sobre herramientas|Configuración|
|-------------------------------|---------------------------|-----------------|
|Secreto \ All Company (Toda la compañía)|Estos datos incluyen información empresarial confidencial, permitida para todos los empleados de la empresa.|**Habilitada**: activada <br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|
|Secreto \ My Group (Mi grupo)|Estos datos incluyen información empresarial confidencial, permitida solo para grupos de empleados.|**Habilitada**: activada <br /><br />**Marcas visuales**: desactivadas<br /><br />**Condiciones**: ninguna<br /><br />**Protección**: ninguna|

## Configuración global

|Configuración|Valor|
|-------------------------------|---------------------------|
|All documents and emails must have a label (applied automatically or by users) [Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios)]|Desactivado|
|Select the default label (Seleccionar la etiqueta predeterminada)|Ninguno|
|Users must provide justification to set a lower classification label, remove a label, or remove protection (Los usuarios deben proporcionar una justificación para establecer una etiqueta de clasificación inferior, quitar una etiqueta o quitar la protección)|Desactivado|


## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización). 



<!--HONumber=Sep16_HO4-->


