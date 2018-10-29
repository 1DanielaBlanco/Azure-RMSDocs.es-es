---
title: 'Conceptos: API en el SDK de MIP.'
description: Este artículo le ayudará a comprender los tres tipos de API en el SDK de MIP, cómo se relacionan entre sí y los casos de uso específicos de cada uno.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 10/16/2018
ms.author: bryanla
ms.openlocfilehash: 5c3f7ee97bfe003f2f215ba95ba196894ab8e197
ms.sourcegitcommit: cc65c3851d4b8169a1a62c83afaf0f75402f7631
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2018
ms.locfileid: "49476194"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>SDK de Microsoft Information Protection: conceptos de API

El SDK de Microsoft Information Protection (MIP) se compone de tres API, tal como se muestra en el diagrama siguiente:

[![Diagrama de la API del SDK de MIP](media/concept-apis-use-cases/mip-sdk-components.png)](media/concept-apis-use-cases/mip-sdk-components.png#lightbox)

Dependiendo de las necesidades de la aplicación, es posible que desee interactuar en la capa de File API o que necesite trabajar directamente con las capas de Policy API o Protection API.

## <a name="file-api"></a>API de archivo

La API de archivo es una abstracción de la API de protección y la API de directiva. Proporciona interfaces de uso fácil para la lectura de etiquetas desde el servicio, la aplicación de etiquetas para los tipos de archivo definidos y la lectura de etiquetas desde estos tipos de archivo. File API se utilizará por cualquier servicio o aplicación en el que:

- esté implicado un tipo de archivo compatible
- las etiquetas deban leerse o escribirse
- el contenido debe estar protegido o cifrado

### <a name="file-api-use-cases"></a>Casos de uso de la API de archivo

- Usted es un ingeniero de software de una entidad de servicios financieros. Desea asegurarse de que los datos de sus aplicaciones LOB, que normalmente se exportan en formato Excel, están etiquetados para la exportación según el contenido. Se puede usar File API para enumerar las etiquetas disponibles y, a continuación, aplicar la etiqueta adecuada a un formato de archivo admitido.

- Su organización desarrolla un agente de seguridad de acceso a la nube (CASB). Sus clientes solicitan tener la capacidad de aplicar etiquetas de MIP a documentos de Microsoft Office y PDF. File API le permite mostrar una lista de etiquetas configuradas y después permite a los clientes crear reglas que se aplican a la etiqueta deseada. File API, a partir del identificador de etiqueta, controlará el resto de archivos que cumplen los criterios del cliente.

- Su organización proporciona una solución de prevención de pérdida de datos basada en el servicio o un CASB que supervisa la actividad de archivos en las aplicaciones SaaS. Para reducir el riesgo de exposición o pérdida de datos allí donde los datos están protegidos con MIP, el servicio debe examinar el contenido de los archivos protegidos. Mediante File API para los formatos admitidos, cuando el servicio es un usuario con privilegios puede:

  1. eliminar la protección
  2. examinar el contenido en busca de contenido confidencial o restringido
  3. descartar el resultado de texto no cifrado
  4. aplicar una regla de servicio para notificar o corregir el riesgo, si se encuentra

## <a name="policy-api"></a>API de directiva

Policy API, o motor de directiva universal (UPE), proporciona a los desarrolladores de software la capacidad de recuperar directivas de etiquetado para un usuario específico. Entonces puede "procesar" las acciones que esas etiquetas deben realizar.

Policy API se utiliza principalmente en las aplicaciones cliente, donde el desarrollador controla la interfaz y el formato de archivo. También se utiliza cuando el único requisito es recuperar la directiva de usuario y no etiquetar los archivos directamente. 

### <a name="policy-api-use-cases"></a>Casos de uso de la API de directiva

- Su organización desarrolla un software de diseño 3D que usa un formato de archivo propio. Sus clientes usan MIP y quieren aplicar las etiquetas de forma nativa mediante la aplicación. Como ingeniero de software, utiliza Policy API y un control personalizado para mostrar las etiquetas disponibles para el usuario autenticado. Después de que el usuario selecciona una etiqueta, se llama al método de acción de proceso de la API. La API le indica exactamente lo que se debe aplicar en cuanto a metadatos, marcado de contenido y protección.

- Su organización desarrolla un servicio de prevención de pérdida de datos (DLP) que permite que los clientes configuren las directivas DLP mediante un portal de administración central. Tiene clientes que utilizan MIP y necesitan leer o aplicar etiquetas AIP, como parte de las directivas de DLP. Como ingeniero de software, puede utilizar Policy API para obtener una lista de etiquetas para la organización del cliente. A continuación, puede leer esas etiquetas como parte de una regla DLP o aplicar la información de la etiqueta como parte de una acción de la regla.

## <a name="protection-api"></a>API de protección

Protection API proporciona a los desarrolladores de software la capacidad de convertir secuencias de texto sin formato en secuencias administradas con derechos y viceversa.

### <a name="protection-api-use-cases"></a>Casos de uso de la API de protección

- Su organización desarrolla un software de impresión 3D con un formato de archivo propio. Desea usar MIP para proteger el archivo y que solo puedan imprimirlo usuarios específicos. Con Protection API puede aplicar protección en el archivo para que solo los consumidores autorizados puedan abrirlo o imprimirlo. 

- Su organización desarrolla una solución de eDiscovery que procesa buzones de Exchange y archivos .PST. La aplicación debe permitir a los usuarios descifrar los mensajes para realizar eDiscovery. Con un analizador RPMSG o de mensajes personalizados y una cuenta con suficientes privilegios, puede usar la API de RMS para:
  - descifrar el archivo cifrado
  - analizar el contenido
  - descartar si está fuera del ámbito o empaquetar si está en el ámbito

## <a name="next-steps"></a>Pasos siguientes

Ahora que ya tiene una idea general de las API de MIP disponibles y de cómo se usan, continúe con los [conceptos de objeto de motor y perfil](concept-profile-engine-cpp.md). Estos conceptos son fundamentales y se aplican a todos los conjuntos de API de MIP.