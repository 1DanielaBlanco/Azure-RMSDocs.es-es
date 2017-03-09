---
title: "Migración de AD RMS-Azure Information Protection: fase 1"
description: "La fase 1 de la migración desde AD RMS a Azure Information Protection, donde se describen los pasos 1 a 4 de la migración de AD RMS a Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: d38d7f89ba780b519ebe4a182161deb5bc9331b5
ms.lasthandoff: 02/24/2017


---

# <a name="migration-phase-1---server-side-configuration-for-ad-rms"></a>Fase 1 de migración: configuración del lado servidor para AD RMS

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use la información siguiente para la fase 1 de la migración desde AD RMS a Azure Information Protection. En estos procedimientos se describen los pasos del 1 al 4 del tema [Migración desde AD RMS a Azure Information Protection](migrate-from-ad-rms-to-azure-rms.md).


## <a name="step-1-download-the-azure-rights-management-administration-tool"></a>Paso 1: descargue la herramienta de administración de Azure Rights Management
Vaya al Centro de descarga de Microsoft y descargue [Azure Rights Management Administration Tool](https://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de Azure Rights Management para Windows PowerShell. Azure Rights Management (Azure RMS) es el servicio que ofrece la protección de datos para Azure Information Protection.

Instale la herramienta. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

> [!NOTE]
> Si anteriormente ya ha descargado este módulo de Windows PowerShell, ejecute el comando siguiente para comprobar que su número de versión sea como mínimo 2.5.0.0: `(Get-Module aadrm -ListAvailable).Version`

## <a name="step-2-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection"></a>Paso 2. Exportar los datos de configuración de AD RMS e importarlos en Azure Information Protection
Este paso es un proceso de dos fases:

1.  Exporte los datos de configuración de AD RMS mediante la exportación de los dominios de publicación de confianza (TPD) a un archivo .xml. Este proceso es el mismo para todas las migraciones.

2.  Importe los datos de configuración en Azure Information Protection. Hay diferentes procesos para este paso, según la configuración de la implementación de AD RMS actual y la topología preferida para su clave de inquilino de Azure RMS.

### <a name="export-the-configuration-data-from-ad-rms"></a>Exportar los datos de configuración de AD RMS

> [!IMPORTANT]
> Antes de realizar este procedimiento, primero confirme que los servidores de AD RMS se ejecuten con el modo criptográfico 2, que es un requisito de Azure Information Protection.
> 
> Para confirmar el modo criptográfico:
> 
> - Para Windows Server 2012 R2 y Windows 2012: Propiedades del clúster de AD RMS > pestaña **General**. 
> 
> - Para todas las versiones compatibles de AD RMS: use [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) y la opción **Administrador de AD RMS** para ver el modo criptográfico en **Información del servicio de RMS**.
> 
> Asegúrese de que el valor del modo criptográfico sea **2**. En caso contrario, consulte las instrucciones para habilitar el modo criptográfico 2 en [Modos criptográficos de AD RMS](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx).


Siga este procedimiento en todos los clústeres de AD RMS, para todos los dominios de publicación confianza que tienen contenido protegido de su organización. No es necesario ejecutar esto en clústeres solo para licencias.

#### <a name="to-export-the-configuration-data-trusted-publishing-domain-information"></a>Para exportar los datos de configuración (información del dominio de publicación de confianza)

1.  Inicie sesión en el clúster de AD RMS como un usuario con permisos de administración de AD RMS.

2.  Desde la consola de administración de AD RMS (**Active Directory Rights Management Services**), expanda el nombre del clúster de AD RMS, expanda **Directivas de confianza**y luego haga clic en **Dominios de publicación de confianza**.

3.  En el panel de resultados, seleccione el dominio de publicación de confianza y luego, en el panel Acciones, haga clic en **Exportar dominio de publicación de confianza**.

4.  En el cuadro de diálogo **Exportar dominio de publicación de confianza** :

    -   Haga clic en **Guardar como** y guárdelo en la ruta de acceso con un nombre de archivo de su elección. Asegúrese de especificar **.xml** como extensión de nombre de archivo (no se adjunta automáticamente).

    -   Especifique y confirme una contraseña segura. Recuerde esta contraseña, ya que la necesitará más adelante, al importar los datos de configuración en Azure Information Protection.

    -   No seleccione la casilla para guardar el archivo de dominio de confianza en RMS 1.0.

Cuando haya exportado todos los dominios de publicación de confianza, estará preparado para empezar el procedimiento para importar estos datos en Azure Information Protection.

Tenga en cuenta que los dominios de publicación de confianza incluyen las claves para descifrar los archivos protegidos con anterioridad, por lo que es importante que exporte (y después importe en Azure) todos los dominios de publicación de confianza y no solo el que está actualmente activo.

Por ejemplo, tendrá varios dominios de publicación de confianza si ha actualizado sus servidores de AD RMS desde el modo criptográfico 1 al modo criptográfico 2. Si no exporta e importa el dominio de publicación de confianza que contiene la clave archivada que utilizó el modo criptográfico 1, al final de la migración, los usuarios no podrán abrir el contenido protegido con la clave del modo criptográfico 1.


### <a name="import-the-configuration-data-to-azure-information-protection"></a>Importar los datos de configuración en Azure Information Protection
Los procedimientos exactos para este paso dependen de la configuración actual de la implementación de AD RMS y de la topología preferida para su clave de inquilino de Azure Information Protection.

La implementación de AD RMS actual usará una de las siguientes configuraciones con la clave del certificado emisor de licencias de servidor (SLC):

-   Protección con contraseña de la base de datos de AD RMS. Se trata de la configuración predeterminada.

-   Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales.

-   Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.

-   Contraseña protegida mediante un proveedor criptográfico externo.

> [!NOTE]
> Para obtener más información acerca del uso de módulos de seguridad de hardware con AD RMS, consulte [Uso de AD RMS con módulos de seguridad de hardware](http://technet.microsoft.com/library/jj651024.aspx).

Estas son las dos opciones de topología de claves de inquilino de Azure Information Protection: Microsoft administra su clave de inquilino (**administrada por Microsoft**) o la administra el usuario (**administrada por el cliente**) en Azure Key Vault. Cuando administra su propia clave de inquilino de Azure Information Protection, esto a veces se conoce como “aportar tu propia clave” (BYOK) y necesita un módulo de seguridad de hardware (HSM) de Thales. Para más información, vea el artículo [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

> [!IMPORTANT]
> Exchange Online no es compatible actualmente con BYOK en Azure Information Protection. Si desea usar BYOK después de la migración y planea usar Exchange Online, asegúrese de que comprende de qué forma esta configuración reduce la funcionalidad IRM para Exchange Online. Revise la información de la sección [Precio y restricciones de BYOK](byok-price-restrictions.md) para que le resulte más fácil elegir la topología de claves de inquilino de Azure Information Protection más adecuada para la migración.

Utilice la tabla siguiente para identificar qué procedimiento se utilizará para la migración. No se admiten las combinaciones que no aparecen.

|Implementación de AD RMS actual|Topología de claves de inquilino de Azure Information Protection elegida|Instrucciones de migración|
|-----------------------------|----------------------------------------|--------------------------|
|Protección con contraseña de la base de datos de AD RMS|Administrada por Microsoft:|Vea el procedimiento **Migración entre claves protegidas por software** después de esta tabla.<br /><br />Esta es la ruta de migración más sencilla y solo necesita transferir los datos de configuración a Azure Information Protection.|
|Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales nShield|Administrada por el cliente (BYOK)|Vea el procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas de BYOK de Azure Key Vault y tres conjuntos de pasos para primero transferir la clave desde el HSM local a los HSM de Azure Key Vault, después autorizar el servicio Azure Rights Management de Azure Information Protection a usar la clave de inquilino y, por último, transferir los datos de configuración a Azure Information Protection.|
|Protección con contraseña de la base de datos de AD RMS|Administrada por el cliente (BYOK)|Vea el procedimiento **Migración de clave protegida por software a clave protegida por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas de BYOK de Azure Key Vault y cuatro conjuntos de pasos para primero extraer la clave de software e importarla en un HSM local, después transferir la clave desde el HSM local a los HSM de Azure Information Protection, luego transferir los datos del almacén de claves a Azure Information Protection y, por último, transferir los datos de configuración a Azure Information Protection.|
|Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor de HSM para obtener instrucciones sobre cómo transferir la clave de este HSM a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
|Contraseña protegida mediante un proveedor criptográfico externo.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor criptográfico para obtener instrucciones sobre cómo transferir su clave a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
Antes de iniciar estos procedimientos, asegúrese de que puede tener acceso a los archivos .xml que creó anteriormente cuando exportó los dominios de publicación de confianza. Por ejemplo, estos podrían estar guardados en una unidad USB que se transfiere desde el servidor de AD RMS a la estación de trabajo conectada a Internet.

> [!NOTE]
> Independientemente de cómo almacene estos datos, aplique las prácticas de seguridad recomendadas para protegerlos, ya que estos incluyen la clave privada.


Para completar el paso 2, elija y seleccione las instrucciones para la ruta de migración: 


- [Migración entre claves protegidas por software](migrate-softwarekey-to-softwarekey.md)
- [Migración entre claves protegidas por HSM](migrate-hsmkey-to-hsmkey.md)
- [Migración de clave protegida por software a clave protegida por HSM](migrate-softwarekey-to-hsmkey.md)


## <a name="step-3-activate-your-azure-information-protection-tenant"></a>Paso 3: Activar el inquilino de Azure Information Protection
Para realizar este paso necesita activar el servicio Azure Rights Management. Las instrucciones se describen por completo en el artículo [Activar Azure Rights Management](../deploy-use/activate-service.md).


> [!TIP]
> Si tiene una suscripción a Office 365, puede activar el servicio Azure Rights Management desde el Centro de administración de Office 365 o el Portal de Azure clásico. Se recomienda usar el Portal de Azure clásico, ya que usará este portal de administración para completar el paso siguiente.

**¿Qué ocurre si el inquilino de Azure Information Protection ya está activado?** Si el servicio Azure Rights Management ya está activado en su organización, es posible que los usuarios ya hayan usado Azure Information Protection para proteger el contenido con una clave de inquilino generada automáticamente (y las plantillas predeterminadas) en lugar de las claves (y plantillas) existentes de AD RMS. Esto es improbable que ocurra en equipos que estén bien administrados en la intranet, ya que se configuran automáticamente para su infraestructura de AD RMS. Pero esto puede suceder en equipos de grupo de trabajo o equipos que se conectan con poca frecuencia a la intranet. Desafortunadamente, también es difícil identificar estos equipos, motivo por el que se recomienda no activar el servicio antes de importar los datos de configuración de AD RMS.

Si ya está activado el inquilino de Azure Information Protection y puede identificar estos equipos, asegúrese de que ejecuta el script CleanUpRMS_RUN_Elevated.cmd en esos equipos, como se describe en el paso 5. La ejecución de este script les obliga a reinicializar el entorno de usuario, así descargan la clave de inquilino y las plantillas importadas actualizadas.

Además, si ha creado plantillas personalizadas que quiera usar después de la migración, debe exportarlas e importarlas. Este procedimiento se explica en el paso siguiente. 

## <a name="step-4-configure-imported-templates"></a>Paso 4. Configure las plantillas importadas.
Como las plantillas que ha importado tienen el estado predeterminado **Archivada**, necesita cambiar este estado a **Publicada** si quiere que los usuarios puedan usar estas plantillas con el servicio Azure Rights Management.

Las plantillas que se importan de AD RMS tienen el mismo aspecto y comportamiento que las plantillas personalizadas que se pueden crear en el Portal de Azure clásico. Para publicar las plantillas importadas para que los usuarios puedan verlas y seleccionarlas desde las aplicaciones, vea [Configuración de plantillas personalizadas para el servicio Azure Rights Management](../deploy-use/configure-custom-templates.md).

Además de publicar las plantillas recién importadas, hay dos cambios importantes para las plantillas que debe realizar antes de continuar con la migración. Para obtener una experiencia más coherente para los usuarios durante el proceso de migración, no realice cambios adicionales en las plantillas importadas y no publique las dos plantillas predeterminadas que se incluyen en Azure Information Protection ni cree plantillas en este momento. En su lugar, espere hasta que se complete el proceso de migración y haya dado de baja los servidores de AD RMS.

Los cambios en la plantilla que debe realizar para este paso:

- Si ha creado plantillas personalizadas de Azure Information Protection antes de la migración, tendrá que exportarlas e importarlas de forma manual.

- Si las plantillas de AD RMS usan el grupo **CUALQUIERA**, debe agregar manualmente el grupo y los derechos equivalentes.

## <a name="procedure-if-you-created-custom-templates-before-the-migration"></a>Procedimiento si ha creado plantillas personalizadas antes de la migración

Si ha creado plantillas personalizadas antes de la migración (antes o después de activar el servicio Azure Rights Management), las plantillas no estarán disponibles para los usuarios después de la migración, incluso si se habían establecido en **Publicada**. Para que estén disponibles para los usuarios, primero debe hacer lo siguiente: 

1. Identificar estas plantillas y anotar el identificador de plantilla, al ejecutar [Get-AadrmTemplate](https://msdn.microsoft.com/library/dn727079.aspx). 

2. Exportar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Export-AadrmTemplate](https://msdn.microsoft.com/library/dn727078.aspx).

3. Importar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Import-AadrmTemplate](https://msdn.microsoft.com/library/dn727077.aspx).

Después puede publicar o archivar estas plantillas como lo haría con cualquier otra plantilla que cree después de la migración.


## <a name="procedure-if-your-templates-in-ad-rms-used-the-anyone-group"></a>Procedimiento si las plantillas de AD RMS usan el grupo **CUALQUIERA**

Si las plantillas de AD RMS estaban asignadas al grupo **CUALQUIERA**, este grupo se quitará automáticamente al importar las plantillas en Azure Information Protection. Necesita agregar de forma manual el grupo o usuarios equivalentes y los mismos derechos a las plantillas importadas. El grupo equivalente de Azure Information Protection se denomina **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<nombre_de_inquilino>.onmicrosoft.com**. Por ejemplo, este grupo puede tener un aspecto similar al siguiente para Contoso: **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Si no está seguro de si las plantillas de AD RMS incluyen el grupo CUALQUIERA, puede usar el siguiente script de Windows PowerShell de ejemplo para identificar estas plantillas. Para más información sobre el uso de Windows PowerShell con AD RMS, vea [Using Windows PowerShell to Administer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx) (Uso de Windows PowerShell para administrar AD RMS).

Puede ver el grupo de su organización creado automáticamente si copia una de las plantillas predeterminadas de directiva de permisos en el Portal de Azure clásico e identifica el **NOMBRE DE USUARIO** en la página **PERMISOS**. Sin embargo, no puede usar el portal clásico para agregar este grupo a una plantilla que se creó o importó manualmente; en su lugar, debe usar una de las siguientes opciones de Azure RMS PowerShell:

-   Use el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) de PowerShell para definir el grupo "AllStaff" y los derechos como un objeto de definición de derechos, y vuelva a ejecutar este comando para cada uno de los demás grupos o usuarios a los que ya se les ha concedido derechos en la plantilla original, además de asignar el grupo CUALQUIERA. Después, agregue estos objetos de definición de derechos a las plantillas mediante el cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx).

-   Use el cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar la plantilla a un archivo .XML que pueda editar para agregar el grupo "AllStaff" y los derechos a los grupos y derechos existentes y, después, use el cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para volver a importar este cambio en Azure Information Protection.

> [!NOTE]
> Este grupo equivalente "AllStaff" no es exactamente igual que el grupo ANYONE de AD RMS: el grupo "AllStaff" incluye a todos los usuarios de su inquilino de Azure, mientras que el grupo CUALQUIERA incluye a todos los usuarios autenticados, que podrían estar fuera de su organización.
> 
> Debido a esta diferencia entre los dos grupos, puede que tenga que agregar también usuarios externos además del grupo "AllStaff". Actualmente no se admiten direcciones de correo electrónico externas para grupos.


### <a name="sample-windows-powershell-script-to-identify-ad-rms-templates-that-include-the-anyone-group"></a>Script de ejemplo de Windows PowerShell para identificar plantillas de AD RMS que incluyen el grupo CUALQUIERA
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
Vaya a [Fase 2: Configuración del lado cliente](migrate-from-ad-rms-phase2.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

