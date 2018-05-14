---
title: Configuración de una etiqueta de Azure Information Protection para protección
description: Puede proteger sus documentos y mensajes de correo electrónico más confidenciales mediante la configuración de una etiqueta para utilizar la protección de Rights Management.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 05/10/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: df26430b-315a-4012-93b5-8f5f42e049cc
ms.openlocfilehash: 8b1024a26e086cb8cbd4696dc37d66350968a0b4
ms.sourcegitcommit: fbc83d699b9e4e9c8e0e7d36f574630af6a4e3d9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="how-to-configure-a-label-for-rights-management-protection"></a>Configuración de una etiqueta para la protección de Rights Management

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Puede proteger los documentos y los correos electrónicos más confidenciales mediante un servicio de Rights Management. Este servicio usa directivas de cifrado, identidad y autorización para ayudarle a impedir la pérdida de datos. La protección se aplica con una etiqueta configurada para usar la protección de Rights Management para documentos y mensajes de correo electrónico, y los usuarios además pueden seleccionar el botón **No reenviar** de Outlook.

Cuando se configura una etiqueta con la configuración de protección de **Azure (clave de nube)**, en segundo plano esta acción crea y configura una plantilla personalizada a la que pueden acceder los servicios y las aplicaciones que se integran con las plantillas de Rights Management. Por ejemplo, las reglas de flujo de correo y Exchange Online, y Outlook en la Web. 

## <a name="how-the-protection-works"></a>Funcionamiento de la protección

Cuando un documento o un mensaje de correo electrónico está protegido mediante un servicio Rights Management, se cifra en reposo y en tránsito. Luego solo puede ser descifrado por usuarios autorizados. Este cifrado permanece con el documento o el correo electrónico, incluso si se cambia de nombre. Además, puede configurar derechos y restricciones de uso, como en los ejemplos siguientes:

- Solo los usuarios de su organización pueden abrir el documento o correo electrónico confidencial de la empresa.

- Solo los usuarios del departamento de marketing pueden editar e imprimir el documento o mensaje de correo electrónico de anuncio de promoción, mientras que los demás usuarios de la organización solo pueden leerlo.

- Los usuarios no pueden reenviar un correo electrónico ni copiar información desde ahí que contenga noticias sobre una reorganización interna.

- La lista de precios actual que se envía a asociados comerciales no se puede abrir después de una fecha especificada.

Para obtener más información sobre la protección de Azure Rights Management y su funcionamiento, vea [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md)

> [!IMPORTANT]
> Para configurar una etiqueta para aplicar esta protección, se debe activar el servicio Azure Rights Management para su organización. Para más información, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

Cuando la etiqueta aplica protección, no es adecuado guardar un documento protegido en SharePoint o en OneDrive. Estas ubicaciones no admiten las características siguientes para los archivos protegidos: coautoría, Office Online, búsqueda, vista previa de documentos, miniaturas, eDiscovery y prevención de pérdida de datos (DLP). 

No es necesario que Exchange esté configurado para Azure Information Protection antes que los usuarios puedan aplicar etiquetas en Outlook para proteger sus correos electrónicos. Sin embargo, hasta que no se configure Exchange para Azure Information Protection, no podrá obtener la funcionalidad completa de la protección de Azure Rights Management con Exchange. Por ejemplo, los usuarios no podrán ver los correos electrónicos protegidos en teléfonos móviles ni con Outlook en Internet, los correos electrónicos protegidos no se podrán indexar para búsquedas y no se podrá configurar la DLP de Exchange Online para la protección de Rights Management. A fin de asegurar que Exchange puede admitir estos escenarios adicionales, consulte los siguientes recursos:

- Para Exchange Online, consulte las instrucciones de [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

- Para Exchange local, debe implementar el [conector RMS y configurar los servidores de Exchange](../deploy-use/deploy-rms-connector.md). 

## <a name="to-configure-a-label-for-protection-settings"></a>Para configurar una etiqueta para los valores de protección

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. En la opción de menú **CLASIFICACIONES** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, seleccione la etiqueta que desee cambiar. 

3. En la hoja **Etiqueta**, busque **Establecer permisos para documentos y correos electrónicos que contengan esta etiqueta** y seleccione una de las opciones siguientes:
    
    - **No configurado**: seleccione esta opción si la etiqueta está configurada actualmente para aplicar la protección y ya no desea que la etiqueta seleccionada aplique la protección. Ahora, vaya al paso 11.
        
        La protección configurada previamente se conserva como una plantilla de protección archivada y se volverá a mostrar si se cambia la opción de nuevo a **Proteger**. No verá esta plantilla en Azure Portal pero, si es necesario, puede administrarla con [PowerShell](configure-templates-with-powershell.md). Este comportamiento significa que el contenido sigue estando disponible si tiene esta etiqueta con la configuración de protección aplicada anteriormente.
    
    - **Proteger**: seleccione esta opción para aplicar la protección y, después, vaya al paso 5 para configurar las opciones de protección.
    
    Nota: puede guardar una etiqueta nueva en esta fase sin tener que aplicar ninguna configuración adicional. Si lo hace, se configurará la etiqueta para aplicar la protección de modo que solo la persona que aplique la etiqueta pueda abrir el documento o el mensaje de correo electrónico sin restricciones de uso. En algunos casos este podría ser el resultado requerido, de manera que un usuario pueda guardar un archivo en cualquier ubicación y garantizar que solo él puede abrirlo. Si este resultado se ajusta a sus necesidades y el resto de los usuarios no tienen que colaborar en el contenido protegido, en lugar de ir al paso 5, vaya directamente al paso 12.
    
    - **Quitar protección**: seleccione esta opción para quitar la protección si un documento o correo electrónico está protegido. Ahora, vaya al paso 11.
        
        La protección configurada previamente se conserva como una plantilla de protección archivada y se volverá a mostrar si se cambia la opción de nuevo a **Proteger**. No verá esta plantilla en Azure Portal pero, si es necesario, puede administrarla con [PowerShell](configure-templates-with-powershell.md). Este comportamiento significa que el contenido sigue estando disponible si tiene esta etiqueta con la configuración de protección aplicada anteriormente.
        
        Tenga en cuenta que para que los usuarios puedan aplicar una etiqueta con esta opción, deben tener permisos para quitar la protección de Rights Management. Este requisito implica que los usuarios deben tener el [derecho de uso](../deploy-use/configure-usage-rights.md) **Exportar** o **Control total**. o bien que sean propietarios de Rights Management (lo que concede automáticamente el derecho de uso Control total) o [superusuarios para Azure Rights Management](../deploy-use/configure-super-users.md). Las plantillas predeterminadas de Azure Rights Management no incluyen los derechos de uso que permiten a los usuarios quitar la protección. 
        
        Si los usuarios no tienen permisos para quitar la protección de Rights Management y seleccionan una etiqueta configurada con la opción **Quitar protección**, se muestra el mensaje siguiente: **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**

4. Si seleccionó **Proteger**, seleccione ahora **Protección** para abrir la hoja **Protección**:
    
    ![Configurar la protección para una etiqueta de Azure Information Protection](../media/info-protect-protection-bar-configured.png)

5. En la hoja **Protección**, seleccione **Azure (clave en la nube)** o **HYOK (AD RMS)**.
    
    En la mayoría de los casos, se selecciona **Azure (clave en la nube)** para la configuración de permisos. No seleccione **HYOK (AD RMS)** a menos que haya leído y comprendido los requisitos previos y restricciones que acompañan a esta configuración "*mantenga su propia clave*" (HYOK). Para obtener más información, consulte [Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS](configure-adrms-restrictions.md). Para continuar con la configuración de Hold your own key (HYOK, Mantenga su propia clave) (AD RMS), vaya al paso 9.
    
6. Seleccione una de las siguientes opciones:
    
    - **Establecer permisos**: para definir una nueva configuración de protección en este portal.
    
    - **Establecer permisos definidos por el usuario (versión preliminar)**: para permitir que los usuarios especifiquen a quién se le debe conceder permisos y cuáles. Después, puede ajustar esta opción y elegir solo Outlook, o Word, Excel, PowerPoint y el Explorador de archivos. Esta opción no se admite, de modo que no funcionará al configurar una etiqueta para la [clasificación automática](configure-policy-classification.md).
        
        Si elige la opción para Outlook: la etiqueta se muestra en Outlook y el comportamiento resultante cuando los usuarios aplican la etiqueta es el mismo que el de la opción No reenviar.
        
        Si elige la opción para Word, Excel, PowerPoint y el Explorador de archivos: si esta opción está establecida, la etiqueta se muestra en estas aplicaciones. El comportamiento resultante cuando los usuarios aplican la etiqueta consiste en mostrar el cuadro de diálogo para que los usuarios seleccionen permisos personalizados. En este cuadro de diálogo, los usuarios deben especificar los permisos, los usuarios o los grupos y las fechas de expiración. Asegúrese de que los usuarios tengan instrucciones e indicaciones sobre cómo proporcionar estos valores.
    
    - **Select a predefined template** (Seleccionar una plantilla predefinida): para usar una de las plantillas predeterminadas o una plantilla personalizada que configuró. Tenga en cuenta que esta opción no se muestra si está modificando una etiqueta en la que antes se usó la opción **Establecer permisos**.
    
    Para seleccionar una plantilla predefinida, la plantilla debe estar publicada (no archivada) y no debe estar vinculada a otra etiqueta. Cuando seleccione esta opción, puede usar el botón **Editar plantilla** para [convertir la plantilla en una etiqueta](configure-policy-templates.md#to-convert-templates-to-labels).
    
    Sugerencia: Si acostumbra a crear y modificar plantillas personalizadas, puede resultarle útil consultar [Tareas que solía realizar con el Portal de Azure clásico](migrate-portal.md).

7. Si ha seleccionado **Establecer permisos** para **Azure (clave en la nube)**, esta opción le permite configurar los mismos valores que puede configurar en una plantilla. 
    
    Seleccione **Agregar permisos** y, en la hoja **Agregar permisos**, seleccione el primer conjunto de usuarios y grupos que tendrán permisos para usar el contenido que se protegerá mediante la etiqueta seleccionada:
    
    - Elija **Seleccione de la lista** para agregar todos los usuarios de su organización mediante la selección de **Agregar \<NombreDeOrganización >-Todos los miembros**. Este parámetro excluye las cuentas de invitado. O bien, busque en el directorio.
        
        Los usuarios o grupos deben disponer de una dirección de correo electrónico. En un entorno de producción, los usuarios y grupos casi siempre tendrán una dirección de correo electrónico, pero en uno simple de pruebas es posible que tenga que agregarlas a las cuentas de usuario o los grupos.
        
    - Seleccione **Escribir detalles** para especificar manualmente las direcciones de correo electrónico de usuarios individuales o grupos (internos o externos). O bien, puede usar esta opción para especificar todos los usuarios de otra organización escribiendo el nombre de dominio de dicha organización. También puede usar esta opción para los proveedores sociales escribiendo su nombre de dominio, como **gmail.com**, **hotmail.com** o **outlook.com**.
        
    >[!NOTE]
    >Si una dirección de correo electrónico cambia después de seleccionar el usuario o grupo, vea la sección [Consideraciones si cambian las direcciones de correo electrónico](../plan-design/prepare.md#considerations-for-azure-information-protection-if-email-addresses-change) de la documentación de planeación.
    
    Como práctica recomendada, use grupos en lugar de usuarios. Esta estrategia simplifica la configuración y reduce la probabilidad de que tenga que actualizar la configuración de etiquetas más adelante y volver a proteger el contenido. Sin embargo, si realiza cambios en el grupo, recuerde que por motivos de rendimiento, Azure Rights Management [almacena en caché la pertenencia al grupo](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). 
    
    Cuando haya especificado el primer conjunto de usuarios y grupos, seleccione los permisos que les quiere conceder. Para más información sobre los permisos que se pueden seleccionar, vea [Configuración de los derechos de uso para Azure Rights Management](configure-usage-rights.md). Tenga en cuenta que las aplicaciones que son compatibles con esta protección pueden aplicar estos permisos de forma diferente. Consulte su documentación y realice sus propias pruebas con las aplicaciones que usan los usuarios para comprobar el comportamiento antes de implementar la plantilla para los usuarios.
    
    Si es necesario, ahora puede agregar un segundo conjunto de usuarios y grupos con derechos de uso. Repita el proceso hasta que haya especificado todos los usuarios y grupos y sus permisos correspondientes.

    >[!TIP]
    >Considere la posibilidad de agregar el permiso personalizado **Guardar como, exportar (EXPORT)** y concedérselo a administradores de recuperación de datos o a personal con otro rol responsable de la recuperación de información. Si es necesario, estos usuarios pueden quitar la protección de archivos y correos electrónicos que se protegerán con esta etiqueta o plantilla. Esta capacidad de quitar la protección en el nivel de permiso para un documento o correo electrónico proporciona un control más minucioso que la [característica de superusuario](configure-super-users.md).
    
    Para todos los usuarios y grupos que ha especificado, en la hoja **Protección**, compruebe si quiere realizar cambios en las opciones siguientes. Tenga en cuenta que esta configuración, al igual que los permisos, no se aplica al [emisor de Rights Management ni al propietario de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) ni a ningún [superusuario](configure-super-users.md) que haya asignado.
    
    ###### <a name="information-about-the-protection-settings"></a>Información sobre la configuración de protección
    
    |Setting|Más información|Configuración recomendada
    |-----------|--------------------|--------------------|
    |**expiración del contenido**|Defina una fecha o un número de días en los que los usuarios seleccionados no puedan abrir los documentos o correos electrónicos protegidos por dicha configuración. Puede especificar una fecha o un número de días a partir del momento en que se aplicación la protección al contenido.<br /><br />Cuando se especifica una fecha, entra en vigor a medianoche en su zona horaria actual.|**El contenido nunca expira** a menos que el contenido tenga un requisito de límite de tiempo específico.|
    |**Permitir acceso sin conexión**|Use esta configuración para equilibrar los requisitos de seguridad que tiene (incluye el acceso después de la revocación) con la capacidad para que los usuarios seleccionados abran el contenido protegido cuando no tengan una conexión a Internet.<br /><br />Si especifica que el contenido no está disponible sin conexión a Internet o que el contenido está disponible solamente durante un número concreto de días, cuando se supere ese umbral, estos usuarios deberán volver a autenticarse y se registrará su acceso. Cuando esto sucede, si sus credenciales no se han almacenado en la memoria caché, se pedirá a los usuarios que inicien sesión antes de que puedan abrir el documento o correo electrónico.<br /><br />Además de la reautenticación, también se vuelven a evaluar la directiva y la pertenencia a grupos de usuarios. Esto significa que los usuarios podrían experimentar diferentes resultados de acceso para el mismo documento o correo electrónico si se producen cambios en la directiva o la pertenencia al grupo desde la última vez que se accedió al contenido. No podría incluir acceso si se [revocó](../rms-client/client-track-revoke.md) el documento.|Según el grado de confidencialidad del contenido:<br /><br />- **Número de días durante los cuales el contenido está disponible sin conexión a Internet** = **7** para datos empresariales confidenciales que podrían causar daños a la empresa si se comparten con personas no autorizadas. Esta recomendación ofrece un compromiso equilibrado entre flexibilidad y seguridad. Ejemplos: contratos, informes de seguridad, resúmenes de previsiones y datos de cuentas de ventas.<br /><br />- **Nunca** para datos comerciales extremadamente confidenciales que podrían ocasionar daños a la empresa si se compartieran con personas no autorizadas. Esta documentación da propiedad a la seguridad por sobre la flexibilidad y garantiza que si se revoca el documento, inmediatamente se impedirá que los usuarios autorizados abran el documento. Ejemplos: información sobre empleados y clientes, contraseñas, código fuente e informes financieros previamente anunciados.|
    
    Cuando haya terminado de configurar los permisos y ajustes, haga clic en **Aceptar**. 
    
    Esta agrupación de configuraciones crea una plantilla personalizada para el servicio Azure Rights Management. Estas plantillas se pueden usar con aplicaciones y servicios que se integran con Azure Rights Management. Para información sobre cómo los equipos y servicios descargan y actualizan estas plantillas, consulte [Refreshing templates for users and services](refresh-templates.md) (Actualización de plantillas para usuarios y servicios).

8. Si ha seleccionado **Seleccionar una plantilla predefinida** para **Azure (clave en la nube)**, haga clic en el cuadro desplegable y seleccione la [plantilla](../deploy-use/configure-policy-templates.md) que quiera usar para proteger documentos y correos electrónicos con esta etiqueta. No verá las plantillas archivadas o las plantillas que ya estén seleccionadas para otra etiqueta.
    
    Si selecciona una **plantilla de departamento** o si ha configurado los [controles de incorporación](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment):
    
    - Los usuarios que estén fuera del ámbito configurado de la plantilla o que se excluyan al aplicar la protección de Azure Rights Management seguirán viendo la etiqueta, pero no podrán aplicarla. Si seleccionan la etiqueta, verán el mensaje siguiente: **Azure Information Protection no puede aplicar esta etiqueta. Si el problema persiste, póngase en contacto con el administrador.**
        
        Observe que siempre se muestran todas las plantillas publicadas, aunque vaya a configurar una directiva de ámbito. Por ejemplo, va a configurar una directiva de ámbito para el grupo Marketing. Las plantillas que puede seleccionar no se limitan a las plantillas cuyo ámbito sea el grupo Marketing, y es posible seleccionar una plantilla de departamento que los usuarios seleccionados no pueden usar. Para facilitar la configuración y reducir la solución de problemas, puede nombrar la plantilla de departamento de forma que coincida con la etiqueta de la directiva de ámbito. 

9. Si ha seleccionado **HYOK (AD RMS)**, elija **Set AD RMS templates details** (Establecer detalles de plantillas de AD RMS) o **Establecer permisos definidos por el usuario (versión preliminar)**. Después, especifique la URL de licencias del clúster de AD RMS.
    
    Para obtener instrucciones sobre cómo especificar un GUID de plantilla y la dirección URL de administración de licencias, vea [Buscar la información para especificar la protección de AD RMS con una etiqueta de Azure Information Protection](configure-adrms-restrictions.md#locating-the-information-to-specify-ad-rms-protection-with-an-azure-information-protection-label).
    
    La opción de permisos definidos por el usuario permite a los usuarios especificar a quién se le deben conceder permisos y cuáles. Después, puede refinar esta opción y elegir solo Outlook (valor predeterminado), o Word, Excel, PowerPoint y el Explorador de archivos. Esta opción no se admite, de modo que no funcionará al configurar una etiqueta para la [clasificación automática](configure-policy-classification.md).
    
    Si elige la opción para Outlook: la etiqueta se muestra en Outlook y el comportamiento resultante cuando los usuarios aplican la etiqueta es el mismo que el de la opción No reenviar.
    
    Si elige la opción para Word, Excel, PowerPoint y el Explorador de archivos: la etiqueta se muestra en estas aplicaciones. El comportamiento resultante cuando los usuarios aplican la etiqueta consiste en mostrar el cuadro de diálogo para que los usuarios seleccionen permisos personalizados. En este cuadro de diálogo, los usuarios deben especificar los permisos, los usuarios o los grupos y las fechas de expiración. Asegúrese de que los usuarios tengan instrucciones e indicaciones sobre cómo proporcionar estos valores.

10. Haga clic en **Aceptar** para cerrar la hoja **Protección** y ver la elección de **Definido por el usuario** o la plantilla elegida para la opción **Protección** de la hoja **Etiqueta**.

11. En la hoja **Etiqueta**, haga clic en **Guardar**.

12. En la hoja **Azure Information Protection**, use la columna **PROTECCIÓN** para confirmar que la etiqueta muestre la configuración de protección que quiera:
    
    - Una marca de verificación si la protección está configurada. 
    
    - Una marca en forma de x para indicar la cancelación si ha configurado una etiqueta para quitar la protección.
    
    - Un campo en blanco cuando no se haya establecido la protección. 

Al hacer clic en **Guardar**, los cambios están disponibles para los usuarios y servicios. Ya no hay una opción de publicación separada.


## <a name="example-configurations"></a>Configuraciones de ejemplo

Las etiquetas secundarias **Todos los empleados** y **Solo destinatarios** de las etiquetas **Confidencial** y **Extremadamente confidencial** de la [directiva predeterminada](configure-policy-default.md) proporcionan ejemplos de cómo puede configurar las etiquetas que aplican la protección. También puede usar los ejemplos siguientes para configurar la protección para diferentes escenarios. 

En cada uno de los ejemplos siguientes, en la hoja de su \<*nombre de etiqueta*>, seleccione **Proteger** y, a continuación, seleccione **Protección** para abrir la hoja  **Protección**.

### <a name="example-1-label-that-applies-do-not-forward-to-send-a-protected-email-to-a-gmail-account"></a>Ejemplo 1: Etiqueta que aplica No reenviar para enviar un correo electrónico protegido a una cuenta de Gmail

Esta etiqueta solo está disponible en Outlook y es adecuada cuando Exchange Online está configurado para las [nuevas capacidades de cifrado de mensajes de Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Indique a los usuarios que seleccionen esta etiqueta cuando deban enviar un correo electrónico protegido a personas con una cuenta de Gmail (o cualquier otra cuenta de correo electrónico ajena a su organización). 

Los usuarios deben escribir la dirección de correo electrónico de Gmail en el cuadro **Para**.  A continuación, deben seleccionar la etiqueta, y la opción No reenviar se agregará automáticamente al correo electrónico. En este caso, los destinatarios no podrán reenviar el correo electrónico, imprimirlo ni guardarlo con otro nombre, así como tampoco copiar contenido de este ni guardar los datos adjuntos. 

1. En la hoja **Protección**, asegúrese de que **Azure (clave en la nube)** esté seleccionado.
    
2. Seleccione **Establecer permisos definidos por el usuario (versión preliminar)**.

3. Asegúrese de activar la opción **En Outlook, seleccione No reenviar**.

4. Si se selecciona, desactive la opción **En Word, Excel, PowerPoint y el Explorador de archivos, solicite al usuario permisos personalizados**.

5. Haga clic en **Aceptar** en hoja **Protección**.


### <a name="example-2-label-that-restricts-read-only-permission-to-all-users-in-another-organization-and-that-supports-immediate-revocation"></a>Ejemplo 2: Etiqueta que restringe el permiso de solo lectura a todos los usuarios de otra organización y que admite la revocación inmediata

Esta etiqueta es adecuada para compartir documentos altamente confidenciales (solo lectura) que siempre requieren una conexión a Internet para verlos. Si se revoca, los usuarios no podrán ver el documento la próxima vez que intenten abrirlo.

Esta etiqueta no es adecuada para los correos electrónicos.

1. En la hoja **Protección**, asegúrese de que **Azure (clave en la nube)** esté seleccionado.
    
2. Asegúrese de que la opción **Establecer permisos** esté seleccionada y, a continuación, seleccione **Agregar permisos**.

3. En la hoja **Agregar permisos** hoja, seleccione **Escribir detalles**.

4. Escriba el nombre de un dominio de la otra organización, por ejemplo, **fabrikam.com**. Después, seleccione **Agregar**.

5. En **Elección de permisos a partir de valores predeterminados**, seleccione **Visor** y, a continuación, seleccione **Aceptar**.

6. De nuevo en la hoja **Protección**, para la opción **Permitir el acceso sin conexión**, seleccione **Nunca**.

7. Haga clic en **Aceptar** en hoja **Protección**.


### <a name="example-3-add-external-users-to-an-existing-label"></a>Ejemplo 3: Agregar usuarios externos a una etiqueta existente

Los nuevos usuarios que agregue podrán abrir documentos y mensajes de correo electrónico que ya se hayan protegido con esta etiqueta. Los permisos que conceda a estos usuarios pueden ser diferentes de los permisos que tengan los usuarios existentes.

1. En la hoja **Protección**, asegúrese de que **Azure (clave de nube)** esté seleccionado.
    
2. Asegúrese de que **Establecer permisos** esté seleccionado y, a continuación, seleccione **Agregar permisos**.

3. En la hoja **Agregar permisos** hoja, seleccione **Escribir detalles**.

4. Escriba la dirección de correo electrónico del primer usuario (o grupo) para agregar y, a continuación, seleccione **Agregar**.

5. Seleccione los permisos para este usuario (o grupo).

6. Repita los pasos 4 y 5 para cada usuario (o grupo) que quiera agregar a esta etiqueta. A continuación, haga clic en **Aceptar**.

7. En la hoja **Protección**, haga clic en **Aceptar**.

### <a name="example-4-label-for-protected-email-that-supports-less-restrictive-permissions-than-do-not-forward"></a>Ejemplo 4: Etiqueta para correo electrónico protegido que admite permisos menos restrictivos que No reenviar

Esta etiqueta no se puede restringir a Outlook, pero proporciona controles menos restrictivos que utilizar No reenviar. Por ejemplo, en el caso de que los destinatarios puedan copiar desde el correo electrónico o un archivo adjunto, o imprimir y guardar un archivo adjunto.

Si especifica usuarios externos que no tengan ninguna cuenta de Azure AD, asegúrese de indicarles que esta etiqueta no debe usarse para documentos, solo para el correo electrónico. Además, para admitir estos usuarios externos, Exchange Online deben configurarse para las [nuevas capacidades de cifrado de mensajes de Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e).  

> [!NOTE]
> Exchange Online está desplegando una nueva opción, [Solo cifrar](configure-usage-rights.md#encrypt-only-option-for-emails). Esta opción no está disponible para la configuración de etiquetas. Pero puede usar este ejemplo para configurar una etiqueta con el mismo conjunto de derechos de uso.

Cuando los usuarios especifican las direcciones de correo electrónico en el cuadro **Para**, las direcciones deben ser de los mismos usuarios que especifique para la configuración de esta etiqueta. Dado que los usuarios pueden pertenecer a grupos y tener más de una dirección de correo electrónico, no es necesario que la que indiquen coincida con la que usted especifique para los permisos. Sin embargo, se trata de la manera más sencilla de asegurarse de que el destinatario quede correctamente autorizado. Para obtener más información sobre cómo se autorizan los permisos para los usuarios, consulte [Preparación de usuarios y grupos para Azure Information Protection](../plan-design/prepare.md). 

1. En la hoja **Protección**, asegúrese de que **Azure (clave en la nube)** esté seleccionado.
    
2. Asegúrese de que **Establecer permisos** esté seleccionado y seleccione **Agregar permisos**.

3. En la hoja **Agregar permisos**: para conceder permisos a los usuarios de su organización, seleccione **Agregar \<nombre de la organización > - Todos los miembros** para seleccionar a todos los usuarios de su inquilino. Este parámetro excluye las cuentas de invitado. O bien, seleccione **Examinar directorio** para seleccionar un grupo específico. Para conceder permisos a usuarios externos, o bien si prefiere escribir la dirección de correo electrónico, seleccione **Escribir detalles** y escriba la dirección de correo electrónico del usuario, o bien un grupo de Azure AD o un nombre de dominio.
    
    Repita este paso para especificar usuarios adicionales que deban tener los mismos permisos.

4. Para **Elección de permisos a partir de valores predeterminados**, seleccione **Copropietario**, **Coautor**, **Revisor** o **Personalizado** para seleccionar los permisos que quiera conceder.
    
    Nota: No seleccione **Visor** para mensajes de correo electrónico y, si selecciona **Personalizado**, asegúrese de incluir **Editar y guardar**.
    
    Para seleccionar los mismos permisos que coincidan con la nueva opción **Solo cifrar** de Exchange Online, seleccione **Personalizado**. Después, seleccione todos los permisos excepto **Guardar como, exportar (EXPORT)** y **Control total (OWNER)**.

5. Para especificar usuarios adicionales que deban tener permisos diferentes, repita los pasos 3 y 4.

6. Haga clic en **Aceptar** en la hoja **Agregar permisos**.

7. En la hoja **Protección**, haga clic en **Aceptar**.

## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]