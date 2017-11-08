---
title: "Preguntas más frecuentes de Azure Information Protection"
description: "Algunas de las preguntas más frecuentes sobre Azure Information Protection y su servicio de protección de datos, Azure Rights Management (Azure RMS)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/20/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 324eb3eb5d749021da93213e807f6316ca784485
ms.sourcegitcommit: a8140a7215c8704f34c247f602e1f12eb7b49aa2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="frequently-asked-questions-for-azure-information-protection"></a>Preguntas más frecuentes sobre Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

¿Tiene alguna pregunta sobre Azure Information Protection o sobre el servicio Azure Rights Management (Azure RMS)? Vea si se ha resuelto aquí.

Las páginas de las preguntas más frecuentes se actualizan de forma periódica, y las nuevas preguntas se incluyen en los anuncios mensuales de actualizaciones de la documentación en el [blog de Enterprise Mobility + Security](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services&content-type=updates).

## <a name="whats-the-difference-between-azure-information-protection-and-azure-rights-management"></a>¿Cuál es la diferencia entre Azure Information Protection y Azure Rights Management?

Azure Information Protection ofrece funciones de clasificación, etiquetado y protección para los documentos y correos electrónicos de una organización. La tecnología de protección usa el servicio Azure Rights Management, que ahora es un componente de Azure Information Protection.

## <a name="what-is-the-role-of-identity-management-for-azure-information-protection"></a>¿Cuál es el rol de la administración de identidades en Azure Information Protection?

Un usuario debe tener un nombre de usuario y contraseña válidos para acceder al contenido protegido mediante Azure Information Protection. Para más información sobre cómo Azure Information Protection ayuda a proteger los datos, consulte [Rol de Azure Information Protection en la protección de datos](/enterprise-mobility-security/solutions/azure-information-protection-securing-data). 

## <a name="what-subscription-do-i-need-for-azure-information-protection-and-what-features-are-included"></a>¿Qué suscripción necesito para Azure Information Protection y qué características se incluyen?
Consulte la [información sobre la suscripción](https://www.microsoft.com/cloud-platform/azure-information-protection-pricing) y la [lista de características](https://www.microsoft.com/cloud-platform/azure-information-protection-features) en el sitio de Azure Information Protection. 

Si tiene una suscripción a Office 365 que incluye Rights Management, descargue la [hoja de datos de licencias de Azure Information Protection](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf) en la página **Características**.

## <a name="is-the-azure-information-protection-client-only-for-subscriptions-that-include-classification-and-labeling"></a>¿Es el cliente de Azure Information Protection únicamente para las suscripciones que incluyen la clasificación y el etiquetado?

No. Aunque la mayoría de las presentaciones y demostraciones que ha visto del cliente de Azure Information Protection muestran cómo este admite la clasificación y el etiquetado, también se puede utilizar con suscripciones que incluyen solo el servicio de Azure Rights Management para proteger los datos.

Cuando se instala el cliente de Azure Information Protection para Windows y no tiene una directiva de Azure Information Protection, el cliente funciona automáticamente en el [modo de solo protección](../rms-client/client-protection-only-mode.md). En este modo, los usuarios pueden aplicar fácilmente las plantillas de Rights Management y permisos personalizados. Si más adelante adquiere una suscripción que incluye la clasificación y el etiquetado, el cliente cambia automáticamente al modo estándar cuando descarga la directiva de Azure Information Protection.

Si actualmente utiliza la aplicación Rights Management sharing para Windows, le recomendamos que reemplace esta aplicación por el cliente de Azure Information Protection. La compatibilidad con la aplicación para uso compartido finalizará el 31 de enero de 2019. Para ayudarle con la transición, consulte [Tareas que solía hacer con la aplicación RMS sharing](../rms-client/upgrade-client-app.md).

## <a name="does-azure-information-protection-support-on-premises-and-hybrid-scenarios"></a>¿Azure Information Protection admite los escenarios híbridos y locales?

Sí. Aunque Azure Information Protection es una solución basada en la nube, puede clasificar, etiquetar y proteger documentos y correos electrónicos almacenados de forma local, así como en la nube.

Si tiene Exchange Server, SharePoint Server y servidores de archivos de Windows, puede implementar el [conector Rights Management](../deploy-use/deploy-rms-connector.md) con el fin de que estos servidores locales utilicen el servicio Azure Rights Management para proteger los correos electrónicos y documentos. También puede sincronizar y federar los controladores de dominio de Active Directory con Azure AD para ofrecer una experiencia de autenticación más sencilla a los usuarios, por ejemplo, mediante el uso de [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

El servicio Azure Rights Management genera automáticamente y administra los certificados XrML según sea necesario, por lo que no usa una PKI local. Para obtener más información sobre la forma en que Azure Rights Management usa los certificados, vea la sección [Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) del artículo [¿Cómo funciona Azure RMS?](../understand-explore/how-does-it-work.md)

## <a name="i-see-azure-information-protection-is-listed-as-an-available-cloud-app-for-conditional-accesshow-does-this-work"></a>Veo que Azure Information Protection aparece como una aplicación en la nube disponible para el acceso condicional. ¿Cómo funciona?

Sí, como oferta de versión preliminar pública, ahora puede configurar el acceso condicional de Azure AD para Azure Information Protection.

Cuando un usuario abre un documento que está protegido con Azure Information Protection, los administradores ahora pueden bloquear o conceder acceso a los usuarios de su inquilino, en función de los controles de acceso condicional estándar. Requerir la autenticación multifactor (MFA) es una de las condiciones solicitadas con más frecuencia. Otra es que los dispositivos deben ser [conformes con las directivas de Intune](/intune/conditional-access-intune-common-ways-use) para que, por ejemplo, los dispositivos móviles cumplan los requisitos de contraseña y una versión mínima del sistema operativo, y los equipos deben estar unidos a un dominio.

Para obtener más información y algunos ejemplos de tutoriales, vea la entrada de blog [Directivas de acceso condicional de Azure Information Protection](https://cloudblogs.microsoft.com/enterprisemobility/2017/10/17/conditional-access-policies-for-azure-information-protection/).

Información adicional:

- Para equipos Windows: para la versión preliminar actual, se evalúan las directivas de acceso condicional de Azure Information Protection cuando [se inicializa el entorno del usuario](../understand-explore/how-does-it-work.md#initializing-the-user-environment), proceso conocido también como "arranque", y posteriormente cada 30 días.

- Puede ajustar la frecuencia con la que se evalúan las directivas de acceso condicional. Puede hacerlo mediante la configuración de la duración del token. Para obtener más información, consulte [Vigencia de tokens configurables de Azure Active Directory (versión preliminar pública)](/azure/active-directory/active-directory-configurable-token-lifetimes).

- Se recomienda no agregar cuentas de administrador a las directivas de acceso condicional porque estas cuentas no podrán tener acceso a la hoja de Azure Information Protection en Azure Portal.

- Si utiliza una gran cantidad de aplicaciones en la nube para el acceso condicional, puede que **Microsoft Azure Information Protection** no se muestre en la lista de selección. En ese caso, utilice el cuadro de búsqueda en la parte superior de la lista. Comience por escribir "Microsoft Azure Information Protection" para filtrar las aplicaciones disponibles. Siempre que tenga una suscripción admitida, verá **Microsoft Azure Information Protection** para su selección. 

## <a name="whats-the-difference-between-labels-in-azure-information-protection-and-labels-in-office-365"></a>¿Cuál es la diferencia entre las etiquetas de Azure Information Protection y las de Office 365?

Las etiquetas de Azure Information Protection permiten aplicar una directiva coherente de clasificación y protección para los documentos y los correos electrónicos tanto si están en local como en la nube. Esta clasificación y protección es independiente de la ubicación en la que se almacene el contenido o de cómo se migre. Las [etiquetas de seguridad y cumplimiento de Office 365](https://support.office.com/article/af398293-c69d-465e-a249-d74561552d30) permiten clasificar documentos y correos electrónicos para retención y auditoría cuando ese contenido se encuentra en servicios de Office 365. 

En la actualidad, estas etiquetas se aplican y se administran por separado, aunque Microsoft está trabajando en una estrategia de etiquetado general y unificada para varios servicios que incluyen Azure Information Protection, Office 365, Microsoft Cloud App Security y Windows Information Protection. Este mismo esquema y almacenamiento de etiquetado también estará disponible para los fabricantes de software. Para obtener más información, vea la sesión de Microsoft Ignite 2017 [Protecting complete data lifecycle using Microsoft information protection capabilities (Protección del ciclo de vida completo de los datos mediante las funcionalidades de Microsoft Information Protection)](https://myignite.microsoft.com/videos/55397).

## <a name="ive-heard-a-new-release-is-going-to-be-available-soon-for-azure-information-protectionwhen-will-it-be-released"></a>He escuchado que pronto estará disponible una nueva versión de Azure Information Protection, ¿cuándo se publicará?

La documentación técnica no contiene información sobre las próximas versiones. Para este tipo de información y para anuncios de versiones, vea [Enterprise Mobility and Security Blog](https://blogs.technet.microsoft.com/enterprisemobility/?product=azure-information-protection,azure-rights-management-services) (Blog de seguridad y movilidad empresarial) y obtenga las actualizaciones más recientes de [Microsoft Mobility@MSFTMobility](https://twitter.com/MSFTMobility) en Twitter. Si está interesado en una versión de Office, asegúrese de consultar también el [blog de Office](https://blogs.office.com/).

## <a name="where-can-i-find-supporting-information-for-azure-information-protectionsuch-as-legal-compliance-and-slas"></a>¿Dónde puedo encontrar información complementaria para Azure Information Protection (como información jurídica, de cumplimiento y sobre contratos de nivel de servicio)?

Vea [Cumplimiento e información complementaria para Azure Information Protection](../understand-explore/compliance.md).

## <a name="how-can-i-report-a-problem-or-send-feedback-for-azure-information-protection"></a>¿Cómo puedo informar de un problema o enviar comentarios de Azure Information Protection?

Para soporte técnico, utilice los canales de soporte estándar o [póngase en contacto con el soporte técnico de Microsoft](information-support.md#to-contact-microsoft-support).

Para obtener comentarios como sugerencias de mejoras o nuevas características: en la aplicación de Office, en la pestaña **Inicio**, en el grupo **Protección**, haga clic en **Proteger** y, después, haga clic en **Ayuda y comentarios**. En el cuadro de diálogo **Microsoft Azure Information Protection**, haga clic en **Enviar comentarios**. Esta opción abre un mensaje de correo electrónico para enviar al equipo de Information Protection.

También lo invitamos a participar en el equipo de ingeniería, en su [sitio de Yammer sobre Azure Information Protection](https://www.yammer.com/askipteam/). 

## <a name="what-do-i-do-if-my-question-isnt-here"></a>¿Qué debo hacer si mi pregunta no aparece aquí?

Primero, revise las preguntas más frecuentes siguientes que sean específicas para la clasificación y el etiquetado, o específicas de la protección de datos. El servicio Azure Rights Management (Azure RMS) proporciona la tecnología de protección de datos para Azure Information Protection. Azure RMS puede usarse con la clasificación y el etiquetado, o por sí mismo. 

- [Preguntas más frecuentes sobre la clasificación y el etiquetado](faqs-infoprotect.md)

- [Preguntas más frecuentes sobre la protección de datos](faqs-rms.md)

Si no encuentra una respuesta a su pregunta, use los vínculos y los recursos que se muestran en [Información y soporte técnico para Azure Information Protection](information-support.md).

Además, hay preguntas más frecuentes diseñadas para usuarios finales:

- [Preguntas más frecuentes sobre la aplicación de Microsoft Azure Information Protection para iOS y Android](../rms-client/mobile-app-faq.md)

- [FAQ for RMS sharing app for Mac computers and Windows Phone](https://technet.microsoft.com/dn451248) (Preguntas más frecuentes sobre la aplicación RMS sharing para equipos Mac y Windows Phone)

- [FAQ for Rights Management Sharing Application for Windows](https://technet.microsoft.com/dn467883) (Preguntas más frecuentes sobre la aplicación Rights Management sharing para Windows)


[!INCLUDE[Commenting house rules](../includes/houserules.md)]

