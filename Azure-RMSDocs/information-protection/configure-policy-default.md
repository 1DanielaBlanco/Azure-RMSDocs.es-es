---
title: Directiva predeterminada de Azure Information Protection | Azure Rights Management
description: 
author: cabailey
manager: mbaldwin
ms.date: 07/21/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 671281c8-f0d1-42b6-aae3-681d1821e2cf
translationtype: Human Translation
ms.sourcegitcommit: 93444affe94b280db2c9e4e2960c6902e491dec6
ms.openlocfilehash: 977cbf2f45cab75aaca9c2a16dd1564c2af2fe4a


---

# Directiva predeterminada de Azure Information Protection

>*Se aplica a: Azure Information Protection (versión preliminar)*

**[Esta información es preliminar y está sujeta a cambios. ]**

Utilice la siguiente información para comprender cómo está configurada la directiva predeterminada de Azure Information Protection. Si modifica la directiva predeterminada, puede tomar estos valores como referencia para devolver la directiva a la configuración predeterminada.

## Barra de Information Protection

Título: **Confidencialidad**

Información sobre herramientas: **Information Sensitivity consta de cuatro niveles distintos (Público, Interno, Confidencial y Secreto), que permiten al usuario identificar el riesgo de exposición de la información a usuarios no autorizados dentro o fuera de la empresa.**


## Etiquetas

Hay 5 etiquetas predeterminadas con los siguientes valores:

### **Personal**

Información sobre herramientas: ** Solo para uso personal. Estos datos no se supervisan en la organización. La información personal no debe incluir datos relacionados con el negocio.**

Color verde claro

Marcas visuales: ninguna

Condiciones: ninguna

Protección: no

----


### **Público**

Información sobre herramientas: **Esta información es interna y todo el mundo puede usarla, tanto dentro como fuera de la empresa.**

Color verde

Marcas visuales: ninguna

Condiciones: ninguna

Protección: no

----

### **Interno**

Información sobre herramientas: **Esta información incluye una amplia variedad de datos empresariales internos que todos los empleados pueden utilizar y que se pueden compartir con clientes y socios comerciales autorizados. Ejemplos de información interna son las directivas de empresa y la mayoría de las comunicaciones internas.**

Color azul

Marcas visuales: pie de página (documentos y correo electrónico)

Condiciones: ninguna

Protección: no

----

### **Confidencial**

Información sobre herramientas: **Estos datos incluyen información empresarial confidencial. Exponer estos datos a usuarios no autorizados puede provocar daños para la organización. Ejemplos de información confidencial son información de los empleados, proyectos o contratos de clientes individuales y datos de cuentas de ventas.**

Color naranja

Marcas visuales: pie de página (documentos y correo electrónico)

Condiciones: ninguna

Protección: no

----

### **Secreto**

Información sobre herramientas: **Estos datos incluyen información confidencial de la empresa que se debe proteger. Exponer datos secretos a usuarios no autorizados puede provocar daños graves para la organización. Ejemplos de información secreta son información de identificación personal, registros de cliente, código fuente e informes financieros previamente anunciados.**

Color rojo

Marcas visuales: pie de página (documentos y correo electrónico)

Condiciones: ninguna

Protección: no

----


## Etiquetas secundarias

Hay 2 etiquetas secundarias predeterminadas con los siguientes valores:

### Secreto > **All Company** (Toda la compañía)

Información sobre herramientas: **Estos datos incluyen información empresarial confidencial, permitida para todos los empleados de la empresa.**

Marcas visuales: ninguna

Condiciones: ninguna

Protección: no

----

### Secreto > **My Group** (Mi grupo)

Información sobre herramientas: **Estos datos incluyen información empresarial confidencial, permitida solo para grupos de empleados.**

Marcas visuales: ninguna

Condiciones: ninguna

Protección: no

## Configuración global

**All documents and emails must have a label (applied automatically or by users)**(Todos los documentos y correos electrónicos deben tener una etiqueta (aplicada automáticamente o por los usuarios): Off (Desactivado)

**Select the default label** (Seleccionar la etiqueta predeterminada): Ninguna

**Users must provide justification when lowering the sensitivity level (for example, from Confidential to Public (Los usuarios deben proporcionar justificación al bajar el nivel de confidencialidad [por ejemplo, de Confidencial a Público])**: Off (Desactivado)

## Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organization-s-policy) (Configuración de la directiva de la organización). 



<!--HONumber=Jul16_HO5-->


