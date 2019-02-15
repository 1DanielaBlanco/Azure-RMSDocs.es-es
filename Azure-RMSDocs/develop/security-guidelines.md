---
title: Procedimientos recomendados de seguridad para Information Protection
description: Las aplicaciones habilitadas para RMS se crean mejor mediante los procedimientos recomendados de Information Protection.
author: bryanla
ms.author: bryanla
manager: barbkess
ms.date: 12/13/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 0a9d8c0c6c86481dbce38d2cafde1c37c54b7b3e
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252867"
---
# <a name="security-best-practices-for-information-protection"></a>Procedimientos recomendados de seguridad para Information Protection

El Kit de desarrollo de Software (SDK) de Information Protection proporciona un sistema sólido para publicar y consumir información protegida de todo tipo. Para que un sistema sea lo más robusto posible, las aplicaciones habilitadas para Information Protection deben compilarse siguiendo procedimientos recomendados. Las aplicaciones comparten la responsabilidad de mantener la seguridad de este ecosistema. La identificación de los riesgos de seguridad y la provisión de mitigaciones para esos riesgos introducidos durante el desarrollo de la aplicación ayudan a reducir la probabilidad de que el software se implemente de una manera menos segura.

Esta información complementa el acuerdo legal que debe firmarse con el fin de obtener los certificados digitales para las aplicaciones mediante el SDK.

## <a name="subjects-not-covered"></a>Temas no cubiertos

Aunque los temas siguientes son consideraciones importantes para la creación de un entorno de desarrollo y aplicaciones seguras, están fuera del ámbito de este artículo:

- **Administración de procesos de desarrollo de software**: administración de la configuración, protección del código fuente, minimización del acceso al código depurado y asignación de prioridades entre los errores. Para algunos clientes, disponer de un proceso de desarrollo de software más seguro reviste una importancia fundamental. Algunos clientes incluso recomiendan un proceso de desarrollo.
- **Errores de codificación comunes**: información sobre cómo evitar las saturaciones del búfer. Para examinar estas amenazas genéricas y mitigaciones, se recomienda la versión más reciente de Writing Secure Code, de Michael Howard y David LeBlanc (Microsoft Press, 2002).
- **Ingeniería social**: incluye información sobre las medidas de seguridad procedimentales y estructurales para ayudar a proteger el código contra el aprovechamiento por desarrolladores u otras personas dentro de la organización del fabricante.
- **Seguridad física**: incluye información sobre cómo bloquear el acceso a la base de código y la firma de certificados.
- **Implementación o distribución de software de versión preliminar**: incluye información acerca de cómo distribuir el software beta.
- **Administración de redes**: incluye información acerca de los sistemas de detección de intrusiones en sus redes físicas.

## <a name="threat-models-and-mitigations"></a>Modelos de amenazas y mitigaciones

Los propietarios de la información digital necesitan la capacidad de evaluar los entornos en los que se van a descifrar sus activos. Una instrucción de estándares de seguridad mínimos puede proporcionar a los propietarios de la información un marco para entender y evaluar el nivel de seguridad de las aplicaciones.

Algunas industrias, como el gobierno y la asistencia sanitaria, tienen procesos y normas de certificación y acreditación que pueden aplicarse a su producto. El cumplimiento con estas recomendaciones de seguridad mínimas no reemplaza en ningún caso las necesidades de acreditación únicas de los clientes. Sin embargo, la intención de las normas de seguridad es ayudarle a prepararse para los requisitos del cliente actuales y futuros, y toda inversión que realice al principio del ciclo de desarrollo beneficiará a la aplicación. Se trata de guías y recomendaciones, no un programa formal de certificación de Microsoft.

Un sistema de Rights Management Services puede presentar diferentes categorías principales de vulnerabilidades, entre las que están las siguientes:

- **Fuga**: la información aparece en ubicaciones no autorizadas.
- **Daño**: el software o los datos se modifican de manera no autorizada.
- **Denegación**: un recurso informático no está disponible para su uso.

Estos temas se centran principalmente en los problemas de fuga. La integridad de un sistema de API depende de su capacidad, con el paso del tiempo, de proteger la información, permitiendo el acceso solo a las entidades designadas. En estos temas también se mencionan los daños. No se tratan los problemas de denegación.

Microsoft no prueba ni revisa los resultados de pruebas relacionados con el cumplimiento del estándar mínimo. El asociado es responsable de garantizar que se cumplen los estándares mínimos. Microsoft proporciona dos niveles adicionales de recomendaciones para ayudar a mitigar las amenazas comunes. En general, estas sugerencias son incrementales. Por ejemplo, el hecho de cumplir las recomendaciones preferidas da por supuesto que se han cumplido los estándares mínimos, en su caso, a menos que se especifique lo contrario.

|Nivel estándar|Descripción|
|---|---|
|Estándar mínimo| Una aplicación que controle la información protegida debe cumplir con el estándar mínimo a fin de que esta pueda firmarse con el certificado de producción recibido de Microsoft. Los asociados generalmente usan el certificado de la jerarquía de producción, en el momento del lanzamiento final del software. Las pruebas internas de un asociado se usan para comprobar si la aplicación cumple este estándar mínimo. El hecho de cumplir con el estándar mínimo no es una garantía de seguridad por parte de Microsoft, ni debe interpretarse como ello. Microsoft no prueba ni revisa los resultados de pruebas relacionados con el cumplimiento del estándar mínimo. El partner es responsable de garantizar que se cumplen los estándares mínimos.|
|Estándar recomendado| Las directrices recomendadas trazan una ruta hacia la mejora de la seguridad de la aplicación y proporcionan una indicación de cómo puede evolucionar el SDK a medida que se implementen más criterios de seguridad. Los proveedores pueden diferenciar sus aplicaciones ascendiendo a este nivel superior de directrices de seguridad.|
|Estándar preferido| Este estándar es la categoría más alta de seguridad definida actualmente. Los proveedores que desarrollen aplicaciones comercializadas bajo la etiqueta de "alta seguridad" deben tratar de alcanzar este estándar. Las aplicaciones que se adhieren este estándar suelen ser menos vulnerable a los ataques.|

## <a name="malicious-software"></a>Software malintencionado

Microsoft ha definido los estándares necesarios mínimos que debe cumplir la aplicación para proteger el contenido frente al software malintencionado.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importación de software malintencionado mediante tablas de direcciones

El SDK de protección de la información no admite la modificación del código en tiempo de ejecución ni la modificación de la tabla de importar direcciones. Se crea una tabla de importar direcciones para cada archivo DLL cargado en el espacio de proceso. Estas especifican las direcciones de todas las funciones que importa la aplicación. Un ataque habitual consiste en modificar las entradas de la tabla de importar direcciones dentro de una aplicación para que, por ejemplo, apunte a software malintencionado. El SDK detiene la aplicación cuando detecta este tipo de ataque.

### <a name="minimum-standard"></a>Estándar mínimo

- No se puede modificar la tabla de importación de direcciones en el proceso de aplicación durante la ejecución. La aplicación especifica muchas de las funciones llamadas en tiempo de ejecución mediante tablas de direcciones. Estas tablas no se pueden modificar durante el tiempo de ejecución o después de este. Esto restricción implica, entre otras cosas, que no es posible crear perfiles de código en una aplicación firmada con el certificado de producción.
- No se puede llamar a la función **DebugBreak** desde ningún DLL especificado en el manifiesto.
- No se puede llamar a **LoadLibrary** con la marca **DONT_RESOLVE_DLL_REFERENCES** configurada. Esta marca indica al cargador que omita el enlace a los módulos importados, modificando así la tabla para importar direcciones.
- No se puede modificar la carga diferida haciendo cambios de tiempo de ejecución o posteriores en el modificador del vinculador /DELAYLOAD.
- No se puede modificar la carga diferida proporcionando su propia versión de la función del asistente de Delayimp.lib.
- No se pueden descargar los módulos que se cargan de manera diferida por módulos autenticados mientras existe el entorno del SDK de protección.
- No se puede usar el modificador del vinculador **`/DELAY:UNLOAD`** para habilitar la descarga de los módulos diferidos.

## <a name="incorrectly-interpreting-license-rights"></a>Interpretación incorrecta de los derechos de licencia

Si la aplicación no interpreta y aplica correctamente los derechos que se expresan en la licencia de emisión de SDK, puede poner una mayor cantidad de información a disposición de otros de una manera que el propietario de la información no pretendía. Por ejemplo, cuando una aplicación permite que un usuario guarde información sin cifrar en un medio nuevo cuando la licencia de emisión solo confiere derechos para ver la información.

### <a name="azure-information-protection-aip"></a>Azure Information Protection (AIP)

El sistema de protección de información organiza derechos en diferentes agrupaciones. Para más información, consulte [Configuración de los derechos de uso para Azure Rights Management](../configure-usage-rights.md).

AIP permite que un usuario descifre información o no. La información no tiene ninguna protección inherente. Si un usuario tiene el derecho de descifrar, la API lo permite. La aplicación es responsable de administrar o proteger esa información cuando está sin cifrar. Una aplicación es responsable de administrar su entorno e interfaz para impedir el uso no autorizado de información. Por ejemplo, deshabilitar los botones **Imprimir** y **Copiar** si una licencia solo concede el derecho de vista. El conjunto de pruebas debe comprobar que la aplicación funciona correctamente en todos los derechos de licencia que reconoce.

### <a name="minimum-standard"></a>Estándar mínimo

- La implementación de cliente de los derechos de XrML v.1.2 debe ser coherente con las definiciones de estos derechos, tal como se describe en las especificaciones de XrML, que están disponibles en el sitio web de XrML (http://www.xrml.org). Los derechos que son específicos de la aplicación deben definirse para todas las entidades que tienen interés en la aplicación.
- El conjunto de pruebas y el proceso de pruebas deben comprobar que la aplicación se ejecuta correctamente según los derechos que admite. También debe comprobar que **no** actúan según derechos que no admite.
- Si va a compilar una aplicación de publicación, debe publicar información que explique los derechos intrínsecos usados. Esto incluye los que son compatibles con la aplicación de publicación y los que no, y cómo se deben interpretar estos derechos. Además, la interfaz de usuario debería dejar claro al usuario final cuáles son las implicaciones derivadas de la concesión o denegación de un dato específico para cada derecho.
- Los derechos que se abstraen por inclusión en nuevos derechos implementados por una aplicación deben asignarse a la nueva terminología. Por ejemplo, un derecho nuevo llamado DIRECTOR puede incluir como derechos abstraídos IMPRIMIR, COPIAR y EDITAR.

### <a name="recommended-standard"></a>Estándar recomendado

Ninguno en este momento.

### <a name="preferred-standard"></a>Estándar preferido

Ninguno en este momento.

## <a name="next-steps"></a>Pasos siguientes

Los procedimientos recomendados para implementar aplicaciones con AIP SDK incluyen estos artículos:

- [Modelos de amenazas y mitigaciones](https://msdn.microsoft.com/library/aa362751.aspx)
- [Ataques de seguridad](https://msdn.microsoft.com/library/aa362736.aspx)
