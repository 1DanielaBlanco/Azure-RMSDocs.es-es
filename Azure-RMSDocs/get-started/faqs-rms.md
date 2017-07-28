---
title: "Preguntas más frecuentes de Azure RMS - AIP"
description: "Algunas de las preguntas más frecuentes sobre el servicio de protección de datos, Azure Rights Management (Azure RMS), desde Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/13/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 90df11c5-355c-4ae6-a762-351b05d0fbed
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: a73dcc5e2a38c5874361f0fc2845229f505b2d3e
ms.sourcegitcommit: 7bec3dfe3ce61793a33d53691046c5b2bdba3fb9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/27/2017
---
# <a name="frequently-asked-questions-about-data-protection-in-azure-information-protection"></a>Preguntas más frecuentes sobre la protección de datos en Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿Tiene alguna pregunta sobre el servicio de protección de datos, Azure Rights Management, desde Azure Information Protection? Vea si se ha resuelto aquí. 

## <a name="do-files-have-to-be-in-the-cloud-to-be-protected-by-azure-rights-management"></a>¿Deben los archivos estar en la nube para tener la protección de Azure Rights Management?
No, se trata de una idea equivocada frecuente. El servicio de Rights Management (y Microsoft) no ve ni almacena sus datos como parte del proceso de protección de la información. La información que protege nunca se envía a Azure, ni se almacena allí, a menos que la almacene de manera explícita en Azure o use otro servicio en la nube que la almacene en Azure. 

Para obtener más información, consulte [How does Azure RMS work? En segundo plano](../understand-explore/how-does-it-work.md) para entender cómo una fórmula de la cola secreta que se crea y almacena localmente tiene la protección del servicio Azure Rights Management sin dejar de ser local.

## <a name="whats-the-difference-between-azure-rights-management-encryption-and-encryption-in-other-microsoft-cloud-services"></a>¿Cuál es la diferencia entre el cifrado de Azure Rights Management y el de otros servicios de la nube de Microsoft?

Microsoft proporciona varias tecnologías de cifrado que le permiten proteger los datos en situaciones diferentes y, a menudo, complementarias. Por ejemplo, mientras que Office 365 ofrece cifrado en reposo para datos almacenados en Office 365, el servicio de Azure Rights Management de Azure Information Protection cifra de modo independiente los datos, de tal forma que quedan protegidos independientemente de dónde se encuentren o cómo se transmitan.

Estas tecnologías de cifrado son complementarias y su uso requiere la habilitación y configuración de forma independiente. En dicho caso, para el cifrado podrá crear su propia clave (acción denominada como "BYOK"). La habilitación de BYOK para una de estas tecnologías no afecta a las demás. Por ejemplo, puede usar BYOK para Azure Information Protection y no usar BYOK para otras tecnologías de cifrado, y viceversa. Las claves utilizadas por estas tecnologías distintas pueden ser las mismas o diferentes, dependiendo de cómo configure las opciones de cifrado para cada servicio.

## <a name="whats-the-difference-between-byok-and-hyok-and-when-should-i-use-them"></a>¿Cuál es la diferencia entre Bring your own key (BYOK, Traiga su propia clave) y Hold your own key (HYOK, Mantenga su propia clave) y cuándo debería usar cada opción?

El sistema **Bring Your Own Key** (BYOK, Traiga su propia clave) en el contexto de Azure Information Protection se da cuando el usuario crea su propia clave local para la protección de Azure Rights Management. A continuación, esa clave se transfiere a un módulo de seguridad de hardware (HSM) en Azure Key Vault, donde el usuario sigue siendo el propietario de la clave y se ocupa de su administración. Si no se completó este proceso, la protección de Azure Rights Management usará una clave que se crea y se administra automáticamente en Azure. Esta configuración predeterminada se conoce como "administrada por Microsoft" en lugar de "administrada por el cliente" (la opción BYOK).

Para obtener más información acerca de BYOK y determinar si debe elegir esta topología de clave para su organización, consulte [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md). 

El sistema **Hold your own key** (HYOK, Mantenga su propia clave) en el contexto de Azure Information Protection está destinado a pocas organizaciones que tienen un subconjunto de documentos o mensajes de correo electrónico que no se pueden proteger mediante una clave almacenada en la nube. Para estas organizaciones, esta restricción se aplica incluso si se creó y la clave y se administró mediante el sistema BYOK. La restricción puede deberse a menudo a motivos legales o normativos, y la configuración de HYOK se debe aplicar solo a información que tenga la clasificación de confidencialidad más alta ("ultrasecreto"), nunca se vaya a compartir fuera de la organización, solo se vaya a usar en la red interna y no tenga que ser accesible desde dispositivos móviles. 

Para estas excepciones (que normalmente suponen menos de 10 % de todo el contenido que requiere protección), las organizaciones pueden usar una solución local, Active Directory Rights Management Services, para crear la clave que se mantiene en el entorno local. Con esta solución, los equipos obtienen su directiva de Azure Information Protection de la nube, pero este contenido identificado puede protegerse mediante la clave local.

Para consultar más información acerca de HYOK y revisar sus limitaciones y restricciones, además de obtener orientaciones sobre cuándo usar esta opción, consulte [Requisitos y restricciones de Mantenga su propia clave (HYOK) para la protección de AD RMS](../deploy-use/configure-adrms-restrictions.md).

## <a name="where-can-i-find-information-about-third-party-solutions-that-integrate-with-azure-rms"></a>¿Dónde puedo encontrar información sobre las soluciones de terceros que se integran con Azure RMS?

Muchos proveedores de software ya tienen soluciones o están implementando soluciones que se integran con Azure Rights Management y la lista está creciendo rápidamente. Puede resultarle útil consultar la lista de [soluciones habilitadas para RMS](requirements-applications.md#rms-enlightened-solutions) y obtener las actualizaciones más recientes de [Dan Plastina @TheRMSGuy](https://twitter.com/TheRMSGuy) en Twitter. En cambio, si tiene una pregunta específica, envíe un mensaje de correo al equipo de Information Protection: askipteam@microsoft.com.

## <a name="is-there-a-management-pack-or-similar-monitoring-mechanism-for-the-rms-connector"></a>¿Hay un módulo de administración o un mecanismo de supervisión similar para el conector RMS?

Aunque el conector Rights Management registra información, advertencia y mensajes de error en el registro de eventos, no hay ningún módulo de administración que incluya la supervisión de estos eventos. En cambio, la lista de eventos y sus descripciones, con más información para ayudarle a tomar acciones correctivas, se documenta en [Supervisión del conector de Azure Rights Management](../deploy-use/monitor-rms-connector.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-rms-or-can-i-delegate-to-other-administrators"></a>¿Debe ser un administrador global para configurar Azure RMS o puedo delegar a otros administradores?

Obviamente, los administradores globales de un inquilino de Azure AD u Office 365 pueden realizar todas las tareas administrativas del servicio Azure Rights Management. En cambio, si desea asignar permisos administrativos a otros usuarios, puede hacerlo mediante el cmdlet de PowerShell de Azure RMS [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator). Puede asignar este rol administrativo por cuenta de usuario o por grupo. Hay dos roles disponibles: **Administrador Global** y **Administrador de conector**. 

Como estos nombres de rol sugieren, el primer rol concede permisos para ejecutar todas las tareas administrativas de Azure Rights Management (sin hacerlos administradores globales para otros servicios en la nube) y el segundo rol concede permisos para ejecutar solo el conector Rights Management (RMS).

Algunos puntos que tener en cuenta:

- Solo los administradores globales de Office 365 y los administradores globales de Azure AD pueden usar los portales de administración (Centro de administración de Office 365 o Portal de Azure clásico) para configurar Azure RMS. Los usuarios a los que asigne el rol de administrador global de Azure RMS deben usar comandos de PowerShell de Azure RMS para configurar Azure RMS. Para ayudarle a encontrar los cmdlets adecuados para tareas específicas, consulte [Administración de Azure Rights Management mediante Windows PowerShell](../deploy-use/administer-powershell.md).

- Si ha configurado [controles de incorporación](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), esta configuración no afecta a la capacidad de administrar Azure RMS, excepto el conector RMS. Por ejemplo, si ha configurado controles de incorporación como que la capacidad de proteger el contenido está restringida al grupo "Departamento de TI", la cuenta que use para instalar y configurar el conector RMS debe ser miembro de ese grupo. 

- Ningún administrador de Azure RMS (el administrador global del inquilino o un administrador global de Azure RMS) puede quitar automáticamente la protección de documentos o correos electrónicos que estaban protegidos por Azure RMS. Solo los usuarios que están asignados como superusuarios de Azure RMS pueden hacer esto, y cuando está habilitada la característica de superusuario. En cambio, el administrador global del inquilino y cualquier administrador global de Azure RMS pueden asignar usuarios como superusuarios, incluida su propia cuenta. También pueden habilitar la característica de superusuario. Estas acciones se graban en el registro del administrador de Azure RMS. Para más información, consulte la sección de procedimientos de seguridad recomendados en [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](../deploy-use/configure-super-users.md). 

>[!NOTE]
> Las plantillas y nuevas opciones para configurar la protección de Azure Rights Management se están migrando a Azure Portal, lo que admite administradores de seguridad además del acceso de administradores globales. Para más información, consulte los siguientes anuncios en entradas de blogs: [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/) (Administración unificada de Azure Information Protection ahora en versión preliminar) y [Azure Information Protection unified administration phase two](https://blogs.technet.microsoft.com/enterprisemobility/2017/05/23/azure-information-protection-unified-administration-phase-two/) (Fase dos de la administración unificada de Azure Information Protection).

## <a name="how-do-i-create-a-new-custom-template-in-the-azure-portal"></a>¿Cómo se puede crear una plantilla personalizada nueva en Azure Portal?

Actualmente en versión preliminar, las plantillas personalizadas se están migrando a Azure Portal donde se puede seguir administrándolas como plantillas o convertirlas en etiquetas. Para crear una plantilla, cree una etiqueta nueva y establezca la configuración de la protección de datos para Azure RMS. De manera encubierta, esto crea una plantilla nueva a la que pueden acceder los servicios y las aplicaciones que se integran con las plantillas de Rights Management.

Para más información sobre cómo configurar plantillas en Azure Portal, consulte [Configuración y administración de plantillas en la directiva de Azure Information Protection](../deploy-use/configure-policy-templates.md).

## <a name="i-have-a-hybrid-deployment-of-exchange-with-some-users-on-exchange-online-and-others-on-exchange-serveris-this-supported-by-azure-rms"></a>Tengo una implementación híbrida de Exchange con algunos usuarios de Exchange Online y otros de Exchange Server. ¿Es compatible con Azure RMS?
Desde luego, y lo mejor es que los usuarios podrán proteger sin problemas y consumir correos electrónicos y archivos adjuntos protegidos en las dos implementaciones de Exchange. Para esta configuración, [active Azure RMS](../deploy-use/activate-service.md) y [habilite IRM para Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx). A continuación, [implemente y configure el conector RMS](../deploy-use/deploy-rms-connector.md) para Exchange Server.

## <a name="if-i-use-this-protection-for-my-production-environment-is-my-company-then-locked-into-the-solution-or-risk-losing-access-to-content-that-we-protected-with-azure-rms"></a>Si uso esta protección para mi entorno de producción, ¿estará mi empresa atada a la solución o se arriesgará a perder el acceso a los contenidos que protegimos con Azure RMS?
No, siempre tendrá el control de los datos y seguirá teniendo acceso a ellos, incluso si decide dejar de usar el servicio Azure Rights Management. Para obtener más información, consulte [Decommissioning and deactivating Azure Rights Management](../deploy-use/decommission-deactivate.md) (Retirada y desactivación de Azure Rights Management).

Sin embargo, antes de retirar la implementación de Azure RMS, nos gustaría conocer su opinión y comprender por qué tomó esta decisión. Si la protección de Azure Rights Management no satisface sus requisitos empresariales, consúltenos para informarse de si planeamos una función nueva para el futuro cercano o si hay alternativas. Envíe un mensaje de correo electrónico a [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS). Estaremos encantados de analizar sus requisitos técnicos y empresariales.

## <a name="can-i-control-which-of-my-users-can-use-azure-rms-to-protect-content"></a>¿Puedo controlar quiénes de mis usuarios pueden usar Azure RMS para proteger el contenido?
Sí, el servicio Azure Rights Management tiene controles de incorporación de usuario para este escenario. Para obtener más información, consulte la sección [Configuring onboarding controls for a phased deployment](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) (Configuración de controles de incorporación para una implementación por fases) del artículo [Activating Azure Rights Management](../deploy-use/activate-service.md) (Activar Azure Rights Management).

## <a name="can-i-prevent-users-from-sharing-protected-documents-with-specific-organizations"></a>¿Se puede impedir que los usuarios compartan documentos protegidos con organizaciones específicas?
Una de las mayores ventajas de usar el servicio Azure Rights Management para la protección de datos es que admite la colaboración de negocio a negocio sin tener que configurar relaciones de confianza explícitas para cada organización asociada, ya que Azure AD se encarga de la autenticación.

No hay ninguna opción de administración para impedir que los usuarios compartan documentos con organizaciones específicas de forma segura. Por ejemplo, supongamos que desea bloquear una organización en la que no confía o que tiene un negocio en competencia. Impedir que el servicio Azure Rights Management envíe documentos protegidos a los usuarios de estas organizaciones no tendría sentido, ya que los usuarios compartirían los documentos sin protección, lo que probablemente sea lo último que quiere que ocurra en este escenario. Por ejemplo, no podría identificar quién comparte documentos confidenciales de la empresa ni con qué usuarios de esas organizaciones lo está haciendo, lo que sí es posible cuando el documento (o correo electrónico) está protegido con el servicio Azure Rights Management.

## <a name="when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated"></a>Cuando comparto un documento protegido con una persona ajena a mi organización, ¿cómo se autentica ese usuario?
El servicio Azure Rights Management siempre usa una cuenta de Azure Active Directory y una dirección de correo electrónico asociada para la autenticación de usuarios, lo que facilita a los administradores la colaboración de negocio a negocio. Si la otra organización usa servicios de Azure, los usuarios ya tienen cuentas en Azure Active Directory, incluso si dichas cuentas se crearon y se administraron localmente y después se sincronizaron con Azure. Si la organización tiene Office 365 de forma encubierta, este servicio también usa Azure Active Directory para las cuentas de usuario. Si la organización del usuario no tiene cuentas administradas en Azure, los usuarios pueden suscribirse a [RMS para usuarios](../understand-explore/rms-for-individuals.md), que crea un inquilino y un directorio de Azure no administrados para la organización con una cuenta para el usuario, de modo que este usuario (y usuarios posteriores) se pueda autenticar para el servicio Azure Rights Management.

El método de autenticación de estas cuentas puede variar, en función de cómo configurase el administrador de la otra organización las cuentas de Azure Active Directory. Por ejemplo, podrían usar contraseñas creadas para estas cuentas, Multi-Factor Authentication (MFA), federación o contraseñas creadas en Servicios de dominio de Active Directory y después sincronizadas con Active Directory de Azure.

## <a name="can-i-add-external-users-people-from-outside-my-company-to-custom-templates"></a>¿Puedo agregar usuarios externos (personas ajenas a mi empresa) a plantillas personalizadas?
Sí. Si crea plantillas personalizadas que los usuarios finales (y los administradores) puedan seleccionar desde las aplicaciones, hará que les resulte más rápido y sencillo aplicar la protección de la información mediante las directivas predefinidas que especifique. Uno de los valores de la plantilla define quién puede acceder al contenido, y puede especificar usuarios y grupos de su organización y usuarios y grupos ajenos a su organización. 

Para especificar usuarios de fuera de su organización, agréguelos como contactos a un grupo que seleccione en el Portal de Azure clásico al configurar las plantillas. Para especificar grupos ajenos a su organización, debe usar el [módulo de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md), que también se puede utilizar para especificar los usuarios externos individuales e incluso todos los usuarios de otra organización:

-   **Use un objeto de Rights Definition para crear o actualizar una plantilla**.    especifique las direcciones de correo electrónico externas y sus derechos en un objeto de Rights Definition, que después usará para crear o actualizar una plantilla. Especifique el objeto de Rights Definition mediante el cmdlet [New-AadrmRightsDefinition](/powershell/module/aadrm/new-aadrmrightsdefinition) para crear una variable y después suministrar esta variable al parámetro -RightsDefinition con el cmdlet [Add-AadrmTemplate](/powershell/module/aadrm/add-aadrmtemplate) (para una nueva plantilla) o [Set-AadrmTemplateProperty](/powershell/module/aadrm/set-aadrmtemplateproperty) (si modifica una plantilla existente). Sin embargo, si agrega estos usuarios a una plantilla existente, tiene que definir objetos de Rights Definition para los grupos existentes en las plantillas y no solo los usuarios externos.

Para obtener más información sobre las plantillas personalizadas, consulte [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

> [!TIP]
> Las plantillas y nuevas opciones para configurar la protección de Azure Rights Management se están migrando a Azure Portal. Estas opciones nuevas permiten que sea más fácil especificar los usuarios externos para que ya no tenga que usar PowerShell o grupos que contienen usuarios externos. Esta funcionalidad actualmente está en versión preliminar: [Azure Information Protection unified administration now in Preview](https://blogs.technet.microsoft.com/enterprisemobility/2017/04/26/azure-information-protection-unified-administration-now-in-preview/) (Administración unificada de Azure Information Protection ahora en versión preliminar). 

> Para instrucciones documentadas, consulte [Para configurar una etiqueta para la protección de Rights Management](../deploy-use/configure-policy-protection.md#to-configure-a-label-for-rights-management-protection).

## <a name="does-azure-rms-work-with-dynamic-groups-in-azure-ad"></a>¿Funciona Azure RMS con grupos dinámicos en Azure AD?
Una característica de Azure AD Premium le permite configurar la pertenencia dinámica para grupos de seguridad mediante [reglas basadas en atributos](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Este tipo de grupo no admite una dirección de correo electrónico, por lo que no se puede usar con el servicio Azure Rights Management. Sin embargo, los grupos de Office 365 admiten la pertenencia a grupos dinámicos y están habilitados para correo. Dado que este grupo está habilitado para correo, puede usarlo con la protección de Azure Rights Management.

Para más información sobre los requisitos de los usuarios y grupos que se pueden usar con el servicio Azure Rights Management, consulte [Preparación de usuarios y grupos para Azure Information Protection](../plan-design/prepare.md).

## <a name="how-do-i-send-a-protected-email-to-a-gmail-or-hotmail-account"></a>¿Cómo envío un correo electrónico protegido a una cuenta de Gmail o Hotmail?

Es posible que haya visto referencias o demostraciones para Azure Information Protection que envía correos electrónicos protegidos a las cuentas de Gmail o Hotmail. Esta característica aún está en versión preliminar privada, por lo que no encontrará más información al respecto en esta documentación hasta que se publique como versión preliminar pública.

## <a name="what-devices-and-which-file-types-are-supported-by-azure-rms"></a>¿Qué dispositivos y tipos de archivo admite Azure RMS?
Para ver la lista de los dispositivos que admiten el servicio Azure Rights Management, consulte [Dispositivos cliente que son compatibles con la protección de datos de Azure Rights Management](../get-started/requirements-client-devices.md). Dado que, actualmente, no todos los dispositivos compatibles admiten todas las funcionalidades de Rights Management, vea también la tabla de [aplicaciones habilitadas para RMS](../get-started/requirements-applications.md#rms-enlightened-applications).

El servicio Azure Rights Management puede admitir todos los tipos de archivo. Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones, Azure Rights Management proporciona protección nativa que incluye cifrado y cumplimiento de derechos (permisos). Para las demás aplicaciones y tipos de archivo, la protección genérica proporciona encapsulación de archivos y autenticación para comprobar si un usuario está autorizado para abrir el archivo.

Para obtener una lista de extensiones de nombre de archivo que se admiten de forma nativa en Azure Rights Management, vea [Tipos de archivos compatibles con el cliente de Azure Information Protection](../rms-client/client-admin-guide-file-types.md). Se admiten las extensiones de nombre de archivo que no están enumeradas si se usa el cliente de Azure Information Protection que aplica automáticamente la protección genérica a estos archivos.

## <a name="how-do-i-configure-a-mac-computer-to-protect-and-track-documents"></a>¿Cómo se configura un equipo Mac para proteger documentos y hacer un seguimiento de ellos?

En primer lugar, asegúrese de haber instalado Office para Mac con el vínculo de instalación de software de https://portal.office.com. Para instrucciones completas, consulte el artículo sobre cómo [descargar e instalar o reinstalar Office 365 u Office 2016 en un PC o un equipo Mac](https://support.office.com/en-us/article/Download-and-install-or-reinstall-Office-365-or-Office-2016-on-a-PC-or-Mac-4414EAAF-0478-48BE-9C42-23ADC4716658).

Abra Outlook y cree un perfil con su cuenta profesional o educativa de Office 365. Luego, cree un mensaje y siga estos pasos para configurar Office de manera que se puedan proteger documentos y correos electrónicos mediante el servicio Azure Rights Management:

1. En la pestaña **Opciones** del mensaje nuevo, haga clic en la pestaña **Permisos** y, luego, en **Verify Credentials** (Comprobar credenciales).

2. Cuando se le solicite, vuelva a especificar los detalles de la cuenta profesional o educativa de Office 365 y seleccione **Iniciar sesión**. 
    
    Con esto se descargan las plantillas de Azure Rights Management y **Verify Credentials** ahora se reemplaza por otras opciones que incluyen **No Restrictions** (Sin restricciones), **Do Not Forward** (No reenviar) y cualquier plantilla de Azure Rights Management que se publiquen para su inquilino. Ahora puede cancelar el mensaje nuevo.

Para proteger un mensaje de correo electrónico o un documento: en la pestaña **Opciones**, haga clic en **Permisos** y elija una opción o plantilla que proteja el correo electrónico o el documento.

Para hacer seguimiento de un documento después de protegerlo: en un equipo Windows que tenga instalado el cliente de Azure Information Protection, registre el documento con el sitio de seguimiento de documentos con una aplicación de Office o el Explorador de archivos. Para instrucciones, consulte [Realizar el seguimiento y revocar los documentos](../rms-client/client-track-revoke.md). En el equipo Mac, ahora puede usar el explorador web para ir al sitio de seguimiento de documentos (https://track.azurerms.com) para realizar el seguimiento de este documento y revocarlo.

## <a name="when-i-open-an-rms-protected-office-document-does-the-associated-temporary-file-become-rms-protected-as-well"></a>Al abrir un documento de Office protegido con RMS, ¿también se protege con RMS el archivo temporal asociado?
No. En este caso, el archivo temporal asociado no contiene los datos del documento original, sino solo lo que escribe el usuario mientras el archivo está abierto. A diferencia del archivo original, el archivo temporal obviamente no está diseñado para el uso compartido y se conservará en el dispositivo, protegido mediante controles de seguridad local, como BitLocker y EFS.

## <a name="we-really-want-to-use-byok-with-azure-information-protection-but-learned-that-this-isnt-compatible-with-exchange-onlinewhats-your-advice"></a>Nos interesa usar BYOK con Azure Information Protection, pero por lo visto no es compatible con Exchange Online. ¿Qué nos aconsejan?
No deje que esta limitación actual retrase el uso del servicio Azure Rights Management de Azure Information Protection. Si tiene Exchange Online y quiere usar Aportar su propia clave (BYOK), se recomienda implementar ahora Azure Information Protection en el modo de administración de claves predeterminado, donde Microsoft genera y administra su clave. De este modo, obtendrá todas las ventajas que supone proteger ahora sus archivos y mensajes de correo electrónico importantes, con la opción de pasarse a BYOK más adelante (por ejemplo, cuando Exchange Online admita BYOK). Cuando migre a BYOK, los correos electrónicos y documentos protegidos anteriormente siguen estando accesibles mediante el uso de una clave archivada.

En cambio, si las directivas de la empresa requieren que se use un módulo de seguridad de hardware (HSM) y esto podría bloquear la implementación de Azure Information Protection, otra opción es implementar ahora Azure Information Protection con BYOK, con una funcionalidad de protección de Rights Management reducida para Exchange. Para obtener más información, consulte [BYOK pricing and restrictions](../plan-design/byok-price-restrictions.md) (Precios y restricciones de BYOK) en [Planning and implementing your Azure Rights Management tenant key](../plan-design/plan-implement-tenant-key.md) (Planeamiento e implementación de la clave de inquilino de Azure Rights Management).

## <a name="a-feature-i-am-looking-for-doesnt-seem-to-work-with-sharepoint-protected-librariesis-support-for-my-feature-planned"></a>Una característica que me interesa no funciona con las bibliotecas protegidas de SharePoint. ¿Está prevista la compatibilidad con esta característica?
Actualmente, SharePoint es compatible con documentos protegidos de Rights Management mediante las bibliotecas protegidas de IRM, que no son compatibles con las plantillas personalizadas, el seguimiento de documentos y otras capacidades. Para obtener más información, consulte la sección [SharePoint Online and SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) (SharePoint Online y SharePoint Server) del artículo [Office applications and services](../understand-explore/office-apps-services-support.md) (Aplicaciones y servicios de Office).

Si está interesado en una función específica que todavía no es compatible, no se pierda los anuncios que se publican en el [Blog de Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-rights-management-services).

## <a name="how-do-i-configure-one-drive-for-business-in-sharepoint-online-so-that-users-can-safely-share-their-files-with-people-inside-and-outside-the-company"></a>¿Cómo configuro OneDrive para la Empresa en SharePoint Online para que los usuarios puedan compartir con seguridad sus archivos con personas de dentro y fuera de la empresa?
De forma predeterminada, como administrador de Office 365, no es usted quien lo configura; lo hacen los usuarios.

Del mismo modo que el administrador del sitio de SharePoint habilita y configura IRM para una biblioteca de SharePoint de su propiedad, OneDrive para la Empresa se ha diseñado para que los usuarios habiliten y configuren IRM para su propia biblioteca de OneDrive para la Empresa. Sin embargo, gracias a PowerShell, puede hacerlo por ellos. Para obtener instrucciones, consulte la sección [SharePoint Online and OneDrive for Business: IRM Configuration](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) (SharePoint Online y OneDrive para la Empresa: configuración de IRM) del artículo [Office 365: Configuration for clients and online services](../deploy-use/configure-office365.md) (Office 365: configuración para clientes y servicios en línea).

## <a name="do-you-have-any-tips-or-tricks-for-a-successful-deployment"></a>¿Hay trucos o sugerencias para una correcta implementación?
Después de supervisar muchas implementaciones y escuchar a nuestros clientes, socios, asesores e ingenieros de soporte, una de las mayores sugerencias que le podemos dar por la experiencia es: **Diseño e implementación de directivas sencillas**.

Dado que Azure Information Protection admite el uso compartido seguro con cualquiera, puede ser ambicioso con el alcance de la protección de los datos. Pero debe ser conservador en cuanto a las directivas de derechos. Para muchas organizaciones, el mayor impacto comercial se centra en evitar las pérdidas de datos mediante la plantilla predeterminada de directivas de derechos que restringe el acceso a las personas de su organización. Claro que puede alcanzar un nivel mucho más pormenorizado si es necesario (evitar que los usuarios impriman, editen, etc.). Pero las restricciones más pormenorizadas deben ser la excepción para los documentos que realmente necesitan un alto nivel de seguridad. Además, no debe implementar estas directivas más restrictivas desde el primer día, sino que conviene planificar un enfoque más escalonado.

## <a name="how-do-we-regain-access-to-files-that-were-protected-by-an-employee-who-has-now-left-the-organization"></a>¿Cómo recupero el acceso a los archivos que protegió un empleado que ya no trabaja en la organización?
Use la [característica de superusuario](../deploy-use/configure-super-users.md), que permite que los usuarios autorizados tengan derechos de uso completos para todas las licencias concedidas por el inquilino de su organización. Esta misma función permite que los servicios autorizados indicen e inspeccionen archivos, según sea necesario.

## <a name="when-i-test-revocation-in-the-document-tracking-site-i-see-a-message-that-says-people-can-still-access-the-document-for-up-to-30-daysis-this-time-period-configurable"></a>Cuando pruebo la revocación en el sitio de seguimiento de documentos, aparece un mensaje que indica que los usuarios pueden seguir accediendo al documento durante un máximo de 30 días. ¿Se puede configurar este período?

Sí. Este mensaje refleja la licencia de uso de ese archivo en concreto. Una licencia de uso es un certificado de cada documento que se concede a un usuario que abre un archivo protegido o un mensaje de correo electrónico. Este certificado contiene los derechos del usuario relativos al archivo o mensaje de correo electrónico y la clave de cifrado que se usó para cifrar el contenido, así como las restricciones de acceso adicionales definidas en la directiva del documento. Cuando expira el período de validez de la licencia de uso y un usuario intenta abrir el archivo o el mensaje de correo electrónico, las credenciales de usuario deben enviarse de nuevo al servicio de Azure Rights Management. 

Si revoca un archivo, dicha acción solo se puede aplicar cuando el usuario se autentica en el servicio de Azure Rights Management. Así, si un archivo tiene un período de validez de licencia de uso de 30 días y el usuario ya ha abierto el documento, puede seguir accediendo al documento durante dicho período. Cuando la licencia de uso expire, el usuario deberá volver a autenticarse; en ese momento, se le denegará el acceso porque el documento ya se ha revocado.

El usuario que ha protegido el documento, el [emisor de Rights Management](../deploy-use/configure-usage-rights.md#rights-management-issuer-and-rights-management-owner), está exento de esta revocación y puede acceder siempre a sus documentos. 

El valor predeterminado para el período de validez de la licencia de uso para un inquilino es de 30 días. Este valor se puede configurar con el cmdlet de PowerShell **Set-AadrmMaxUseLicenseValidityTime**. Este valor se puede reemplazar por una configuración más restrictiva en una plantilla personalizada. 

Para obtener más información y ejemplos de cómo funciona la licencia de uso, consulte la descripción detallada de [Set-AadrmMaxUseLicenseValidityTime](/powershell/module/aadrm/set-aadrmmaxuselicensevaliditytime).

## <a name="can-rights-management-prevent-screen-captures"></a>¿Puede impedir Rights Management las capturas de pantalla?
Si no se concede el [derecho de uso](../deploy-use/configure-usage-rights.md) **Copiar**, Rights Management puede impedir las capturas de pantalla de muchas de las herramientas de captura de pantalla que se usan habitualmente en las plataformas Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) y Android. Sin embargo, los dispositivos iOS y Mac no permiten a ninguna aplicación impedir las capturas de pantalla y los navegadores (por ejemplo, cuando se usan con Outlook Web App y Office Online) tampoco pueden evitar las capturas de pantalla.

Impedir las capturas de pantalla puede ayudar a evitar la divulgación accidental o por negligencia de información confidencial. Sin embargo, existen muchas formas en que un usuario puede compartir datos que se muestran en una pantalla y hacer una captura de pantalla es solo un método. Por ejemplo, un usuario decidido a compartir la información mostrada puede tomar una foto de ella con su teléfono con cámara, volver a escribir los datos o simplemente transmitírsela verbalmente a alguien.

Como demuestran estos ejemplos, aunque todas las plataformas y todo el software admitieran las API de Rights Management para bloquear las capturas de pantalla, la tecnología por si sola no siempre puede impedir que los usuarios compartan datos que no deberían. Rights Management puede ayudar a proteger sus datos importantes mediante directivas de autorización y uso, pero esta solución de administración de derechos empresariales debe utilizarse con otros controles. Por ejemplo, implemente seguridad física, preste especial atención a aquellas personas con acceso autorizado a los datos de su organización e invierta en la educación de los usuarios para que sepan qué datos no deben compartir.

## <a name="whats-the-difference-between-a-user-protecting-an-email-with-do-not-forward-and-a-template-that-doesnt-include-the-forward-right"></a>¿Cuál es la diferencia entre un usuario que protege un correo electrónico con No reenviar y una plantilla que no incluye el derecho Reenviar?

A pesar de su nombre y apariencia, **No reenviar** no es lo contrario del derecho Reenviar, ni tampoco una plantilla. En realidad es un conjunto de derechos que incluyen la restricción de copiar, imprimir y guardar datos adjuntos, además de restringir el reenvío de mensajes de correo electrónico. Los derechos no los asigna estáticamente el administrador, sino que se aplican dinámicamente a los usuarios a través de los destinatarios elegidos. Para obtener más información, consulte la sección [Do Not Forward option for emails](../deploy-use/configure-usage-rights.md#do-not-forward-option-for-emails) (Opción No reenviar para correos electrónicos) de [Configuring usage rights for Azure Rights Management](../deploy-use/configure-usage-rights.md) (Configuración de los derechos de uso para Azure Rights Management).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


