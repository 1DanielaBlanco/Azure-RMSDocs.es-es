---
# required metadata

title: Supervisión del conector de Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/09/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Supervisión del conector de Azure Rights Management

*Se aplica a: Azure Rights Management, Windows Server 2012, Windows Server 2012 R2*

Una vez que haya instalado y configurado el conector de RMS, puede usar los siguientes métodos e información para ayudarle a supervisar el conector y el uso de Azure RMS por parte de la organización.

## Entradas del registro de eventos de aplicación

El conector de RMS usa el registro de eventos de la aplicación para registrar las entradas del **conector de Microsoft RMS**. 

Por ejemplo, los eventos de información como Id. 1000 confirman que el servicio del conector se ha iniciado, Id. 1002 cuando un servidor se conecta correctamente al conector de RMS e Id. 1004 cada vez que la lista de cuentas autorizadas (se enumera cada cuenta) se descarga al conector. 

Si no ha configurado el conector para que use HTTPS, espere a ver una identificación de la advertencia 2002 de que un cliente está usando una conexión (HTTP) no segura.

Si el conector no se puede conectar a Azure RMS, probablemente vea el Error 3001. Por ejemplo, este podría ser el resultado de un problema DNS o de la falta de acceso a Internet de uno o más servidores que ejecutan el conector de RMS. 

> [!TIP] Cuando los servidores del conector de RMS no pueden conectarse a Azure RMS, las configuraciones de proxy web suelen ser el motivo.

Al igual que con todas las entradas de registro de eventos, explore el mensaje para obtener más detalles.

Además de comprobar el registro de eventos cuando implemente por primera vez el conector, compruebe si hay advertencias y errores de forma regular. Por ejemplo, el conector puede estar funcionando como se esperaba inicialmente pero otros administradores pueden cambiar las configuraciones dependientes. Por ejemplo, otro administrador cambia la configuración del servidor de proxy web de forma que los servidores del conector de RMS ya no tengan acceso a Internet (Error 3001) o quita una cuenta de equipo de un grupo que ha especificado como autorizado para usar el conector (Advertencia 2001).

## Contadores de rendimiento

Cuando instale el conector de RMS, automáticamente crea contadores de rendimiento del **conector de Microsoft Rights Management** que puede encontrar útiles para ayudarle a supervisar el rendimiento del uso de Azure RMS a través del conector. 

Por ejemplo, si habitualmente experimenta retrasos al proteger sus documentos o correos electrónicos, o cuando abre documentos o correos electrónicos protegidos, los contadores de rendimiento pueden ayudarle a determinar si el retraso se debe al tiempo de procesamiento del conector, al tiempo de procesamiento de Azure RMS o a retrasos de red. Para ayudarle a identificar dónde se produce el retraso, busque contadores que incluyan recuentos promedio para el **tiempo de procesamiento del conector**, el **tiempo de respuesta del servicio** y el **tiempo de respuesta del conector**. Por ejemplo: **Tiempo de respuesta medio del conector de procesamiento de solicitudes por lotes correctas de licencias**.

Si ha agregado recientemente nuevas cuentas de servidor para usar el conector, un buen contador para comprobar es **Tiempo desde la última actualización de la directiva de autorización** para confirmar que el conector ha descargado la lista desde que la ha actualizado o si necesita esperar un poco más (hasta 15 minutos).

## RMS Analyzer

Puede usar la herramienta Rights Management Services Analyzer para ayudarle a supervisar el estado del conector y a identificar cualquier problema de configuración.

Si todavía no ha descargado esta herramienta, puede hacerlo desde el [Centro de descarga](https://www.microsoft.com/en-us/download/details.aspx?id=46437) y, después, instalarla en cualquier equipo que tenga acceso a Internet y que pueda conectarse al conector de RMS. Ejecute la herramienta y, en la página de **Bienvenida**, seleccione la opción **Conector de Azure RMS**.

Para obtener información e instrucciones adicionales, vea los **Detalles** y las **Instrucciones de instalación** en la página de descarga.

## Registro

El registro de uso le ayuda a identificar cuándo los correos electrónicos y los documentos están protegidos y consumidos. Cuando esto se realiza mediante el conector de RMS, el campo Identificador de usuario de los registros contiene el nombre de la entidad de servicio que se genera automáticamente cuando instala el conector de RMS.

Para más información, consulte [Registro y análisis del uso de Azure Rights Management](log-analyze-usage.md).

Si necesita un registro más detallado para fines de diagnóstico, puede usar [DebugView](http://go.microsoft.com/fwlink/?LinkID=309277) de Windows Sysinternals y habilitar el seguimiento para el conector de RMS mediante la modificación del archivo web.config para el sitio predeterminado en IIS. Para ello:

1. Localice el archivo web.config desde **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Localice la línea siguiente:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Reemplace esa línea con lo siguiente:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Detenga e inicie IIS para activar el seguimiento. 

5.  Cuando haya capturado los seguimientos que necesita, revierta la línea en el paso 3 y detenga e inicie IIS de nuevo.



<!--HONumber=Jun16_HO2-->


