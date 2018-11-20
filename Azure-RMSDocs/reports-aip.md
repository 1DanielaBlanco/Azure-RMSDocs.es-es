---
title: Informes centrales para Azure Information Protection
description: Cómo usar los informes centrales para realizar el seguimiento de la adopción de las etiquetas de Azure Information Protection e identificar los archivos que contienen información confidencial
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/13/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: 85ca097a1808c2940ce534c7ce3d0542aaf3f27a
ms.sourcegitcommit: 0f9e2ba05b61f8db08387576a697b8deff45fd36
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51611427"
---
# <a name="central-reporting-for-azure-information-protection"></a>Informes centrales para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Esta característica se encuentra actualmente en versión preliminar y está sujeta a cambios. Puede que no todos los datos recopilados durante esta versión preliminar se admitan cuando la característica pase a disponibilidad general.


Use el análisis de Azure Information Protection para la generación de informes centrales a fin de realizar el seguimiento de la adopción de las etiquetas de Azure Information Protection, así como para supervisar el acceso del usuario a los documentos y correos electrónicos etiquetados y los cambios en su clasificación. También puede identificar los documentos que contienen información confidencial que debe protegerse.

Actualmente, los datos que ve se agregan desde los clientes de Azure Information Protection y los análisis de Azure Information Protection.

Por ejemplo, podrá ver lo siguiente:

- Desde **Usage report** (Informe de uso), donde puede seleccionar un período de tiempo:
    
    - Qué etiquetas se aplican
    
    - Cuántos documentos y correos electrónicos se etiquetan
    
    - Cuántos documentos y correos electrónicos se protegen
    
    - Cuántos usuarios y dispositivos están etiquetando documentos y correos electrónicos
    
    - Qué aplicaciones se usan para el etiquetado

- Desde el informe **Data discovery** (Detección de datos):

    - Qué archivos se encuentran en los repositorios de datos examinados
    
    - Qué archivos están etiquetados y protegidos, y la ubicación de los archivos por etiquetas
    
    - Qué archivos contienen información confidencial para categorías conocidas, como datos financieros e información personal, y la ubicación de los archivos por estas categorías
    
Los informes usan [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) para almacenar los datos en un área de trabajo de su propiedad. Si está familiarizado con el lenguaje de consulta, puede modificar las consultas y crear nuevos informes y paneles de Power BI. Puede que el siguiente tutorial le ayude a comprender el lenguaje de consulta: [Introducción a las consultas en Log Analytics](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal). 

Para más información, lea la entrada de blog: [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Detección de datos, informes y análisis de todos los datos con Microsoft Information Protection).

### <a name="information-collected-and-sent-to-microsoft"></a>Información recopilada y enviada a Microsoft

Para generar estos informes, los puntos de conexión envían los siguientes tipos de información a Microsoft:

- La acción de la etiqueta. Por ejemplo, establecer una etiqueta, cambiar una etiqueta, agregar o quitar la protección, etiquetas automáticas y recomendadas.

- El nombre de etiqueta antes y después de la acción de la etiqueta.

- El identificador del inquilino de la organización.

- El identificador de usuario (dirección de correo electrónico o UPN).

- El nombre del dispositivo del usuario.

- Para documentos: la ruta de acceso y el nombre de archivo de los documentos etiquetados.

- Para correos electrónicos: el asunto, el remitente y los destinatarios de correo electrónico para los correos electrónicos etiquetados. 

- Los tipos de información confidencial ([predefinidos](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) y personalizados) que se han detectado en el contenido.

- La versión del cliente de Azure Information Protection.

- La versión del sistema operativo cliente.

Esta información se almacena en un área de trabajo de Azure Log Analytics de su propiedad y que pueden ver los usuarios que tienen derechos de acceso a esta área de trabajo. Para obtener información acerca de cómo configurar el acceso al área de trabajo, vea la sección [Administración de cuentas y usuarios](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users) de la documentación de Azure.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Requisitos previos de análisis de Azure Information Protection
Para ver los informes de Azure Information Protection y crear los suyos propios, asegúrese de que se hayan satisfecho los siguientes requisitos previos.

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción a Azure que incluya Log Analytics|Consulte la página [Precios de Azure Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si no tiene una suscripción a Azure o actualmente no usa Azure Log Analytics, la página de precios incluye un vínculo a una evaluación gratuita.|
|La versión preliminar actual del cliente de Azure Information Protection.|Si aún no ha instalado la versión preliminar actual del cliente, puede descargarla e instalarla desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Para el informe **Discovery and risk** (Detección y riesgo): <br /><br />-Ha implementado al menos una instancia del analizador de Azure Information Protection (versión preliminar actual)|Para obtener instrucciones de instalación, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](deploy-aip-scanner.md). <br /><br />Si va a actualizar desde una versión anterior del analizador, consulte [Actualización del analizador de Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).|


## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configuración de un área de trabajo de Log Analytics para los informes

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
2. Busque las opciones de menú **Administrar** y seleccione **Configurar análisis (versión preliminar)**.

3. En la hoja **Azure Information Protection log analytics** (Análisis de registro de Azure Information Protection), verá una lista de áreas de trabajo de Log Analytics que son propiedad de su inquilino. Realice una de las siguientes acciones:
    
    - Para crear un área de trabajo de Log Analytics, seleccione **Create new workspace** (Crear área de trabajo) y, en la hoja **Log analytics workspace** (Área de trabajo de Log Analytics), proporcione la información solicitada.
    
    - Para usar un área de trabajo de Log Analytics existente, selecciónela de la lista.

Si necesita ayuda para crear el área de trabajo de Log Analytics, consulte [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Cuando esté configurada el área de trabajo, estará listo para ver los informes.

## <a name="how-to-view-the-reports"></a>Cómo ver los informes

En la hoja Azure Information Protection, busque las opciones de menú **Paneles** y seleccione una de las siguientes opciones:

- **Informe de uso (versión preliminar)**: use este informe para ver cómo se usan las etiquetas. 

- **Detección de datos (versión preliminar)**: use este informe para ver información sobre los archivos encontrados por los detectores.

## <a name="how-to-modify-the-reports"></a>Modificación de los informes

Seleccione el icono de consulta en el panel para abrir una hoja **Log Search** (Búsqueda de registros): 

![Icono de Log Analytics para personalizar los informes de Azure Information Protection](./media/log-analytics-icon.png)


Los datos registrados de Azure Information Protection se almacenan en la tabla siguiente: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Pasos siguientes
Después de revisar la información de los informes, podría decidir realizar cambios en la directiva de Azure Information Protection. Para obtener instrucciones, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).