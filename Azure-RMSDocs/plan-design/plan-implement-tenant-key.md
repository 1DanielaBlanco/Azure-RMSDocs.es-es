---
title: "Planeamiento e implementación de la clave de inquilino de Azure Rights Management | Azure Information Protection"
description: "Información para ayudarle a planear y a administrar su clave de inquilino de Azure Information Protection. En lugar de que Microsoft administre su clave de inquilino (opción predeterminada), podría administrarla por su cuenta para cumplir con las normas específicas que se aplican a su organización. La administración de su propia clave de inquilino también se conoce aportar su propia clave, o BYOK, por sus siglas del inglés."
author: cabailey
manager: mbaldwin
ms.date: 11/04/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d5b3f3fc473661022a4f17b6587d58a252d07d1a
ms.openlocfilehash: b8380389267d77da53a5b87ffd606b6e754de7f3


---

# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Planeamiento e implementación de su clave de inquilino de Azure Information Protection

>*Se aplica a: Azure Information Protection, Office 365*

Use la información de este artículo como ayuda para planear y administrar su clave de inquilino de Azure Information Protection. Por ejemplo, en lugar de que Microsoft administre su clave de inquilino (valor predeterminado), podría administrar su propia clave de inquilino para cumplir con las normas específicas que se aplican a su organización. La administración de su propia clave de inquilino también se conoce aportar su propia clave, o BYOK, por sus siglas del inglés.

> [!NOTE]
> El equivalente local de la clave de inquilino de Azure Information Protection se conoce como la clave del Certificado emisor de licencias de servidor (SLC). Azure Information Protection conserva una o varias claves para cada organización que tenga una suscripción a Azure Information Protection. Siempre que se usan claves para Azure Information Protection en una organización (como por ejemplo claves de usuario, claves de equipo o claves de cifrado de documentos), se encadenan criptográficamente a su clave de inquilino de Azure Information Protection.

**En resumen:** Use la tabla siguiente como guía rápida de la topología de clave de inquilino recomendada. A continuación, use documentación adicional para más información.

Si implementa Azure Information Protection mediante una clave de inquilino que administre Microsoft, podrá cambiar más adelante a BYOK. Sin embargo, actualmente no puede cambiar su clave de inquilino de Azure Information Protection de BYOK a la opción de que la administre Microsoft.

|Requisito empresarial|Topología de clave de inquilino recomendada|
|------------------------|-----------------------------------|
|Implementar Azure Information Protection rápidamente y sin necesidad de hardware especial|Administrada por Microsoft|
|Necesidad de funcionalidad completa en Exchange Online con el servicio Azure Rights Management|Administrada por Microsoft|
|Las claves las crea el usuario y están protegidas en un módulo de seguridad de hardware (HSM).|BYOK<br /><br />Actualmente, esta configuración dará lugar a funcionalidad reducida de IRM en Exchange Online. Para más información, consulte [Precio y restricciones de BYOK](byok-price-restrictions.md).|

## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Elija su topología de clave de inquilino: Administrada por Microsoft (opción predeterminada) o por usted (BYOK)
Decide qué topología de clave de inquilino es la mejor para su organización. De forma predeterminada, Azure Information Protection genera su clave de inquilino y administra la mayoría de los aspectos del ciclo de vida de la clave de inquilino. Esta es la opción más simple con las mínimas sobrecargas administrativas. En la mayoría de casos, no es necesario ni tan siquiera que sepa que tiene una clave de inquilino. Simplemente, regístrese en Azure Information Protection y Microsoft se encargará del resto del proceso de administración de la clave.

Como alternativa, puede tener un control total sobre la clave de inquilino con el [Almacén de claves de Azure](https://azure.microsoft.com/services/key-vault/). Para este escenario es necesario crear una clave de inquilino y mantener la copia maestra de forma local. Con frecuencia este escenario también se conoce como Aportar tu propia clave (BYOK). Con esta opción, el proceso es:

1.  Genere la clave de inquilino de forma local según sus directivas de seguridad y de TI.

2.  Transfiera de forma segura la clave de inquilino desde un módulo de seguridad de hardware (HSM) de su propiedad a los HSM que administra y son propiedad de Microsoft con el Almacén de claves de Azure. A lo largo de este proceso, su clave de inquilino nunca traspasa la frontera de la protección del hardware.

3.  Al transferir su clave de inquilino a Microsoft, esta continúa protegida con el Almacén de claves de Azure.

Aunque es opcional, es probable que quiera usar los registros de uso en tiempo casi real de Azure Information Protection para consultar exactamente cómo y cuándo se usa su clave de inquilino.

> [!NOTE]
> Como medida de protección adicional, el Almacén de claves de Azure usa dominios de seguridad independientes para sus centros de datos en regiones como Norteamérica, EMEA (Europa, Oriente Medio y África) y Asia. También para diferentes instancias de Azure, como Microsoft Azure Alemania y Azure Government. Si administra su propia clave de inquilino, estará vinculada al dominio de seguridad de la región o instancia donde se haya registrado el inquilino de Azure Information Protection. Por ejemplo, una clave de inquilino de un cliente europeo no puede usarse en centros de datos de América del Norte o Asia.

## <a name="the-tenant-key-lifecycle"></a>El ciclo de vida de la clave de inquilino
Si decide que Microsoft debe encargarse de administrar su clave de inquilino, se hará cargo de la mayoría de operaciones del ciclo de vida de la clave. Sin embargo, si decide administrar por su cuenta la clave de inquilino, será responsable de muchas de las operaciones del ciclo de vida de la clave y de algunos procedimientos adicionales en el Almacén de claves de Azure.

Los diagramas siguientes muestran y comparan estas dos opciones. El primer diagrama muestra las pocas sobrecargas de administrador que se dan en la configuración predeterminada cuando Microsoft administra la clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure Information Protection (la opción predeterminada que administra Microsoft)](../media/RMS_BYOK_cloud.png)

El segundo diagrama muestra los pasos adicionales necesarios cuando eres tú el que administra su propia clave de inquilino.

![Ciclo de vida de la clave de inquilino de Azure Information Protection (la que administra su usuario, BYOK)](../media/RMS_BYOK_onprem4.png)

Si decide dejar que Microsoft administre su clave de inquilino, no se necesita hacer nada más para generar la clave y puede ir directamente a [Pasos siguientes](plan-implement-tenant-key.md#next-steps).  

Si decide administrar usted mismo la clave de inquilino, lea las secciones siguientes para obtener más información.

## <a name="implementing-your-azure-information-protection-tenant-key"></a>Implementación de su clave de inquilino de Azure Information Protection

Usa la información y los procedimientos de esta sección si ha decidido generar y administrar su clave de inquilino; el escenario Aportar tu propia clave (BYOK):


> [!IMPORTANT]
> Si se ha empezado a usar Azure Information Protection con una clave de inquilino que administra Microsoft y ahora quiere administrar su clave de inquilino (migrar a BYOK), los correos electrónicos y documentos protegidos con anterioridad seguirán estando accesibles mediante el uso de una clave archivada. Sin embargo, si tiene usuarios que ejecutan Office 2010, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) antes de ejecutar estos procedimientos. Estos equipos necesitan algunos pasos de configuración adicionales.
> 
> [Póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) también si su organización tiene directivas específicas para el manejo de claves.

### <a name="prerequisites-for-byok"></a>Requisitos previos para BYOK
Consulte la tabla siguiente para consultar una lista de requisitos previos para Aportar tu propia clave (BYOK).

|Requisito|Más información|
|---------------|--------------------|
|Una suscripción que admita Azure Information Protection.|Para obtener más información acerca de las suscripciones disponibles, consulte la [página de precios](https://go.microsoft.com/fwlink/?LinkId=827589) de Azure Information Protection.|
|No use RMS para individuos o Exchange Online. O bien, si usa Exchange Online, comprenda y acepte las limitaciones de uso de BYOK con esta configuración.|Para más información sobre las restricciones y limitaciones actuales para BYOK, vea [Precio y restricciones de BYOK](byok-price-restrictions.md).<br /><br />**Importante**: actualmente, BYOK no es compatible con Exchange Online.|
|Todos los requisitos previos para BYOK de Key Vault, que incluye una suscripción a Azure de pago o de prueba. |Vea los [Requisitos previos de BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) en la documentación de Azure Key Vault. <br /><br /> La suscripción a Azure gratuita que proporciona acceso para configurar Azure Active Directory y la configuración de las plantillas personalizadas de Azure Rights Management (**acceso a Azure Active Directory**) no es suficiente para usar Azure Key Vault. Para confirmar que tiene una suscripción de Azure que puede usar para BYOK, use los cmdlets de PowerShell de [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx): <br /><br /> 1. Empiece una sesión de Azure PowerShell e inicie sesión en su cuenta de Azure mediante el comando siguiente: `Login-AzureRmAccount`<br /><br />2. Escriba lo siguiente y confirme que ve los valores mostrados para su nombre e ID de suscripción, así como su ID de inquilino, y que el estado está habilitado: `Get-AzureRmSubscription`<br /><br />Si no se muestra ningún valor y es redireccionado al símbolo del sistema, no tiene una suscripción de Azure que pueda utilizarse para BYOK. <br /><br />**Nota**: Además de los requisitos previos de BYOK, si migra de AD RMS a Azure Information Protection y cambia una clave de software por una clave de hardware, debe tener como mínimo la versión 11.62 del firmware de Thales.|
|Módulo de administración de Azure Rights Management para Windows PowerShell.|Para obtener instrucciones de instalación, consulte [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md). <br /><br />Si ya ha instalado este módulo de Windows PowerShell anteriormente, ejecute el comando siguiente para comprobar que el número de versión sea como mínimo **2.5.0.0**: `(Get-Module aadrm -ListAvailable).Version`|

Para obtener más información sobre los HSM de Thales y sobre su uso con el Almacén de claves de Azure, consulte el [sitio web de Thales](https://www.thales-esecurity.com/msrms/cloud).

Para generar y transferir su propia clave de inquilino al Almacén de claves de Azure, siga los procedimientos que se indican en [Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/) en la documentación del Almacén de claves de Azure.

Cuando la clave se transfiere al almacén de claves, se le asigna un identificador de clave en el almacén de claves, que es una URL que contiene el nombre del almacén, el contenedor de claves, el nombre de la clave y la versión de la clave. Por ejemplo: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Deberá indicar al servicio Azure Rights Management de Azure Information Protection que use esta clave mediante la especificación de esta URL.

Pero para que Azure Information Protection pueda usar la clave, deberá autorizar al servicio Azure Rights Management para que use la clave en el almacén de claves de su organización. Para llevar a cabo esta acción, el administrador de Azure Key Vault usa el cmdlet de PowerShell para Azure Key Vault [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/es-es/library/mt603625(v=azure.300\).aspx) y concede permisos a la entidad de servicio de Azure Rights Management, **Microsoft.Azure.RMS**. Por ejemplo:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName Microsoft.Azure.RMS -PermissionsToKeys decrypt,encrypt,unwrapkey,wrapkey,verify,sign,get

Ahora lo tiene todo preparado para configurar Azure Information Protection y usar esta clave como la clave de inquilino de Azure Information Protection de la organización. Al usar cmdlets de Azure RMS, primero conéctese al servicio Azure Rights Management e inicie sesión:

    Connect-AadrmService

Después, ejecute el [cmdlet Use-AadrmKeyVaultKey](https://msdn.microsoft.com/library/azure/mt759829.aspx) y especifique la URL de clave. Por ejemplo:

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

Si necesita confirmar que la URL de clave se ha configurado correctamente en el servicio Azure RMS, ejecute [Get-AzureKeyVaultKey] (https://msdn.microsoft.com/en-us/library/dn868053(v=azure.300\).aspx) en Azure Key Vault para verla.


## <a name="next-steps"></a>Pasos siguientes

Ahora que ha realizado la planeación, y si es necesario, ha generado su clave de inquilino, haga lo siguiente:

1.  Empiece a usar su clave de inquilino:

    -   Si no lo ha hecho todavía, deberá activar el servicio Rights Management para que su organización pueda empezar a usar Azure Information Protection. Los usuarios empiezan inmediatamente a usar su clave de inquilino (administrada por Microsoft o por su usuario en el Almacén de claves de Azure).

        Para más información sobre la activación, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).

    -   Si ya ha activado el servicio Rights Management y, a continuación, ha decidido administrar su propia clave de inquilino, los usuarios harán la transición gradualmente de la clave de inquilino antigua a la nueva. Esta transición escalonada puede tardar unas semanas en completarse. Documentos y archivos que se protegieron con la clave de inquilino antiguo siguen siendo accesibles a usuarios autorizados.

2.  Considere la posibilidad de usar el registro de uso, que registra todas las transacciones que realiza el servicio Azure Rights Management.

    Si ha decidido administrar tu propia clave de inquilino, el registro incluye información acerca del uso de su clave de inquilino. Consulte el fragmento de código siguiente de un archivo de registro abierto en Excel, donde los tipos de solicitud **KeyVaultDecryptRequest** y **KeyVaultSignRequest** indican que la clave de inquilino está en uso.

    ![archivo de registro en Excel donde se usa la clave de inquilino](../media/RMS_Logging.png)

    Para obtener más información sobre el registro de uso, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).

3.  Mantenga su clave de inquilino.

    Para más información, consulte [Operaciones para la clave de inquilino de Azure Rights Management](../deploy-use/operations-tenant-key.md).




<!--HONumber=Nov16_HO1-->


