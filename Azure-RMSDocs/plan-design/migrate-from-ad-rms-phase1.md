---
title: "Migración desde AD RMS a Azure Rights Management - Fase 1 | Azure RMS"
description: "Use la siguiente información para la fase 1 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen los pasos del 1 al 4 del tema Migración desde AD RMS a Azure Rights Management."
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 5a189695-40a6-4b36-afe6-0823c94993ef
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: d4e5502568147a51025434ad78cbfdede3eb3207


---

# Fase 1 de migración: configuración del lado servidor para AD RMS

>*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*

Use la siguiente información para la fase 1 de migración desde AD RMS a Azure Rights Management (Azure RMS). Estos procedimientos incluyen los pasos del 1 al 4 del tema [Migración desde AD RMS a Azure Rights Management](migrate-from-ad-rms-to-azure-rms.md).


## Paso 1: descargue la herramienta de administración de Azure Rights Management
Vaya al Centro de descarga de Microsoft y descargue la [herramienta de administración de Azure Rights Management](https://go.microsoft.com/fwlink/?LinkId=257721), que contiene el módulo de administración de Azure RMS para Windows PowerShell.

Instale la herramienta. Para obtener instrucciones, vea [Instalación de Windows PowerShell para Azure Rights Management](../deploy-use/install-powershell.md).

> [!NOTE]
> Si anteriormente ya ha descargado este módulo de Windows PowerShell, ejecute el comando siguiente para comprobar que su número de versión sea como mínimo 2.5.0.0: `(Get-Module aadrm -ListAvailable).Version`

## Paso 2. Exporte los datos de configuración de AD RMS e impórtelos en Azure RMS.
Este paso es un proceso de dos fases:

1.  Exporte los datos de configuración de AD RMS mediante la exportación de los dominios de publicación de confianza (TPD) a un archivo .xml. Este proceso es el mismo para todas las migraciones.

2.  Importe los datos de configuración a Azure RMS. Hay diferentes procesos para este paso, según la configuración de la implementación de AD RMS actual y la topología preferida para su clave de inquilino de Azure RMS.

### Exportar los datos de configuración de AD RMS

> [!IMPORTANT]
> Antes de realizar este procedimiento, primero confirme que los servidores de AD RMS se ejecuten con el modo criptográfico 2, que es un requisito de Azure RMS.
> 
> Para confirmar el modo criptográfico:
> 
> - Para Windows Server 2012 R2 y Windows 2012: Propiedades del clúster de AD RMS > pestaña **General**. 
> 
> - Para todas las versiones compatibles de AD RMS: use [RMS Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=46437) y la opción **Administrador de AD RMS** para ver el modo criptográfico en **Información del servicio de RMS**.
> 
> Asegúrese de que el valor del modo criptográfico sea **2**. En caso contrario, consulte las instrucciones para habilitar el modo criptográfico 2 en [Modos criptográficos de AD RMS](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx).


Siga este procedimiento en todos los clústeres de AD RMS, para todos los dominios de publicación confianza que tienen contenido protegido de su organización. No es necesario ejecutar esto en clústeres solo para licencias.

#### Para exportar los datos de configuración (información del dominio de publicación de confianza)

1.  Inicie sesión en el clúster de AD RMS como un usuario con permisos de administración de AD RMS.

2.  Desde la consola de administración de AD RMS (**Active Directory Rights Management Services**), expanda el nombre del clúster de AD RMS, expanda **Directivas de confianza**y luego haga clic en **Dominios de publicación de confianza**.

3.  En el panel de resultados, seleccione el dominio de publicación de confianza y luego, en el panel Acciones, haga clic en **Exportar dominio de publicación de confianza**.

4.  En el cuadro de diálogo **Exportar dominio de publicación de confianza** :

    -   Haga clic en **Guardar como** y guárdelo en la ruta de acceso con un nombre de archivo de su elección. Asegúrese de especificar **.xml** como extensión de nombre de archivo (no se adjunta automáticamente).

    -   Especifique y confirme una contraseña segura. Recuerde esta contraseña, porque la necesitará más adelante, al importar los datos de configuración a Azure RMS.

    -   No seleccione la casilla para guardar el archivo de dominio de confianza en RMS 1.0.

Cuando se exportan todos los dominios de publicación de confianza, está listo para empezar el procedimiento para importar estos datos en Azure RMS.

### Importar los datos de configuración a Azure RMS
Los procedimientos exactos para este paso dependen de la configuración actual de la implementación de AD RMS y de la topología preferida para su clave de inquilino de Azure RMS.

La implementación de AD RMS actual usará una de las siguientes configuraciones con la clave del certificado emisor de licencias de servidor (SLC):

-   Protección con contraseña de la base de datos de AD RMS. Se trata de la configuración predeterminada.

-   Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales.

-   Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.

-   Contraseña protegida mediante un proveedor criptográfico externo.

> [!NOTE]
> Para obtener más información acerca del uso de módulos de seguridad de hardware con AD RMS, consulte [Uso de AD RMS con módulos de seguridad de hardware](http://technet.microsoft.com/library/jj651024.aspx).

Estas son las dos opciones de topología de claves de inquilino de Azure RMS: Microsoft administra su clave de inquilino (**administrada por Microsoft**), o bien es el usuario quien se encarga de ello (**administrada por el cliente**) en el Almacén de claves de Azure. Cuando administra su propia clave de inquilino de Azure RMS, esto se conoce a veces como "aporte su propia clave" (BYOK) y requiere un módulo de seguridad de hardware (HSM) de Thales. Para más información, vea [Planning and implementing your Azure Rights Management tenant keyt](plan-implement-tenant-key.md) (Planeación e implementación de la clave de inquilino de Azure Rights Managemen).

> [!IMPORTANT]
> Actualmente, Exchange Online no es compatible con BYOK de Azure RMS.  Si desea usar BYOK después de la migración y planea usar Exchange Online, asegúrese de que comprende de qué forma esta configuración reduce la funcionalidad IRM para Exchange Online. Revise la información de la sección [BYOK pricing and restrictions](byok-price-restrictions.md) (Precios y restricciones de BYOK) para ayudarle a elegir la mejor topología de clave de inquilino de Azure RMS para la migración.

Utilice la tabla siguiente para identificar qué procedimiento se utilizará para la migración. No se admiten las combinaciones que no aparecen.

|Implementación de AD RMS actual|Topología de clave de inquilino de Azure RMS elegida|Instrucciones de migración|
|-----------------------------|----------------------------------------|--------------------------|
|Protección con contraseña de la base de datos de AD RMS|Administrada por Microsoft:|Vea el procedimiento **Migración entre claves protegidas por software** después de esta tabla.<br /><br />Esta es la ruta de migración más sencilla y solo requiere que transfiera los datos de configuración a Azure RMS.|
|Protección de HSM mediante el uso de un módulo de seguridad de hardware (HSM) de Thales nShield|Administrada por el cliente (BYOK)|Vea el procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas de BYOK del Almacén de claves de Azure y tres conjuntos de pasos para, en primer lugar, transferir la clave desde el HSM local a los HSM del Almacén de claves de Azure, después autorizar a Azure RMS a usar la clave de inquilino y, por último, transferir los datos de configuración a Azure RMS.|
|Protección con contraseña de la base de datos de AD RMS|Administrada por el cliente (BYOK)|Vea el procedimiento **Migración de clave protegida por software a clave protegida por HSM** después de esta tabla.<br /><br />Para este procedimiento se necesita el conjunto de herramientas de BYOK del Almacén de claves de Azure y cuatro conjuntos de pasos para, en primer lugar, extraer la clave de software e importarla en un HSM local, después transferir la clave desde el HSM local a los HSM de Azure RMS, a continuación transferir los datos del almacén de Azure RMS y, por último, transferir los datos de configuración Azure RMS.|
|Protección de HSM mediante un módulo de seguridad de hardware (HSM) desde un proveedor distinto de Thales.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor de HSM para obtener instrucciones sobre cómo transferir la clave de este HSM a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
|Contraseña protegida mediante un proveedor criptográfico externo.|Administrada por el cliente (BYOK)|Póngase en contacto con el proveedor criptográfico para obtener instrucciones sobre cómo transferir su clave a un módulo de seguridad de hardware (HSM) de Thales nShield. Después, siga las instrucciones del procedimiento **Migración entre claves protegidas por HSM** después de esta tabla.|
Antes de iniciar estos procedimientos, asegúrese de que puede tener acceso a los archivos .xml que creó anteriormente cuando exportó los dominios de publicación de confianza. Por ejemplo, estos podrían estar guardados en una unidad USB que se transfiere desde el servidor de AD RMS a la estación de trabajo conectada a Internet.

> [!NOTE]
> Independientemente de cómo almacene estos datos, aplique las prácticas de seguridad recomendadas para protegerlos, ya que estos incluyen la clave privada.


Para completar el paso 2, elija y seleccione las instrucciones para la ruta de migración: 


- [Migración entre claves protegidas por software](migrate-softwarekey-to-softwarekey.md)
- [Migración entre claves protegidas por HSM](migrate-hsmkey-to-hsmkey.md)
- [Migración de clave protegida por software a clave protegida por HSM](migrate-softwarekey-to-hsmkey.md)


## Paso 3: Active el inquilino de RMS.
Las instrucciones de este paso se incluyen íntegramente en el artículo [Activating Azure Rights Management](../deploy-use/activate-service.md) (Activar Azure Rights Management).


> [!TIP]
> Si tiene una suscripción de Office 365, puede activar Azure RMS desde el centro de administración de Office 365 o el Portal de Azure clásico. Se recomienda usar el Portal de Azure clásico, ya que usará este portal de administración para completar el paso siguiente.

**¿Qué ocurre si ya está activado el inquilino de Azure RMS?** Si el servicio de Azure RMS ya está activado en su organización, es posible que los usuarios ya hayan usado Azure RMS para proteger el contenido con una clave de inquilino generada automáticamente (y las plantillas predeterminadas) en lugar de las claves (y plantillas) existentes de AD RMS. Esto es improbable que ocurra en equipos que estén bien administrados en la intranet, ya que se configuran automáticamente para su infraestructura de AD RMS. Pero esto puede suceder en equipos de grupo de trabajo o equipos que se conectan con poca frecuencia a la intranet. Desafortunadamente, también es difícil identificar estos equipos, motivo por el que se recomienda no activar el servicio antes de importar los datos de configuración de AD RMS.

Si ya está activado el inquilino de Azure RMS y puede identificar estos equipos, asegúrese de que ejecuta el script CleanUpRMS_RUN_Elevated.cmd en estos equipos, tal como se describe en el paso 5. La ejecución de este script les obliga a reinicializar el entorno de usuario, así descargan la clave de inquilino y las plantillas importadas actualizadas.

Además, si ha creado plantillas personalizadas que quiera usar después de la migración, debe exportarlas e importarlas. Este procedimiento se explica en el paso siguiente. 

## Paso 4. Configure las plantillas importadas.
Dado que las plantillas que importó tienen un estado predeterminado de **Archivada**, debe cambiar este estado a **Publicada** si desea que los usuarios puedan utilizar estas plantillas con Azure RMS.

Las plantillas que se importan de AD RMS tienen el mismo aspecto y comportamiento que las plantillas personalizadas que se pueden crear en el Portal de Azure clásico. Para cambiar las plantillas importadas para publicarlas de modo que los usuarios puedan verlas y seleccionarlas desde las aplicaciones, consulte [Configuración de plantillas personalizadas para Azure Rights Management](../deploy-use/configure-custom-templates.md).

Además de publicar las plantillas recién importadas, hay dos cambios importantes para las plantillas que debe realizar antes de continuar con la migración. Para obtener una experiencia más coherente para los usuarios durante el proceso de migración, no realice cambios adicionales en las plantillas importadas y no publique las dos plantillas predeterminadas que vienen con Azure RMS ni cree plantillas nuevas en este momento. En su lugar, espere hasta que se complete el proceso de migración y haya dado de baja los servidores de AD RMS.

Los cambios en la plantilla que debe realizar para este paso:

- Si ha creado plantillas personalizadas en Azure RMS antes de la migración, debe exportarlas e importarlas manualmente.

- Si las plantillas de AD RMS usan el grupo **CUALQUIERA**, debe agregar manualmente el grupo y los derechos equivalentes.

## Procedimiento si ha creado plantillas personalizadas antes de la migración

Si ha creado plantillas personalizadas antes de la migración, ya sea antes o después de activar Azure RMS, las plantillas no estarán disponibles para los usuarios después de la migración, incluso si se habían establecido en **Publicada**. Para que estén disponibles para los usuarios, primero debe hacer lo siguiente: 

1. Identificar estas plantillas y anotar el identificador de plantilla, al ejecutar [Get-AadrmTemplate](https://msdn.microsoft.com/library/dn727079.aspx). 

2. Exportar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Export-AadrmTemplate](https://msdn.microsoft.com/library/dn727078.aspx).

3. Importar las plantillas mediante el cmdlet de PowerShell de Azure RMS [Import-AadrmTemplate](https://msdn.microsoft.com/library/dn727077.aspx).

Después puede publicar o archivar estas plantillas como lo haría con cualquier otra plantilla que cree después de la migración.


## Procedimiento si las plantillas de AD RMS usan el grupo **CUALQUIERA**

Si sus plantillas de AD RMS usaban el grupo **CUALQUIERA**, este grupo desaparecerá automáticamente al importar las plantillas a Azure RMS. Debe agregar manualmente el grupo o usuarios equivalentes y los mismos derechos a las plantillas importadas. El grupo equivalente para Azure RMS se denomina **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@<tenant_name>.onmicrosoft.com**. Por ejemplo, este grupo podría tener un aspecto similar al siguiente grupo de Contoso: **AllStaff-7184AB3F-CCD1-46F3-8233-3E09E9CF0E66@contoso.onmicrosoft.com**.

Si no está seguro de si las plantillas de AD RMS incluyen el grupo CUALQUIERA, puede usar el siguiente script de Windows PowerShell de ejemplo para identificar estas plantillas. Para más información sobre el uso de Windows PowerShell con AD RMS, vea [Using Windows PowerShell to Administer AD RMS](https://technet.microsoft.com/library/ee221079%28v=ws.10%29.aspx) (Uso de Windows PowerShell para administrar AD RMS).

Puede ver el grupo de su organización creado automáticamente si copia una de las plantillas predeterminadas de directiva de permisos en el Portal de Azure clásico e identifica el **NOMBRE DE USUARIO** en la página **PERMISOS**. Sin embargo, no puede usar el portal clásico para agregar este grupo a una plantilla que se creó o importó manualmente; en su lugar, debe usar una de las siguientes opciones de Azure RMS PowerShell:

-   Use el cmdlet [New-AadrmRightsDefinition](https://msdn.microsoft.com/library/azure/dn727080.aspx) de PowerShell para definir el grupo "AllStaff" y los derechos como un objeto de definición de derechos, y ejecute de nuevo este comando para cada uno de los demás grupos o usuarios a los que ya se les ha otorgado derechos en la plantilla original además de para el grupo CUALQUIERA. Después, agregue estos objetos de definición de derechos a las plantillas mediante el cmdlet [Set-AadrmTemplateProperty](https://msdn.microsoft.com/library/azure/dn727076.aspx).

-   Use el cmdlet [Export-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727078.aspx) para exportar la plantilla a un archivo .XML que pueda editar para agregar el grupo "AllStaff" y los derechos a los grupos y derechos existentes y después use el cmdlet [Import-AadrmTemplate](https://msdn.microsoft.com/library/azure/dn727077.aspx) para importar este cambio de nuevo en Azure RMS.

> [!NOTE]
> Este grupo equivalente "AllStaff" no es exactamente igual que el grupo ANYONE de AD RMS: el grupo "AllStaff" incluye a todos los usuarios de su inquilino de Azure, mientras que el grupo CUALQUIERA incluye a todos los usuarios autenticados, que podrían estar fuera de su organización.
> 
> Debido a esta diferencia entre los dos grupos, puede que tenga que agregar también usuarios externos además del grupo "AllStaff". Actualmente no se admiten direcciones de correo electrónico externas para grupos.


### Script de ejemplo de Windows PowerShell para identificar plantillas de AD RMS que incluyen el grupo CUALQUIERA
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


## Pasos siguientes
Vaya a [Fase 2: Configuración del lado cliente](migrate-from-ad-rms-phase2.md).




<!--HONumber=Aug16_HO4-->


