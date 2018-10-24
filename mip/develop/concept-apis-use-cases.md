---
title: 'Conceptos: API en el SDK de MIP.'
description: Este artículo le ayudará a comprender los tres tipos de API en el SDK de MIP, cómo se relacionan entre sí y los casos de uso específicos de cada uno.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a625df159a00a955d155850ff4e326d1e0d204e5
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453339"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>SDK de Microsoft Information Protection: conceptos de API

El SDK de MIP se compone de tres API:

- [API de protección](#protection-api)
- [API de directiva](#policy-api)
- [API de archivo](#file-api)

## <a name="protection-api"></a>API de protección

La API de protección proporciona a los desarrolladores de software la capacidad de convertir secuencias de texto sin formato en secuencias administradas con derechos y viceversa.

### <a name="protection-api-use-cases"></a>Casos de uso de la API de protección

- Su organización desarrolla un software de impresión 3D con un formato de archivo propio. Desea usar MIP para proteger el archivo y que solo puedan imprimirlo usuarios específicos. Con la API de protección, puede aplicar protección en el archivo para que solo los consumidores autorizados puedan abrirlo o imprimirlo. 

- Su organización desarrolla una solución de eDiscovery que procesa buzones de Exchange y archivos PST. Su aplicación debe poder permitir al usuario descifrar los mensajes para realizar un eDiscovery completo. Mediante un analizador de mensajes/RPMSG personalizado y una cuenta con privilegios suficientes, puede aprovechar la API de RMS para descifrar el archivo cifrado, examinar su contenido y descartarlo si está dentro del ámbito o empaquetarlo si está dentro del ámbito.

## <a name="policy-api"></a>API de directiva

La API de directiva, o motor de directiva universal (UPE), proporciona a los desarrolladores de software la capacidad de obtener directivas de etiquetado para un usuario específico y, a continuación, “procesar” las acciones que estas etiquetas llevarán a cabo.

La API de la directiva la aprovecharán principalmente las aplicaciones cliente en las cuales el desarrollo controla la interfaz y el formato de archivo, o donde el único requisito es obtener la directiva de usuario y no necesariamente etiquetar los archivos directamente. 

### <a name="policy-api-use-cases"></a>Casos de uso de la API de directiva

- Su organización desarrolla un software de diseño 3D que usa un formato de archivo propio. Sus clientes usan Microsoft Information Protection y quieren poder aplicar las etiquetas de forma nativa a través de la aplicación. Como ingeniero de software, usará la API de directiva y un control personalizado para mostrar las etiquetas disponibles para el usuario autenticado. Una vez que el usuario haya seleccionado una etiqueta, usted llamará al método de acción de proceso de la API para saber exactamente lo que debe aplicarse en cuanto a los metadatos, marcado de contenido y protección.

- Su organización desarrolla un servicio DLP que permite que sus clientes configuren las directivas DLP a través de un portal de administración central. Tiene clientes que usan Microsoft Information Protection y quiere poder leer o aplicar etiquetas de AIP como parte de las directivas DLP. Como ingeniero de software, puede usar la API de directiva para obtener una lista de etiquetas para la organización del cliente y, a continuación, leer las etiquetas como parte de una regla DLP o aplicar la información de etiqueta como parte de una acción de regla.

## <a name="file-api"></a>API de archivo

La API de archivo es una abstracción de la API de protección y la API de directiva. Proporciona interfaces de uso fácil para la lectura de etiquetas desde el servicio, la aplicación de etiquetas para los tipos de archivo definidos y la lectura de etiquetas desde estos tipos de archivo. La API de archivo la usará cualquier servicio o aplicación con un tipo de archivo compatible implicado; ademas, las etiquetas deben ser leídas o escritas, o el contenido debe estar protegido o descifrado.

### <a name="file-api-use-cases"></a>Casos de uso de la API de archivo

- Usted es un ingeniero de software de una entidad de servicios financieros. Desea asegurarse de que los datos de sus aplicaciones LOB, que normalmente se exportan en formato Excel, están etiquetados para la exportación según el contenido. La API de archivo se puede usar para enumerar las etiquetas disponibles y, a continuación, aplicar la etiqueta adecuada a un formato de archivo admitido.

- Su organización desarrolla un agente de seguridad de acceso a la nube (CASB). Sus clientes solicitan tener la capacidad de aplicar etiquetas de MIP a documentos de Microsoft Office y PDF. La API de archivo le permite mostrar una lista de etiquetas configuradas y posteriormente permite a los clientes compilar reglas que se aplicarán a la etiqueta deseada. La API de archivo, a partir del identificador de etiqueta, controlará el resto de archivos que cumplen los criterios del cliente.

- Su organización proporciona una solución de prevención de pérdida de datos basada en el servicio y/o un CASB que supervisa la actividad de archivos en las aplicaciones SaaS. Para reducir el riesgo de exposición o pérdida de datos allí donde los datos están protegidos con MIP, el servicio debe poder examinar el contenido de los archivos protegidos. Con la API de archivo para los formatos compatibles, cuando el servicio es un usuario con privilegios, puede eliminar la protección, examinar el contenido para buscar contenido restringido o confidencial, descartar el resultado de texto sin formato y aplicar una regla de servicio para informar acerca de un posible riesgo o para corregirlo si se detecta.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ya tiene una idea general de las API de MIP disponibles y de cómo se usan, continúe con los [conceptos de objeto de motor y perfil](concept-profile-engine-cpp.md). Estos conceptos son fundamentales y se aplican a todos los conjuntos de API de MIP.