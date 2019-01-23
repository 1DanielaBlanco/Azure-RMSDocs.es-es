---
title: Preguntas más frecuentes de Azure Information Protection
description: Algunas de las preguntas más frecuentes sobre Azure Information Protection y su servicio de protección de datos, Azure Rights Management (Azure RMS).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/16/2019
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: ef9836a6e3b651986642d2c93128ea0f6b1e6112
ms.sourcegitcommit: 2c90f5bf11ec34ab94824a39ccab75bde71fc3aa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/15/2019
ms.locfileid: "54314856"
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Preguntas más frecuentes de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

¿Tiene alguna pregunta sobre Azure Information Protection o sobre el servicio Azure Rights Management (Azure RMS)? Vea si se ha resuelto aquí.

Las páginas de las preguntas más frecuentes se actualizan de forma periódica, y las nuevas preguntas se incluyen en los anuncios mensuales de actualizaciones de la documentación en el [blog técnico de Azure Information Protection](https://aka.ms/AIPblog).

## <a name="whats-the-difference-between-azure-information-protection-and-microsoft-information-protection"></a>¿Cuál es la diferencia entre Azure Information Protection y Microsoft Information Protection?

A diferencia de Azure Information Protection, Microsoft Information Protection no es una suscripción o producto que pueda comprar. En su lugar, se trata de una plataforma para productos y funcionalidades integradas que le ayudan a proteger la información confidencial de la organización:

- Los productos individuales en esta plataforma incluyen Azure Information Protection, Office 365 Information Protection (por ejemplo, Office 365 DLP), Windows Information Protection y Microsoft Cloud App Security. 

- Las funcionalidades integradas en esta plataforma incluyen la administración unificada de etiquetas, las experiencias de etiquetado del usuario final integradas en las aplicaciones de Office, la capacidad de Windows para comprender las etiquetas unificadas y aplicar protección a los datos, el SDK de Microsoft Information Protection y la nueva funcionalidad de Adobe Acrobat Reader para ver los archivos PDF etiquetados y protegidos.

Para más información, consulte el artículo [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Anuncio de la disponibilidad de las funcionalidades de protección de la información para ayudar a proteger los datos confidenciales).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>¿Cuál es la diferencia entre Azure Information Protection y Azure Rights Management?

Azure Information Protection ofrece funciones de clasificación, etiquetado y protección para los documentos y correos electrónicos de una organización. La tecnología de protección usa el servicio Azure Rights Management, que ahora es un componente de Azure Information Protection.

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>¿Cuál es el rol de la administración de identidades en Azure Information Protection?

Un usuario debe tener un nombre de usuario y contraseña válidos para acceder al contenido protegido mediante Azure Information Protection. Para más información sobre cómo Azure Information Protection ayuda a proteger los datos, consulte [Rol de Azure Information Protection en la protección de datos](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>¿Qué suscripción necesito para Azure Information Protection y qué características se incluyen?
Puede consultar la información sobre la suscripción y la lista de características en la página [Precios de Azure Information Protection](https://azure.microsoft.com/en-us/pricing/details/information-protection). 

Si tiene una suscripción a Office 365 que incluye la protección de datos de Azure Rights Management, descargue la [hoja de datos de licencias de Azure Information Protection](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf), en la que también se incluyen algunas preguntas frecuentes sobre las licencias.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>¿Es el cliente de Azure Information Protection únicamente para las suscripciones que incluyen la clasificación y el etiquetado?

No. Aunque la mayoría de las presentaciones y demostraciones que ha visto del cliente de Azure Information Protection muestran cómo este admite la clasificación y el etiquetado, también se puede utilizar con suscripciones que incluyen solo el servicio de Azure Rights Management para proteger los datos.

Cuando se instala el cliente de Azure Information Protection para Windows y no tiene una directiva de Azure Information Protection, el cliente funciona automáticamente en el [modo de solo protección](./rms-client/client-protection-only-mode.md). En este modo, los usuarios pueden aplicar fácilmente las plantillas de Rights Management y permisos personalizados. Si más adelante adquiere una suscripción que incluye la clasificación y el etiquetado, el cliente cambia automáticamente al modo estándar cuando descarga la directiva de Azure Information Protection.

Si actualmente utiliza la aplicación Rights Management sharing para Windows, le recomendamos que reemplace esta aplicación por el cliente de Azure Information Protection. La compatibilidad con la aplicación para uso compartido finalizará el 31 de enero de 2019. Para ayudarle con la transición, consulte [Tareas que solía hacer con la aplicación RMS sharing](./rms-client/upgrade-client-app.md).

## <a name="do-you-need-to-be-a-global-admin-to-configure-azure-information-protection-or-can-i-delegate-to-other-administrators"></a>¿Hay que ser un administrador global para configurar Azure Information Protection o puedo delegar a otros administradores?

Obviamente, los administradores globales de un inquilino de Azure AD u Office 365 pueden realizar todas las tareas administrativas de Azure Information Protection. Con todo, si quiere asignar permisos administrativos a otros usuarios, dispone de las siguientes opciones:

- **Administrador de Information Protection**: este rol de administrador de Azure Active Directory permite a los administradores configurar todos los aspectos de Azure Information Protection, pero no otros servicios. Un administrador con este rol puede activar y desactivar el servicio de protección de Azure Rights Management, configurar etiquetas y opciones de protección y, asimismo, configurar la directiva de Azure Information Protection. Además, un administrador con este rol puede ejecutar todos los cmdlets de PowerShell para el [cliente de Azure Information Protection](./rms-client/client-admin-guide-powershell.md) y desde el [módulo AADRM](administer-powershell.md). 
    
    Para asignar este rol administrativo a un usuario, vea [Asignación de un usuario a roles de administrador en Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal).

- **Administrador de seguridad**: este rol de administrador de Azure Active Directory permite a los administradores configurar todos los aspectos de Azure Information Protection en Azure Portal, además de algunos aspectos de otros servicios de Azure. Un administrador con este rol no puede ejecutar ningún [cmdlet de PowerShell desde el módulo AADRM](administer-powershell.md).
    
    Para asignar este rol administrativo a un usuario, vea [Asignación de un usuario a roles de administrador en Azure Active Directory](/azure/active-directory/active-directory-users-assign-role-azure-portal). Para ver qué otros permisos tiene un usuario con este rol, vea la sección [Roles disponibles](/azure/active-directory/active-directory-assign-admin-roles-azure-portal#available-roles) de la documentación de Azure Active Directory.

- **Administrador Global** y **Administrador de conector** de Azure Rights Management: el primero de estos roles de administrador de Azure Rights Management concede permisos de usuario para ejecutar todos los [cmdlets de PowerShell desde el módulo AADRM](administer-powershell.md) sin hacerlos un administrador global para otros servicios en la nube, mientras que el segundo concede permisos para ejecutar solo el conector Rights Management (RMS). Ninguno de estos roles administrativos concede permisos a las consolas de administración o para usar el modo de administrador en el sitio de seguimiento de documentos.

    Para asignar cualquiera de estos dos roles administrativos, use el cmdlet de PowerShell de AADRM [Add-AadrmRoleBasedAdministrator](/powershell/module/aadrm/add-aadrmrolebasedadministrator).

Algunos puntos que tener en cuenta:

- Si ha configurado [controles de incorporación](activate-service.md#configuring-onboarding-controls-for-a-phased-deployment), esta configuración no afecta a la capacidad para administrar Azure Information Protection, salvo el conector RMS. Por ejemplo, si ha configurado controles de incorporación como que la capacidad de proteger el contenido está restringida al grupo "Departamento de TI", la cuenta que use para instalar y configurar el conector RMS debe ser miembro de ese grupo. 

- Los usuarios que tengan asignado un rol administrativo no pueden quitar automáticamente la protección de los documentos o correos electrónicos protegidos con Azure Information Protection. Solo pueden los usuarios que estén asignados como superusuarios y siempre y cuando esté habilitada la característica de superusuario. No obstante, cualquier usuario que tenga asignados permisos administrativos en Azure Information Protection puede designar usuarios como superusuarios (incluida su propia cuenta). También pueden habilitar la característica de superusuario. En el registro del administrador se deja constancia de estas acciones. Para más información, consulte la sección de procedimientos de seguridad recomendados en [Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos](configure-super-users.md). 

- Si va a migrar las etiquetas de Azure Information Protection a Office 365, asegúrese de leer la siguiente sección de la documentación de migración de etiquetas: [Información importante acerca de los roles administrativos](configure-policy-migrate-labels.md#important-information-about-administrative-roles).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>¿Azure Information Protection admite los escenarios híbridos y locales?

Sí. Aunque Azure Information Protection es una solución basada en la nube, puede clasificar, etiquetar y proteger documentos y correos electrónicos almacenados de forma local, así como en la nube.

Si tiene Exchange Server, SharePoint Server y servidores de archivos de Windows, puede implementar el [conector Rights Management](deploy-rms-connector.md) con el fin de que estos servidores locales utilicen el servicio Azure Rights Management para proteger los correos electrónicos y documentos. También puede sincronizar y federar los controladores de dominio de Active Directory con Azure AD para ofrecer una experiencia de autenticación más sencilla a los usuarios, por ejemplo, mediante el uso de [Azure AD Connect](/azure/active-directory/hybrid/whatis-azure-ad-connect).

El servicio Azure Rights Management genera automáticamente y administra los certificados XrML según sea necesario, por lo que no usa una PKI local. Para más información sobre la manera en que Azure Rights Management usa los certificados, vea la sección [Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido](./how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) del artículo [¿Cómo funciona Azure RMS? En segundo plano](./how-does-it-work.md).

## <a name="what-types-of-data-can-azure-information-protection-classify-and-protect"></a>¿Qué tipos de datos puede clasificar y proteger Azure Information Protection?

Azure Information Protection puede clasificar y proteger documentos y mensajes de correo electrónico, independientemente de si están almacenados localmente o en la nube. Estos documentos pueden ser documentos de Word, hojas de cálculo de Excel, presentaciones de PowerPoint, documentos PDF, archivos de texto y archivos de imagen. Para obtener una lista de los tipos de documento admitidos, vea la lista [Tipos de archivo compatibles](./rms-client/client-admin-guide-file-types.md) en la guía del administrador.

Azure Information Protection no clasifica ni protege datos estructurados como los archivos de base de datos, los elementos de calendario, los informes de Power BI, las publicaciones de Yammer, el contenido de Sway ni los blocs de notas de OneNote.

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Veo que Azure Information Protection aparece como una aplicación en la nube disponible para el acceso condicional. ¿Cómo funciona?

Sí, como oferta de versión preliminar, ahora puede configurar el acceso condicional de Azure AD para Azure Information Protection.

Cuando un usuario abre un documento que está protegido con Azure Information Protection, los administradores ahora pueden bloquear o conceder acceso a los usuarios de su inquilino, en función de los controles de acceso condicional estándar. Requerir la autenticación multifactor (MFA) es una de las condiciones solicitadas con más frecuencia. Otra es que los dispositivos deben ser [conformes con las directivas de Intune](/intune/conditional-access-intune-common-ways-use) para que, por ejemplo, los dispositivos móviles cumplan los requisitos de contraseña y una versión mínima del sistema operativo, y los equipos deben estar unidos a un dominio.

Para más información y algunos ejemplos de tutoriales, vea la siguiente entrada de blog: [Conditional Access policies for Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/) (Directivas de acceso condicional para Azure Information Protection).

Información adicional:

- Para equipos Windows: para la versión preliminar actual, se evalúan las directivas de acceso condicional de Azure Information Protection cuando [se inicializa el entorno del usuario](./how-does-it-work.md#initializing-the-user-environment), proceso conocido también como "arranque", y posteriormente cada 30 días.

- Puede ajustar la frecuencia con la que se evalúan las directivas de acceso condicional. Puede hacerlo mediante la configuración de la duración del token. Para obtener más información, consulte [Vigencia de tokens configurables de Azure Active Directory (versión preliminar pública)](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Se recomienda no agregar cuentas de administrador a las directivas de acceso condicional porque estas cuentas no podrán tener acceso a la hoja de Azure Information Protection en Azure Portal.

- Si usa MFA en las directivas de acceso condicional para colaborar con otras organizaciones (B2B), tendrá que usar [colaboración B2B de Azure AD](/azure/active-directory/b2b/what-is-b2b) y crear cuentas de invitado para los usuarios con los que quiera compartir en la otra organización.

- A partir de la versión preliminar de Azure AD de diciembre de 2018 puede solicitar a los usuarios que acepten los términos de uso antes de abrir un documento protegido por primera vez. Para obtener más información, vea el anuncio de la siguiente entrada de blog: [Updates to Azure AD Terms of Use functionality within conditional access](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Updates-to-Azure-AD-Terms-of-Use-functionality-within/ba-p/294822) (Actualizaciones a la función Términos de uso de Azure AD de acceso condicional)

- Si usa muchas aplicaciones en la nube para el acceso condicional, puede que **Microsoft Azure Information Protection** no se muestre en la lista de selección. En ese caso, utilice el cuadro de búsqueda en la parte superior de la lista. Comience por escribir "Microsoft Azure Information Protection" para filtrar las aplicaciones disponibles. Siempre que tenga una suscripción admitida, verá **Microsoft Azure Information Protection** para su selección. 

## <a name="i-see-azure-information-protection-is-listed-as-a-security-provider-for-microsoft-graph-securityhow-does-this-work-and-what-alerts-will-i-receive"></a>Veo que Azure Information Protection aparece como proveedor de seguridad para Microsoft Graph Security. ¿Cómo funciona y qué alertas voy a recibir?

Sí, como oferta de versión preliminar pública, ahora puede recibir una alerta para el **acceso anómalo a datos de Azure Information Protection**. Esta alerta se desencadena cuando hay intentos no habituales de acceder a los datos protegidos por Azure Information Protection. Por ejemplo, acceder a un volumen inusualmente elevado de datos, en un momento inusual del día o desde una ubicación desconocida.

Estas alertas pueden ayudarle a detectar ataques avanzados relacionados con los datos y amenazas internas en el entorno. Estas alertas utilizan aprendizaje automático para trazar un perfil del comportamiento de los usuarios que tienen acceso a los datos protegidos. 

Se puede acceder a las alertas de Azure Information Protection [mediante la API de Microsoft Graph Security](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/security-api-overview), o bien puede [transmitir alertas](https://developer.microsoft.com/en-us/graph/docs/concepts/security_siemintegration) a soluciones SIEM, como Splunk e IBM Qradar, mediante el uso de Azure Monitor.

Para obtener más información acerca de la API de Microsoft Graph Security, consulte [Microsoft Graph Security API overview](https://developer.microsoft.com/graph/docs/concepts/security-concept-overview) (Información general de la API de Microsoft Graph Security).

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>¿Cuál es la diferencia entre las etiquetas de Azure Information Protection y las de Office 365?

Hasta hace poco, Office 365 solo tenía [etiquetas de retención](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) que permitían clasificar los documentos y correos electrónicos para retención y auditoría cuando ese contenido se encontraba en servicios de Office 365. En comparación, las etiquetas de Azure Information Protection permiten aplicar una directiva coherente de clasificación y protección para los documentos y los correos electrónicos tanto si están en local como en la nube.

Como se anunció en Microsoft Ignite 2018, ahora empezará a ver una opción para crear y configurar [etiquetas de confidencialidad](https://docs.microsoft.com/Office365/SecurityCompliance/sensitivity-labels) además de las etiquetas de retención en el Centro de seguridad y cumplimiento de Office 365. Además, ahora en versión preliminar, puede migrar sus etiquetas de Azure Information Protection existentes a la nueva tienda unificada de etiquetado. 

Para más información sobre la administración de etiquetado unificado y cómo estas etiquetas se van a admitir, lea la entrada de blog, [Announcing availability of information protection capabilities to help protect your sensitive data](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Announcing-availability-of-information-protection-capabilities/ba-p/261967) (Anuncio de la disponibilidad de las funcionalidades de protección de la información para ayudar a proteger los datos confidenciales).

Para más información sobre la migración de etiquetas existentes, consulte [Cómo migrar etiquetas de Azure Information Protection al Centro de seguridad y cumplimiento de Office 365](configure-policy-migrate-labels.md).

## <a name="whats-the-difference-between-windows-server-fci-and-the-azure-information-protection-scanner"></a>¿Cuál es la diferencia entre FCI de Windows Server y el analizador de Azure Information Protection?

La infraestructura de clasificación de archivos de Windows Server ha sido desde siempre una opción para clasificar documentos y después protegerlos mediante el [conector de Rights Management](deploy-rms-connector.md) (solo para documentos de Office) o un [script de PowerShell ](./rms-client/configure-fci.md) (para todos los tipos de archivo). 

Ahora le recomendamos usar el [analizador de Azure Information Protection](deploy-aip-scanner.md). El analizador usa el cliente y la directiva de Azure Information Protection para etiquetar documentos (para todos los tipos de archivo) para después clasificarlos y, opcionalmente, protegerlos.

Principales diferencias entre estas dos soluciones:

|FCI de Windows Server|Analizador de Azure Information Protection|
|--------------------------------|-------------------------------------|
|Almacenes de datos admitidos: <br /><br />- Carpetas locales de Windows Server|Almacenes de datos admitidos: <br /><br />- Carpetas locales de Windows Server<br /><br />- Recursos compartidos de archivos de Windows y almacenamiento conectado a la red<br /><br />- SharePoint Server 2016 y SharePoint Server 2013. SharePoint Server 2010 también se admite en clientes que tengan [compatibilidad ampliada para esta versión de SharePoint](https://support.microsoft.com/lifecycle/search?alpha=SharePoint%20Server%202010).|
|Modo operativo: <br /><br />- En tiempo real|Modo operativo: <br /><br />- Rastrea los almacenes de datos de forma sistemática, y este ciclo se puede ejecutar una o varias veces.|
|Compatibilidad con tipos de archivo: <br /><br />- Todos los tipos de archivo están protegidos de manera predeterminada <br /><br />- Determinados tipos de archivos se pueden excluir de la protección mediante la edición del Registro|Compatibilidad con tipos de archivo: <br /><br />- Los tipos de archivo de Office y documentos PDF están protegidos de forma predeterminada <br /><br />- Tipos adicionales de archivos se pueden incluir para la protección mediante la edición del Registro|

En la actualidad, hay diferencias en la configuración del [propietario de Rights Management](configure-usage-rights.md#rights-management-issuer-and-rights-management-owner) para los archivos que están protegidos en una carpeta local o un recurso compartido de red. De forma predeterminada, para ambas soluciones, el propietario de Rights Management se establece en la cuenta que protege el archivo, pero esta configuración se puede invalidar:

- Para FCI de Windows Server: se puede establecer el propietario de Rights Management en una sola cuenta para todos los archivos, o bien establecerlo de forma dinámica para cada archivo. Para establecer de forma dinámica el propietario de Rights Management, use el parámetro y valor **-OwnerMail [Correo electrónico del propietario del archivo de origen]**. Esta configuración recupera de Active Directory la dirección de correo electrónico del usuario utilizando su nombre de cuenta, situado en la propiedad Propietario del archivo.

- Para el analizador de Azure Information Protection: En el caso de archivos protegidos recientemente, se puede establecer el propietario de Rights Management en una sola cuenta para todos los archivos de un almacén de datos específico, pero no se puede establecer de forma dinámica para cada archivo. No se cambia el propietario de Rights Management para archivos protegidos con anterioridad. Para establecer la cuenta para los archivos recién protegidos, especifique la configuración **-Propietario predeterminado** en el perfil del analizador. 

Cuando el analizador protege los archivos de bibliotecas y sitios de SharePoint, el propietario de Rights Management se establece de forma dinámica para cada archivo con el valor de Editor de SharePoint.

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>He escuchado que pronto estará disponible una nueva versión de Azure Information Protection, ¿cuándo se publicará?

La documentación técnica no contiene información sobre las próximas versiones. Para este tipo de información y para anuncios de versiones, vea [Enterprise Mobility and Security Blog](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/bg-p/enterprisemobilityandsecurity?product=azure-information-protection,azure-rights-management-services) (Blog de seguridad y movilidad empresarial) y obtenga las actualizaciones más recientes de [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) en Twitter. Si está interesado en una versión de Office, asegúrese de consultar también el [blog de Office 365](https://techcommunity.microsoft.com/t5/Office-365-Blog/bg-p/Office365Blog) y el [blog de aplicaciones de Office](https://techcommunity.microsoft.com/t5/Office-Apps-Blog/bg-p/OfficeAppsBlog).

## <a name="is-azure-information-protection-suitable-for-my-country"></a>¿Se puede usar Azure Information Protection en mi país?

Las normativas y las regulaciones varían en función del país. Para ayudarle a responder a esta pregunta para su organización, consulte [Idoneidad para distintos países](./compliance.md#suitability-for-different-countries).

## <a name="how-can-azure-information-protection-help-with-gdpr"></a>¿Cómo puede ayudar Azure Information Protection con el RGPD?

Para ver cómo Azure Information Protection puede ayudarle a cumplir el Reglamento general de protección de datos (RGPD), vea la siguiente entrada de blog (incluye vídeo): [Microsoft 365 provides an information protection strategy to help with the GDPR](https://blogs.office.com/2018/02/22/microsoft-365-provides-an-information-protection-strategy-to-help-with-the-gdpr) (Microsoft 365 proporciona una estrategia de protección de la información para ayudar a cumplir con el RGPD).

## <a name="where-can-i-find-supporting-information-for-azureinformation-protectionsuch-as-legal-compliance-and-slas"></a>¿Dónde puedo encontrar información complementaria para Azure Information Protection (como información jurídica, de cumplimiento y sobre contratos de nivel de servicio)?
Vea [Cumplimiento e información complementaria para Azure Information Protection](./compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>¿Cómo puedo informar de un problema o enviar comentarios de Azure Information Protection?

Para soporte técnico, utilice los canales de soporte estándar o [póngase en contacto con el soporte técnico de Microsoft](information-support.md#to-contact-microsoft-support).

Para obtener comentarios, como sugerencias de mejoras o nuevas características: En la aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y luego en **Ayuda y comentarios**. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Enviar comentarios**. Esta opción abre un mensaje de correo electrónico para enviar al equipo de Information Protection.

También lo invitamos a participar en el equipo de ingeniería, en su [sitio de Yammer sobre Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>¿Qué debo hacer si mi pregunta no aparece aquí?

Primero, revise las preguntas más frecuentes siguientes que sean específicas para la clasificación y el etiquetado, o específicas de la protección de datos. El servicio Azure Rights Management (Azure RMS) proporciona la tecnología de protección de datos para Azure Information Protection. Azure RMS puede usarse con la clasificación y el etiquetado, o por sí mismo. 

- [Preguntas más frecuentes sobre la clasificación y el etiquetado](faqs-infoprotect.md)

- [Preguntas más frecuentes sobre la protección de datos](faqs-rms.md)

Si no encuentra una respuesta a su pregunta, use los vínculos y los recursos que se muestran en [Información y soporte técnico para Azure Information Protection](information-support.md).

Además, hay preguntas más frecuentes diseñadas para usuarios finales:

- [Preguntas más frecuentes sobre la aplicación de Microsoft Azure Information Protection para iOS y Android](./rms-client/mobile-app-faq.md)

- [FAQ for RMS sharing app for Mac computers and Windows Phone](https://technet.microsoft.com/dn451248) (Preguntas más frecuentes sobre la aplicación RMS sharing para equipos Mac y Windows Phone)

- [FAQ for Rights Management Sharing Application for Windows](https://technet.microsoft.com/dn467883) (Preguntas más frecuentes sobre la aplicación Rights Management sharing para Windows)



