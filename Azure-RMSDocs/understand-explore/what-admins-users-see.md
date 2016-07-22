---
title: "¿Qué ven los administradores y los usuarios? | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 013e0eb4-49a7-4e81-9e4d-f56c0ceb017f
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7a9c8b531ec342e7d5daf0cbcacd6597a79e6a55
ms.openlocfilehash: 213d077a65abd5115b7e0491dfc9cd8145752b23


---


# Azure RMS en acción: Qué ven los administradores y los usuarios

*Se aplica a: Azure Rights Management, Office 365*

En este artículo se muestran algunos ejemplos típicos de cómo los administradores y los usuarios ven y pueden usar Azure Rights Management (Azure RMS) para ayudar a proteger la información importante o confidencial.

> [!NOTE]
> En todos estos ejemplos de protección de datos con Azure RMS, el propietario del contenido sigue teniendo pleno acceso a los mismos (archivo o correo electrónico), incluso aunque la protección aplicada conceda permisos a un grupo del que el propietario no sea miembro o esta incluya una fecha de expiración.
>
> Asimismo, el departamento de TI siempre podrá tener acceso a los datos protegidos sin restricciones mediante la característica de superusuario de Rights Management, que concede acceso delegado a los usuarios o servicios autorizados que especifique. Además, TI puede realizar un seguimiento y supervisar el uso de los datos protegidos, por ejemplo, quién tiene acceso a estos y cuándo.

Para otras capturas de pantalla y vídeos que muestran RMS en acción, consulte el [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services) (Blog de seguridad y movilidad empresarial).

## Activación y configuración de Rights Management
Aunque puede usar Windows PowerShell para activar y configurar Azure RMS, es más fácil hacerlo desde el portal de administración. Al activar el servicio, tendrá dos plantillas predeterminadas que los administradores y los usuarios pueden seleccionar para aplicar la protección de la información a los archivos de forma rápida y fácil. También puede crear sus propias plantillas personalizadas para contar con opciones adicionales.

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1](../media/AzRMS_StoryboardActivate_small1.png)


**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1:** Puede usar el centro de administración de Office 365 (primera imagen) o el Portal de Azure clásico (segunda imagen) para activar RMS.<br /><br />Con un solo clic para activar y otro para confirmar, la protección de la información se habilita para los administradores y los usuarios de la organización.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2](../media/AzRMS_TemplatesPortal_small.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2:** Tras la activación, habrá dos plantillas de directivas de derechos automáticamente disponibles para la organización. Una de ellas es de solo lectura (**Solo vista confidencial** se incluye en el nombre) y la otra puede leerse y modificarse (**Confidencial**).

Cuando estas plantillas se aplican a archivos o mensajes de correo electrónico, restringen el acceso a los usuarios de la organización. Se trata de una forma muy rápida y sencilla de ayudar a evitar que los datos de la compañía pasen a personas externas a la organización.

> [!TIP]
> Estas plantillas predeterminadas pueden reconocerse fácilmente porque automáticamente tienen como prefijo el nombre de la organización. En nuestro ejemplo, **VanArsdel, Ltd**.

Si no quiere que los usuarios vean estas plantillas o bien quiere crear las suyas propias, puede hacerlo desde el Portal de Azure clásico. Como se muestra en esta imagen, un asistente le guiará por el proceso de creación de plantillas personalizadas.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 3](../media/AzRMS_TemplatesSettings3.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 3:** El acceso sin conexión, la configuración de la expiración y la publicación o no de la plantilla de inmediato (hacer que aparezca en las aplicaciones que admiten Rights Management) son algunas de las opciones de configuración disponibles si decide crear sus propias plantillas.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 4](../media/AzRMS_TemplatesPortal_ExplorerWord3.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 4:** Como resultado de la publicación de estas plantillas, ahora los usuarios puedan seleccionarlas en aplicaciones como el Explorador de archivos y Microsoft Word:

- Un usuario puede elegir la plantilla predeterminada, **VanArsdel, Ltd – Confidencial**. A partir de entonces, solo los empleados de la organización VanArsdel podrán abrir y usar este documento, aunque se envíe posteriormente por correo electrónico a un usuario externo a la organización o se guarde en una ubicación pública.

- Un usuario podría elegir la plantilla personalizada creada por el administrador, **Ventas y marketing – Solo leer e imprimir**. Al hacerlo, el archivo no solo se protege frente a usuarios externos a la organización, sino que además su uso se restringe a los empleados del departamento de Ventas y marketing. Asimismo, estos empleados no tienen plenos derechos en el documento, solo de lectura e impresión. Por ejemplo, no pueden modificarlo ni copiar su contenido.

---

**Más información sobre este escenario:**

- Para obtener instrucciones detalladas, consulte [Activating Azure Rights Management](../deploy-use/activate-service.md) (Activar Azure Rights Management) y [Configuring custom templates for Azure Rights Management](../deploy-use/configure-custom-templates.md) (Configurar plantillas personalizadas para Azure Rights Management).

- Para ayudar a los usuarios a proteger archivos importantes de la empresa, consulte [Helping users to protect files by using Azure Rights Management](../deploy-use/help-users.md) (Ayudar a los usuarios a proteger archivos mediante Azure Rights Management).

A continuación se muestran algunos ejemplos de cómo los administradores pueden aplicar las plantillas para configurar automáticamente la protección de la información para archivos y correos electrónicos.

## Protección automática de archivos en los servidores de archivos con Windows Server y la infraestructura de clasificación de archivos

En este ejemplo se muestra cómo usar Azure RMS para proteger archivos automáticamente en los servidores de archivos que ejecutan como mínimo Windows Server 2012 y están configurados para usar la infraestructura de clasificación de archivos.

Hay muchas formas de aplicar valores de clasificación a los archivos. Por ejemplo, puede inspeccionar el contenido de los archivos y aplicar clasificaciones integradas en consecuencia, como Confidencialidad e Información de identificación personal. Sin embargo, en este ejemplo, un administrador crea una clasificación personalizada de **Marketing** que se aplica automáticamente a todos los documentos de usuario se guarden en la carpeta **Marketing Promotions** . Aunque esta carpeta está protegida con permisos NTFS que restringen el acceso a los miembros del grupo Marketing, el administrador sabe que dichos permisos pueden perderse si alguien del grupo cambia de ubicación o envía los archivos por correo electrónico. En ese caso, usuarios no autorizados podrían tener acceso a la información de los archivos.

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1](../media/AzRMS_FCI_ConnectorSmall.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1:** El administrador instala y configura el conector de Rights Management (RMS), que actúa como punto de retransmisión entre los servidores locales y Azure RMS.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2](../media/AzRMS_ExampleFCI_ConfigurationSmall.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2:** En el servidor de archivos, el administrador configura las tareas y las reglas de clasificación para que todos los archivos de usuario de la carpeta **Marketing Promotions** se clasifiquen automáticamente como **Marketing** y se protejan mediante cifrado RMS.

Asimismo, selecciona la plantilla personalizada de RMS creada en el primer ejemplo, que restringe el acceso a los miembros del departamento de Ventas y marketing: **Ventas y marketing - Solo leer e imprimir**

Como resultado, todos los documentos de esa carpeta se configuran automáticamente con la clasificación de Marketing y se protegen mediante la plantilla de Ventas y marketing de RMS.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 3](../media/AzRMS_FCI_EmailSmall.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 3:** Cómo ayuda RMS a evitar la filtración de datos a personas que no deben tener acceso a información importante o confidencial:

- Una empleada del departamento de Marketing envía por correo electrónico un informe confidencial de la carpeta Marketing Promotions. Este informe, solicitado por un compañero que se encuentra actualmente en viaje de negocios, contiene nuevas características del producto y planes publicitarios. Sin embargo, la empleada lo envía por error a la persona equivocada al no darse cuenta de que accidentalmente seleccionó un destinatario con un nombre parecido, perteneciente a otra compañía.<br><br>
El destinatario no puede leer el informe confidencial porque no es miembro del grupo de ventas y marketing.

---

**Más información sobre este escenario:**

- Para obtener instrucciones detalladas, consulte [Deploying the Azure Rights Management Connector](../deploy-use/deploy-rms-connector.md) (Implementar el conector de Azure Rights Management).

## Proteger automáticamente los correos electrónicos con Exchange Online y directivas de prevención de pérdida de datos

En el ejemplo anterior se mostraba cómo pueden protegerse automáticamente los archivos que contienen información importante o confidencial, pero ¿qué ocurre si la información no está en un archivo, sino en un mensaje de correo electrónico? Aquí es donde entran en juego las directivas de prevención de pérdida de datos (DLP) de Exchange Online, ya sea solicitando a los usuarios que apliquen la protección de la información (mediante las sugerencias de directiva) o aplicándola automáticamente (mediante reglas de transporte).

En este ejemplo, el administrador configura una directiva para ayudar a la organización a cumplir las normativas de EE. UU. sobre protección de la información de identificación personal, pero también pueden configurarse reglas para otras normativas de conformidad o bien reglas personalizadas definidas por el usuario.

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1](../media/AzRMS_DLPExample1.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1:** En el Centro de administración de Exchange, el administrador usa la plantilla de Exchange denominada **U.S. Personally Identifiable Information (PII) Data** (Información de identificación personal de EE. UU.) para crear y configurar una nueva directiva DLP. Esta plantilla busca información en los mensajes de correo electrónico como los números de la seguridad social y del permiso de conducción.

Las reglas están configuradas de forma que se aplique automáticamente la protección de derechos a los mensajes de correo electrónico que contengan esta información y se envíen fuera de la organización mediante una plantilla de RMS que restrinja el acceso únicamente a los empleados de la empresa.

En este caso, la regla está configurada para usar una de las plantillas predeterminadas del primer ejemplo, **VanArsdel, Ltd – Confidencial**. Sin embargo, también puede ver que las opciones de plantillas incluyen todas las plantillas personalizadas que ha creado, así como la opción **No reenviar** específica de Exchange.

> [!NOTE]
> Si las opciones de configuración que ve son ligeramente diferentes de las de la imagen, quizás necesite seleccionar primero **Más opciones** cuando configure la regla. Después, puede seleccionar **Modificar la seguridad del mensaje** > **Aplicar protección de derechos** y luego seleccionar la plantilla de RMS.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2](../media/AzRMS_DLPUnprotectedEmail_small.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 2:** El jefe de contratación escribe un mensaje de correo electrónico que contiene el número de la seguridad social de un empleado contratado recientemente y lo envía a una empleada del departamento de recursos humanos.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 3](../media/AzRMS_DLPProtectedEmail_small.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 3:** Si este mensaje de correo electrónico se envía o se reenvía a cualquier usuario externo a la organización, la regla DLP aplica automáticamente la protección de derechos.

El mensaje de correo electrónico se cifra al salir de la infraestructura de la organización, por lo que el número de la seguridad social incluido en este no se podrá leer mientras esté en tránsito o se encuentre en la bandeja de entrada del destinatario. El destinatario no podrá leer el mensaje a menos que sea empleado de VanArsdel.

---

**Más información sobre este escenario:**

-   Para obtener más información sobre cómo funciona Azure RMS con Exchange Online, consulte la sección [Exchange Online y Exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) de [Cómo son compatibles las aplicaciones con Azure Rights Management](applications-support.md).

-   Para obtener instrucciones detalladas sobre cómo configurar Exchange Online para Azure RMS, vea [Exchange Online: IRM Configuration](../deploy-use/configure-office365.md#exchange-online-irm-configuration) (Exchange Online: Configuración de IRM) de [Configuring Applications for Azure Rights Management](../deploy-use/configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).

## Protección automática de archivos con SharePoint Online y las bibliotecas protegidas

Aquí se muestra cómo proteger los documentos fácilmente al usar SharePoint Online y las bibliotecas protegidas.

En este ejemplo, el administrador de SharePoint en Contoso ha creado una biblioteca para cada departamento destinada a almacenar y desproteger los documentos de forma centralizada para el control de versiones y la edición. Así, hay una biblioteca para Ventas, otra para Marketing, otra para Recursos humanos, etc. Al cargar o crear un nuevo documento en una de estas bibliotecas protegidas, este hereda la protección de la biblioteca (no es necesario seleccionar ninguna plantilla de directiva de derechos) y queda protegido automáticamente, incluso aunque se mueva fuera de la biblioteca de SharePoint.

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1](../media/AzRMS_StoryboardSPO_small1.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 1:** El administrador habilita Information Rights Management para el sitio de SharePoint.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2](../media/AzRMS_StoryboardSPO_small2.png)

**QUÉ VEN LOS ADMINISTRADORES EN EL PASO 2:** A continuación, habilita Rights Management para una biblioteca. Aunque hay opciones adicionales, esta sencilla configuración suele ser lo único requerido.

Al descargarse ahora los documentos de esta biblioteca, Rights Management los protege automáticamente, heredando así la protección configurada para la biblioteca.

---

![QUÉ VEN LOS ADMINISTRADORES EN EL PASO 3](../media/AzRMS_StoryboardSPO_small3.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 3:** Si un empleado del departamento de ventas desprotege este informe de ventas de la biblioteca, podrá ver claramente en el banner informativo de la parte superior que es un documento protegido con acceso restringido.

El documento permanece protegido aunque el usuario cambie el nombre, lo guarde en otra ubicación o lo comparta mediante correo electrónico. Independientemente del nombre del archivo, su ubicación de almacenamiento o el uso compartido de este por correo electrónico, solo los miembros del departamento de ventas podrán leerlo.

---

**Más información sobre este escenario:**

-   Para obtener más información sobre cómo funciona Azure RMS con SharePoint, consulte la sección [SharePoint Online y SharePoint Server](office-apps-services-support.md#sharepoint-online-and-sharepoint-server) de [Cómo son compatibles las aplicaciones con Azure Rights Management](applications-support.md).

-   Para obtener instrucciones detalladas sobre cómo configurar SharePoint para Azure RMS, vea [SharePoint Online and OneDrive for Business: IRM Configuration (SharePoint Online y OneDrive para la Empresa: Configuración de IRM)](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) de [Configuring Applications for Azure Rights Management](../deploy-use/configure-applications.md) (Configuración de aplicaciones para Azure Rights Management).

## Uso compartido seguro de datos adjuntos con los usuarios móviles

En los ejemplos anteriores se ha mostrado cómo los administradores pueden aplicar automáticamente la protección de la información a los datos importantes y confidenciales. Sin embargo, es posible que en algunas ocasiones los usuarios tengan que aplicar esta protección por sí mismos. Por ejemplo, cuando colaboren con asociados de otra organización y necesiten valores o permisos personalizados no definidos en las plantillas para situaciones ad hoc no cubiertas por los ejemplos anteriores. En estos casos, los usuarios pueden aplicar las plantillas de RMS por sí mismos o configurar permisos personalizados.

En este ejemplo se muestra cómo los usuarios pueden compartir fácilmente un documento con un empleado de otra empresa con el que colaboren y aun así proteger dicho documento y estar seguros de que el destinatario pueda leerlo, incluso desde un dispositivo móvil de uso extendido. En este escenario se usa la aplicación de uso compartido Rights Management, que puede implementarse automáticamente a los equipos Windows de la organización o bien instalarla los usuarios.

En este ejemplo, una empleada de Contoso envía por correo electrónico un documento confidencial de Word a un empleado de Fabrikam. Este lee el documento en su iPad, pero también podría leerlo fácilmente en un iPhone, una tableta o teléfono Android, un equipo Mac o bien un teléfono o equipo Windows.

![QUÉ VEN LOS USUARIOS EN EL PASO 1](../media/AzRMS_StoryboardEmail_small1.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 1:** Alice crea un mensaje de correo electrónico estándar y adjunta un documento desde su equipo Windows.

Hace clic en **Uso compartido seguro** en la cinta de opciones, lo que carga el cuadro de diálogo **Uso compartido seguro** de la aplicación para uso compartido de RMS.

Desea aplicar restricciones al empleado de Fabrikam para ver y modificar el documento y que no pueda copiarlo o imprimirlo, por lo que selecciona **REVISOR - Ver y editar**. También desea recibir un mensaje de correo electrónico cuando alguien intenta abrir el documento y tiene la capacidad de revocar el documento más adelante si es necesario y sabe que la revocación surtirá efecto de inmediato.

---

![QUÉ VEN LOS USUARIOS EN EL PASO 2](../media/AzRMS_StoryboardEmail_small2.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 2:** Bob ve el correo electrónico en su iPad.

Además del mensaje y los datos adjuntos recibidos, se incluyen instrucciones que este sigue para registrarse e instalar la aplicación para uso compartido de RMS en su iPad.

---

![QUÉ VEN LOS USUARIOS EN EL PASO 3](../media/AzRMS_StoryboardEmail_small3.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 3:** Bob ahora puede abrir los datos adjuntos. En primer lugar se le pide que inicie sesión para confirmar que es el destinatario correcto.

Al ver el documento, también ve la información de acceso restringido que le indica que puede ver y editar el documento, pero no copiarlo o imprimirlo.

---

![QUÉ VEN LOS USUARIOS EN EL PASO 4](../media/AzRMS_StoryboardEmail_small4.png)

**QUÉ VEN LOS USUARIOS EN EL PASO 4:** Alice recibe un mensaje de correo electrónico que le indica que Bob ha abierto correctamente el documento que le envió y cuándo obtuvo acceso al mismo.

Aunque este reenvíe el correo electrónico con los datos adjuntos, lo guarde en una ubicación a la que tengan acceso otras personas o se intercepte en la red, el documento no lo podrán leer otros usuarios.

---

**Más información sobre este escenario:**

- Para obtener información detallada, consulte [Proteger un archivo que se comparte por correo electrónico](../rms-client/sharing-app-protect-by-email.md) y [Ver y usar los archivos protegidos](../rms-client/sharing-app-view-use-files.md) de la [Guía de usuario de la aplicación de uso compartido Rights Management](../rms-client/sharing-app-user-guide.md).

- En [Quick start tutorial for Azure Rights Management](../get-started/quick-start-tutorial.md) (Tutorial de inicio rápido de Azure Rights Management) se incluyen instrucciones detalladas para este escenario.

## Pasos siguientes

Ahora que ha visto algunos ejemplos de lo que Azure RMS puede hacer, es posible que le interese cómo lo hace. Para obtener información técnica sobre cómo funciona Azure RMS, consulte [How does Azure RMS work?](how-does-it-work.md) (¿Cómo funciona Azure RMS?).



<!--HONumber=Jun16_HO4-->


