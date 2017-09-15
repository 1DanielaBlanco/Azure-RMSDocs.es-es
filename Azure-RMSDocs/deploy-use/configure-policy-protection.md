---
title: "Configuración de una etiqueta de Azure Information Protection para protección"
description: "Puede proteger sus documentos y mensajes de correo electrónico más confidenciales mediante la configuración de una etiqueta para utilizar la protección de Rights Management."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/12/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: fce3c905f2f48c2723ee7f0b55ff5ddb77f6258a
ms.sourcegitcommit: 94a9b6714c555b95f6064088e77ed94f08224a15
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Configuración de una etiqueta para la protección de Rights Management

>*Se aplica a: Azure Information Protection*

Puede proteger los documentos y los correos electrónicos más confidenciales mediante un servicio de Rights Management. Este servicio usa directivas de cifrado, identidad y autorización para ayudarle a impedir la pérdida de datos. La protección se aplica al configurar una etiqueta para usar la protección de Rights Management para documentos y correos electrónicos, o la opción **No reenviar** para los mensajes de correo electrónico de Outlook. 

## <a name="how-the-protection-works"></a>Funcionamiento de la protección

Cuando un documento o un correo electrónico están protegidos con Rights Management, se cifran en reposo y en tránsito y solo los usuarios autorizados pueden descifrarlos. Este cifrado permanece con el documento o el correo electrónico, incluso si se cambia de nombre. Además, puede configurar derechos y restricciones de uso, como en los ejemplos siguientes:

- Solo los usuarios de su organización pueden abrir el documento o correo electrónico confidencial de la empresa.

- Solo los usuarios del departamento de marketing pueden editar e imprimir el documento o correo electrónico de anuncio de promoción, mientras que los demás usuarios de la organización solo pueden leerlo.

- Los usuarios no pueden reenviar un correo electrónico ni copiar información desde ahí que contenga noticias sobre una reorganización interna.

- La lista de precios actual que se envía a asociados comerciales no se puede abrir después de una fecha especificada.

Para obtener más información sobre la protección de Azure Rights Management y su funcionamiento, vea [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar una etiqueta para aplicar esta protección, se debe activar el servicio Azure Rights Management para su organización. Si aún no lo ha hecho, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

Cuando la etiqueta aplica protección, no es adecuado guardar un documento protegido en SharePoint o en OneDrive. Estas ubicaciones no admiten las características siguientes para los archivos protegidos: coautoría, Office Online, búsqueda, vista previa de documentos, miniaturas, eDiscovery y prevención de pérdida de datos (DLP). 

No es necesario que Exchange esté configurado para Information Rights Management (IRM) para que los usuarios puedan aplicar las etiquetas en Outlook para proteger sus mensajes de correo electrónico. Sin embargo, hasta que no se configure Exchange para IRM, no disfrutará de toda la funcionalidad derivada del uso de la protección de Azure Rights Management con Exchange. Por ejemplo, los usuarios no podrán ver los correos electrónicos protegidos en teléfonos móviles o con Outlook en la web, los correos electrónicos protegidos no se podrán indexar para la búsqueda, y no podrá configurar Exchange Online DLP para la protección de Rights Management. A fin de configurar Exchange para admitir estos escenarios adicionales, consulte los siguientes recursos:

- Para Exchange Online, consulte las instrucciones de [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Para Exchange local, debe implementar el [conector RMS y configurar los servidores de Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-rights-management-protection"></a>Para configurar una etiqueta para la protección de Rights Management

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global. Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global). Pero si la etiqueta que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. Seleccione la etiqueta que quiere configurar, que abre la hoja **Etiqueta**. 

4. En la hoja **Etiqueta**, busque **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta** y seleccione una de las opciones siguientes.
    
    - **No configurado**: seleccione esta opción si la etiqueta está configurada actualmente para aplicar la protección y ya no desea que la etiqueta seleccionada aplique la protección. Ahora, vaya al paso 11.
    
    - **Proteger**: seleccione esta opción para aplicar la protección y, a continuación, vaya al paso 5.
    
    - **Quitar protección**: seleccione esta opción para quitar la protección si un documento o correo electrónico está protegido. Ahora, vaya al paso 11.
        
        Tenga en cuenta que para que los usuarios puedan aplicar una etiqueta con esta opción, deben tener permisos para quitar la protección de Rights Management. Este requisito implica que los usuarios deben tener el [derecho de uso](../deploy-use/configure-usage-rights.md) **Exportar** o **Control total**. o bien que sean propietarios de Rights Management (lo que concede automáticamente el derecho de uso Control total) o [superusuarios para Azure Rights Management](../deploy-use/configure-super-users.md). Las plantillas predeterminadas de Azure Rights Management no incluyen los derechos de uso que permiten a los usuarios quitar la protección. 
        
        Si los usuarios no tienen permisos para quitar la protección de Rights Management y seleccionan una etiqueta configurada con la opción **Quitar protección**, se muestra el mensaje siguiente: **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**

5. Si seleccionó **Proteger**, seleccione ahora **Protección** para abrir la hoja **Protección**:
    
    ![Configurar la protección para una etiqueta de Azure Information Protection](../media/info-protect-protection-bar-configured.png)

6. En la hoja **Protección**, seleccione **Azure RMS**, **Azure (clave en la nube)** o **HYOK (AD RMS)**. La primera opción cambiará de nombre próximamente.
    
    En la mayoría de los casos, se selecciona **Azure RMS** o **Azure (clave en la nube)** para la configuración de permisos. No seleccione **HYOK (AD RMS)** a menos que haya leído y comprendido los requisitos previos y restricciones que acompañan a esta configuración "*mantenga su propia clave*" (HYOK). Para obtener más información, consulte [Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS](configure-adrms-restrictions.md). Para continuar con la configuración de Hold your own key (HYOK, Mantenga su propia clave) (AD RMS), vaya al paso 10.
    
7. Seleccione una de las siguientes opciones:
    
    - **Select a predefined template** (Seleccionar una plantilla predefinida): para usar una de las plantillas predeterminadas o una plantilla personalizada que configuró. Esta plantilla debe estar publicada (no archivada) y no debe estar vinculada a otra etiqueta. Cuando seleccione esta opción, puede usar el botón **Editar plantilla** para [convertir la plantilla en una etiqueta](configure-policy-templates.md#to-convert-templates-to-labels).
    
    - **Establecer permisos**: para definir una nueva configuración de protección en este portal.
    
    - **Establecer permisos definidos por el usuario (versión preliminar)**: para permitir que los usuarios especifiquen a quién se le debe conceder permisos y cuáles. Después, puede refinar esta opción y elegir solo Outlook (valor predeterminado), o Word, Excel, PowerPoint y el Explorador de archivos. 
        
        Si elige la opción para Outlook: la etiqueta se muestra en Outlook y el comportamiento resultante cuando los usuarios aplican la etiqueta es el mismo que el de la opción No reenviar.
        
        Si elige la opción para Word, Excel, PowerPoint y el Explorador de archivos: esta opción requiere la versión preliminar del cliente de Azure Information Protection. Cuando se establece esta opción y los usuarios tienen el cliente de versión preliminar, la etiqueta se muestra en estas aplicaciones. El comportamiento resultante cuando los usuarios aplican la etiqueta consiste en mostrar el cuadro de diálogo para que los usuarios seleccionen permisos personalizados. En este cuadro de diálogo, los usuarios deben especificar los permisos, los usuarios o los grupos y las fechas de expiración. Asegúrese de que los usuarios tengan instrucciones e indicaciones sobre cómo proporcionar estos valores.

8. Si ha seleccionado **Seleccionar una plantilla predefinida** para **Azure RMS** o **Azure (clave en la nube)**, haga clic en el cuadro desplegable y seleccione la [plantilla](../deploy-use/configure-policy-templates.md) que quiera usar para proteger documentos y correos electrónicos con esta etiqueta. No verá las plantillas archivadas o las plantillas que ya estén seleccionadas para otra etiqueta.
    
    Si selecciona una **plantilla de departamento** o si ha configurado los [controles de incorporación](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Los usuarios que estén fuera del ámbito configurado de la plantilla o que se excluyan al aplicar la protección de Azure Rights Management seguirán viendo la etiqueta, pero no podrán aplicarla. Si seleccionan la etiqueta, verán el mensaje siguiente: **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**
        
        Observe que siempre se muestran todas las plantillas publicadas, aunque vaya a configurar una directiva de ámbito. Por ejemplo, va a configurar una directiva de ámbito para el grupo Marketing. Las plantillas que puede seleccionar no se limitan a las plantillas cuyo ámbito sea el grupo Marketing, y es posible seleccionar una plantilla de departamento que los usuarios seleccionados no pueden usar. Para facilitar la configuración y reducir la solución de problemas, puede nombrar la plantilla de departamento de forma que coincida con la etiqueta de la directiva de ámbito. 
            
9. Si ha seleccionado **Establecer permisos** para **Azure RMS** o **Azure (clave en la nube)**, esta opción le permite configurar los mismos valores que puede configurar en una plantilla. 
    
    Seleccione **Agregar permisos** y, en la hoja **Agregar permisos**, seleccione el primer conjunto de usuarios y grupos que tendrán permisos para usar el contenido que se protegerá mediante la etiqueta seleccionada:
    
    - Elija **Seleccionar de la lista** para agregar todos los usuarios de la organización o vaya al directorio.
        
        Los usuarios o grupos deben disponer de una dirección de correo electrónico. En un entorno de producción esto no será un problema, pero en un entorno de pruebas simple es posible que tenga que agregar direcciones de correo electrónico para cuentas de usuario o grupos.
        
    - Seleccione **Escribir detalles** para especificar manualmente las direcciones de correo electrónico de usuarios individuales o grupos (internos o externos). También puede escribir el nombre de dominio de una organización para especificar todos los usuarios de dicha organización. 
        
    >[!NOTE]
    >Si una dirección de correo electrónico cambia después de seleccionar el usuario o grupo, vea la sección [Consideraciones si cambian las direcciones de correo electrónico](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) de la documentación de planeación.
    
    Como práctica recomendada, use grupos en lugar de usuarios. Esta estrategia simplifica la configuración y hace que sea menos probable que tenga que actualizar la configuración de etiqueta más adelante y volver a proteger el contenido. Sin embargo, si realiza cambios en el grupo, recuerde que por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](../plan-design/prepare.md#group-membership-caching-by-azure-rights-management ). 
    
    Cuando haya especificado el primer conjunto de usuarios y grupos, seleccione los permisos que les quiere conceder. Para más información sobre los permisos que se pueden seleccionar, vea [Configuración de los derechos de uso para Azure Rights Management](configure-usage-rights.md). Tenga en cuenta que las aplicaciones que son compatibles con esta protección pueden aplicar estos permisos de forma diferente. Consulte su documentación y realice sus propias pruebas con las aplicaciones que usan los usuarios para comprobar el comportamiento antes de implementar la plantilla para los usuarios.
    
    Si es necesario, ahora puede agregar un segundo conjunto de usuarios y grupos con derechos de uso. Repita el proceso hasta que haya especificado todos los usuarios y grupos y sus permisos correspondientes.

    >[!TIP]
    >Considere la posibilidad de agregar el permiso personalizado **Copiar y extraer contenido** y concedérselo a administradores de recuperación de datos o a personal de otros roles responsable de la recuperación de información. Si es necesario, estos usuarios pueden quitar la protección de archivos y correos electrónicos que se protegerán con esta etiqueta o plantilla. Esta capacidad de quitar la protección en el nivel de permiso para un documento o correo electrónico proporciona un control más minucioso que la [característica de superusuario](configure-super-users.md).
    
    Para todos los usuarios y grupos que ha especificado, en la hoja **Protección**, compruebe si quiere realizar cambios en las opciones siguientes. Tenga en cuenta que esta configuración, al igual que los permisos, no se aplica al [emisor de Rights Management ni al propietario de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) ni a ningún [superusuario](configure-super-users.md) que haya asignado.
    
    |Configuración|Más información|Configuración recomendada
    |-----------|--------------------|--------------------|
    |**expiración del contenido**|Defina una fecha o un número de días para esta plantilla cuando los documentos o correos electrónicos que están protegidos por dicha plantilla no deben abrirse para los usuarios seleccionados. Puede especificar una fecha o un número de días a partir del momento en que se aplicación la protección al contenido.<br /><br />Cuando se especifica una fecha, entra en vigor a medianoche en su zona horaria actual.|**El contenido nunca expira** a menos que el contenido tenga un requisito de límite de tiempo específico.|
    |**Permitir acceso sin conexión**|Use esta configuración para equilibrar los requisitos de seguridad que tiene (incluye el acceso después de la revocación) con la capacidad para que los usuarios seleccionados abran el contenido protegido cuando no tengan una conexión a Internet.<br /><br />Si especifica que el contenido no está disponible sin conexión a Internet o que el contenido está disponible solamente durante un número concreto de días, cuando se supere ese umbral, estos usuarios deberán volver a autenticarse y se registrará su acceso. Cuando esto sucede, si sus credenciales no se han almacenado en la memoria caché, se pedirá a los usuarios que inicien sesión antes de que puedan abrir el documento o correo electrónico.<br /><br />Además de la reautenticación, también se vuelve a evaluar la directiva y la pertenencia al grupos de usuarios. Esto significa que los usuarios podrían experimentar diferentes resultados de acceso para el mismo documento o correo electrónico si se producen cambios en la directiva o la pertenencia al grupo desde la última vez que se accedió al contenido. No podría incluir acceso si se [revocó](../rms-client/client-track-revoke.md) el documento.|Según el grado de confidencialidad del contenido:<br /><br />- **Número de días durante los cuales el contenido está disponible sin conexión a Internet** = **7** para datos empresariales confidenciales que podrían causar daños a la empresa si se comparten con personas no autorizadas. Esta recomendación ofrece un compromiso equilibrado entre flexibilidad y seguridad. Ejemplos: contratos, informes de seguridad, resúmenes de previsiones y datos de cuentas de ventas.<br /><br />- **Nunca** para datos comerciales extremadamente confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Esta documentación da propiedad a la seguridad por sobre la flexibilidad y garantiza que si se revoca el documento, inmediatamente se impedirá que los usuarios autorizados abran el documento. Ejemplos: información sobre empleados y clientes, contraseñas, código fuente e informes financieros previamente anunciados.|
    
    Cuando haya terminado de configurar los permisos, haga clic en **Aceptar**. 
    
    Esta agrupación de configuraciones crea una plantilla personalizada para el servicio Azure Rights Management. Estas plantillas se pueden usar con aplicaciones y servicios que se integran con Azure Rights Management. Para información sobre cómo los equipos y servicios descargan y actualizan estas plantillas, consulte [Refreshing templates for users and services](refresh-templates.md) (Actualización de plantillas para usuarios y servicios).

10. Si ha seleccionado **HYOK (AD RMS)**, elija **Set AD RMS templates details** (Establecer detalles de plantillas de AD RMS) o **Establecer permisos definidos por el usuario (versión preliminar)** y, después, especifique la dirección URL de administración de licencias del clúster de AD RMS.
    
    Para obtener instrucciones sobre cómo especificar un GUID de plantilla y la dirección URL de administración de licencias, vea [Buscar la información para especificar la protección de AD RMS con una etiqueta de Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    Para usar la opción de permisos definidos por el usuario, debe tener la versión preliminar del cliente de Azure Information Protection. Esta opción permite que los usuarios especifiquen a quién se le debe conceder permisos y cuáles. Después, puede refinar esta opción y elegir solo Outlook (valor predeterminado), o Word, Excel, PowerPoint y el Explorador de archivos. 
    
    Si elige la opción para Outlook: la etiqueta se muestra en Outlook y el comportamiento resultante cuando los usuarios aplican la etiqueta es el mismo que el de la opción No reenviar.
    
    Si elige la opción para Word, Excel, PowerPoint y el Explorador de archivos: la etiqueta se muestra en estas aplicaciones. El comportamiento resultante cuando los usuarios aplican la etiqueta consiste en mostrar el cuadro de diálogo para que los usuarios seleccionen permisos personalizados. En este cuadro de diálogo, los usuarios deben especificar los permisos, los usuarios o los grupos y las fechas de expiración. Asegúrese de que los usuarios tengan instrucciones e indicaciones sobre cómo proporcionar estos valores. Actualmente, esta opción en el Explorador de archivos siempre usa la protección de Azure RMS, en lugar de la protección de HYOK (AD RMS).

11. Haga clic en **Aceptar** para cerrar la hoja **Protección** y ver la opción de **No reenviar** o la pantalla de la plantilla elegida para la opción **Protección** de la hoja **Etiqueta**.

12. En la hoja **Etiqueta**, haga clic en **Guardar**.

13. En la hoja **Azure Information Protection**, use la columna **PROTECCIÓN** para confirmar que la etiqueta muestre la configuración de protección que quiera:
    
    - **Azure RMS** o **HYOK (AD RMS)**, o bien una marca de verificación si la protección está configurada. 
    
    - **Quitar la protección** o una marca en forma de x para indicar la cancelación si ha configurado una etiqueta para quitar la protección.
    
    - Un campo en blanco cuando no se haya establecido la protección. 

13. Para que los cambios estén disponibles para los usuarios, haga clic en **Publicar**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]