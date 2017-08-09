---
title: "Migración de AD RMS-Azure Information Protection: fase 2"
description: "Fase 2 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos del 4 al 6 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 07/31/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 9f04698064037343719d274e793eb560b703b031
ms.sourcegitcommit: 55a71f83947e7b178930aaa85a8716e993ffc063
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2017
---
# <a name="migration-phase-2---server-side-configuration-for-ad-rms"></a>Fase 2 de la migración: configuración del lado servidor para AD RMS

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use la información siguiente para la fase 2 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos del 4 al 6 del tema [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>Paso 4. Exportar los datos de configuración de AD RMS e importarlos en Azure Information Protection
Este paso es un proceso de dos fases:

1. Exporte los datos de configuración de AD RMS mediante la exportación de los dominios de publicación de confianza (TPD) a un archivo .xml. Este proceso es el mismo para todas las migraciones.

2. Importe los datos de configuración en Azure Information Protection. Hay diferentes procesos para este paso, según la configuración de la implementación de AD RMS actual y la topología preferida para su clave de inquilino de Azure RMS.

### <a name="export-the-configuration-data-from-ad-rms"></a>Exportar los datos de configuración de AD RMS

Siga este procedimiento en todos los clústeres de AD RMS, para todos los dominios de publicación confianza que tienen contenido protegido de su organización. No es necesario ejecutar este procedimiento en clústeres solo para licencias.

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>Para exportar los datos de configuración (información del dominio de publicación de confianza)

1. Inicie sesión en el clúster de AD RMS como un usuario con permisos de administración de AD RMS.

2. Desde la consola de administración de AD RMS (**Active Directory Rights Management Services**), expanda el nombre del clúster de AD RMS, expanda **Directivas de confianza**y luego haga clic en **Dominios de publicación de confianza**.

3. En el panel de resultados, seleccione el dominio de publicación de confianza y luego, en el panel Acciones, haga clic en **Exportar dominio de publicación de confianza**.

4. En el cuadro de diálogo **Exportar dominio de publicación de confianza** :

    - Haga clic en **Guardar como** y guárdelo en la ruta de acceso con un nombre de archivo de su elección. Asegúrese de especificar **.xml** como extensión de nombre de archivo (no se adjunta automáticamente).

    - Especifique y confirme una contraseña segura. Recuerde esta contraseña, ya que la necesitará más adelante, al importar los datos de configuración en Azure Information Protection.

    - No seleccione la casilla para guardar el archivo de dominio de confianza en RMS 1.0.

Cuando haya exportado todos los dominios de publicación de confianza, estará preparado para empezar el procedimiento para importar estos datos en Azure Information Protection.

Tenga en cuenta que los dominios de publicación de confianza incluyen las claves del certificado emisor de licencias de servidor (SLC) para descifrar los archivos protegidos con anterioridad, por lo que es importante que exporte (y después importe en Azure) todos los dominios de publicación de confianza y no solo el que está actualmente activo.

Por ejemplo, tendrá varios dominios de publicación de confianza si ha actualizado sus servidores de AD RMS desde el modo criptográfico 1 al modo criptográfico 2. Si no exporta e importa el dominio de publicación de confianza que contiene la clave archivada que utilizó el modo criptográfico 1, al final de la migración, los usuarios no podrán abrir el contenido protegido con la clave del modo criptográfico 1.


### <a name="import-the-configuration-data-to-azure-information-protection"></a>Importar los datos de configuración en Azure Information Protection
Los procedimientos exactos para este paso dependen de la configuración actual de la implementación de AD RMS y de la topología preferida para su clave de inquilino de Azure Information Protection.

La implementación de AD RMS actual usa una de las siguientes configuraciones con la clave del certificado emisor de licencias de servidor (SLC):

- Protección con contraseña de la base de datos de AD RMS. Se trata de la configuración predeterminada.

- Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales.

- Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.

- Contraseña protegida mediante un proveedor criptográfico externo.

> [!NOTE]
> Para obtener más información acerca del uso de módulos de seguridad de hardware con AD RMS, consulte [Uso de AD RMS con módulos de seguridad de hardware](http://technet.microsoft.com/library/jj651024.aspx).

Estas son las dos opciones de topología de claves de inquilino de Azure Information Protection: Microsoft administra su clave de inquilino (**administrada por Microsoft**) o la administra el usuario (**administrada por el cliente**) en Azure Key Vault. Cuando administra su propia clave de inquilino de Azure Information Protection, esto a veces se conoce como “aportar tu propia clave” (BYOK) y necesita un módulo de seguridad de hardware (HSM) de Thales. Para más información, vea el artículo [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Exchange Online no es compatible actualmente con BYOK en Azure Information Protection. Si desea usar BYOK después de la migración y planea usar Exchange Online, asegúrese de que comprende de qué forma esta configuración reduce la funcionalidad IRM para Exchange Online. Revise la información de la sección [Precio y restricciones de BYOK](byok-price-restrictions.md) para que le resulte más fácil elegir la topología de claves de inquilino de Azure Information Protection más adecuada para la migración.

Utilice la tabla siguiente para identificar qué procedimiento se utilizará para la migración. 

|Implementación de AD RMS actual|Topología de claves de inquilino de Azure Information Protection elegida|Instrucciones de migración|
|-----------------------------|----------------------------------------|--------------------------|
|Protección con contraseña de la base de datos de AD RMS|Administrada por Microsoft:|Vea el procedimiento **Migración entre claves protegidas por software** después de esta tabla.<br /><br />Esta es la ruta de migración más sencilla y solo necesita transferir los datos de configuración a Azure Information Protection.|
|Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales nShield |Administrada por el cliente (BYOK)|Vea el procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas BYOK de Azure Key Vault y tres conjuntos de pasos para, en primer lugar, transferir la clave del HSM local a los HSM de Azure Key Vault. Seguidamente, se autoriza al servicio Azure Rights Management de Azure Information Protection a usar la clave de inquilino y, por último, transferir los datos de configuración a Azure Information Protection.|
|Protección con contraseña de la base de datos de AD RMS|Administrada por el cliente (BYOK)|Vea el procedimiento **Migración de clave protegida por software a clave protegida por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas de BYOK de Azure Key Vault y cuatro conjuntos de pasos para primero extraer la clave de software e importarla en un HSM local, después transferir la clave desde el HSM local a los HSM de Azure Information Protection, luego transferir los datos del almacén de claves a Azure Information Protection y, por último, transferir los datos de configuración a Azure Information Protection.|
|Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales. |Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor de HSM para obtener instrucciones sobre cómo transferir la clave de este HSM a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
|Contraseña protegida mediante un proveedor criptográfico externo.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor criptográfico para obtener instrucciones sobre cómo transferir su clave a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|

Si tiene una clave protegida de HSM que no puede exportar y quiere realizar la migración a Azure Information Protection, puede configurar el modo de solo lectura de su clúster de AD RMS. En este modo, se puede abrir el contenido protegido anteriormente, pero el que haya protegido más recientemente usará una nueva clave de inquilino que administrarán usted (BYOK) o Microsoft. Para obtener más información, consulte [An update is available for Office to support migrations from AD RMS to Azure RMS](https://support.microsoft.com/help/4023955/an-update-is-available-for-office-to-support-migrations-from-ad-rms-to) (Actualización para Office disponible para permitir las migraciones de AD RMS a Azure RMS).

Antes de iniciar estos procedimientos de migración de claves, asegúrese de tener acceso a los archivos .xml que creó anteriormente cuando exportó los dominios de publicación de confianza. Por ejemplo, estos podrían estar guardados en una unidad USB que se transfiere desde el servidor de AD RMS a la estación de trabajo conectada a Internet.

> [!NOTE]
> Independientemente de cómo almacene estos datos, aplique las prácticas de seguridad recomendadas para protegerlos, ya que estos incluyen la clave privada.

Para completar el paso 4, elija y seleccione las instrucciones para la ruta de migración: 

- [Migración entre claves protegidas por software](migrate-softwarekey-to-softwarekey.md)
- [Migración entre claves protegidas por HSM](migrate-hsmkey-to-hsmkey.md)
- [Migración de clave protegida por software a clave protegida por HSM](migrate-softwarekey-to-hsmkey.md)

## <a name="step-5-activate-the-azure-rights-management-service"></a>Paso 5. Activación del servicio Azure Rights Management

Abra una sesión de PowerShell y ejecute los comandos siguientes:

1. Conéctese al servicio Azure Rights Management y, cuando se le pida, especifique las credenciales de administrador global:
    
        Connect-Aadrmservice

2. Activación del servicio Azure Rights Management:
    
        Enable-Aadrmservice

**¿Qué ocurre si el inquilino de Azure Information Protection ya está activado?** Si el servicio Azure Rights Management ya está activado en su organización, es posible que los usuarios ya hayan usado Azure Information Protection para proteger el contenido con una clave de inquilino generada automáticamente (y las plantillas predeterminadas) en lugar de las claves (y plantillas) existentes de AD RMS. Es poco probable que ocurra en equipos que estén bien administrados en la intranet, ya que se configuran automáticamente para su infraestructura de AD RMS. Pero esto puede suceder en equipos de grupo de trabajo o equipos que se conectan con poca frecuencia a la intranet. Desafortunadamente, también es difícil identificar estos equipos, motivo por el que se recomienda no activar el servicio antes de importar los datos de configuración de AD RMS.

Si el inquilino de Azure Information Protection ya está activado y puede identificar estos equipos, asegúrese de que ejecuta el script CleanUpRMS.cmd en estos equipos, como se describe en el [paso 7](migrate-from-ad-rms-phase3.md#step-7-reconfigure-clients-to-use-azure-information-protection). La ejecución de este script les obliga a reinicializar el entorno de usuario, así descargan la clave de inquilino y las plantillas importadas actualizadas.

Además, si ha creado plantillas personalizadas que quiera usar después de la migración, debe exportarlas e importarlas. Este procedimiento se explica en el paso siguiente. 

## <a name="step-6-configure-imported-templates"></a>Paso 6. Configure las plantillas importadas.

Como las plantillas que ha importado tienen el estado predeterminado **Archivada**, necesita cambiar este estado a **Publicada** si quiere que los usuarios puedan usar estas plantillas con el servicio Azure Rights Management.

Las plantillas que se importan de AD RMS tienen el mismo aspecto y comportamiento que las plantillas personalizadas que se pueden crear en Azure Portal. Para cambiar las plantillas importadas para publicarlas de modo que los usuarios puedan verlas y seleccionarlas desde las aplicaciones, vea [Configuración y administración de plantillas para Azure Information Protection](../deploy-use/configure-policy-templates.md).

Además de publicar las plantillas recién importadas, hay dos cambios importantes para las plantillas que debe realizar antes de continuar con la migración. Para obtener una experiencia más coherente para los usuarios durante el proceso de migración, no realice cambios adicionales en las plantillas importadas y no publique las dos plantillas predeterminadas que se incluyen en Azure Information Protection ni cree plantillas en este momento. En su lugar, espere hasta que se complete el proceso de migración y haya desaprovisionado los servidores de AD RMS.

Los cambios en la plantilla que debe realizar para este paso:

- Si ha creado plantillas personalizadas de Azure Information Protection antes de la migración, tendrá que exportarlas e importarlas de forma manual.

- Si las plantillas de AD RMS usan el grupo **CUALQUIERA**, debe agregar manualmente el grupo y los derechos equivalentes.

### <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>Procedimiento si ha creado plantillas personalizadas antes de la migración

Si ha creado plantillas personalizadas antes de la migración (antes o después de activar el servicio Azure Rights Management), las plantillas no estarán disponibles para los usuarios después de la migración, incluso si se habían establecido en **Publicada**. Para que estén disponibles para los usuarios, primero debe hacer lo siguiente: 

1. Identificar estas plantillas y anotar el identificador de plantilla, al ejecutar [Get-AadrmTemplate](/powershell/aadrm/vlatest/get-aadrmtemplate). 

2. Exportar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate).

3. Importar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Import-AadrmTemplate](/powershell/aadrm/vlatest/Import-AadrmTpd).

Después puede publicar o archivar estas plantillas como lo haría con cualquier otra plantilla que cree después de la migración.

### <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>Procedimiento si las plantillas de AD RMS usan el grupo **CUALQUIERA**

Si las plantillas de AD RMS estaban asignadas al grupo **CUALQUIERA**, este grupo se quitará automáticamente al importar las plantillas en Azure Information Protection. Necesita agregar de forma manual el grupo o usuarios equivalentes y los mismos derechos a las plantillas importadas. El grupo equivalente de Azure Information Protection se denomina **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@\<nombre_inquilino>.onmicrosoft.com**. Por ejemplo, este grupo puede tener un aspecto similar al siguiente para Contoso: **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Si no está seguro de si las plantillas de AD RMS incluyen el grupo CUALQUIERA, puede usar el siguiente script de Windows PowerShell de ejemplo para identificar estas plantillas. Para más información sobre el uso de Windows PowerShell con AD RMS, vea [Using Windows PowerShell to Administer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx) (Uso de Windows PowerShell para administrar AD RMS).

Puede ver el grupo de su organización creado automáticamente si copia una de las plantillas predeterminadas de directiva de permisos en el Portal de Azure clásico e identifica el **NOMBRE DE USUARIO** en la página **PERMISOS**. Sin embargo, no puede usar el portal clásico para agregar este grupo a una plantilla que se creó o importó manualmente; en su lugar, debe usar una de las siguientes opciones de Azure RMS PowerShell:

- Use el cmdlet [New-AadrmRightsDefinition](/powershell/aadrm/vlatest/new-aadrmrightsdefinition) de PowerShell para definir el grupo "AllStaff" y los derechos como un objeto de definición de derechos, y vuelva a ejecutar este comando para cada uno de los demás grupos o usuarios a los que ya se les ha concedido derechos en la plantilla original, además de asignar el grupo CUALQUIERA. Después, agregue estos objetos de definición de derechos a las plantillas mediante el cmdlet [Set-AadrmTemplateProperty](/powershell/aadrm/vlatest/set-aadrmtemplateproperty).

- Use el cmdlet [Export-AadrmTemplate](/powershell/aadrm/vlatest/export-aadrmtemplate) para exportar la plantilla a un archivo .XML que pueda editar para agregar el grupo "AllStaff" y los derechos a los grupos y derechos existentes y, después, use el cmdlet [Import-AadrmTemplate](/powershell/aadrm/vlatest/import-aadrmtemplate) para volver a importar este cambio en Azure Information Protection.

> [!NOTE]
> Este grupo equivalente "AllStaff" no es exactamente igual que el grupo ANYONE de AD RMS: el grupo "AllStaff" incluye a todos los usuarios de su inquilino de Azure, mientras que el grupo CUALQUIERA incluye a todos los usuarios autenticados, que podrían estar fuera de su organización.
> 
> Debido a esta diferencia entre los dos grupos, puede que tenga que agregar también usuarios externos además del grupo "AllStaff". Actualmente no se admiten direcciones de correo electrónico externas para grupos.


#### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>Script de ejemplo de Windows PowerShell para identificar plantillas de AD RMS que incluyen el grupo CUALQUIERA
Esta sección contiene el script de ejemplo que le ayuda a identificar plantillas de AD RMS que tienen definido el grupo CUALQUIERA, tal como se ha descrito en la sección anterior.

**Aviso de declinación de responsabilidades:** este script de ejemplo no es compatible con ningún servicio o programa de soporte técnico Standard de Microsoft. Este script de ejemplo se proporciona TAL CUAL sin garantía de ningún tipo.

```
import-module adrmsadmin 

New-PSDrive -Name MyRmsAdmin -PsProvider AdRmsAdmin -Root https://localhost -Force 

$ListofTemplates=dir MyRmsAdmin:\RightsPolicyTemplate

foreach($Template in $ListofTemplates) 
{ 
                $templateID=$Template.id

                $rights = dir MyRmsAdmin:\RightsPolicyTemplate\$Templateid\userright

     $templateName=$Template.DefaultDisplayName 

        if ($rights.usergroupname -eq "anyone")

                         {
                           $templateName = $Template.defaultdisplayname

                           write-host "Template " -NoNewline

                           write-host -NoNewline $templateName -ForegroundColor Red

                           write-host " contains rights for " -NoNewline

                           write-host ANYONE  -ForegroundColor Red
                         }
 } 
Remove-PSDrive MyRmsAdmin -force
```


## <a name="next-steps"></a>Pasos siguientes
Vaya a [Fase 3: configuración del lado cliente](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]