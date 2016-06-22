---
# required metadata

title: Planeamiento e implementación de la clave de inquilino de Azure Rights Management | Azure RMS
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Planeamiento e implementación de la clave de inquilino de Azure Rights Management

*Se aplica a: Azure Rights Management, Office 365*

Use la información de este artículo para tratar de planificar y administrar la clave de inquilino de Rights Management (RMS) para Azure RMS. Por ejemplo, en lugar de que Microsoft administre su clave de inquilino (valor predeterminado), podría administrar su propia clave de inquilino para cumplir con las normas específicas que se aplican a su organización.  La administración de su propia clave de inquilino también se conoce aportar su propia clave, o BYOK, por sus siglas del inglés.

> [!NOTE]
> También se conoce a la clave de inquilino de RMS como la clave del Certificado emisor de licencias de servidor (SLC). Azure RMS mantiene una clave o más para cada organización que se suscribe a Azure RMS. Siempre que se usa una clave para RMS en una organización (como por ejemplo claves de usuario, claves del equipo, claves de cifrado de documentos), se encadena criptográficamente a su clave de inquilino de RMS.

**En resumen:** Use la tabla siguiente como guía rápida de la topología de clave de inquilino recomendada. A continuación, use documentación adicional para más información.

Si implementa Azure RMS mediante una clave de inquilino administrada por Microsoft, puede cambiar más adelante a BYOK. Sin embargo, actualmente no puede cambiar su clave de inquilino de Azure RMS de BYOK a administrada por Microsoft.

|Requisito empresarial|Topología de clave de inquilino recomendada|
|------------------------|-----------------------------------|
|Implementación de Azure RMS rápidamente y sin necesidad de hardware especial|Administrada por Microsoft|
|Necesidad de funcionalidad completa en Exchange Online con Azure RMS|Administrada por Microsoft|
|Las claves las crea el usuario y están protegidas en un módulo de seguridad de hardware (HSM).|BYOK<br /><br />Actualmente, esta configuración dará lugar a funcionalidad reducida de IRM en Exchange Online. Para más información, consulte [Precio y restricciones de BYOK](byok-price-restrictions.md).|

## Elija su topología de clave de inquilino: Administrada por Microsoft (opción predeterminada) o por usted (BYOK)
Decide qué topología de clave de inquilino es la mejor para su organización. De forma predeterminada, Azure RMS genera su clave de inquilino y administra la mayoría de aspectos del ciclo de vida de la clave de inquilino. Esta es la opción más simple con las mínimas sobrecargas administrativas. En la mayoría de casos, no es necesario ni tan siquiera que sepa que tiene una clave de inquilino. Simplemente regístrese para Azure RMS y el resto del proceso de administración de la clave será manejado por Microsoft.

De otra forma, podría querer poseer control absoluto sobre tu clave de inquilino, lo que implica la creación de su clave de inquilino y mantener la copia maestra en su infraestructura local. Con frecuencia este escenario también se conoce como Aportar tu propia clave (BYOK). Con esta opción, el proceso es:

1.  Genera su clave de inquilino en la infraestructura local, en línea con sus políticas de TI.

2.  Transfiere de forma segura la clave de inquilino desde un módulo de seguridad de hardware (HSM) que posea hasta los HSM que posee y administra Microsoft. A lo largo de este proceso, su clave de inquilino nunca traspasa la frontera de la protección del hardware.

3.  Cuando transfiere su clave de inquilino a Microsoft, esta continúa protegida gracias a los módulos HSM Thales. Microsoft ha trabajado con Thales a fin de garantizar que su clave de inquilino no se puede extraer de los HSM de Microsoft.

Aunque es opcional, también querrá con toda probabilidad utilizar los registros de uso en tiempo casi real de Azure RMS para consultar cómo y cuándo exactamente se usa la clave de inquilino.

> [!NOTE]
> Como medida de protección adicional, Azure RMS utiliza espacios de seguridad independientes para sus centros de datos en América del Norte, EMEA (Europa, Oriente Medio y África) y Asia. Cuando administra su propia clave de inquilino, está ligada al espacio de seguridad de la región en que está registrado el inquilino de RMS. Por ejemplo, una clave de inquilino de un cliente europeo no puede usarse en centros de datos de América del Norte o Asia.

## El ciclo de vida de la clave de inquilino
Si decide que Microsoft debe encargarse de administrar su clave de inquilino, se hará cargo de la mayoría de operaciones del ciclo de vida de la clave. Sin embargo, si decide administrar usted mismo la clave de inquilino, será el responsable de muchas de las operaciones del ciclo de vida de la clave y de algunos procedimientos adicionales.

Los diagramas siguientes muestran y comparan estas dos opciones. El primer diagrama muestra las pocas sobrecargas de administrador que se dan en la configuración predeterminada cuando Microsoft administra la clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure RMS: administrado por Microsoft, valor predeterminado.](../media/RMS_BYOK_cloud.png)

El segundo diagrama muestra los pasos adicionales necesarios cuando eres tú el que administra su propia clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure RMS: administrado por el usuario, BYOK.](../media/RMS_BYOK_onprem.png)

Si decide dejar que Microsoft administre su clave de inquilino, no se necesita hacer nada más para generar la clave y puede ir directamente a [Pasos siguientes](plan-implement-tenant-key.md#next-steps).

Si decide administrar usted mismo la clave de inquilino, lea las secciones siguientes para obtener más información.

## Planeación de la clave de inquilino de Azure Rights Management

Usa la información y los procedimientos de esta sección si ha decidido generar y administrar su clave de inquilino; el escenario Aportar tu propia clave (BYOK):


> [!IMPORTANT]
> Si ya ha empezado a usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (el servicio está activado) y tiene usuarios que ejecutan Office 2010, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support#to-contact-microsoft-support) antes de ejecutar estos procedimientos. En función del escenario y las solicitudes, aún puede usar BYOK pero con algunas limitaciones o pasos adicionales.
> 
> [Póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support#to-contact-microsoft-support) también si su organización tiene directivas específicas para el manejo de claves.

### Requisitos previos para BYOK
Consulte la tabla siguiente para consultar una lista de requisitos previos para Aportar tu propia clave (BYOK).

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción que admita Azure RMS.|Para más información sobre las suscripciones disponibles, consulte [Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md).|
|No use RMS para individuos o Exchange Online. O bien, si usa Exchange Online, comprenda y acepte las limitaciones de uso de BYOK con esta configuración.|Para más información sobre las restricciones y limitaciones actuales para BYOK, vea [Precio y restricciones de BYOK](byok-price-restrictions.md).<br /><br />**Importante**: actualmente, BYOK no es compatible con Exchange Online.|
|HSM de Thales, tarjetas inteligentes y software de soporte.<br /><br />**Nota**: Si migra de AD RMS a Azure RMS mediante una clave de software a una clave de hardware, debe tener como mínimo una versión 11.62 de los controladores de Thales.|Debe tener acceso al módulo de seguridad de hardware de Thales y al conocimiento operacional básico de los HSM de Thales. Vea [Módulo de seguridad de hardware de Thales](http://www.thales-esecurity.com/msrms/buy) para ver la lista de modelos compatibles o para comprar un HSM si no tiene ninguno.|
|Si quiere transferir su clave de inquilino a través de Internet en lugar de encontrarse presente físicamente en Redmond, EE. UU., hay tres requisitos:<br /><br />1: Una estación de trabajo sin conexión x64 con un sistema operativo Windows 7 como mínimo y un software Thales nShield que sea como mínimo la versión 11.62.<br /><br />Si esta estación de trabajo funciona con Windows 7, debe [instalar Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkId=225702).<br /><br />2: Una estación de trabajo que esté conectada a Internet y tenga un sistema operativo Windows 7 como mínimo.<br /><br />3: Una unidad USB u otro dispositivo de almacenamiento portátil que tenga al menos un espacio libre de 16 MB.|Estos requisitos previos no son necesarios si viajas a Redmond y transfiere su clave de inquilino en persona.<br /><br />Por motivos de seguridad, recomendamos que la primera estación de trabajo no esté conectada a una red. Sin embargo, esto no es de obligado cumplimiento.<br /><br />Nota: En las instrucciones que se indican a continuación, a esta primera estación de trabajo se la conoce como la **estación de trabajo desconectada**.<br /><br />Además, si la clave de inquilino es para una red de producción, es recomendable que use una segunda estación de trabajo independiente para descargar el conjunto de herramientas y cargar la clave de inquilino. Sin embargo, con el fin de realizar una prueba, puede usar la misma estación de trabajo como la primera.<br /><br />Nota: En las instrucciones que se indican a continuación, a esta segunda estación de trabajo se la conoce como la **estación de trabajo conectada a Internet**.|

Los procedimientos para generar y usar su propia clave de inquilino dependen de si desea hacerlo a través de Internet o en persona:

-   **A través de Internet:** Este procedimiento requiere algunos pasos adicionales sobre la configuración, como la descarga y el uso de un conjunto de herramientas y los cmdlets de Windows PowerShell. Sin embargo, no tiene que encontrarse físicamente en una instalación de Microsoft para transferir su clave de inquilino. Se conserva la seguridad mediante los métodos siguientes:

    -   Genera la clave de inquilino desde una estación de trabajo fuera de línea, lo que reduce la superficie de ataque.

    -   La clave de inquilino está cifrada con una Clave de intercambio de claves (KEK), que permanece cifrada hasta que se transfiere a los HSM de Azure RMS. Solo la versión cifrada de su clave de inquilino abandona la estación de trabajo original.

    -   Una herramienta establece las propiedades de su clave de inquilino que enlaza su clave de inquilino con el mundo de seguridad de Azure RMS. De modo que, después de que los HSM de Azure RMS reciban y descifren su clave de inquilino, sean solamente dichos HSM los que puedan usarla. No se puede exportar su clave de inquilino. Este enlace es impuesto por los HSM de Thales.

    -   La Clave de intercambio de claves (KEK) que se usa para cifrar tu clave de inquilino se genera dentro de los HSM de Azure RMS y no es exportable. Los HSM provocan que no pueda haber una versión neta de la KEK fuera de los HSM. Además, el conjunto de herramientas incluye la atestación desde Thales de que la KEK no es exportable y se generó dentro de un HSM genuino que fabricó Thales.

    -   El conjunto de herramientas incluye la atestación desde Thales de que el universo de seguridad de Azure RMS también se generó en un HSM genuino fabricado por Thales. Así se demuestra que Microsoft usa hardware genuino.

    -   Microsoft usa KEK independientes, así como Universos de seguridad independientes en cada región geográfica, lo cual garantiza que su clave de inquilino pueda usarse solamente en centros de datos de la región en que se ha cifrado. Por ejemplo, una clave de inquilino de un cliente europeo no puede usarse en centros de datos de América del Norte o Asia.

    > [!NOTE]
    > Su clave de inquilino se puede transferir con seguridad a través de equipos y redes que no son de confianza porque está cifrada y es segura con permisos de nivel de control de acceso, que hacen que solo se pueda usar dentro de tus HSM y los HSM de Microsoft para Azure RMS. Puede usar los scripts proporcionados en el conjunto de herramientas para comprobar las medidas de seguridad y leer más información acerca de cómo funciona en Thales: [Administración de la clave de hardware en la nube de RMS Cloud](https://www.thales-esecurity.com/knowledge-base/white-papers/hardware-key-management-in-the-rms-cloud).

-   **En persona:** este método precisa que se [ponga en contacto con el soporte técnico de Microsoft](../get-started/information-support#to-contact-microsoft-support) para programar una cita a fin de transferir la clave para Azure RMS. Debe viajar a la oficina de Microsoft en Redmond, Washington, Estados Unidos de América, para transferir su clave de inquilino al universo de seguridad de Azure RMS.

Para obtener instrucciones sobre procedimientos, seleccione si va a generar y transferir la clave de inquilino a través de Internet o en persona: 

- [A través de Internet](generate-tenant-key-internet.md)
- [En persona](generate-tenant-key-in-person.md)


## Pasos siguientes

Ahora que ha realizado la planeación, y si es necesario, ha generado su clave de inquilino, haga lo siguiente:

1.  Empiece a usar su clave de inquilino:

    -   Si no lo ha hecho todavía, debe activar Rights Management para que su organización pueda empezar a usar RMS. Los usuarios empiezan a usar su clave de inquilino (administrada por Microsoft o por ti).

        Para más información sobre la activación, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

    -   Si ya has activado Rights Management y, a continuación, ha decidido administrar su propia clave de inquilino, los usuarios harán la transición gradualmente desde la clave de inquilino antigua hacia la clave de inquilino nueva, y esta transición escalonada puede tardar en acabarse unas cuantas semanas. Documentos y archivos que se protegieron con la clave de inquilino antiguo siguen siendo accesibles a usuarios autorizados.

2.  Considere la utilización del registro de uso, que registra todas las transacciones que lleva a cabo RMS.

    Si ha decidido administrar tu propia clave de inquilino, el registro incluye información acerca del uso de su clave de inquilino. Vea el ejemplo siguiente de un archivo de registro que se muestra en Excel, donde los tipos de solicitud **Decrypt** y **SignDigest** muestran que se está usando la clave de inquilino.

    ![archivo de registro en Excel donde se usa la clave de inquilino](../media/RMS_Logging.gif)

    Para más información sobre el registro de uso, consulte [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Mantenga su clave de inquilino.

    Para más información, consulte [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).



<!--HONumber=Jun16_HO2-->


