---
# required metadata

title: Escenario: Mantener el control de los documentos almacenados en SharePoint | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 1b6244c7-5ab9-4881-bc8f-6fa960390d89

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Escenario: Mantener el control de los documentos almacenados en SharePoint

*Se aplica a: Azure Rights Management, Office 365*

En este escenario y en la documentación de usuario correspondiente se usa Azure Rights Management para garantizar que los documentos de Office almacenados en SharePoint siguen bajo su control mediante el uso de las bibliotecas protegidas. Por ejemplo, los documentos están protegidos automáticamente frente a filtraciones accidentales o intencionadas por parte de los usuarios y puede bloquear el acceso al contenido incluso después de descargarlo o sincronizarlo. Los archivos que quiere proteger podrían usarse para colaborar internamente en documentos o planes de diseño, o bien para otras entregas. Al configurar bibliotecas protegidas para SharePoint, los archivos de Office almacenados en ellas estarán protegidos con Azure Rights Management.

Las instrucciones son adecuadas para el conjunto de circunstancias siguiente:

-   Los empleados comparten y colaboran con documentos de Office que están en una biblioteca de SharePoint.

-   Los empleados no necesitan establecer ni cambiar los permisos que establece un administrador en el nivel de la biblioteca.

-   Los empleados no tienen que compartir estos documentos con personas ajenas a la organización.

## Instrucciones de implementación
![Instrucciones para el administrador para la implementación rápida de Azure RMS](../media/AzRMS_AdminBanner.png)

Asegúrese de que se cumplen los siguientes requisitos y los procedimientos correspondientes antes de pasar a la documentación del usuario.

## Requisitos para este escenario
Para que este escenario funcione, debe disponer de lo siguiente:

|Requisito|Si necesita más información|
|---------------|--------------------------------|
|Ha preparado cuantas y grupos para Office 365 o Azure Active Directory|[Preparación de Azure Rights Management](https://technet.microsoft.com/library/jj585029.aspx)|
|Azure Rights Management no está activado|[Activar Rights Management de Azure](https://technet.microsoft.com/library/jj658941.aspx)|
|Si va a usar SharePoint Server: Implementar el conector RMS y configurarlo para SharePoint|[Implementación del conector de Azure Rights Management](https://technet.microsoft.com/library/dn375964.aspx)|
|Configurar permisos para el sitio de SharePoint que va a proteger|[Administrar permisos para una lista, biblioteca, carpeta, documento o elemento de lista](https://support.office.com/en-ca/article/Manage-permissions-for-a-list-library-folder-document-or-list-item-9d13e7df-a770-4646-91ab-e3c117fcef45)<br /><br />[Aplicación de Information Rights Management a una lista o biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|
|Configurar SharePoint para IRM y bibliotecas protegidas|[Configuración de Information Rights Management (IRM) en el centro de administración de SharePoint](https://support.office.com/en-us/article/Set-up-Information-Rights-Management-IRM-in-SharePoint-admin-center-239ce6eb-4e81-42db-bf86-a01362fed65c)<br /><br />[Aplicación de Information Rights Management a una lista o biblioteca](http://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)|

### Para configurar la biblioteca de SharePoint para la configuración de IRM

1.  Tras configurar SharePoint para que use el servicio IRM, vaya a la biblioteca de SharePoint que quiere proteger con Azure RMS. En la página del sitio **Configuración** &gt; **Information Rights Management (IRM)**, además de seleccionar **Limitar permisos de descarga de esta biblioteca** y de especificar un título de directiva para los administradores y descripciones de directiva para los usuarios, haga clic en **MOSTRAR OPCIONES**.

2.  Seleccione lo siguiente:

    -   **No permitir a los usuarios cargar documentos que no admitan IRM**

    -   Opcional: **Permitir la protección de grupos. Grupo predeterminado** y, luego, especifique el nombre de un grupo adicional que puede que necesite colaborar en documentos almacenados en esta biblioteca, pero fuera de SharePoint. Por ejemplo, el grupo de ventas tiene permisos de edición en el sitio y alguien de este grupo descarga un documento, lo guarda en el disco y lo envía por correo electrónico a un compañero que no está en el grupo de ventas. Si el compañero está en el grupo que especifique aquí, heredará automáticamente los mismos permisos configurados para el sitio y podrá modificar el documento.

        Sin esta opción, solo los usuarios que tienen acceso a la biblioteca de SharePoint podrán colaborar en estos documentos, únicamente mediante descarga de los documentos directamente desde SharePoint. En muchos casos, esta restricción es adecuada.

## Instrucciones de la documentación del usuario
No hay instrucciones de procedimiento específicas para los usuarios sobre este escenario, porque las bibliotecas protegidas no requieren ninguna acción especial por su parte. Los documentos se protegen automáticamente al descargarse, según los permisos que establezca un administrador de SharePoint para el sitio. Con todo, conviene informar a los usuarios de este cambio para que sepan qué esperar y, también, indicar al departamento de soporte técnico qué bibliotecas están protegidas y cómo esto puede restringir el uso de los documentos. Por ejemplo, debido a las limitaciones actuales, estos documentos pueden verse pero no editarse con dispositivos móviles. Si configuró la protección de grupos, haga saber a los usuarios qué grupos pueden tener acceso a los documentos fuera de SharePoint, así como editarlos.

Con la siguiente plantilla, copie y pegue el anuncio en una comunicación dirigida a sus usuarios finales y realice estas modificaciones para reflejar su entorno:

1.  Reemplace cada instancia de *&lt;nombre de la biblioteca de SharePoint&gt;* por el nombre y el vínculo de la biblioteca de SharePoint que ha configurado para Azure Rights Management. Si esta comunicación versa sobre más de una biblioteca protegida, cambie las instrucciones según corresponda.

2.  Si configuró la opción **Permitir la protección de grupos. Grupo predeterminado**, reemplace *&lt;nombre de grupo&gt;* por el nombre del grupo que ha configurado e indique el motivo para &lt;motivo por el que este grupo tiene permisos de acceso para colaborar en los archivos, pero no mediante la biblioteca de SharePoint&gt;. Si no configuró esta opción, borre esta frase.

3.  Reemplace *&lt;detalles de contacto&gt;* por instrucciones sobre cómo los usuarios pueden ponerse en contacto con el departamento de soporte técnico, por ejemplo, un vínculo de sitio web, una dirección de correo electrónico o un número de teléfono.

4.  Haga los cambios que quiera en este anuncio y, después, envíelo a estos usuarios.

En la documentación de ejemplo se muestra cómo ven los usuarios este anuncio tras las personalizaciones.

![Documentación de usuario de la plantilla para la implementación rápida de Azure RMS](../media/AzRMS_UsersBanner.png)

### Anuncio de TI: Cambios en el sitio de &lt;nombre de la biblioteca de SharePoint&gt;
El sitio de SharePoint, **&lt;nombre de la biblioteca de SharePoint&gt;**, está configurado ahora para poder colaborar de forma segura. Por ahora, solo los miembros de &lt;nombre de grupo&gt; pueden abrir estos documentos desde este sitio, aunque los guarde localmente o los envíe por correo electrónico a otra persona. La excepción reside en que estos documentos se pueden compartir con los miembros de &lt;nombre de grupo&gt; tras descargarlos, de forma que &lt;motivo por el que este grupo tiene permisos de acceso para colaborar en los archivos, pero no mediante la biblioteca de SharePoint&gt;. Al editar los archivos, verá un banner informativo amarillo en la parte superior del documento en el que se le indicará que tiene esta protección y quién puede acceder.

Este cambio ayuda a proteger los datos confidenciales de la empresa, ya que los mantiene a salvo de personas que no deberían verlos. Si usa un dispositivo móvil para acceder a estos documentos protegidos, puede verlos, aunque para editarlos deberá usar un dispositivo de escritorio.

No podrá cargar documentos en el sitio &lt;nombre del sitio de SharePoint&gt; si estos no cumplen los requisitos para colaborar de forma segura.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: &lt;detalles de contacto&gt;

### Documentación de usuario de ejemplo
![Documentación de usuario de ejemplo para la implementación rápida de Azure RMS](../media/AzRMS_ExampleBanner.png)

#### Anuncio de TI: Cambios en el sitio de informes y previsiones de ventas
El sitio de SharePoint **Previsiones e informes de ventas**ahora está configurado para poder colaborar de forma segura. Por ahora, solo los miembros de nuestro equipo de ventas y marketing pueden abrir estos documentos desde este sitio, incluso aunque los guarde localmente o los envíe por correo electrónico a otra persona. La excepción es que, después de descargar los documentos, puede compartirlos con los miembros del equipo de finanzas para que puedan extraer las cifras de las previsiones mensuales. Al editar los archivos, verá un banner informativo amarillo en la parte superior del documento en el que se le indicará que tiene esta protección y quién puede acceder.

Este cambio ayuda a proteger los datos confidenciales de la empresa, ya que los mantiene a salvo de personas que no deberían verlos. Si usa un dispositivo móvil para acceder a estos documentos protegidos, puede verlos, aunque para editarlos deberá usar un dispositivo de escritorio.

No podrá cargar documentos en el sitio de informes y previsiones de ventas si estos no cumplen los requisitos para colaborar de forma segura.

**¿Necesita ayuda?**

-   Póngase en contacto con el departamento de soporte técnico: helpdesk@vanarsdelltd.com



<!--HONumber=May16_HO2-->


