---
title: Informes centrales para Azure Information Protection
description: Cómo usar los informes centrales para realizar el seguimiento de la adopción de las etiquetas de Azure Information Protection e identificar los archivos que contienen información confidencial
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/05/2019
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.assetid: b2da2cdc-74fd-4bfb-b3c2-2a3a59a6bf2e
ms.reviewer: lilukov
ms.suite: ems
ms.openlocfilehash: eb9ff9dd73422813a80b41ee516876bfc4c50663
ms.sourcegitcommit: 1cd3a3bc19cd973f81a62419c946bfaf2796dfb2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/06/2019
ms.locfileid: "55760793"
---
# <a name="central-reporting-for-azure-information-protection"></a>Informes centrales para Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

> [!NOTE]
> Esta característica se encuentra actualmente en versión preliminar y está sujeta a cambios. Puede que no todos los datos recopilados durante esta versión preliminar se admitan cuando la característica pase a disponibilidad general.

Use los análisis de Azure Information Protection para generar informes centrales que le permitan realizar el seguimiento de la adopción de las etiquetas de Azure Information Protection. Además:

- Supervise el acceso de los usuarios a documentos y correos electrónicos con etiquetas y los cambios realizados en su clasificación. 

- Identifique los documentos que contienen información confidencial que debe protegerse.

Actualmente, los datos que ve se agregan de los clientes y analizadores de Azure Information Protection, y de los equipos que ejecutan [Protección contra amenazas avanzada de Windows Defender (ATP de Windows Defender)](/windows/security/threat-protection/windows-defender-atp/overview).

Por ejemplo, podrá ver lo siguiente:

- Desde **Usage report** (Informe de uso), donde puede seleccionar un período de tiempo:
    
    - Qué etiquetas se aplican
    
    - Cuántos documentos y correos electrónicos se etiquetan
    
    - Cuántos documentos y correos electrónicos se protegen
    
    - Cuántos usuarios y dispositivos están etiquetando documentos y correos electrónicos
    
    - Qué aplicaciones se usan para el etiquetado

- Desde **Registros de actividades**, donde puede seleccionar un período de tiempo:
    
    - Qué acciones de etiquetado se realizaron por un usuario específico
    
    - Qué acciones de etiquetado se realizaron desde un dispositivo específico
    
    - Qué usuarios han tenido acceso a un documento etiquetado específico
    
    - Qué acciones de etiquetado se realizaron para una ruta de acceso de archivos específica
    
    - Qué acciones de etiquetado se realizaron por una aplicación específica, como el Explorador de archivos y clic derecho, o el módulo de PowerShell de AzureInformationProtection

- Desde el informe **Data discovery** (Detección de datos):

    - Qué archivos se encuentran en los repositorios de datos examinados, o equipos con Windows 10
    
    - Qué archivos están etiquetados y protegidos, y la ubicación de los archivos por etiquetas
    
    - Qué archivos contienen información confidencial para categorías conocidas, como datos financieros e información personal, y la ubicación de los archivos por estas categorías
    
Los informes usan [Azure Log Analytics](/azure/log-analytics/log-analytics-overview) para almacenar los datos en un área de trabajo de su organización. Si está familiarizado con el lenguaje de consulta, puede modificar las consultas y crear nuevos informes y paneles de Power BI. Puede que el siguiente tutorial le ayude a comprender el lenguaje de consulta: [Introducción a las consultas en Log Analytics](https://docs.loganalytics.io/docs/Learn/Getting-Started/Getting-started-with-the-Analytics-portal). 

Para más información, lea las siguientes entradas de blog: 

- [Data discovery, reporting and analytics for all your data with Microsoft Information Protection](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Data-discovery-reporting-and-analytics-for-all-your-data-with/ba-p/253854) (Detección de datos, informes y análisis de todos los datos con Microsoft Information Protection).

- [Discover and protect sensitive data through Azure Information Protection and Windows Defender ATP](https://techcommunity.microsoft.com/t5/Azure-Information-Protection/Discover-and-protect-sensitive-data-through-Azure-Information/ba-p/297292) (Detectar y proteger datos confidenciales mediante Azure Information Protection y Windows Defender ATP)

### <a name="information-collected-and-sent-to-microsoft"></a>Información recopilada y enviada a Microsoft

Para generar estos informes, los puntos de conexión envían los siguientes tipos de información a Microsoft:

- La acción de la etiqueta. Por ejemplo, establecer una etiqueta, cambiar una etiqueta, agregar o quitar la protección, etiquetas automáticas y recomendadas.

- El nombre de etiqueta antes y después de la acción de la etiqueta.

- El identificador del inquilino de la organización.

- El identificador de usuario (dirección de correo electrónico o UPN).

- El nombre del dispositivo del usuario.

- Para documentos: La ruta de acceso y el nombre de archivo de los documentos etiquetados.

- Para correos electrónicos: el asunto, el remitente y los destinatarios de correo electrónico para los correos electrónicos etiquetados. 

- Los tipos de información confidencial ([predefinidos](https://docs.microsoft.com/office365/securitycompliance/what-the-sensitive-information-types-look-for) y personalizados) que se han detectado en el contenido.

- La versión del cliente de Azure Information Protection.

- La versión del sistema operativo cliente.

Esta información se almacena en un área de trabajo de Azure Log Analytics de su organización y que pueden ver los usuarios que tienen derechos de acceso a esta área de trabajo. Para obtener información acerca de cómo configurar el acceso al área de trabajo, vea la sección [Administración de cuentas y usuarios](/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor#manage-accounts-and-users) de la documentación de Azure.

> [!NOTE]
> El área de trabajo de Azure Log Analytics para Azure Information Protection incluye una casilla para las coincidencias de contenido del documento. Cuando se selecciona esta casilla, también se recopilan los datos reales que se identifican mediante los tipos de información confidencial o sus condiciones personalizadas. Por ejemplo, esto puede incluir números de tarjeta de crédito que se encuentran, así como números de la seguridad social, números de pasaportes y números de cuentas bancarias. Si no desea recopilar estos datos, no seleccione esta casilla.
>
> Actualmente, esta información no se muestra en los informes pero puede verse y recuperarse con consultas.

## <a name="prerequisites-for-azure-information-protection-analytics"></a>Requisitos previos de análisis de Azure Information Protection
Para ver los informes de Azure Information Protection y crear los suyos propios, asegúrese de que se hayan satisfecho los siguientes requisitos previos.

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción a Azure que incluya Log Analytics|Consulte la página [Precios de Azure Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics).<br /><br />Si no tiene una suscripción a Azure o actualmente no usa Azure Log Analytics, la página de precios incluye un vínculo a una evaluación gratuita.|
|La versión actual disponible con carácter general o la versión preliminar del cliente de Azure Information Protection.|Si aún no ha instalado este cliente, puede descargarlo e instalarlo desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018).|
|Para el informe **Discovery and risk** (Detección y riesgo): <br /><br />- Para mostrar datos desde los almacenes de datos locales, ha implementado al menos una instancia del analizador de Azure Information Protection (versión de disponibilidad general o versión preliminar actual) <br /><br />-Para mostrar los datos desde equipos con Windows 10, estos deben pertenecer al menos a una compilación 1809, usted debe usar Protección contra amenazas avanzada de Windows Defender (ATP de Windows Defender) y ha habilitado la característica de integración de Azure Information Protection en el Centro de seguridad de Windows Defender|Para obtener instrucciones de instalación del analizador, consulte [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](deploy-aip-scanner.md). Si va a actualizar desde una versión anterior del analizador, consulte [Actualización del analizador de Azure Information Protection](./rms-client/client-admin-guide.md#upgrading-the-azure-information-protection-scanner).<br /><br />Para obtener información sobre cómo configurar y usar la característica de integración de Azure Information Protection del Centro de seguridad de Windows Defender, consulte [Protección de información de información general de Windows](/windows/security/threat-protection/windows-defender-atp/information-protection-in-windows-overview).|

## <a name="configure-a-log-analytics-workspace-for-the-reports"></a>Configuración de un área de trabajo de Log Analytics para los informes

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
2. Busque las opciones de menú **Administrar** y seleccione **Configurar análisis (versión preliminar)**.

3. En la hoja **Azure Information Protection log analytics** (Análisis de registro de Azure Information Protection), verá una lista de áreas de trabajo de Log Analytics que son propiedad de su inquilino. Realice una de las siguientes acciones:
    
    - Para crear una nueva área de trabajo de Log Analytics: seleccione **Crea nueva área de trabajo** y, en la hoja **Área de trabajo de Log Analytics**, proporcione la información solicitada.
    
    - Para usar un área de trabajo de Log Analytics existente: seleccione el área de trabajo de la lista.

Si necesita ayuda para crear el área de trabajo de Log Analytics, vea [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/azure/log-analytics/log-analytics-quick-create-workspace).

Cuando esté configurada el área de trabajo, estará listo para ver los informes.

## <a name="how-to-view-the-reports"></a>Cómo ver los informes

En la hoja Azure Information Protection, busque las opciones de menú **Paneles** y seleccione una de las siguientes opciones:

- **Informe de uso (versión preliminar)**: use este informe para ver cómo se usan las etiquetas. 

- **Registros de actividad (versión preliminar)**: use este informe para ver las acciones de etiquetado de los usuarios y en dispositivos y rutas de acceso de archivos.
    
    Este informe está implementando actualmente en los inquilinos, así que si no lo ve, vuelva a intentarlo en unos días.
    
    Este informe tiene una opción **Columnas**, que le permite mostrar más información de actividad que la visualización predeterminada.

- **Detección de datos (versión preliminar)**: use este informe para ver información sobre los archivos encontrados por los analizadores o ATP de Windows Defender.

> [!NOTE]
> Actualmente hay un problema conocido que muestra signos de interrogación (**?**) en rutas de acceso y nombres de archivo en lugar de caracteres no ASCII cuando la configuración regional del sistema operativo de envío es inglés.

## <a name="how-to-modify-the-reports"></a>Modificación de los informes

Seleccione el icono de consulta en el panel para abrir una hoja **Log Search** (Búsqueda de registros): 

![Icono de Log Analytics para personalizar los informes de Azure Information Protection](./media/log-analytics-icon.png)


Los datos registrados de Azure Information Protection se almacenan en la siguiente tabla: **InformationProtectionLogs_CL**

## <a name="next-steps"></a>Pasos siguientes
Después de revisar la información de los informes, podría decidir realizar cambios en la directiva de Azure Information Protection. Para obtener instrucciones, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).