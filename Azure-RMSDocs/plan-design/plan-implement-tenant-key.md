---
title: "Planeamiento e implementación de la clave de inquilino de Azure Rights Management | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a80866576dc7d6400bcebc2fc1c37bc0367bcdf3
ms.openlocfilehash: ee7b9b5f251856f102651f1e8f379f7bbacea77e


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

Como alternativa, puede tener un control total sobre la clave de inquilino con el [Almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/). Para este escenario es necesario crear una clave de inquilino y mantener la copia maestra de forma local. Con frecuencia este escenario también se conoce como Aportar tu propia clave (BYOK). Con esta opción, el proceso es:

1.  Genere la clave de inquilino de forma local según sus directivas de seguridad y de TI.

2.  Transfiera de forma segura la clave de inquilino desde un módulo de seguridad de hardware (HSM) de su propiedad a los HSM que administra y son propiedad de Microsoft con el Almacén de claves de Azure. A lo largo de este proceso, su clave de inquilino nunca traspasa la frontera de la protección del hardware.

3.  Al transferir su clave de inquilino a Microsoft, esta continúa protegida con el Almacén de claves de Azure.

Aunque es opcional, también querrá con toda probabilidad utilizar los registros de uso en tiempo casi real de Azure RMS para consultar cómo y cuándo exactamente se usa la clave de inquilino.

> [!NOTE]
> Como medida de protección adicional, el Almacén de claves de Azure usa dominios de seguridad independientes para sus centros de datos en regiones como Norteamérica, EMEA (Europa, Oriente Medio y África) y Asia. También para diferentes instancias de Azure, como Microsoft Azure Alemania y Azure Government. Si administra su propia clave de inquilino, estará vinculada al dominio de seguridad de la región o instancia donde se haya registrado el inquilino de RMS. Por ejemplo, una clave de inquilino de un cliente europeo no puede usarse en centros de datos de América del Norte o Asia.

## El ciclo de vida de la clave de inquilino
Si decide que Microsoft debe encargarse de administrar su clave de inquilino, se hará cargo de la mayoría de operaciones del ciclo de vida de la clave. Sin embargo, si decide administrar por su cuenta la clave de inquilino, será responsable de muchas de las operaciones del ciclo de vida de la clave y de algunos procedimientos adicionales en el Almacén de claves de Azure.

Los diagramas siguientes muestran y comparan estas dos opciones. El primer diagrama muestra las pocas sobrecargas de administrador que se dan en la configuración predeterminada cuando Microsoft administra la clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure RMS: administrado por Microsoft, valor predeterminado.](../media/RMS_BYOK_cloud.png)

El segundo diagrama muestra los pasos adicionales necesarios cuando eres tú el que administra su propia clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure RMS: administrado por el usuario, BYOK.](../media/RMS_BYOK_onprem4.png)

Si decide dejar que Microsoft administre su clave de inquilino, no se necesita hacer nada más para generar la clave y puede ir directamente a [Pasos siguientes](plan-implement-tenant-key.md#next-steps).

Si decide administrar usted mismo la clave de inquilino, lea las secciones siguientes para obtener más información.

## Planeación de la clave de inquilino de Azure Rights Management

Usa la información y los procedimientos de esta sección si ha decidido generar y administrar su clave de inquilino; el escenario Aportar tu propia clave (BYOK):


> [!IMPORTANT]
> Si ya ha empezado a usar [!INCLUDE[aad_rightsmanagement_1](../includes/aad_rightsmanagement_1_md.md)] (el servicio está activado) y tiene usuarios que ejecutan Office 2010, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) antes de ejecutar estos procedimientos. En función del escenario y las solicitudes, aún puede usar BYOK pero con algunas limitaciones o pasos adicionales.
> 
> [Póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) también si su organización tiene directivas específicas para el manejo de claves.

### Requisitos previos para BYOK
Consulte la tabla siguiente para consultar una lista de requisitos previos para Aportar tu propia clave (BYOK).

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción que admita Azure RMS.|Para más información sobre las suscripciones disponibles, consulte [Suscripciones en la nube que son compatibles con Azure RMS](../get-started/requirements-subscriptions.md).|
|No use RMS para individuos o Exchange Online. O bien, si usa Exchange Online, comprenda y acepte las limitaciones de uso de BYOK con esta configuración.|Para más información sobre las restricciones y limitaciones actuales para BYOK, vea [Precio y restricciones de BYOK](byok-price-restrictions.md).<br /><br />**Importante**: actualmente, BYOK no es compatible con Exchange Online.|
|Todos los requisitos previos indicados para el almacén de claves BYOK.|Vea [Requisitos previos de BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) en la documentación del Almacén de claves de Azure. <br /><br />**Nota**: Si migra de AD RMS a Azure RMS con una clave de software a una clave de hardware, necesita tener como mínimo la versión 11.62 del firmware de Thales.|
|El módulo de administración de Azure RMS para Windows PowerShell.|Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md). <br /><br />Si ya ha instalado este módulo de Windows PowerShell anteriormente, ejecute el comando siguiente para comprobar que el número de versión sea como mínimo **2.5.0.0**: `(Get-Module aadrm -ListAvailable).Version`|

Para obtener más información sobre los HSM de Thales y sobre su uso con el Almacén de claves de Azure, consulte el [sitio web de Thales](https://www.thales-esecurity.com/msrms/cloud).

Para generar y transferir su propia clave de inquilino al Almacén de claves de Azure, siga los procedimientos que se indican en [Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) en la documentación del Almacén de claves de Azure.

Cuando la clave se transfiere al almacén de claves, se le asigna un identificador de clave en el almacén de claves, que es una URL que contiene el nombre del almacén, el contenedor de claves, el nombre de la clave y la versión de la clave. Por ejemplo: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Necesitará configurar Azure RMS para que use esta clave (para hacerlo, especifique esta URL).

Sin embargo, antes de que Azure RMS pueda usar la clave, es necesario autorizar a Azure RMS para usar la clave en el almacén de claves de la organización. Para hacerlo, el administrador del Almacén de claves de Azure usa el cmdlet de PowerShell [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx) y concede permisos a la entidad de servicio de Azure RMS, **Microsoft.Azure.RMS**. Por ejemplo:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign 

Ahora está preparado para configurar Azure RMS y usar esta clave como la clave de inquilino de Azure RMS de la organización. Con los cmdlets de Azure RMS, primero conéctese al Azure RMS e inicie sesión:

    Connect-AadrmService

Después, ejecute el [cmdlet Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx) y especifique la URL de clave. Por ejemplo:

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

Si necesita confirmar que la URL de clave se ha configurado correctamente en Azure RMS, ejecute [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) en el Almacén de claves de Azure para ver la URL de clave.


## Pasos siguientes

Ahora que ha realizado la planeación, y si es necesario, ha generado su clave de inquilino, haga lo siguiente:

1.  Empiece a usar su clave de inquilino:

    -   Si no lo ha hecho todavía, debe activar Rights Management para que su organización pueda empezar a usar RMS. Los usuarios empiezan inmediatamente a usar su clave de inquilino (administrada por Microsoft o por su usuario en el Almacén de claves de Azure).

        Para más información sobre la activación, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

    -   Si ya has activado Rights Management y, a continuación, ha decidido administrar su propia clave de inquilino, los usuarios harán la transición gradualmente desde la clave de inquilino antigua hacia la clave de inquilino nueva, y esta transición escalonada puede tardar en acabarse unas cuantas semanas. Documentos y archivos que se protegieron con la clave de inquilino antiguo siguen siendo accesibles a usuarios autorizados.

2.  Puede usar el registro de uso, que registra todas las transacciones que realiza Azure Rights Management.

    Si ha decidido administrar tu propia clave de inquilino, el registro incluye información acerca del uso de su clave de inquilino. Consulte el fragmento de código siguiente de un archivo de registro abierto en Excel, donde los tipos de solicitud **KeyVaultDecryptRequest** y **KeyVaultSignRequest** indican que la clave de inquilino está en uso.

    ![archivo de registro en Excel donde se usa la clave de inquilino](../media/RMS_Logging.png)

    Para más información sobre el registro de uso, consulte [Registro y análisis del uso de Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Mantenga su clave de inquilino.

    Para más información, consulte [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Aug16_HO3-->


