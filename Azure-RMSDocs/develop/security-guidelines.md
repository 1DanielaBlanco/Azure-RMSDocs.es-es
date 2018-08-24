---
title: Procedimientos recomendados de seguridad | Microsoft Information Protection
description: Las aplicaciones habilitadas para RMS se crean mejor mediante los procedimientos recomendados de Azure Information Protection.
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.assetid: 4e9f72d5-9e7c-43e1-bb8a-5972dd22dcee
ms.service: information-protection
ms.suite: ems
ms.reviewer: kartikk
ms.openlocfilehash: 2b6c8e0d9e568c9ee87f9754240781695d2de2ba
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42807295"
---
# <a name="security-best-practices-for-azure-information-protection"></a>Procedimientos recomendados de seguridad para Azure Information Protection

El Kit de desarrollo de Software (SDK) de Azure Information Protection (AIP) proporciona un sistema sólido para publicar y consumir información protegida de todo tipo. Para que un sistema AIP sea lo más robusto posible, las aplicaciones habilitadas para AIP deben compilarse siguiendo prácticas recomendadas de AIP. Las aplicaciones habilitadas para AIP comparten la responsabilidad de mantener la seguridad de este ecosistema. La identificación de los riesgos de seguridad y la provisión de mitigaciones para esos riesgos introducidos durante el desarrollo de la aplicación ayudan a reducir la probabilidad de que el software se implemente de una manera menos segura.

Entre los procedimientos recomendados para implementar aplicaciones por medio del Kit de desarrollo de software (SDK) de Azure Information Protection se encuentran las siguientes categorías de sugerencias:
- [Modelos de amenazas y mitigaciones](https://msdn.microsoft.com/library/aa362751.aspx)
- [Ataques de seguridad](https://msdn.microsoft.com/library/aa362736.aspx)

Esta información complementa el acuerdo legal que debe firmarse con el fin de obtener los certificados digitales necesarios para implementar aplicaciones mediante el SDK de AIP.

## <a name="subjects-not-covered-in-these-topics"></a>Asuntos que no se tratan en estos temas
Estos temas describen brevemente los problemas siguientes, que son importantes al intentar crear un entorno de desarrollo y una aplicación segura:
- **Administración de procesos de desarrollo de software**: incluye información acerca de la administración de la configuración, la protección del código fuente, la minimización del acceso al código depurado y la asignación de prioridades entre los errores. Para algunos de sus clientes, disponer de un proceso de desarrollo de software más seguro reviste una importancia fundamental. Algunos clientes incluso recomiendan un proceso de desarrollo.
- **Errores de codificación comunes**: incluye información sobre cómo evitar las saturaciones del búfer. Para examinar estas amenazas genéricas y mitigaciones, se recomienda la versión más reciente de Writing Secure Code, de Michael Howard y David LeBlanc (Microsoft Press, 2002).
- **Ingeniería social**: incluye información acerca de las medidas de seguridad procedimentales y estructurales que ayudan a proteger contra el aprovechamiento de código por desarrolladores u otras personas dentro de la organización del fabricante.
- **Seguridad física**: incluye información sobre cómo bloquear el acceso a la base de código y la firma de certificados.
- **Implementación o distribución de software de versión preliminar**: incluye información acerca de cómo distribuir el software beta.
- **Administración de redes**: incluye información acerca de los sistemas de detección de intrusiones en sus redes físicas.

## <a name="threat-models-and-mitigations"></a>Modelos de amenazas y mitigaciones
Los propietarios de la información digital necesitan la capacidad de evaluar los entornos en los que se van a descifrar sus activos. Una instrucción de estándares de seguridad mínimos puede proporcionar a los propietarios de la información un marco para entender y evaluar el nivel de seguridad de las aplicaciones a las que confían su información.

Algunas industrias, como el gobierno y la asistencia sanitaria, tienen procesos y normas de certificación y acreditación que pueden aplicarse a su producto. El cumplimiento con estas recomendaciones de seguridad mínimas no reemplaza en ningún caso las necesidades de acreditación únicas de los clientes. Sin embargo, la intención de las normas de seguridad es ayudarle a prepararse para los requisitos del cliente actuales y futuros, y toda inversión que realice al principio del ciclo de desarrollo beneficiará a la aplicación. Se trata de recomendaciones, no un programa formal de certificación de Microsoft.

Un sistema de Rights Management Services puede presentar diferentes categorías principales de vulnerabilidades, entre las que están las siguientes:
- **Fuga**: la información aparece en ubicaciones no autorizadas.
- **Daño**: el software o los datos se modifican de manera no autorizada.
- **Denegación**: un recurso informático no está disponible para su uso.

Estos temas se centran principalmente en los problemas de fuga. La integridad de un sistema de API depende de su capacidad, con el paso del tiempo, de proteger la información, permitiendo el acceso solo a las entidades designadas. En estos temas también se mencionan los daños. No se tratan los problemas de denegación.

Microsoft no prueba ni revisa resultados de pruebas relacionados con el cumplimiento del estándar mínimo; es responsabilidad total del asociado asegurarse de que se cumplen los estándares mínimos. Microsoft proporciona dos niveles adicionales de recomendaciones para ayudar a mitigar las amenazas comunes. En general, estas sugerencias son incrementales; por ejemplo, el hecho de cumplir las recomendaciones preferidas da por supuesto que se han cumplido los estándares mínimos, en su caso, a menos que se especifique lo contrario.

|Nivel estándar|    Descripción|
|---|---|
|Estándar mínimo|  Debe determinarse una aplicación que controle la información protegida de AIP para cumplir con el estándar mínimo a fin de que esta pueda firmarse con el certificado de producción recibido de Microsoft. Los asociados por lo general utilizan el certificado de la jerarquía de producción solo en el momento del lanzamiento final del software, cuando las pruebas internas de los propios asociados han verificado que la aplicación cumple con este estándar mínimo. El hecho de cumplir con el estándar mínimo no es una garantía de seguridad por parte de Microsoft, ni debe interpretarse como ello. Microsoft no prueba ni revisa resultados de pruebas relacionados con el cumplimiento del estándar mínimo; es responsabilidad total del asociado asegurarse de que se cumple el mínimo.|
|Estándar recomendado|  Las directrices recomendadas trazan una ruta hacia la mejora de la seguridad de la aplicación y proporcionan una indicación de cómo puede evolucionar API a medida que se implementen más criterios de seguridad. Los proveedores pueden intentar diferenciar sus aplicaciones ascendiendo a este nivel superior de directrices de seguridad.|
|Estándar preferido|    Se trata de la categoría más alta de seguridad definida actualmente. Los proveedores que desarrollen aplicaciones comercializadas bajo la etiqueta de "alta seguridad" deben tratar de alcanzar este estándar. Las aplicaciones que se adhieren este estándar suelen ser menos vulnerable a los ataques.|




## <a name="malicious-software"></a>Software malintencionado
Microsoft ha definido los estándares necesarios mínimos que debe cumplir la aplicación para proteger el contenido frente al software malintencionado.

### <a name="importing-malicious-software-by-using-address-tables"></a>Importación de software malintencionado mediante tablas de direcciones
AIP no admite la modificación del código en tiempo de ejecución ni la modificación de la tabla de importar direcciones. Se crea una tabla de importar direcciones para cada archivo DLL cargado en el espacio de proceso. Estas especifican las direcciones de todas las funciones que importa la aplicación. Un ataque habitual consiste en modificar las entradas de la tabla de importar direcciones dentro de una aplicación para que, por ejemplo, apunte a software malintencionado. AIP detiene la aplicación cuando detecta este tipo de ataque.

### <a name="minimum-standard"></a>Estándar mínimo
- No se puede modificar la tabla de importar direcciones en el proceso de aplicación durante la ejecución. - La aplicación especifica muchas de las funciones llamadas en tiempo de ejecución mediante tablas de direcciones, y estas no se pueden modificar durante el tiempo de ejecución o después de este. Esto significa, entre otras cosas, que no es posible crear perfiles de código en una aplicación firmada con el certificado de producción.
- No se puede llamar a la función **DebugBreak** desde ningún DLL especificado en el manifiesto.
- No se puede llamar a **LoadLibrary** con la marca **DONT_RESOLVE_DLL_REFERENCES** configurada. Esta marca indica al cargador que omita el enlace a los módulos importados, modificando así la tabla para importar direcciones.
- No se puede modificar la carga diferida haciendo cambios de tiempo de ejecución o posteriores en el modificador del vinculador /DELAYLOAD.
- No se puede modificar la carga diferida proporcionando su propia versión de la función auxiliar de Delayimp.lib.
- No se pueden descargar los módulos que se han cargado de manera diferida por módulos autenticados mientras existe el entorno AIP.
- No se puede utilizar el modificador del vinculador **/DELAY:UNLOAD** para habilitar la descarga de los módulos diferidos.


## <a name="incorrectly-interpreting-license-rights"></a>Interpretación incorrecta de los derechos de licencia

Si la aplicación no interpreta y aplica correctamente los derechos que se expresan en la licencia de emisión de AIP, puede poner una mayor cantidad de información a disposición de otros de una manera que el propietario de la información no pretendía. Un ejemplo de esto es cuando una aplicación permite que un usuario guarde información sin cifrar en un medio nuevo cuando la licencia de emisión solo confiere derechos para ver la información.

El sistema AIP organiza los derechos en diferentes agrupaciones. Para más información, consulte [Configuración de los derechos de uso para Azure Rights Management](../configure-usage-rights.md).

### <a name="azure-information-protection"></a>Azure Information Protection  
API permite que un usuario descifre información o no; la información no tiene ninguna protección inherente. Si un usuario tiene el derecho para descifrar la información, la API lo permite, y la aplicación es responsable de administrar o proteger esa información una vez descifrada. Una aplicación es responsable de administrar su entorno e interfaz para impedir el uso no autorizado de información; por ejemplo, deshabilitando los botones **Imprimir** y **Copiar** si una licencia solo concede el derecho REPRODUCIR. El conjunto de pruebas debe comprobar que la aplicación funciona correctamente en todos los derechos de licencia que reconoce.

### <a name="minimum-standard"></a>Estándar mínimo
- La implementación de cliente de los derechos de XrML v.1.2 debe ser coherente con las definiciones de estos derechos, tal como se describe en las especificaciones de XrML, que están disponibles en el sitio web de XrML (http://www.xrml.org). Los derechos que son específicos de la aplicación deben definirse para todas las entidades que tienen interés en la aplicación.
- El conjunto de pruebas y el proceso de pruebas deben comprobar que la aplicación se ejecuta correctamente según los derechos que admite y que no actúa según derechos que no admite.
- Si está compilando una aplicación de publicación, debe publicar información que explique qué derechos intrínsecos son y no son compatibles con la aplicación de publicación y cómo deben interpretarse tales derechos. Además, la interfaz de usuario debería dejar claro al usuario final cuáles son las implicaciones derivadas de la concesión o denegación de un dato específico para cada derecho.

- Los derechos que se abstraen por inclusión en nuevos derechos implementados por una aplicación deben asignarse a la nueva terminología. Por ejemplo, un derecho nuevo llamado DIRECTOR puede incluir como derechos abstraídos IMPRIMIR, COPIAR y EDITAR.
Estándar recomendado   Ninguno en este momento.
Estándar preferido   Ninguno en este momento.
