---
title: "Guía de implementación rápida de Azure RMS - AIP"
description: "Una guía para ayudarlo a implementar y usar el servicio Azure Rights Management con más rapidez para proteger los datos de su organización. Empiece por elegir una de las opciones de una lista de escenarios de implementación específicos."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/08/2017
ms.topic: get-started-article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c994d616-cff6-4930-9228-a7f7d198a160
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: 2e50dc9d53550f35f5c589cdb1b384e0abf585e0
ms.lasthandoff: 02/24/2017


---

# <a name="rapid-deployment-guide-for-azure-rights-management"></a>Guía de implementación rápida de Azure Rights Management

>*Se aplica a: Azure Information Protection, Office 365*

Use esta guía, además de la información sobre la configuración en la sección **Implementación y uso**, como ayuda para implementar y usar rápidamente una solución de solo protección que usa el servicio Azure Rights Management de Azure Information Protection. Elija una opción en la lista de escenarios específicos para implementarla.

> [!NOTE]
> En este momento, la guía contiene escenarios de solo protección y no contiene escenarios para clasificación y protección o el cliente Azure Information Protection. 

Los escenarios contienen instrucciones para el administrador y documentación complementaria para el usuario final. Antes de proporcionarles la documentación (instrucciones o anuncios) a los usuarios finales, tendrá primero que personalizarla en función de sus necesidades empresariales y su flujo de trabajo. Un conjunto de instrucciones o un anuncio de ejemplo muestran el aspecto definitivo de la documentación para el usuario final.

Cada escenario tiene una lista de requisitos con vínculos para más información, en caso de ser necesario, por lo que puede implementar estas soluciones de manera independiente y en cualquier orden.

Los escenarios aquí mencionados son una muestra de los más comunes. Como Azure Information Protection se puede usar para proteger la información en un gran número de escenarios (tanto dentro de una misma organización como en varias organizaciones), puede usar este mismo modelo para definir sus propios escenarios e implementarlos en su entorno y en sus usuarios. Al centrarse en escenarios específicos, la implementación de Azure Information Protection se adaptará mejor a sus objetivos empresariales. Además, nuestra experiencia es que los usuarios suelen seguir las instrucciones específicas de un escenario de forma mucho más atenta y sistemática que cuando se trata de instrucciones generales como "proteger documentos confidenciales".

Antes de implementar estas soluciones, puede enviar un anuncio general a los usuarios finales informándoles de los cambios que se producirán en materia de protección de los datos de la empresa, así como de las posibles modificaciones que deban realizar por su parte. Después de la tabla siguiente encontrará un ejemplo de este tipo de comunicación.

Si tiene preguntas y comentarios sobre esta guía, use los mecanismos de comentarios de esta página o envíe un correo a [AskIPTeam@Microsoft.com](mailto:%20askipteam@microsoft.com?subject=Rapid%20Deployment%20Guide%20feedback).

## <a name="scenarios-for-azure-information-protection"></a>Escenarios de Azure Information Protection
Para que pueda implementar Azure Information Protection con mayor rapidez para solucionar problemas empresariales específicos, elija los escenarios que se acerquen más a sus objetivos empresariales y adáptelos según sea necesario.



**Enviar por correo electrónico de manera segura un archivo de Office a los usuarios de otra organización con la capacidad de realizar un seguimiento de cómo se obtiene acceso a él (colaboración de negocio a negocio)**

Ejemplos:

- Envíe una lista de precios, un plan o planes de lanzamiento a un cliente.

- Envíe un pedido de trabajo o una especificación de marketing a un proveedor.

- Envíe una forma de pago o una solicitud de presupuesto a un socio.

Vea [Escenario: Compartir un archivo de Office con usuarios de otra organización](scenario-share-office-file-externally.md)

**Asegurarse de mantener el control de los documentos almacenados en una biblioteca de SharePoint**

Ejemplos:

- Informes y hojas de cálculo por departamentos

- Colaboración entre equipos para el diseño de documentos y otros productos

Vea [Escenario: Mantener el control de los documentos almacenados en SharePoint](scenario-sharepoint.md)

**Los ejecutivos pueden intercambiar información confidencial de manera segura por correo electrónico**

Ejemplos:

- Uso compartido de planes de adquisición

- Análisis o divulgación de asuntos legales

- Información sobre posibles despidos u otros temas confidenciales

Vea [Escenario: Ejecutivos intercambian de forma segura información confidencial](scenario-executives-email.md)

**Proteger automáticamente todos los archivos en un servidor de archivos**

Ejemplos:

- Documentos CAD que se deben mantener internos para evitar la pérdida de propiedad intelectual

- Planes de promoción de marketing y fechas que deben mantenerse en secreto para mantener una ventaja competitiva

Vea [Escenario: Proteger archivos en un recurso compartido de servidor de archivos](scenario-fci.md)

**Proteger perfectamente los documentos más confidenciales y con mayor impacto empresarial**

Ejemplos:

- Información de recetas o fórmulas exclusivas de su empresa

- Planes de fusión o adquisición altamente confidenciales

- Datos de exploración de recursos naturales

Vea [Escenario: Proteger &#40;algunos&#41; archivos de gran valor](scenario-secure-most-valuable-files.md)

**Enviar de manera segura correos electrónicos y datos adjuntos confidenciales**

Ejemplos:

- Declaración de la estrategia empresarial

- Organigramas, noticias de reorganización o anuncios de promoción

- Información sobre políticas de la empresa

Vea [Escenario: Enviar un correo electrónico confidencial de la empresa](scenario-company-confidential-email.md)

**Aplicar protección constante a archivos de Office en carpetas de trabajo**

Ejemplos:

- Editar localmente los documentos de Word correspondientes a un proyecto confidencial de la compañía

- Hojas de cálculo creadas localmente que contienen datos confidenciales o datos de gran impacto para la empresa

- Presentaciones de PowerPoint en desarrollo y almacenadas localmente que no deben filtrarse ni compartirse accidentalmente con personas ajenas a la organización hasta que no estén finalizadas

Vea [Escenario: Configurar carpetas de trabajo para protección persistente](scenario-work-folders.md)




## <a name="announcement-for-users-before-rollout"></a>Anuncio para los usuarios antes de la implementación
Puede usar el siguiente mensaje de comunicación de ejemplo para informar a los usuarios de que la implementación de Azure Information Protection supone algunos cambios futuros. Copie y pegue el texto siguiente para que alguien del equipo directivo de su empresa (preferiblemente el director ejecutivo) lo envíe por correo electrónico a todos los usuarios. Puede modificar el texto del mensaje para que sea más relevante para los usuarios y la organización.

![Banner de documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

### <a name="changes-were-making-to-safeguard-our-data"></a>Cambios en la protección de nuestros datos
¿Alguna vez ha querido bloquear el acceso a un documento que envió a sus socios por error? ¿Le gustaría saber si los clientes han leído la información que les ha remitido sobre algún producto? ¿Necesita compartir información confidencial sobre un producto sin preocuparse de que se envíe a gente que no debería verla?

Pronto podrá hacer todo esto, ya que el departamento de TI está realizando algunos cambios para implementar Microsoft Azure Information Protection como solución para la protección de datos empresariales. La protección que necesitamos se aplicará en muchas de estas soluciones sin necesidad de que usted intervenga. Pero puede que tenga que tomar medidas en algunos cambios. De ser así, el departamento de TI le enviará la información y las instrucciones pertinentes. Si tiene alguna duda o problema, cuenta con el apoyo del departamento de soporte técnico.

Por ejemplo, para realizar un seguimiento de los documentos que comparta (o revocarlos, en caso necesario), usará un sitio de seguimiento de documentos:

![Capturas de pantalla de seguimiento de documentos de Azure RMS](../media/AzRMS_Tutorial_5_Screenshots.png)

Para un ver un anticipo de su funcionamiento, eche un vistazo a este breve vídeo: [Azure RMS Document Tracking and Revocation](https://channel9.msdn.com/Series/Information-Protection/Azure-RMS-Document-Tracking-and-Revocation) (Revocación y seguimiento de documentos de Azure RMS)

Uno de los activos más valiosos de esta organización son los datos que generamos, almacenamos y usamos a diario. Es lo que nos permite contar con ventaja competitiva y tener éxito. Por eso es tan importante mantener el control sobre los datos y asegurarnos de que no acceda a ellos toda persona que no deba.

Las soluciones que estamos implementando nos ayudarán a proteger nuestra valiosa información y nos proporcionarán las herramientas para mantener el control de los datos. Gracias por su colaboración durante la implementación de estos cambios.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

