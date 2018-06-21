---
title: Clave de inquilino de Azure Information Protection
description: Información para ayudarle a planear y a administrar su clave de inquilino de Azure Information Protection. En lugar de que Microsoft administre su clave de inquilino (opción predeterminada), podría administrarla por su cuenta para cumplir con las normas específicas que se aplican a su organización. La administración de su propia clave de inquilino también se conoce aportar su propia clave, o BYOK, por sus siglas del inglés.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/05/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: f0d33c5f-a6a6-44a1-bdec-5be1bc8e1e14
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 714d00036d263cc64e44b67b547d743ff4cbab4b
ms.sourcegitcommit: dbbfadc72f4005f81c9f28c515119bc3098201ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
ms.locfileid: "30208658"
---
# <a name="planning-and-implementing-your-azure-information-protection-tenant-key"></a>Planeamiento e implementación de su clave de inquilino de Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Use la información de este artículo como ayuda para planear y administrar su clave de inquilino de Azure Information Protection. Por ejemplo, en lugar de que Microsoft administre su clave de inquilino (valor predeterminado), podría administrar su propia clave de inquilino para cumplir con las normas específicas que se aplican a su organización. La administración de su propia clave de inquilino también se conoce aportar su propia clave, o BYOK, por sus siglas del inglés.

¿Qué es la clave de inquilino de Azure Information Protection?

- La clave de inquilino de Azure Information Protection es una clave raíz para la organización. Se pueden derivar otras claves de esta clave raíz, como claves de usuario, claves de equipo y claves de cifrado de documentos. Cada vez que Azure Information Protection usa estas claves para la organización, se encadenan criptográficamente a la clave de inquilino de Azure Information Protection.

- La clave de inquilino de Azure Information Protection es el equivalente en línea de la clave de certificado emisor de licencias de servidor (SLC) de Active Directory Rights Management Services (AD RMS). 

**En resumen:** Use la tabla siguiente como guía rápida de la topología de clave de inquilino recomendada. A continuación, use documentación adicional para más información.

|Requisito empresarial|Topología de clave de inquilino recomendada|
|------------------------|-----------------------------------|
|Implementar Azure Information Protection rápidamente y sin hardware especial, software adicional o una suscripción de Azure.<br /><br />Por ejemplo: en entornos de prueba y cuando la organización no tiene requisitos normativos para la administración de claves.|Administrada por Microsoft|
|Normas de cumplimiento, seguridad adicional y control sobre todas las operaciones del ciclo de vida. <br /><br />Por ejemplo: la clave debe estar protegida por un módulo de seguridad de hardware (HSM).|BYOK [[1]](#footnote-1)|


Si es necesario, puede cambiar la topología de clave de inquilino tras realizar la implementación con el cmdlet [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties).


## <a name="choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok"></a>Elija su topología de clave de inquilino: Administrada por Microsoft (opción predeterminada) o por usted (BYOK)
Decide qué topología de clave de inquilino es la mejor para su organización. De forma predeterminada, Azure Information Protection genera su clave de inquilino y administra la mayoría de los aspectos del ciclo de vida de la clave de inquilino. Esta es la opción más simple con las mínimas sobrecargas administrativas. En la mayoría de casos, no es necesario ni tan siquiera que sepa que tiene una clave de inquilino. Simplemente, regístrese en Azure Information Protection y Microsoft se encargará del resto del proceso de administración de la clave.

Decide qué topología de clave de inquilino es la mejor para la organización:

- **Administrada por Microsoft**: Microsoft genera automáticamente una clave de inquilino para su organización que se usa exclusivamente para Azure Information Protection. De manera predeterminada, Microsoft usa esta clave para el inquilino y administra la mayoría de los aspectos del ciclo de vida de la clave de inquilino. 
    
    Esta es la opción más simple con las mínimas sobrecargas administrativas. En la mayoría de casos, no es necesario ni tan siquiera que sepa que tiene una clave de inquilino. Simplemente, regístrese en Azure Information Protection y Microsoft se encargará del resto del proceso de administración de la clave.

- **Administrada por el usuario (BYOK)**: para un control completo sobre su clave de inquilino, use [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) con Azure Information Protection. Para esta topología de clave de inquilino, cree la clave, ya sea directamente en Key Vault, o cree una local. Si la crea de forma local, después tiene que transferirla o importarla a Key Vault. Después, configure Azure Information Protection para que use esta clave y adminístrela en Azure Key Vault.
    

### <a name="more-information-about-byok"></a>Más información sobre BYOK
Tiene estas opciones para crear su propia clave:

- **Creación de una clave localmente y transferencia o importación a Key Vault**:
    
    - Una clave protegida por HSM que crea de forma local y después transfiere a Key Vault como una clave protegida por HSM.
    
    - Una clave protegida por software que crea de forma local, después la convierte y la transfiere a Key Vault como una clave protegida por HSM. Esta opción se admite solo cuando [migra desde Active Directory Rights Management Services (AD RMS)](migrate-from-ad-rms-to-azure-rms.md).
    
    - Una clave protegida por software que crea de forma local y después la importa a Key Vault como una clave protegida por software. Esta opción requiere un archivo de certificado .PFX.
    
- **Creación de una clave en Key Vault**:
    
    - Una clave protegida por HSM que se crea en Key Vault.
    
    - Una clave protegida por software que se crea en Key Vault.

De estas opciones de BYOK, la más habitual es la clave protegida por HSM que se crea de forma local y después se transfiere a Key Vault como una clave protegida por HSM. Aunque esta opción es la que tiene más sobrecarga administrativa, puede que la organización la exija para cumplir determinadas normas. Los HSM que usa Azure Key Vault son FIPS 140-2 nivel 2 validado.

Con esta opción, el proceso es:

1. Genere la clave de inquilino de forma local según sus directivas de seguridad y de TI. Esta clave es la copia maestra. Permanece almacenada de forma local y el usuario es el encargado de realizar copias de seguridad.

2. Cree una copia de esta clave y transfiérala de forma segura del HSM a Azure Key Vault. A lo largo de este proceso, la copia maestra de esta clave nunca traspasa la frontera de protección de hardware.

3. La copia de la clave está protegida por Azure Key Vault.

> [!NOTE]

> Como medida de protección adicional, Azure Key Vault usa dominios de seguridad independientes para sus centros de datos en regiones como Norteamérica, EMEA (Europa, Oriente Medio y África) y Asia. Azure Key Vault también usa distintas instancias de Azure, como Microsoft Azure Alemania y Azure Government. 

Aunque es opcional, es probable que quiera usar los registros de uso en tiempo casi real de Azure Information Protection para consultar exactamente cómo y cuándo se usa su clave de inquilino.

### <a name="when-you-have-decided-your-tenant-key-topology"></a>Cuando ha decidido la topología de clave de inquilino

Si decide dejar que Microsoft administre su clave de inquilino: 

- A menos que vaya a migrar desde AD RMS, no se necesita hacer nada más para generar la clave de inquilino y puede ir directamente a [Pasos siguientes](plan-implement-tenant-key.md#next-steps).

- Si ahora tiene AD RMS y quiere migrar a Azure Information Protection, use las instrucciones de migración de Migración desde AD RMS a Azure Information Protection. 

Si decide administrar usted mismo la clave de inquilino, lea las secciones siguientes para obtener más información.

## <a name="implementing-byok-for-your-azure-information-protection-tenant-key"></a>Implementación de BYOK para la clave de inquilino de Azure Information Protection

Usa la información y los procedimientos de esta sección si ha decidido generar y administrar su clave de inquilino; el escenario Aportar tu propia clave (BYOK):

> [!NOTE]
> Si se ha empezado a usar Azure Information Protection con una clave de inquilino que administra Microsoft y ahora quiere administrar su clave de inquilino (migrar a BYOK), los correos electrónicos y documentos protegidos con anterioridad seguirán estando accesibles mediante el uso de una clave archivada. 

### <a name="prerequisites-for-byok"></a>Requisitos previos para BYOK
Consulte la tabla siguiente para consultar una lista de requisitos previos para Aportar tu propia clave (BYOK).

|Requisito|Más información|
|---------------|--------------------|
|El inquilino de Azure Information Protection debe tener una suscripción de Azure. Si aún no tiene una, puede solicitar una [cuenta gratuita](https://azure.microsoft.com/pricing/free-trial/). <br /><br /> Para usar una clave protegida por HSM, debe tener el nivel de servicio Premium de Azure Key Vault.|La suscripción a Azure gratuita que proporciona acceso para configurar Azure Active Directory y la configuración de las plantillas personalizadas de Azure Rights Management (**acceso a Azure Active Directory**) no es suficiente para usar Azure Key Vault. Para confirmar que tiene una suscripción de Azure que puede usar para BYOK, use los cmdlets de PowerShell de [Azure Resource Manager](https://msdn.microsoft.com/library/azure/mt786812\(v=azure.300\).aspx): <br /><br /> 1. Inicie una sesión de Azure PowerShell con la opción **Ejecutar como administrador** e inicie sesión como administrador global para el inquilino de Azure Information Protection con el siguiente comando:`Login-AzureRmAccount`<br /><br />2. Escriba lo siguiente y confirme que ve los valores mostrados para su nombre e identificador de suscripción, así como su identificador de inquilino de Azure Information Protection, y que el estado está habilitado: `Get-AzureRmSubscription`<br /><br />Si no se muestra ningún valor y es redireccionado al símbolo del sistema, no tiene una suscripción de Azure que pueda utilizarse para BYOK. <br /><br />**Nota**: Además de los requisitos previos de BYOK, si migra de AD RMS a Azure Information Protection y cambia una clave de software por una clave de hardware, debe tener como mínimo la versión 11.62 del firmware de Thales.|
|Para usar una clave protegida por HSM creada localmente: todos los requisitos previos enumerados para BYOK de Key Vault. |Vea los [Requisitos previos de BYOK](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/#prerequisites-for-byok) en la documentación de Azure Key Vault. <br /><br /> **Nota**: Además de los requisitos previos de BYOK, si migra de AD RMS a Azure Information Protection y cambia una clave de software por una clave de hardware, debe tener como mínimo la versión 11.62 del firmware de Thales.|
|Módulo de administración de Azure Rights Management para Windows PowerShell.|Para obtener instrucciones de instalación, vea [Instalación del módulo de PowerShell para AADRM](../deploy-use/install-powershell.md). <br /><br />Si ya ha instalado este módulo de Windows PowerShell anteriormente, ejecute el comando siguiente para comprobar que el número de versión sea como mínimo **2.9.0.0**: `(Get-Module aadrm -ListAvailable).Version`|

Para obtener más información sobre los HSM de Thales y sobre su uso con el Almacén de claves de Azure, consulte el [sitio web de Thales](https://www.thales-esecurity.com/msrms/cloud).

### <a name="choosing-your-key-vault-location"></a>Elegir la ubicación del almacén de claves

Cuando crea un almacén de claves para almacenar la clave que usará como clave de inquilino para Azure Information Protection, debe especificar una ubicación. Esta ubicación es una región de Azure o una instancia de Azure.

Realice su elección primero por cumplimiento y luego para minimizar la latencia de red:

- Si ha elegido la topología de claves BYOK por motivos de cumplimiento, es posible que esos requisitos de cumplimiento exijan a la región de Azure o a la instancia de Azure que almacene la clave de inquilino de Azure Information Protection.

- Debido a todas las llamadas cifradas para la cadena de protección que se realizan a la clave de inquilino de Azure Information Protection, es preferible minimizar la latencia de red generada por estas llamadas. Para ello, cree el almacén de claves en la misma región o instancia de Azure que el inquilino de Azure Information Protection.

Para identificar la ubicación del inquilino de Azure Information Protection, use el cmdlet [Get-AadrmConfiguration](/powershell/module/aadrm/get-aadrmconfiguration) de PowerShell e identifique la región de las direcciones URL. Por ejemplo:

    LicensingIntranetDistributionPointUrl : https://5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com/_wmcs/licensing

La región se puede identificar a partir de **rms.na.aadrm.com** y, en este ejemplo, se encuentra en Norteamérica.

En la tabla de abajo podrá identificar qué región o instancia de Azure se recomienda para reducir al mínimo la latencia de red.

|Región o instancia de Azure|Ubicación recomendada para el almacén de claves|
|---------------|--------------------|
|rms.**na**.aadrm.com|**Centro y norte de EE. UU.** o **Este de EE. UU.**|
|rms.**eu**.aadrm.com|**Europa del Norte** o **Europa Occidental**|
|rms.**ap**.aadrm.com|**Asia Oriental** o **Sudeste Asiático**|
|rms.**sa**.aadrm.com|**Oeste de EE. UU.** o **Este de EE. UU.**|
|rms.**govus**.aadrm.com|**Centro de EE. UU.** o **Este de EE. UU. 2**|


### <a name="instructions-for-byok"></a>Instrucciones de BYOK

Use la documentación de Azure Key Vault para crear un almacén de claves y la clave que quiere usar para Azure Information Protection. Por ejemplo, vea [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started).

Asegúrese de que la longitud de clave es de 2048 bits (recomendada) o 1024 bits. Azure Information Protection no admite otras longitudes de clave.

Para crear una clave protegida por HSM de manera local y transferirla al almacén de claves como una clave protegida por HSM, siga los procedimientos de [Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/key-vault-hsm-protected-keys/).

Una clave que se almacena en Key Vault como un identificador de clave. Este identificador de clave es una URL que contiene el nombre del almacén de claves, el contenedor de claves, el nombre de la clave y la versión de la clave. Por ejemplo: **https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333**. Debe especificar la URL del almacén de claves en Azure Information Protection para configurarlo para que use esta clave.

Para que Azure Information Protection pueda usar la clave, deberá autorizar al servicio Azure Rights Management para que use la clave en el almacén de claves de su organización. Para hacerlo, el administrador de Azure Key Vault usa el cmdlet de PowerShell [Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) y concede permisos a la entidad de servicio de Azure Rights Management mediante el uso de GUID 00000012-0000-0000-c000-000000000000. Por ejemplo:

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoRMS-kv' -ResourceGroupName 'ContosoRMS-byok-rg' -ServicePrincipalName 00000012-0000-0000-c000-000000000000 -PermissionsToKeys decrypt,sign,get

Ahora lo tiene todo preparado para configurar Azure Information Protection y usar esta clave como la clave de inquilino de Azure Information Protection de la organización. Al usar cmdlets de Azure RMS, primero conéctese al servicio Azure Rights Management e inicie sesión:

    Connect-AadrmService

Después, ejecute el [cmdlet Use-AadrmKeyVaultKey](/powershell/module/aadrm/use-aadrmkeyvaultkey) y especifique la URL de clave. Por ejemplo:

    Use-AadrmKeyVaultKey -KeyVaultKeyUrl "https://contosorms-kv.vault.azure.net/keys/contosorms-byok/aaaabbbbcccc111122223333"

> [!IMPORTANT]
> En este ejemplo, "aaaabbbbcccc111122223333" es la versión de la clave que se va a usar. Si no se especifica la versión, se usa la versión actual de la clave sin avisar y el comando parece funcionar. En cambio, si la clave en Key Vault se actualiza posteriormente (se renueva), el servicio de Azure Rights Management dejará de funcionar para el inquilino, aunque vuelva a ejecutar el comando Use-AadrmKeyVaultKey.
>
>Asegúrese de que especifica la versión de la clave, además del nombre de clave al ejecutar este comando. Puede usar el cmd de Azure Key Vault, [Get-AzureKeyVaultKey](/powershell/module/azurerm.keyvault\get-azurekeyvaultkey), para obtener el número de versión de la clave actual. Por ejemplo: `Get-AzureKeyVaultKey -VaultName 'contosorms-kv' -KeyName 'contosorms-byok'`

Si necesita confirmar que la URL de la clave se ha configurado correctamente en Azure Information Protection: ejecute [Get-AzureKeyVaultKey](/powershell/module/azurerm.keyvault\get-azurekeyvaultkey) en Azure Key Vault para verla.

Por último, si el servicio Azure Rights Management ya está activado, ejecute [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) para indicar a Azure Information Protection que use esta clave como la clave de inquilino activa para el servicio Azure Rights Management. Si no completa este paso, Azure Information Protection seguirá usando la clave predeterminada administrada por Microsoft que creó automáticamente para el inquilino.


## <a name="next-steps"></a>Pasos siguientes

Después de planear y, si es necesario, crear y configurar la clave de inquilino, siga estos pasos:

1.  Empiece a usar su clave de inquilino:
    
    - Si no lo ha hecho todavía, deberá activar el servicio Rights Management para que su organización pueda empezar a usar Azure Information Protection. Los usuarios empiezan a usar inmediatamente la clave de inquilino (administrada por Microsoft o por usted en Azure Key Vault).
    
        Para más información sobre la activación, consulte [Activación de Azure Rights Management](../deploy-use/activate-service.md).
        
    - Si ya ha activado el servicio Rights Management y, a continuación, ha decidido administrar su propia clave de inquilino, los usuarios harán la transición gradualmente de la clave de inquilino antigua a la nueva. Esta transición escalonada puede tardar unas semanas en completarse. Documentos y archivos que se protegieron con la clave de inquilino antiguo siguen siendo accesibles a usuarios autorizados.
        
2. Considere la posibilidad de usar el registro de uso, que registra todas las transacciones que realiza el servicio Azure Rights Management.
    
    Si ha decidido administrar tu propia clave de inquilino, el registro incluye información acerca del uso de su clave de inquilino. Consulte el fragmento de código siguiente de un archivo de registro abierto en Excel, donde los tipos de solicitud **KeyVaultDecryptRequest** y **KeyVaultSignRequest** indican que la clave de inquilino está en uso.
    
    ![archivo de registro en Excel donde se usa la clave de inquilino](../media/RMS_Logging.png)
    
    Para obtener más información sobre el registro de uso, consulte [Registro y análisis del uso del servicio Azure Rights Management](../deploy-use/log-analyze-usage.md).
    
3.  Administre la clave de inquilino.
    
    Para más información sobre las operaciones del ciclo de vida de la clave de inquilino, vea [Operaciones para la clave de inquilino de Azure Information Protection](../deploy-use/operations-tenant-key.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]