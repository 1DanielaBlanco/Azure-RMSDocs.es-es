---
title: "Supervisión del conector de Rights Management - AIP"
description: "Información para ayudarle a supervisar el conector y el uso de la organización del servicio Azure Rights Management de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 8a1b3e54-f788-4f84-b9d7-5d5079e50b4e
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a5a40277c95e376042fc77b7ba39bfc66a948fde
ms.sourcegitcommit: 31e128cc1b917bf767987f0b2144b7f3b6288f2e
translationtype: HT
---
# <a name="monitor-the-azure-rights-management-connector"></a>Supervisión del conector de Azure Rights Management

>*Se aplica a: Azure Information Protection, Windows Server 2012, Windows Server 2012 R2*

Después de instalar y configurar el conector RMS, puede usar los siguientes métodos e información para que le resulte más fácil supervisar el conector y el uso que realiza la organización del servicio Azure Rights Management de Azure Information Protection.

## <a name="application-event-log-entries"></a>Entradas del registro de eventos de aplicación

El conector de RMS usa el registro de eventos de la aplicación para registrar las entradas del **conector de Microsoft RMS**. 

Por ejemplo, los eventos de información como Id. 1000 confirman que el servicio del conector se ha iniciado, Id. 1002 cuando un servidor se conecta correctamente al conector de RMS e Id. 1004 cada vez que la lista de cuentas autorizadas (se enumera cada cuenta) se descarga al conector. 

Si no ha configurado el conector para que use HTTPS, espere a ver una identificación de la advertencia 2002 de que un cliente está usando una conexión (HTTP) no segura.

Si el conector no puede establecer conexión con el servicio Azure Rights Management, es muy probable que vea el error 3001. Por ejemplo, este podría ser el resultado de un problema DNS o de la falta de acceso a Internet de uno o más servidores que ejecutan el conector de RMS. 

> [!TIP]
> Si los servidores del conector RMS no pueden conectarse al servicio Azure Rights Management, las configuraciones de proxy web suelen ser el motivo.

Al igual que con todas las entradas de registro de eventos, explore el mensaje para obtener más detalles.

Además de comprobar el registro de eventos cuando implemente por primera vez el conector, compruebe si hay advertencias y errores de forma regular. Por ejemplo, el conector puede estar funcionando como se esperaba inicialmente pero otros administradores pueden cambiar las configuraciones dependientes. Por ejemplo, otro administrador cambia la configuración del servidor de proxy web de forma que los servidores del conector de RMS ya no tengan acceso a Internet (Error 3001) o quita una cuenta de equipo de un grupo que ha especificado como autorizado para usar el conector (Advertencia 2001).

### <a name="event-log-ids-and-descriptions"></a>Id. de registro de eventos y descripciones

Use las siguientes secciones para identificar los id. de eventos posibles, descripciones y cualquier información adicional.

-----

Información **1000**

**Se ha iniciado el servicio web del conector Microsoft RMS.**

Este evento se registra cuando el conector RMS intenta iniciar primero.

----

Información **1001**

**Se ha detenido el servicio web del conector Microsoft RMS.**

Este evento se registra cuando se detiene el conector RMS como resultado de una operación normal. Por ejemplo, IIS se reinicia o se apaga el equipo. 

----

Información **1002**

**Se ha permitido el acceso al conector Microsoft RMS para un servidor autorizado.**

Este evento se registra cuando una cuenta de un servidor local se conecta primero al conector RMS, después de que el administrador de Azure RMS ha autorizado la cuenta en la herramienta de administración del conector de RMS. El SID, el nombre de cuenta y el nombre del equipo que realiza la conexión están en el mensaje de evento.

----

Información **1003**

**La conexión desde el cliente que se enumera a continuación ha cambiado de una conexión (HTTP) no segura a una conexión (HTTPS) segura.**

Este evento se registra cuando un servidor local cambia su conexión al conector RMS de HTTP (menos segura) a HTTPS (más segura). El SID, el nombre de cuenta y el nombre del equipo que realiza la conexión están en el mensaje de evento.

----

Información **1004**

**Se ha actualizado la lista de cuentas autorizadas.**

Este evento se registra cuando el conector RMS ha descargado la lista más reciente de cuentas (cuentas existentes y cualquier cambio) que están autorizadas para usar el conector RMS. Esta lista se descarga cada quince minutos (siempre que el conector RMS se pueda establecer comunicación con el servicio Azure Rights Management).

----

Advertencia **2000**

**Falta la entidad de seguridad de usuario en el contexto HTTP o no es válida, compruebe que el sitio web del conector Microsoft RMS tiene deshabilitada la autenticación anónima en IIS y que solo está habilitada la autenticación de Windows.**

Este evento se registra cuando el conector RMS no puede identificar la cuenta que intenta conectarse al conector RMS. Esto podría ser resultado de una autenticación anónima configurada incorrectamente para IIS o la cuenta es de un bosque que no es de confianza.

----

Advertencia **2001**

**Intento de acceso no autorizado al conector Microsoft RMS.**

Este evento se registra cuando una cuenta intenta conectarse al conector RMS, pero se produce un error. El motivo más habitual es que la cuenta que realiza la conexión no está en la lista descargada de cuentas autorizadas que descarga el conector RMS del servicio Azure Rights Management. Por ejemplo, la lista más reciente aún no se ha descargado (esto ocurre cada 15 minutos) o la cuenta no está en la lista. 

Otra razón puede ser si ha instalado el conector RMS en el mismo servidor que está configurado para usar el conector. Por ejemplo, si instala el conector RMS en un servidor que ejecuta Exchange Server y autoriza una cuenta de Exchange para que use el conector. Esta configuración no se admite porque el conector RMS no puede identificar correctamente la cuenta cuando intenta establecer conexión.

El mensaje de evento contiene información sobre la cuenta y el equipo que intenta conectarse al conector RMS:

- Si la cuenta que intenta conectarse al conector RMS es una cuenta válida, use la herramienta de administrador del conector RMS para agregar la cuenta a la lista de cuentas autorizadas. Para más información sobre qué cuentas deben estar autorizadas, consulte [Agregar un servidor a la lista de servidores autorizados](install-configure-rms-connector.md#add-a-server-to-the-list-of-allowed-servers). 

- Si la cuenta que intenta conectarse al conector RMS es del mismo equipo que el servidor del conector RMS, instale el conector en un servidor independiente. Para más información sobre los requisitos previos para el conector, consulte [Requisitos previos para el conector RMS]( deploy-rms-connector.md#prerequisites-for-the-rms-connector).

----

Advertencia **2002**

**La conexión desde el cliente que se enumera a continuación usa una conexión (HTTP) no segura.**

Este evento se registra cuando un servidor local realiza una conexión correcta al conector RMS, pero la conexión usa HTTP (menos seguro) en lugar de HTTPS (más seguro). Se registra un evento por cuenta en vez de por conexión. Este evento se desencadena de nuevo si la cuenta ha cambiado correctamente a usar HTTPS, pero vuelve a HTTP.

El mensaje de evento contiene el SID de la cuenta, el nombre de cuenta y el nombre del equipo que realiza la conexión al conector RMS.

Para más información sobre cómo configurar el conector RMS para las conexiones HTTPS, consulte [Configuración del conector RMS para usar HTTPS](install-configure-rms-connector.md#configuring-the-rms-connector-to-use-https).

----

Advertencia **2003**

**La lista de autorizaciones está vacía. El servicio no se podrá usar hasta que se rellene la lista de usuarios y grupos autorizados para el conector.**

Este evento se registra cuando el conector RMS no tiene una lista de cuentas autorizadas, por lo que no se puede conectar a él ningún servidor local. El conector RMS descarga la lista de Azure RMS cada 15 minutos. 

Para especificar las cuentas, use la herramienta de administrador del conector RMS. Para más información, consulte [Autorización para que los servidores usen el conector RMS]( install-configure-rms-connector.md#authorizing-servers-to-use-the-rms-connector). 

----

Error **3000**

**Se ha producido una excepción no controlada en el conector Microsoft RMS.**

Este evento se registra cada vez que el conector RMS encuentra un error inesperado, con los detalles del error en el mensaje de evento.

Una posible causa puede identificarse mediante el texto **Error de solicitud con una respuesta vacía** del mensaje de evento. Si ve este texto, puede ser porque tiene un dispositivo de red que está realizando la inspección de SSL en los paquetes entre los servidores locales y el servidor del conector de RMS. Esto no se admite y generará un error de comunicación y este mensaje del registro de eventos.

----

Error **3001**

**Se ha producido una excepción mientras se descargaba la información de autorización.**

Este evento se registra si el conector RMS no puede descargar la lista más reciente de cuentas que tienen autorización para usar el conector RMS, con los detalles del error en el mensaje de evento.



----

## <a name="performance-counters"></a>Contadores de rendimiento

Al instalar el conector RMS, este crea automáticamente contadores de rendimiento del **conector Microsoft Rights Management**, que pueden resultar útiles para supervisar el rendimiento de uso del servicio Azure Rights Management a través del conector. Por ejemplo, si suelen producirse retrasos al proteger documentos o correos electrónicos, o al abrir documentos o correos electrónicos protegidos, los contadores de rendimiento pueden ayudarle a determinar si el retraso se debe al tiempo de procesamiento del conector, al tiempo de procesamiento del servicio Azure Rights Management o a retrasos en la red. Para ayudarle a identificar dónde se produce el retraso, busque contadores que incluyan recuentos promedio para el **tiempo de procesamiento del conector**, el **tiempo de respuesta del servicio** y el **tiempo de respuesta del conector**. Por ejemplo: **Tiempo de respuesta medio del conector de procesamiento de solicitudes por lotes correctas de licencias**.

Si ha agregado recientemente nuevas cuentas de servidor para usar el conector, un buen contador para comprobar es **Tiempo desde la última actualización de la directiva de autorización** para confirmar que el conector ha descargado la lista desde que la ha actualizado o si necesita esperar un poco más (hasta 15 minutos).

## <a name="rms-analyzer"></a>RMS Analyzer

Aunque esta herramienta incluye un soporte técnico "tal cual", puede usar la herramienta Rights Management Services Analyzer para ayudarle a supervisar el estado del conector y a identificar cualquier problema de configuración. Si no ha descargado aún esta herramienta, puede hacerlo desde el [Centro de descarga](https://www.microsoft.com/en-us/download/details.aspx?id=46437). 

Inicie sesión en uno de los servidores que ha configurado para el conector RMS, con una cuenta que ha autorizado para usar el conector para esa carga de trabajo. Por ejemplo, si ha configurado el conector RMS para Exchange, inicie sesión en ese servidor mediante una de las cuentas que ha autorizado para Exchange en la herramienta de configuración del conector de RMS. A continuación, ejecute la herramienta de analizador de RMS con la opción **Ejecutar como administrador**.

Cuando cargue la herramienta, en la página de **Bienvenida**, seleccione la opción **Conector de Azure RMS**. Escriba la dirección URL del conector RMS como la dirección activa y haga clic en la flecha verde. Debería ver los detalles del inquilino mostrados, lo que confirma que el conector puede conectarse correctamente al servicio de Azure Rights Management. Si se produce un error en esta prueba inicial, asegúrese de comprobar la configuración del servidor proxy y los firewalls que podrían estar bloqueando el tráfico del servidor. Después de que se muestren correctamente los detalles del inquilino, puede continuar ejecutando las pruebas de diagnóstico para esa carga de trabajo de servidor, que se comprueba para elementos como números de versión compatibles, requisitos previos y configuración del registro.

Para obtener información e instrucciones adicionales, vea los **Detalles** y las **Instrucciones de instalación** en la página de descarga.

## <a name="logging"></a>Registro

El registro de uso le ayuda a identificar cuándo los correos electrónicos y los documentos están protegidos y consumidos. Cuando esto se realiza mediante el conector RMS, el campo Identificador de usuario de los registros contiene el nombre de la entidad de servicio de **Aadrm_S-1-7-0** que se crea automáticamente para el conector RMS.

Para obtener más información sobre el registro de uso, consulte [Registro y análisis del uso del servicio Azure Rights Management](log-analyze-usage.md).

Si necesita un registro más detallado para fines de diagnóstico, puede usar [DebugView](http://go.microsoft.com/fwlink/?LinkID=309277) de Windows Sysinternals y habilitar el seguimiento para el conector de RMS mediante la modificación del archivo web.config para el sitio predeterminado en IIS. Para ello:

1. Localice el archivo web.config desde **%programfiles%\Microsoft Rights Management connector\Web Service**.

2. Localice la línea siguiente:

        <trace enabled="false" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

3. Reemplace esa línea con lo siguiente:

        <trace enabled="true" requestLimit="10" pageOutput="false" traceMode="SortByTime" localOnly="true"/>

4.  Detenga e inicie IIS para activar el seguimiento. 

5.  Cuando haya capturado los seguimientos que necesita, revierta la línea en el paso 3 y detenga e inicie IIS de nuevo.

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
