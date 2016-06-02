---
# required metadata

title: Preguntas más frecuentes de Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 05/13/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 71ce491f-41c1-4d15-9646-455a6eaa157d

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Preguntas más frecuentes de Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Algunas de las preguntas más frecuentes sobre Microsoft [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)], también conocido como Azure RMS:

## ¿Qué necesito para implementar Azure RMS y cómo lo hago?
En primer lugar, consulte en [Requirements for Azure Rights Management](requirements-azure-rms.md) (Requisitos de Azure Rights Management) información sobre las opciones de suscripción en la nube, cómo puede usar los servidores locales con Azure RMS, qué escenarios de implementación no se admiten actualmente, qué dispositivos y aplicaciones admiten Azure RMS y un vínculo si necesita una lista de direcciones IP y nombres de domino para firewalls o servidores proxy. También puede consultar otros artículos en la sección **Get Started** (Introducción) y en la sección **Understand & Explore** (Conceptos básicos y exploración) para comprender los aspectos básicos de cómo [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] puede ayudar a proteger los datos de su organización, cómo funciona con las aplicaciones y cómo es en comparación con la versión local de Active Directory Rights Management, así como los términos y las abreviaturas específicas de [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)].

## ¿Deben los archivos estar en la nube para tener la protección de Azure RMS?
No, se trata de una idea equivocada frecuente. El servicio de Rights Management (y Microsoft) no ve ni almacena sus datos como parte del proceso de protección de la información. La información que protege nunca se envía a Azure, ni se almacena allí, a menos que la almacene de manera explícita en Azure o use otro servicio en la nube que la almacene en Azure. 

Para obtener más información, consulte [How does Azure RMS work? Under the hood](../understand-explore/how-does-it-work.md) (¿Cómo funciona RMS Azure? En segundo plano) para entender cómo una fórmula de la cola secreta que se crea y almacena localmente tiene la protección de Azure RMS sin dejar de ser local.

## ¿Puedo integrar Azure RMS con mis servidores locales?
Sí. Azure RMS se puede integrar con sus servidores locales, como servidores de archivos de Exchange Server, SharePoint y Windows. Para hacerlo, use el [conector de Rights Management](../deploy-use/deploy-rms-connector.md). O bien, si solo le interesa usar la infraestructura de clasificación de archivos (FC) con Windows Server, puede usar los [cmdlets de protección de RMS](https://technet.microsoft.com/library/mt601315%28v=ws.10%29.aspx). También puede sincronizar y federar los controladores de dominio de Active Directory con Azure AD para ofrecer una experiencia de autenticación más sencilla a los usuarios, por ejemplo, mediante el uso de [Azure AD Connect](http://azure.microsoft.com/documentation/articles/active-directory-aadconnect/).

Azure RMS genera automáticamente y administra los certificados XrML según sea necesario, por lo que no usa una PKI local. Para obtener más información sobre la forma en que Azure RMS usa los certificados, consulte la sección [Walkthrough of how Azure RMS works: First use, content protection, content consumption](../understand-explore/how-does-it-work.md#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) (Tutorial del funcionamiento de Azure RMS: primer uso, protección de contenido, consumo de contenido) del artículo [How does Azure RMS work?](../understand-explore/how-does-it-work.md) (¿Cómo funciona Azure RMS?).

## Tengo una implementación híbrida de Exchange con algunos usuarios de Exchange Online y otros de Exchange Server. ¿Es compatible con Azure RMS?
Desde luego, y lo mejor es que los usuarios podrán proteger sin problemas y consumir correos electrónicos y archivos adjuntos protegidos en las dos implementaciones de Exchange. Para esta configuración, [active Azure RMS](../deploy-use/activate-service.md) y [habilite IRM para Exchange Online](https://technet.microsoft.com/library/dn151475%28v=exchg.150%29.aspx). A continuación, [implemente y configure el conector RMS](../deploy-use/deploy-rms-connector.md) para Exchange Server.

## ¿Hay instrucciones paso a paso para configurar Exchange Online para usar Azure RMS?

Sí. Consulte [Exchange Online: IRM Configuration](../deploy-use/configure-office365.md#exchange-online-irm-configuration.md ) (Exchange Online: Configuración de IRM) para ver un conjunto típico de comandos que permite a Exchange Online usar Azure RMS, la razón por la que Outlook Web App no muestra inmediatamente las opciones del menú **Establecer permisos** y el comando que debe ejecutar si cambia o actualiza las plantillas de Azure RMS. 

## Si implemento Azure RMS en producción, ¿estará mi empresa atada a la solución o se arriesgará a perder el acceso a los contenidos que protegimos con Azure RMS?
No, siempre tendrá el control de los datos y seguirá teniendo acceso a ellos, incluso si decide dejar de usar Azure RMS. Para obtener más información, consulte [Decommissioning and deactivating Azure Rights Management](../deploy-use/decommission-deactivate.md) (Retirada y desactivación de Azure Rights Management).

Sin embargo, antes de retirar la implementación de Azure RMS, nos gustaría conocer su opinión y comprender por qué tomó esta decisión. Si Azure RMS no satisface sus requisitos empresariales, consúltenos para informarse de si planeamos una funcionalidad nueva para el futuro cercano o si hay alternativas. Envíe un mensaje de correo electrónico a [AskIPTeam@Microsoft.com](mailto:askipteam@microsoft.com?subject=Planning%20to%20decommission%20Azure%20RMS) . Estaremos encantados de analizar sus requisitos técnicos y empresariales.

## ¿Puedo controlar quiénes de mis usuarios pueden usar Azure RMS para proteger el contenido?
Sí, Azure RMS tiene controles de incorporación de usuario para este escenario. Para obtener más información, consulte la sección [Configuring onboarding controls for a phased deployment](../deploy-use/activate-service.md#configuring-onboarding-controls-for-a-phased-deployment) (Configuración de controles de incorporación para una implementación por fases) del artículo [Activating Azure Rights Management](../deploy-use/activate-service.md) (Activar Azure Rights Management).

## ¿Se puede impedir que los usuarios compartan documentos protegidos con organizaciones específicas?
Una de las mayores ventajas de Azure RMS es que admite la colaboración de negocio a negocio sin tener que configurar relaciones de confianza explícitas para cada organización asociada, ya que Azure AD se encarga de la autenticación.

No hay ninguna opción de administración para impedir que los usuarios compartan documentos con organizaciones específicas de forma segura. Por ejemplo, supongamos que desea bloquear una organización en la que no confía o que tiene un negocio en competencia. Impedir que Azure RMS envíe documentos protegidos a los usuarios de estas organizaciones no tendría sentido, ya que los usuarios compartirían los documentos sin protección, lo que probablemente sea lo último que desea que ocurra en este escenario. Por ejemplo, no podría identificar quién comparte documentos confidenciales de la empresa ni con qué usuarios de esas organizaciones lo está haciendo, lo que sí es posible cuando el documento (o correo electrónico) está protegido con Azure RMS.

## Cuando comparto un documento protegido con una persona ajena a mi organización, ¿cómo se autentica ese usuario?
Azure RMS siempre usa una cuenta de Azure Active Directory y una dirección de correo electrónico asociada para la autenticación de usuarios, lo que facilita a los administradores la colaboración de negocio a negocio. Si la otra organización usa servicios de Azure, los usuarios ya tendrán cuentas en Azure Active Directory, incluso si dichas cuentas se crearon y se administraron localmente y después se sincronizaron con Azure.  Si la organización tiene Office 365 de forma encubierta, este servicio también usa Azure Active Directory para las cuentas de usuario.  Si la organización del usuario no tiene cuentas administradas en Azure, los usuarios pueden suscribirse a [RMS para usuarios](../understand-explore/rms-for-individuals.md), que crea un inquilino y un directorio de Azure no administrados para la organización con una cuenta para el usuario, de modo que este usuario se pueda autenticar para Azure RMS.

El método de autenticación de estas cuentas puede variar, en función de cómo configurase el administrador de la otra organización las cuentas de Azure Active Directory. Por ejemplo, podrían usar contraseñas creadas para estas cuentas, Multi-Factor Authentication (MFA), federación o contraseñas creadas en Servicios de dominio de Active Directory y después sincronizadas con Active Directory de Azure.

## ¿Puedo agregar usuarios ajenos a mi empresa a plantillas personalizadas?
Sí.  Si crea plantillas personalizadas que los usuarios finales (y los administradores) puedan seleccionar desde las aplicaciones, hará que les resulte más rápido y sencillo aplicar la protección de la información mediante las directivas predefinidas que especifique. Uno de los valores de la plantilla define quién puede acceder al contenido, y puede especificar usuarios y grupos de su organización y usuarios ajenos a su organización.

Para especificar usuarios de fuera de su organización, use el [módulo de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md):

-   **Use un objeto de Rights Definition para crear o actualizar una plantilla**.    especifique las direcciones de correo electrónico externas y sus derechos en un objeto de Rights Definition, que después usará para crear o actualizar una plantilla. Especifique el objeto de Rights Definition mediante el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) para crear una variable y después suministrar esta variable al parámetro -RightsDefinition con el cmdlet [Add-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727075.aspx) (para una nueva plantilla) o [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx) (si modifica una plantilla existente). Sin embargo, si agrega estos usuarios a una plantilla existente, tendrá que definir objetos de Rights Definition para los grupos existentes en las plantillas y no solo los usuarios externos.

Para obtener más información sobre las plantillas personalizadas, consulte [Configuring custom templates for Azure Rights Management](../deploy-use/configure-custom-templates.md) (Configurar plantillas personalizadas para Azure Rights Management).

## ¿Funciona Azure RMS con grupos dinámicos en Azure AD?
Una característica de Azure AD Premium le permite configurar la pertenencia dinámica para grupos mediante [reglas basadas en atributos](https://azure.microsoft.com/documentation/articles/active-directory-accessmanagement-groups-with-advanced-rules/). Cuando se crea un grupo de seguridad en Azure AD, este tipo de grupo admite la pertenencia dinámica pero no es compatible con una dirección de correo electrónico, por lo que no se puede usar con Azure RMS. Sin embargo, ahora puede crear un nuevo tipo de grupo en Azure AD que admita la pertenencia dinámica y que esté habilitado para correo. Cuando agrega un nuevo grupo en el Portal de Azure clásico, puede elegir **Office 365 Preview** como **TIPO DE GRUPO**. Dado que este grupo está habilitado para correo, puede usarlo con Azure RMS.

Como indica el nombre de la opción, este nuevo tipo de grupo todavía está en vista previa, pero se espera que próximamente tenga funcionalidades adicionales y documentación nueva. Hasta entonces, nos interesa confirmar que puede usar este nuevo tipo de grupo con Azure RMS.


## ¿Qué dispositivos y tipos de archivo admite Azure RMS?
Para obtener una lista de dispositivos compatibles, consulte [Client devices that support Azure RMS](../get-started/requirements-client-devices.md) (Dispositivos cliente que son compatibles con Azure RMS). Dado que, actualmente, no todos los dispositivos compatibles admiten todas las funcionalidades de RMS, consulte también la tabla [Client device capabilities](../get-started/requirements-client-devices.md#client-device-capabilities) (Funcionalidades de los dispositivos cliente) de este mismo artículo.

Azure RMS admite todos los tipos de archivo. Para archivos de texto, imagen, Microsoft Office (Word, Excel, PowerPoint), archivos .pdf y otros tipos de archivo de aplicaciones, Azure RMS proporciona protección nativa que incluye cifrado y cumplimiento de derechos (permisos). Para las demás aplicaciones y tipos de archivo, la protección genérica proporciona encapsulación de archivos y autenticación para comprobar si un usuario está autorizado para abrir el archivo.

Para obtener una lista de extensiones de nombre de archivo que se admiten de forma nativa en Azure RMS, consulte la sección [Supported file types and file name extensions](../rms-client/sharing-app-admin-guide-technical.md#supported-file-types-and-file-name-extensions) (Tipos de archivo y extensiones de nombre de archivo compatibles) en [Rights Management sharing application administrator guide](../rms-client/sharing-app-admin-guide.md) (Guía del administrador de la aplicación de uso compartido de Rights Management). Se admiten las extensiones de nombre de archivo que no están enumeradas si se usa la aplicación para uso compartido de RMS, que aplica automáticamente la protección genérica a estos archivos.

## Al abrir un documento de Office protegido con RMS, ¿también se protege con RMS el archivo temporal asociado?

No. En este caso, el archivo temporal asociado no contiene los datos del documento original, sino solo lo que escribe el usuario mientras el archivo está abierto. A diferencia del archivo original, el archivo temporal obviamente no está diseñado para el uso compartido y se conservará en el dispositivo, protegido mediante controles de seguridad local, como BitLocker y EFS.

## ¿Cuándo se admitirá la migración de AD RMS?
Inicialmente, Azure RMS no admitía la migración de una implementación local de Rights Management, como AD RMS. Pero ahora sí se admite.

Para obtener más información, consulte [Migrating from AD RMS to Azure Rights Management](../plan-design/migrate-from-ad-rms-to-azure-rms.md) (Migración de AD RMS a Azure Rights Management).

## Nos interesa usar BYOK con Azure RMS, pero por lo visto no es compatible con Exchange Online. ¿Qué nos aconsejan?
No permitan que esta limitación actual retrase su implementación de Azure RMS. Si tiene Exchange Online y desea usar Aportar su propia clave (BYOK), se recomienda implementar ahora Azure RMS en el modo de administración de claves predeterminado, donde Microsoft genera y administra su clave. De este modo, obtendrá todas las ventajas que supone proteger ahora sus archivos y mensajes de correo electrónico importantes, con la opción de pasarse a BYOK más adelante (por ejemplo, cuando Exchange Online admita BYOK).

Sin embargo, si las directivas de la empresa requieren que se use un módulo de seguridad de hardware (HSM) y esto podría bloquear la implementación de Azure RMS, otra opción es implementar ahora Azure RMS con BYOK, con una funcionalidad de RMS reducida para Exchange. Para obtener más información, consulte [BYOK pricing and restrictions](../plan-design/byok-price-restrictions.md) (Precios y restricciones de BYOK) en [Planning and implementing your Azure Rights Management tenant key](../plan-design/plan-implement-tenant-key.md) (Planeamiento e implementación de la clave de inquilino de Azure Rights Management).

## Una característica que me interesa no funciona con las bibliotecas protegidas de SharePoint. ¿Está prevista la compatibilidad con esta característica?
Actualmente, SharePoint es compatible con documentos protegidos de RMS mediante las bibliotecas protegidas de IRM, que no son compatibles con las plantillas personalizadas, el seguimiento de documentos y otras capacidades. Para obtener más información, consulte la sección [SharePoint Online and SharePoint Server](../understand-explore/office-apps-services-support.md#sharepoint-online-and-sharepoint-server) (SharePoint Online y SharePoint Server) del artículo [Office applications and services](../understand-explore/office-apps-services-support.md) (Aplicaciones y servicios de Office).

Si está interesado en una función específica que todavía no es compatible, no se pierda los anuncios que se publican en el [blog del equipo de RMS](http://blogs.technet.com/b/rms/).

## ¿Cómo configuro OneDrive para la Empresa en SharePoint Online para que los usuarios puedan compartir con seguridad sus archivos con personas de dentro y fuera de la empresa?
De forma predeterminada, como administrador de Office 365, no es usted quien lo configura; lo hacen los usuarios.

Del mismo modo que el administrador del sitio de SharePoint habilita y configura IRM para una biblioteca de SharePoint de su propiedad, OneDrive para la Empresa se ha diseñado para que los usuarios habiliten y configuren IRM para su propia biblioteca de OneDrive para la Empresa.  Sin embargo, gracias a PowerShell, puede hacerlo por ellos. Para obtener instrucciones, consulte la sección [SharePoint Online and OneDrive for Business: IRM Configuration](../deploy-use/configure-office365.md#sharepoint-online-and-onedrive-for-business-irm-configuration) (SharePoint Online y OneDrive para la Empresa: configuración de IRM) del artículo [Office 365: Configuration for clients and online services](../deploy-use/configure-office365.md) (Office 365: configuración para clientes y servicios en línea).

## ¿Hay trucos o sugerencias para una correcta implementación de RMS?
Después de supervisar muchas implementaciones y escuchar a nuestros clientes, socios, asesores e ingenieros de soporte, una de las mayores sugerencias que le podemos dar por la experiencia es: **Diseño e implementación de directivas de permisos sencillas**.

Dado que Azure RMS admite el uso compartido seguro con cualquiera, puede ser ambicioso con el alcance de la protección de la información. Pero debe ser conservador en cuanto a las directivas de derechos. Para muchas organizaciones, el mayor impacto comercial se centra en evitar las pérdidas de datos mediante la plantilla predeterminada de directivas de derechos que restringe el acceso a las personas de su organización. Claro que puede alcanzar un nivel mucho más pormenorizado si es necesario (evitar que los usuarios impriman, editen, etc.). Pero las restricciones más pormenorizadas deben ser la excepción para los documentos que realmente necesitan un alto nivel de seguridad. Además, no debe implementar estas directivas más restrictivas desde el primer día, sino que conviene planificar un enfoque más escalonado.

## ¿Qué características se pueden usar y cuáles no con las diferentes suscripciones de Azure RMS?
Para la suscripciones de pago que admiten Azure RMS (Office 365, Azure RMS Premium y Enterprise Mobility Suite), hay algunas diferencias en las características RMS que se admiten. Para obtener una lista, consulte [Comparación de las ofertas de Rights Management Services (RMS)](http://technet.microsoft.com/dn858608).

La suscripción gratuita compatible con Azure RMS (RMS Para individuos) admite el consumo de contenido que se ha protegido mediante Azure RMS. Para obtener más información, consulte [RMS for individuals and Azure Rights Management](../understand-explore/rms-for-individuals.md) (RMS para usuarios y Azure Rights Management).

## ¿Dónde puedo obtener información técnica sobre la suscripción gratuita de Azure RMS (RMS para usuarios), por ejemplo sobre cómo funciona, cómo controlar las cuentas y qué dominios no se pueden utilizar?
Encontrará respuestas a estas preguntas en [RMS for individuals and Azure Rights Management](../understand-explore/rms-for-individuals.md) (RMS para usuarios y Azure Rights Management) y en artículos relacionados.

## ¿Cómo recupero el acceso a los archivos que protegió un empleado que ya no trabaja en la organización?
Use la característica de superusuario de Azure RMS, que permite que los usuarios autorizados tengan derechos de propietario completos para todas las licencias de uso concedidas por el inquilino de RMS de su organización. Esta misma función permite que los servicios autorizados indicen e inspeccionen archivos, según sea necesario.

Para obtener más información, consulte [Configuring super users for Azure Rights Management and discovery services or data recovery](../deploy-use/configure-super-users.md) (Configuración de superusuarios para Azure Rights Management y los servicios de detección o la recuperación de datos).

## ¿Puede impedir Rights Management las capturas de pantalla?
Si no se concede el [derecho de uso](../deploy-use/configure-usage-rights.md) **Copiar**, Rights Management puede impedir las capturas de pantalla de muchas de las herramientas de captura de pantalla que se usan habitualmente en las plataformas Windows (Windows 7, Windows 8.1, Windows 10, Windows Phone) y Android. Sin embargo, los dispositivos iOS y Mac no permiten a ninguna aplicación impedir las capturas de pantalla y los navegadores (por ejemplo, cuando se usan con Outlook Web App y Office Online) tampoco pueden evitar las capturas de pantalla.

Impedir las capturas de pantalla puede ayudar a evitar la divulgación accidental o por negligencia de información confidencial. Sin embargo, existen muchas formas en que un usuario puede compartir datos que se muestran en una pantalla y hacer una captura de pantalla es solo un método. Por ejemplo, un usuario decidido a compartir la información mostrada puede tomar una foto de ella con su teléfono con cámara, volver a escribir los datos o simplemente transmitírsela verbalmente a alguien.

Como demuestran estos ejemplos, aunque todas las plataformas y todo el software admitieran las API de Rights Management para bloquear las capturas de pantalla, la tecnología por si sola no siempre puede impedir que los usuarios compartan datos que no deberían. Rights Management puede ayudar a proteger sus datos importantes mediante directivas de autorización y uso, pero esta solución de administración de derechos empresariales debe utilizarse con otros controles. Por ejemplo, implemente seguridad física, preste especial atención a aquellas personas con acceso autorizado a los datos de su organización e invierta en la educación de los usuarios para que sepan qué datos no deben compartir.

## ¿Dónde puedo encontrar información complementaria para Azure RMS, como información de tipo legal, de cumplimiento y contratos de nivel de servicio (SLA)?
Azure RMS admite otros servicios y también se basa en otros servicios. Si está buscando información relacionada con Azure RMS pero no acerca de cómo utilizar el servicio Azure RMS, compruebe los recursos siguientes:

**Información legal y privacidad:**

-   Para información contractual de Microsoft Azure: [Contrato de Microsoft Azure](http://azure.microsoft.com/support/legal/subscription-agreement/)

-   Para información de privacidad de Microsoft Azure: [Declaración de privacidad de Microsoft Azure](http://azure.microsoft.com/support/legal/privacy-statement/)

**Seguridad, cumplimiento y auditoría:**

Consulte la sección [Security, compliance, and regulatory requirements](../understand-explore/azure-rms-problems-it-solves.md#security-compliance-and-regulatory-requirements) (Requisitos de seguridad, normativos y regulatorios) del artículo [What problems does Azure RMS solve?](../understand-explore/azure-rms-problems-it-solves.md) (¿Qué problemas resuelve Azure RMS?). Además:

-   Para certificaciones externas de Azure RMS: [Centro de confianza de Microsoft Azure](http://azure.microsoft.com/support/trust-center/)

-   Para obtener información sobre FIPS 140: [Validación conforme a FIPS 140](https://technet.microsoft.com/library/security/cc750357.aspx)

**Contratos de nivel de servicio:**

-   Contrato de nivel de servicio para Azure RMS, por región seleccionada: [descárguelo de la página de búsqueda de licencias de productos](http://microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&amp;DocumentTypeId=37)

    - Por ejemplo, haga clic en **OnlineSvcsConsolidatedSLA(WW)(English)(March2016)** para descargar el contrato de nivel de servicio de marzo de 2016 para Norteamérica.

-   Contrato de nivel de servicio para Azure Active Directory: [Contratos de nivel de servicio](http://azure.microsoft.com/support/legal/sla/)

**Documentación:**

-   Sitio de documentación de Azure Active Directory: [Azure Active Directory](http://azure.microsoft.com/documentation/services/active-directory/)

-   Biblioteca de Azure Active Directory: [Azure Active Directory](http://msdn.microsoft.com/library/azure/jj673460.aspx)

-   Biblioteca de Office 365: [Office 365](http://technet.microsoft.com/library/dn127064%28v=office.14%29.aspx)

## ¿Qué debo hacer si mi pregunta no aparece aquí?
Use los vínculos y los recursos que aparecen en [Information and support for Azure Rights Management](information-support.md) (Información y servicio de atención de Azure Rights Management).

Además, hay preguntas frecuentes diseñadas para usuarios finales:

-   [Preguntas más frecuentes sobre la aplicación de uso compartido de Rights Management para Windows](https://technet.microsoft.com/dn467883)

-   [Preguntas frecuentes sobre la aplicación Rights Management sharing para plataformas Mac y móviles](https://technet.microsoft.com/dn451248)

-   [Preguntas más frecuentes sobre seguimiento de documentos](http://go.microsoft.com/fwlink/?LinkId=523977)

Esta página de Preguntas más frecuentes se actualizará regularmente, con nuevas adiciones enumeradas en los anuncios mensuales de actualización de la documentación en el blog del [equipo de Rights Management (RMS) de Microsoft](http://blogs.technet.com/b/rms/) .

> [!TIP] Use la [etiqueta docs](http://blogs.technet.com/b/rms/archive/tags/docs/) en el blog para encontrar estos anuncios sobre la documentación con más facilidad.




<!--HONumber=May16_HO2-->


