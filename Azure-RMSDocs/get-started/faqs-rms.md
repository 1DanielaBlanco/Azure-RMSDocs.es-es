---
title: "Preguntas más frecuentes sobre Azure RMS: AIP"
description: "Algunas de las preguntas más frecuentes sobre el servicio de protección de datos, Azure Rights Management (Azure RMS), de Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/08/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.custom: askipteam
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 776293c73b5ca63d0bfd409d8330bfe8295c792e
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Preguntas más frecuentes sobre la protección de datos en Azure Information Protection

>*Válido para: Azure Information Protection, Office 365*

¿Alguna pregunta sobre el servicio de protección de datos, Azure Rights Management (Azure RMS), de Azure Information Protection? Compruebe si se ha resuelto aquí. 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>¿Deben estar los archivos en la nube para que estén protegidos con Azure Rights Management?
No, se trata de una idea equivocada habitual. Azure Rights Management Service (y Microsoft) no ve ni almacena sus datos como parte del proceso de protección de la información. La información que protege nunca se envía a Azure ni se almacena allí, a menos que la almacene explícitamente en Azure o use otro servicio en la nube que lo haga. 

Para más información, consulte [¿Cómo funciona Azure RMS? En segundo plano](../understand-explore/how-does-it-work.md) para entender cómo Azure Rights Management Service protege una fórmula de refresco de cola secreta que se crea, se almacena y se mantiene en local.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>¿Cuál es la diferencia entre el cifrado de Azure Rights Management y el de otros servicios en la nube de Microsoft?

Microsoft proporciona varias tecnologías de cifrado que permiten proteger los datos en escenarios diferentes y a menudo complementarios. Por ejemplo, mientras que Office 365 ofrece cifrado en reposo para los datos almacenados en Office 365, Azure Rights Management Service de Azure Information Protection cifra los datos de manera individual para que estén protegidos independientemente de dónde se encuentren o cómo se transmitan.

Estas tecnologías de cifrado son complementarias y es necesario habilitarlas y configurarlas independientemente para usarlas. Para ello, tendrá la opción de aportar su propia clave de cifrado, un escenario que también se denomina "BYOK". La habilitación de BYOK para una de estas tecnologías no afecta a las demás. Por ejemplo, puede usar BYOK para Azure Information Protection y no con otras tecnologías de cifrado, y viceversa. Las claves que utilizan estas distintas tecnologías pueden ser las mismas o diferentes, dependiendo de cómo configure las opciones de cifrado de cada servicio.

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>¿Cuál es la diferencia entre BYOK y HYOK y cuándo debo utilizarlos?

**Bring your own key** (BYOK) en el contexto de Azure Information Protection, sirve para crear su propia clave local para la protección con Azure Rights Management. A continuación, esa clave se transfiere a un módulo de seguridad de hardware (HSM) de Azure Key Vault, donde aún poseerá y administrará su clave. Si no hizo esto, protección de Azure Rights Management usaría una clave que creada y administrada automáticamente en Azure. Esta configuración predeterminada se conoce a como "administrada por Microsoft" en lugar de "administrada por el cliente" (la opción de BYOK).

Para más información acerca de BYOK y si debería elegir esta topología de clave para su organización, consulte [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

**Hold your own key** (HYOK) en el contexto de Azure Information Protection, está diseñado para algunas organizaciones que tienen un subconjunto de documentos o correos electrónicos que no se pueden proteger mediante una clave almacenada en la nube. Para estas organizaciones, esta restricción se aplica incluso si la clave se creó y se administró mediante BYOK. A menudo, la restricción puede deberse a motivos legales o de cumplimiento y la configuración de HYOK se debe aplicar únicamente a la información "ultrasecreta", que nunca se comparta fuera de la organización, que solo se consuma en la red interna y que no requiera el acceso desde dispositivos móviles. 

Para estas excepciones (normalmente menos del 10 % del contenido que necesita protección), las organizaciones pueden usar una solución local, Active Directory Rights Management Services, para crear la clave que permanece en local. Con esta solución, los equipos obtienen su directiva de Azure Information Protection de la nube, pero se puede proteger este contenido específico mediante la clave local.

Para más información acerca de HYOK, para asegurarse de que comprende sus limitaciones y restricciones y para instrucciones de cuándo usarlo, consulte [Requisitos y restricciones de Hold your own key (HYOK) para la protección de AD RMS](../deploy-use/configure-adrms-restrictions.md).

## <a name="can-i-now-use-byok-with-exchange-online"></a>¿Puedo usar ahora BYOK con Exchange Online?

Sí, ahora puede usar BYOK con Exchange Online al seguir las instrucciones de [Configuración de nuevas funcionalidades de cifrado de mensajes de Office 365 a partir de Azure Information Protection](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e). Estas instrucciones habilitan las nuevas funcionalidades de Exchange Online que admiten BYOK de Azure Information Protection, así como el nuevo cifrado de mensajes de Office 365.

Para más información acerca de este cambio, consulte el anuncio del blog sobre el [cifrado de mensajes de Office 365 con las nuevas funcionalidades](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801).

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>¿Dónde puedo encontrar información acerca de las soluciones de terceros que se integran con Azure RMS?

Muchos proveedores de software ya tienen soluciones que se integran con Azure Rights Management (o están implementándolas), y la lista crece rápidamente. Le resultará útil comprobar la lista de [Soluciones habilitadas para RMS](requirements-applications.md#rms-enlightened-solutions) y conocer las últimas actualizaciones de [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) en Twitter. Compruebe también la [guía del desarrollador](../develop/developers-guide.md) y publique las preguntas de integración específicas en el [sitio de Yammer](https://www.yammer.com/AskIPTeam) de Azure Information Protection.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>¿Hay un módulo de administración o mecanismo de supervisión similar para el conector RMS?

Aunque el conector de Rights Management registra información, advertencias y mensajes de error en el registro de eventos, no hay un módulo de administración que incluya la supervisión de estos eventos. Sin embargo, la lista de eventos y sus descripciones, con más información para ayudarle a tomar acciones correctivas se documenta en [Supervisión del conector de Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>Tengo que ser administrador global para configurar Azure RMS o puedo delegar en otros administradores?

Los administradores globales de un inquilino de Office 365 o de Azure AD obviamente pueden ejecutar todas las tareas administrativas de Azure Rights Management Service. Sin embargo, si desea asignar permisos administrativos a otros usuarios, puede hacerlo mediante el cmdlet de PowerShell de Azure RMS, [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Puede asignar este rol administrativo por cuenta de usuario o por grupo. Hay dos roles disponibles: **administrador global** y **administrador del conector**. 

Como estos nombres de rol sugieren, el primero concede permisos para ejecutar todas las tareas administrativas de Azure Rights Management (sin crear un administrador global para otros servicios de nube) y el segundo concede permisos para ejecutar el conector de Rights Management (RMS).

Cosas que tener en cuenta:

- Solo los administradores globales de Office 365 y los de Azure AD pueden usar el centro de administración de Office 365 para configurar Azure RMS. Si para Azure Information Protection utiliza Azure Portal, puede iniciar sesión como administrador global o como administrador de seguridad.

- Los usuarios a quienes asigne el rol de administrador global para Azure RMS deben usar comandos de PowerShell de Azure RMS para configurarlo. Para ayudarle a encontrar los cmdlets adecuados para tareas específicas, consulte [Administración de Azure Rights Management Service mediante Windows PowerShell](../deploy-use/administer-powershell.md).

- Si ha configurado [controles de incorporación](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), esta configuración no afecta a la capacidad de administrar Azure RMS, excepto al conector RMS. Por ejemplo, si ha configurado controles de incorporación de modo que la capacidad de proteger el contenido se limite al grupo "Departamento de TI", la cuenta que utilice para instalar y configurar el conector RMS debe pertenecer a ese grupo. 

- Ningún administrador de Azure RMS (por ejemplo, un administrador global del inquilino o uno de Azure RMS) puede quitar automáticamente la protección de documentos o correos electrónicos que estuvieran protegidos con Azure RMS. Solo los usuarios asignados como superusuarios para Azure RMS pueden hacer esto, siempre que la característica de superusuario esté habilitada. Sin embargo, el administrador global del inquilino y cualquier administrador global de Azure RMS pueden asignar superusuarios a los usuarios, incluida su propia cuenta. También pueden habilitar la característica de superusuario. Estas acciones se graban en el registro del administrador de Azure RMS. Para más información, consulte la sección de procedimientos recomendados de seguridad [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md). 

>[!NOTE]
> Las plantillas y nuevas opciones para configurar la protección de Azure Rights Management se han movido a Azure Portal, que es compatible con los administradores de seguridad además de con el acceso de administrador global. 

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>¿Cómo se crea una plantilla personalizada en Azure Portal?

Las plantillas personalizadas se han movido a Azure Portal, donde puede seguir administrándolas como plantillas o convertirlos a etiquetas. Para crear una plantilla, cree una nueva etiqueta y configure las opciones de protección de datos de Azure RMS. En segundo planto, esto crea una plantilla que a la que pueden acceder servicios y aplicaciones que se integren con las plantillas de Rights Management.

Para más información acerca de las plantillas de Azure Portal, consulte [Configuración y administración de plantillas para Azure Information Protection](../deploy-use/configure-policy-templates.md).

## <a name="ive-protected-a-document-and-now-want-to-change-the-usage-rights-or-add-usersdo-i-need-to-reprotect-the-document"></a>He protegido un documento y ahora quiero cambiar los derechos de uso o agregar usuarios, ¿es necesario volver a proteger el documento?

Si el documento está protegido mediante una etiqueta o una plantilla, no es necesario volver a protegerlo. Modifique la etiqueta o la plantilla con los cambios en los derechos de uso o agregue nuevos grupos (o usuarios), guarde los cambios y publíquelos:

- Si el usuario no ha accedido al documento antes de los cambios, estos surten efecto en cuanto el usuario abra el documento. 

- Si el usuario ya ha accedido el documento, estos cambios surten efecto cuando su [licencia de uso](../deploy-use/configure-usage-rights.md#rights-management-use-license) expira. Vuelva a proteger el documento solo si no puede esperar a que la licencia de uso expire. Al volver a proteger de forma eficaz, se crea una nueva versión del documento y, por lo tanto, una nueva licencia de uso para el usuario.

O bien, si ya ha configurado un grupo con los permisos necesarios, puede cambiar la pertenencia al grupo para incluir o excluir usuarios y no es necesario para cambiar la etiqueta o la plantilla. Los cambios pueden tardar un poco en surtir efecto, porque Azure Rights Management Service almacena la pertenencia a grupos [en caché](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection).

Si el documento se ha protegido mediante permisos personalizados, no se pueden cambiar para el documento existente. Debe proteger el documento de nuevo y especificar todos los usuarios y todos los derechos de uso necesarios para la nueva versión del documento. Para volver a proteger un documento protegido, debe tener el derecho de uso Control total.

Sugerencia: Para comprobar si un documento estaba protegido con una plantilla o mediante permisos personalizados, use el cmdlet [Get-AIPFileStatus](/powershell/module/azureinformationprotection/get-aipfilestatus) de PowerShell. Siempre se ve una descripción de la plantilla de **acceso restringido** para los permisos personalizados, con un identificador de plantilla único que no se muestra al ejecutar [Get-RMSTemplate](/powershell/module/azureinformationprotection/get-rmstemplate).

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>Tengo una implementación híbrida de Exchange con unos usuarios de Exchange Online y otros de Exchange Server, ¿es esto compatible con Azure RMS?
Sin duda y lo mejor es que los usuarios podrán proteger y consumir correos electrónicos protegidos, así como los datos adjuntos, en las dos implementaciones de Exchange perfectamente. Para esta configuración, [active Azure RMS](../deploy-use/activate-service.md) y [habilite IRM para Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx), a continuación, [implemente y configure el conector RMS](../deploy-use/deploy-rms-connector.md) para Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>Si uso esta protección para el entorno de producción, ¿queda mi empresa bloqueada en la solución o puede perder el acceso al contenido que se proteja con Azure RMS?
No, siempre tendrá control de los datos y puede acceder a ellos, aunque decida dejar de utilizar Azure Rights Management Service. Para más información, consulte [Retirada y desactivación de la protección de Azure Information Protection](../deploy-use/decommission-deactivate.md).

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>¿Puedo controlar cuáles de mis usuarios pueden usar Azure RMS para proteger contenido?
Sí, Azure Rights Management Service tiene controles de incorporación de usuario para este escenario. Para más información, consulte la sección [Configuración de controles de incorporación para una implementación por fases](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) del artículo [Activar Azure Rights Management](../deploy-use/activate-service.md).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>¿Se puede impedir que los usuarios compartan documentos protegidos con organizaciones específicas?
Una de las mayores ventajas de usar Azure Rights Management Service para la protección de datos es que admite la colaboración interempresarial sin tener que configurar relaciones de confianza explícitas para cada organización asociada, ya que Azure AD se encarga de la autenticación.

No hay ninguna opción de administración para impedir que los usuarios compartan documentos con organizaciones específicas de forma segura. Por ejemplo, desea bloquear una organización en la que no confía o que tiene una empresa de la competencia. Impedir que Azure Rights Management Service envíe documentos protegidos a los usuarios de estas organizaciones no tendría sentido, ya que compartirían los documentos sin protección, que probablemente sería lo menos deseable en este escenario. Por ejemplo, no podría identificar quién comparte documentos empresariales confidenciales con qué usuarios de estas organizaciones, lo cual permite la protección de documentos (o correos electrónicos) del servicio de Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Cuando comparto un documento protegido con una persona ajena a la organización, ¿cómo se autentica ese usuario?

De forma predeterminada, Azure Rights Management Service usa una cuenta de Azure Active Directory y una dirección de correo electrónico asociada para la autenticación de usuario, lo que facilita enormemente la colaboración interempresarial para los administradores. Si la otra organización usa servicios de Azure, los usuarios ya tendrán cuentas de Azure Active Directory, aunque se creen y se administren localmente y después se sincronicen con Azure. Si la organización tiene Office 365, en segundo plano, este servicio también usa Azure Active Directory para las cuentas de usuario. Si la organización del usuario no tiene cuentas administradas en Azure, los usuarios pueden suscribirse a [RMS para individuos](../understand-explore/rms-for-individuals.md), que crea un inquilino de Azure no administrado y un directorio para la organización con una cuenta para el usuario, de manera que este (y los usuarios posteriores) se pueda autenticar en Azure Rights Management Service.

El método de autenticación para estas cuentas puede variar en función de la configuración de las cuentas de Azure Active Directory del administrador de la otra organización. Por ejemplo, podrían usar contraseñas creadas para estas cuentas, la autenticación multifactor (MFA), la federación o contraseñas creadas en Active Directory Domain Services que después se sincronizaran con Azure Active Directory.

Si protege un correo electrónico con un documento adjunto de Office a un usuario sin cuenta de Azure AD, el método de autenticación cambia. Azure Rights Management Service está federado con algunos proveedores de identidades sociales populares, como Gmail. Si se admite el proveedor de correo electrónico del usuario, este último puede iniciar sesión ese servicio y su proveedor de correo electrónico le autenticará. Si no se admite el proveedor de correo electrónico del usuario o si el usuario lo prefiere, puede solicitar un código de acceso de un solo uso que le autentique y muestre el correo electrónico con el documento protegido en un explorador web.

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>¿Puedo agregar usuarios externos (personas ajenas a mi empresa) a las plantillas personalizadas?

Sí. La [configuración de protección](../deploy-use/configure-policy-protection.md) de Azure Portal permite agregar permisos a usuarios y grupos ajenos a la organización e incluso a todos los usuarios de otra organización. A menos que la plantilla se vaya a utilizar exclusivamente para el envío de correo electrónico mediante las [nuevas funcionalidades de cifrado de mensajes de Office 365](https://support.office.com/article/7ff0c040-b25c-4378-9904-b1b50210d00e), no agregue cuentas de identidades sociales (como Gmail y Microsoft) u otras cuentas que no estén en Azure AD.

Tenga en cuenta que si tiene etiquetas de Azure Information Protection, primero debe convertir la plantilla personalizada a una etiqueta para configurar estas opciones de protección en Azure Portal. Para más información, consulte [Configuración y administración de plantillas para Azure Information Protection](../deploy-use/configure-policy-templates.md).

Como alternativa, puede agregar usuarios externos a las plantillas personalizadas (y a las etiquetas) mediante PowerShell. Esta configuración requiere un objeto de definición de derechos para actualizar la plantilla:

1. Especifique las direcciones de correo electrónico externas y sus derechos en un objeto de definición de derechos mediante el cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) para crear una variable.

2. Proporcione esta variable al parámetro RightsDefinition con el cmdlet [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty).
    
    Al agregar usuarios a una plantilla existente, debe definir objetos de definición de derechos para los usuarios existentes en las plantillas, además de para los nuevos usuarios. En este escenario, puede resultarle útil **Example 3: Add new users and rights to a custom template** (Ejemplo 3: Incorporación de usuarios nuevos y derechos a una plantilla personalizada) de la sección [Examples](/powershell/module/aadrm/set-aadrmtemplateproperty#examples) (Ejemplos) del cmdlet. 

## <a name="what-type-of-groups-can-i-use-with-azure-rms"></a>¿Qué tipo de grupos puedo usar con Azure RMS?
Para la mayoría de los escenarios, puede utilizar cualquier tipo de grupo con dirección de correo electrónico en Azure AD. Esta regla general siempre se aplica al asignar derechos de uso, pero existen algunas excepciones para la administración de Azure Rights Management Service. Para más información, consulte [Requisitos de Azure Information Protection para cuentas de grupo](../plan-design/prepare.md#azure-information-protection-requirements-for-group-accounts).

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>¿Cómo se envía un correo electrónico protegido a una cuenta de Gmail o Hotmail?

Al usar Exchange Online y Azure Rights Management Service, simplemente envía el correo electrónico al usuario como mensaje protegido. Por ejemplo, puede seleccionar el nuevo botón **Proteger** de la barra de comandos de Outlook en la web, use el botón **No reenviar** de Outlook o la opción del menú. O bien, puede seleccionar una etiqueta de Azure Information Protection que aplique automáticamente la acción de No reenviar clasifique el correo electrónico. 

El destinatario verá una opción para iniciar sesión en su cuenta de Gmail, Yahoo o Microsoft y tendrá permiso para leer el correo electrónico protegido. También puede elegir el código de acceso de un solo uso para leer el correo electrónico en un explorador.

Para admitir este escenario, Exchange Online debe habilitarse para Azure Rights Management Service y las nuevas funcionalidades de cifrado de mensajes de Office 365. Para más información acerca de esta configuración, consulte [Exchange Online: Configuración de IRM](../deploy-use/configure-office365.md#exchange-online-irm-configuration).

Para más información acerca de las nuevas funcionalidades que incluyen la compatibilidad con todas las cuentas de correo electrónico en todos los dispositivos, consulte la siguiente entrada de blog: [Announcing new capabilities available in Office 365 Message Encryption](https://techcommunity.microsoft.com/t5/Security-Privacy-and-Compliance/Email-Encryption-and-Rights-Protection/ba-p/110801) (Anuncio de las nuevas funcionalidades disponibles para el cifrado de mensajes de Office 365).

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>¿Qué dispositivos y qué tipos de archivos son compatibles con Azure RMS?
Para una lista de los dispositivos compatibles con Azure Rights Management Service, consulte [Dispositivos cliente que son compatibles con la protección de datos de Azure Rights Management](../get-started/requirements-client-devices.md). Como no todos los dispositivos compatibles admiten actualmente todas las funcionalidades de Rights Management, asegúrese de comprobar también la tabla de [aplicaciones habilitadas para RMS](../get-started/requirements-applications.md#rms-enlightened-applications).

Azure Rights Management Service admite todos los tipos de archivo. Para los archivos de texto, de imagen, de Microsoft Office (Word, Excel, PowerPoint), .pdf y otros tipos de archivo de aplicación, Azure Rights Management proporciona protección nativa que incluye cifrado y cumplimiento de derechos (permisos). Para todas las demás aplicaciones y tipos de archivo, la protección genérica proporciona encapsulación de archivos y autenticación para comprobar si el usuario está autorizado para abrir el archivo.

Para una lista de las extensiones de nombre de archivo que se admiten de forma nativa en Azure Rights Management, consulte [Tipos de archivos compatibles con el cliente de Azure Information Protection](../rms-client/client-admin-guide-file-types.md). Las extensiones de nombre de archivo que no aparecen se admiten con el cliente de Azure Information Protection, que aplica automáticamente la protección genérica a estos archivos.

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>¿Cómo configuro un equipo Mac para proteger documentos y realizar su seguimiento?

En primer lugar, asegúrese de que ha instalado Office para Mac mediante el vínculo de instalación de software de https://portal.office.com. Para más información, consulte [Descargar e instalar o volver a instalar Office 365 u Office 2016 en su equipo PC o Mac](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Abra Outlook y cree un perfil desde su cuenta profesional o educativa de Office 365. A continuación, cree un nuevo mensaje y realice lo siguiente para configurar Office de manera que proteja los documentos y los correos electrónicos mediante Azure Rights Management Service:

1. En el nuevo mensaje, en la pestaña **Opciones**, haga clic en **Permisos** y en **Comprobar credenciales**.

2. Cuando se le solicite, especifique los detalles de la cuenta profesional o educativa de Office 365 de nuevo y seleccione **Iniciar sesión**. 
    
    Así se descargarán las plantillas de Azure Rights Management y **Comprobar credenciales** se sustituirá por opciones que incluyen **Sin restricciones**, **No reenviar** y las plantillas de Azure Rights Management publicadas para el inquilino. Ahora puede cancelar el mensaje nuevo.

Para proteger un mensaje de correo electrónico o un documento: en la pestaña **Opciones**, haga clic en **Permisos** y elija una opción o plantilla que proteja el correo electrónico o el documento.

Para realizar el seguimiento de un documento una vez protegido: desde un equipo Windows con el cliente de Azure Information Protection instalado, registre el documento en el sitio de seguimiento de documentos mediante una aplicación de Office o el Explorador de archivos. Para instrucciones, consulte el artículo sobre [seguimiento y revocación de documentos](../rms-client/client-track-revoke.md). Desde el equipo Mac, ahora puede usar el explorador web para ir al sitio de seguimiento de documentos (https://track.azurerms.com) para el seguimiento y la revocación de este documento.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Al abrir un documento de Office protegido con RMS, ¿se protege también con RMS el archivo temporal asociado?
No. En este escenario, el archivo temporal asociado no contiene datos del documento original, solo lo que escribe el usuario con el archivo abierto. A diferencia del archivo original, el temporal obviamente no está diseñado para su uso compartido y se conservará en el dispositivo, protegido mediante controles de seguridad locales, como BitLocker y EFS.

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Una característica que me interesa no funciona con las bibliotecas protegidas de SharePoint, ¿se planea la compatibilidad con esta característica?
Actualmente, SharePoint admite documentos protegidos con RMS mediante las bibliotecas protegidas con IRM, que no admiten plantillas de Rights Management, el seguimiento de documentos y otras funcionalidades. Para más información, consulte la sección [SharePoint Online y SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) del artículo de [servicios y aplicaciones de Office](../understand-explore/office-apps-services-support.md).

Si está interesado en una funcionalidad específica que todavía no se admite, no pierda de vista los anuncios del [blog de seguridad y movilidad empresarial](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>¿Cómo se configura OneDrive para la Empresa en SharePoint Online de manera que los usuarios puedan compartir con seguridad sus archivos con personas de la empresa y ajenas?
De forma predeterminada, el administrador de Office 365 no configura esto; lo hacen los usuarios.

Igual que un administrador del sitio de SharePoint habilita y configura IRM para una biblioteca de SharePoint que le pertenece, OneDrive para la Empresa está diseñado para que los usuarios habiliten y configuren IRM para su propia biblioteca de OneDrive para la Empresa. Sin embargo, mediante PowerShell, puede hacerlo por ellos. Para instrucciones, consulte la sección [SharePoint Online y OneDrive para la Empresa: Configuración de IRM](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) del artículo [Office 365: configuración para clientes y servicios en línea que usan Azure Rights Management Service](../deploy-use/configure-office365.md).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>¿Existen trucos o sugerencias para la implementación?

Después de supervisar muchas implementaciones y escuchar a nuestros clientes, asociados, asesores e ingenieros de soporte, una de las mayores sugerencias que podemos dar por experiencia es **diseñar e implementar directivas sencillas**.

Dado que Azure Information Protection admite el uso compartido seguro con cualquiera, puede permitirse ser ambicioso con el alcance de la protección de datos. Pero sea conservador al configurar las restricciones para los derechos de uso. Para muchas organizaciones, el mayor impacto comercial se centra en evitar las pérdidas de datos mediante la restricción del acceso a las personas de la organización. Obviamente, puede hacerlo mucho más pormenorizado si es necesario: evitar que los usuarios impriman, editen, etc. Pero mantenga las restricciones más pormenorizadas como una excepción para los documentos que realmente necesiten un alto nivel de seguridad y no implemente estos derechos de uso más restrictivos desde el primer día; planifique un enfoque más escalonado.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>¿Cómo recupero el acceso a los archivos que estaban protegidos por un empleado que ha dejado la organización?
Use la [característica de superusuario](../deploy-use/configure-super-users.md), que concede derechos de uso de Control total a los usuarios autorizados para todos los documentos y correos electrónicos protegidos por el inquilino. Los superusuarios siempre pueden leer este contenido protegido y, si es necesario, quitar la protección o volver a protegerlo para distintos usuarios. Esta misma característica permite que los servicios autorizados indexen e inspeccionen archivos, según proceda.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Cuando pruebo la revocación en el sitio de seguimiento de documentos, veo un mensaje que indica que el acceso al documento sigue permitido durante 30 días, ¿se puede configurar este plazo?

Sí. Este mensaje se refleja la [licencia de uso](../deploy-use/configure-usage-rights.md#rights-management-use-license) de ese archivo en concreto. 

Si se revoca un archivo, se puede aplicar esa acción únicamente cuando el usuario se autentica en Azure Rights Management Service. Por lo tanto, si un archivo tiene un período de validez de la licencia de uso de 30 días y el usuario ya ha abierto el documento, seguirá teniendo acceso al documento durante la vigencia de la licencia de uso. Cuando la licencia de uso expire, el usuario deberá repetir la autenticación, momento en el cual al usuario se le deniega el acceso, ya que se ha revocado el documento.

El usuario que ha protegido el documento, el [emisor de Rights Management](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) está exento de esta revocación y puede acceder a sus documentos siempre. 

El período de validez predeterminado de la licencia de uso de un inquilino es 30 días; este valor puede reemplazarse por una configuración más restrictiva en una etiqueta o una plantilla. Para más información acerca de la licencia de uso y cómo configurarla, consulte la documentación [Licencia de uso de Rights Management](../deploy-use/configure-usage-rights.md#rights-management-use-license).

## <a name="can-rights-management-prevent-screen-captures"></a>¿Puede Rights Management impedir las capturas de pantalla?
Al no conceder el [derecho de uso](../deploy-use/configure-usage-rights.md) **Copiar**, Rights Management puede impedir las capturas de pantalla de muchas de las herramientas de captura de pantalla que se utilizan habitualmente en las plataformas Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) y Android. Sin embargo, los dispositivos iOS y Mac no permiten que ninguna aplicación impida las capturas de pantalla y los navegadores (por ejemplo, cuando se usa con Outlook Web App y Office Online) tampoco pueden impedirlas.

Impedir las capturas de pantalla puede ayudar a evitar la divulgación accidental o por negligencia de información confidencial o delicada. Pero hay muchas maneras en que los usuarios pueden compartir los datos que se muestran en una pantalla, hacer una captura de pantalla es solo una de ellas. Por ejemplo, un usuario decidido a compartir la información mostrada puede tomar una foto con el teléfono con cámara, volver a escribir los datos o simplemente transmitírselos verbalmente a alguien.

Como demuestran estos ejemplos, aunque todas las plataformas y el software permitieran las API de Rights Management de bloqueo de las capturas de pantalla, la tecnología por sí sola no siempre puede evitar que los usuarios compartan datos que no deberían. Rights Management puede ayudar a proteger sus datos importantes mediante directivas de uso y autorización, pero esta solución de administración de derechos empresariales debe utilizarse con otros controles. Por ejemplo, puede implementar seguridad física, prestar atención y supervisar a aquellas personas con acceso autorizado a los datos de la organización e invertir en la educación de los usuarios para que conozcan los datos que no deben compartir.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>¿Cuál es la diferencia entre un usuario que protege un correo electrónico con No reenviar y una plantilla que no incluye el derecho Reenviar?

A pesar de su nombre y apariencia, **No reenviar** no es lo contrario del derecho Reenviar o una plantilla. En realidad es un conjunto de derechos que incluyen la restricción de copiar, imprimir y guardar datos adjuntos, y que limita el reenvío de mensajes de correo electrónico. Los derechos se aplican dinámicamente a los usuarios a través de los destinatarios elegidos y no los asigna estáticamente el administrador. Para más información, consulte la sección [Opción No reenviar para correos electrónicos](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) de [Configuración de los derechos de uso para Azure Rights Management](../deploy-use/configure-usage-rights.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


