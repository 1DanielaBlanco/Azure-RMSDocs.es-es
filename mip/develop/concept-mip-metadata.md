---
title: 'Conceptos: etiqueta de metadatos en el SDK de MIP'
description: Este artículo le ayudará a comprender los metadatos que se generan mediante el SDK de Microsoft Information Protection.
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 990f729edaa0a2e212812f84fc5a4c63f82e37fb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253976"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft Information Protection SDK - metadatos

El SDK de Microsoft Information Protection genera el conjunto de metadatos que se deben aplicar a un archivo. Estos metadatos son una representación de la etiqueta. Este documento describe los metadatos que genera el SDK para aplicar al correo electrónico, documentos y otros registros.

## <a name="labels"></a>Etiquetas

Las etiquetas en el SDK de Microsoft Information Protection se aplican a la información para describir la confidencialidad de dicha información. Datos de etiqueta se guardan en el archivo o un registro en un conjunto de pares clave-valor que describen la etiqueta. El nombre de metadatos se basa en la siguiente estructura:

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

Cuando se aplica a los datos etiquetados con Microsoft Information Protection, el resultado es:

`MSIP_Label_GUID_Enabled = true`

El GUID es un identificador único para cada etiqueta de una organización.

## <a name="microsoft-information-protection-sdk-metadata"></a>Metadatos SDK de Microsoft Information Protection

El SDK de MIP se aplica el siguiente conjunto de metadatos.

| Atributo | Tipo de valor                 | Descripción                                                                                                                                                                                                                                        | obligatorio |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Enabled**   | True o False                 | Este atributo indica si está habilitada la clasificación representada por este conjunto de pares de clave y valor para el elemento de datos. Productos DLP normalmente validan la existencia de esta clave para identificar la etiqueta de clasificación. | Sí       |
| **SiteId**    | GUID                          | Identificador de inquilino de Azure Active Directory                                                                                                                                                                                                                   | Sí       |
| **ActionId**  | GUID                          | ActionID cambia cada vez que se establece una etiqueta. Los registros de auditoría incluirá actionID antiguo y nuevo para permitir el encadenamiento de etiquetado de actividad para el elemento de datos.                                                                                 | Sí       |
| **Método**    | Estándar con privilegios o Auto        | Establecer a través de MIP:: assignmentmethod                                                                                                                                                                                                                 | No        |
| **SetDate**   | Formato de fecha extendido ISO 8601 | La marca de tiempo cuando se estableció la etiqueta.                                                                                                                                                                                                              | No        |
| **Name**      | string                        | Nombre único de etiqueta en el inquilino. No se corresponde necesariamente para mostrar el nombre.                                                                                                                                                              | No      |
| **ContentBits** | integer | Máscara de bits que describe los tipos de contenido de marcado que se debe aplicar a un archivo. CONTENT_HEADER = 0X1, CONTENT_FOOTER = 0X2, WATERMARK = 0X4
 | No |

Cuando se aplica a un archivo, el resultado es similar a la tabla siguiente.

| Key                                                         | Valor                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | Con privilegios                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | Confidencial                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>Extender metadatos con atributos personalizados

Metadatos personalizados se pueden anexar a través de archivo y la directiva de API. Los atributos personalizados deben mantener la base de `MSIP_Label_GUID` prefijo. 

Por ejemplo, una aplicación escrita por Contoso Corporation debe aplicar metadatos que indican que el sistema que genera un archivo con la etiqueta. La aplicación puede crear una nueva etiqueta con el prefijo `MSIP_Label_GUID`. El nombre del proveedor de software y el atributo personalizado se anexan al prefijo para generar los metadatos personalizados.

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> Para mantener la compatibilidad de aplicaciones comunes, la longitud máxima para cada una clave y un valor es de 255 caracteres.

## <a name="versioning"></a>Control de versiones

Con el tiempo, los atributos se se introdujo, modificados o retirados. Se espera que las aplicaciones seguirá controlando estos antiguo o retirado los atributos, como reemplazar el valor en toda la empresa pueden tardar años.

Cuando se reemplaza un atributo con una versión más reciente, debe agregarse un sufijo de versión para el atributo:

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>Correo electrónico

Metadatos que se aplica al correo electrónico mantiene un par clave/valor de formato similar de documentos. La principal diferencia es que todos los atributos se serializan en a un encabezado de correo electrónico único llamado **MSIP_Labels**. Los pares clave/valor están delimitados por punto y coma y un espacio en blanco y coloca en el encabezado nuevo.

Uso de los metadatos del ejemplo anterior:

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
