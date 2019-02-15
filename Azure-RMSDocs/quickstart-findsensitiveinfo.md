---
title: 'Guía de inicio rápido: Búsqueda de información confidencial en los archivos mediante el analizador de Azure Information Protection (AIP)'
description: Utilice el analizador de Azure Information Protection para buscar la información confidencial que tiene en los archivos almacenados en un entorno local.
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 02/15/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: information-protection
ms.openlocfilehash: 07baee062d994b6efd97084bf0b293adb2d5fb84
ms.sourcegitcommit: 89d2c2595bc7abda9a8b5e505b7dcf963e18c822
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56266019"
---
# <a name="quickstart-find-what-sensitive-information-you-have-in-files-stored-on-premises"></a>Inicio rápido: Búsqueda de la información confidencial de los archivos almacenados en un entorno local

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

En este tutorial, deberá instalar y configurar el analizador de Azure Information Protection para buscar la información confidencial que tiene en los archivos que se encuentran en un almacén de datos local. Por ejemplo, una carpeta local, un recurso compartido de red o un servidor de SharePoint Server.

Nota: Este tutorial rápido usa la versión de disponibilidad general actual del analizador y la versión preliminar, donde se utiliza Azure Portal para la configuración.

Puede finalizar esta configuración en menos de 10 minutos.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará:

1. Una suscripción que incluya el plan 1 o el plan 2 de Azure Information Protection.
    
    Si no tiene una de estas suscripciones, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

2. El cliente de Azure Information Protection está instalado en su equipo. 
    
    Para instalar el cliente, vaya al [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargue **AzInfoProtection.exe** en la página de Azure Information Protection.
    
3. También se instala SQL Server Express en el equipo.
    
    Si esta edición de SQL Server no está todavía instalada, puede descargarla desde el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/sql-server/sql-server-editions-express) y seleccionar una instalación básica.

4. Su cuenta de dominio se sincroniza con Azure AD.

Para ver una lista completa de los requisitos previos par utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).

## <a name="prepare-a-test-folder-and-file"></a>Preparación de una carpeta y un archivo de prueba

Para realizar una prueba inicial que confirme que el analizador funciona:

1. Cree la carpeta local en su equipo. Por ejemplo, **TestScanner** en la unidad C local.

2. Cree y guarde un documento de Word en esa carpeta, que incluya el texto **4242-4242-4242-4242** (un número de tarjeta de crédito conocido para realizar pruebas).

## <a name="install-the-scanner"></a>Instalación del escáner

1. Inicie una sesión de PowerShell con la opción **Ejecutar como administrador**.

2. Use el siguiente comando para instalar el analizador, especificando su propio nombre de equipo:
    
        Install-AIPScanner -SqlServerInstance <your computer name>\SQLEXPRESS
    
    Cuando se le pida, proporcione sus propias credenciales para el analizador con el formato \<dominio\nombre usuario> y, a continuación, la contraseña. 

## <a name="specify-your-test-data-store"></a>Especificación del almacén de datos de prueba

En la sesión de PowerShell, escriba el siguiente comando:

    Add-AIPScannerRepository -Path C:\TestScanner

## <a name="configure-the-scanner-to-discover-all-information-types"></a>Configuración del analizador para detectar todos los tipos de información

En la sesión de PowerShell, escriba el siguiente comando:

    Set-AIPScannerConfiguration -Enforce Off -Schedule Manual -DiscoverInformationTypes All

Este comando configura el analizador para realizar una detección de una sola vez de todos los archivos en el repositorio de datos especificado. Este análisis busca todos los tipos conocidos de información confidencial, y no requiere que configure primero las etiquetas o las opciones de directiva de Azure Information Protection.

## <a name="start-the-scan-and-confirm-it-finished"></a>Inicio del análisis y confirmación de finalización

1. En la sesión de PowerShell, escriba el siguiente comando para iniciar el analizador:
    
        Start-AIPScan
    
    Hay solo un archivo pequeño para inspeccionar, por lo que este análisis de prueba inicial será muy rápido. 

2. Vaya al registro de eventos **Visor de eventos** > **Aplicaciones y servicios** > **Azure Information Protection** de Windows. 
    
    Confirme que Azure Information Protection muestra el identificador de evento informativo **911** para el proceso **MSIP.Scanner**. La entrada del registro de eventos también contiene un resumen de los resultados del análisis.

## <a name="see-detailed-results"></a>Revisión de resultados detallados

Mediante el Explorador de archivos, busque los informes del analizador en %*localappdata*%\Microsoft\MSIP\Scanner\Reports. Abra el archivo de informe detallado con el formato .csv.

En Excel, las dos primeras columnas muestran el repositorio del almacén de datos y el nombre de archivo. Al consultar las columnas, verá una denominada **Information Type Name** (Nombre de tipo de información), que es la que más le interesa. Para nuestra prueba inicial, muestra **Credit Card Number** (Número de tarjeta de crédito), uno de los muchos tipos de información confidencial que puede encontrar el analizador.

## <a name="scan-your-own-data"></a>Análisis de sus propios datos

1. Vuelva a ejecutar Add-AIPScannerRepository, esta vez especificando sus propios almacenes de datos locales donde desee buscar información confidencial. 
    
    Puede especificar una carpeta local, un recurso compartido de red (ruta de acceso UNC) o una dirección URL de servidor de SharePoint Server para un sitio o una biblioteca de SharePoint. 
    
    - Ejemplo de una carpeta local:
        
            Add-AIPScannerRepository -Path D:\Data\Finance
    
    - Ejemplo de un recurso compartido de red
        
            Add-AIPScannerRepository -Path \\NAS\HR
    
    - Ejemplo de una carpeta de SharePoint:
        
            Add-AIPScannerRepository -Path "http://sp2016/Shared Documents"

2. Reinicie el analizador:
    
        Start-AIPScan

3. Vea los resultados nuevo cuando el análisis haya finalizado. 
    
    El tiempo que tarde el análisis depende de la cantidad de archivos que haya en el almacén de datos, su tamaño y su tipo. 

## <a name="clean-up-resources"></a>Limpieza de recursos

En un entorno de producción, ejecutaría el analizador en un servidor de Windows Server, con una cuenta de servicio que se autentica en modo silencioso en el servicio de Azure Information Protection. También usaría una versión de nivel empresarial de SQL Server y es probable que especificase varios repositorios de datos. 

Para limpiar los recursos, una vez que esté listo para esa implementación en producción, ejecute el siguiente comando para desinstalar el analizador en la sesión de PowerShell:

    Uninstall-AIPScanner

Luego, reinicie el equipo.

Este comando no quita los elementos siguientes; por ello, debe quitarlos manualmente si no los necesita una vez finalizado este tutorial de inicio rápido:

- La base de datos de SQL Server denominada **AzInfoProtection** que se creó mediante la ejecución del cmdlet Install-AIPScanner cuando se instaló el analizador de Azure Information Protection. 

- Los informes del analizador se encuentran en %*localappdata*%\Microsoft\MSIP\Scanner\Reports.

- La asignación de derechos de usuario **Iniciar sesión como un servicio** que se concedió a la cuenta de dominio para el equipo local.


## <a name="next-steps"></a>Pasos siguientes

Este inicio rápido incluye la configuración mínima para que pueda ver rápidamente cómo puede el analizador encontrar información confidencial en un recurso compartido de red. Si está listo para instalar el analizador en un entorno de producción, vea [Implementación del analizador de Azure Information Protection para clasificar y proteger automáticamente los archivos](deploy-aip-scanner.md).

Si desea clasificar y proteger los archivos que contienen información confidencial, debe configurar las etiquetas de Azure Information Protection para la clasificación y protección automáticas:

- [Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection](configure-policy-classification.md)

- [Cómo configurar una etiqueta para la protección de Rights Management](configure-policy-protection.md)
