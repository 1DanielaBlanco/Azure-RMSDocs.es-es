---
title: "Migración de AD RMS-Azure Information Protection"
description: "Instrucciones para migrar la implementación de Active Directory Rights Management Services (AD RMS) a Azure Information Protection. Después de la migración, los usuarios seguirán teniendo acceso a los documentos y mensajes de correo electrónico protegidos por su organización con AD RMS, y el nuevo contenido protegido usará Azure Information Protection."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 08/11/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 8f81eee3c15b771e60c24a83f66d13a4a654a7e3
ms.sourcegitcommit: 17f593b099dddcbb1cf0422353d594ab964b2736
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/11/2017
---
# <a name="migrating-from-ad-rms-to-azure-information-protection"></a>Migración desde AD RMS a Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use el siguiente conjunto de instrucciones para migrar su implementación de Active Directory Rights Management Services (AD RMS) a Azure Information Protection. 

Después de la migración, los servidores de AD RMS ya no se usarán, pero los usuarios seguirán teniendo acceso a documentos y mensajes de correo electrónico que su organización protege mediante AD RMS. El contenido protegido recientemente usará el servicio Azure Rights Management (Azure RMS) de Azure Information Protection.

¿No está seguro de si esta migración de AD RMS es conveniente para su organización?

-   Consulte una introducción a Azure Information Protection en [¿Qué es Azure Information Protection?](../understand-explore/what-is-information-protection.md)

-   Vea una comparación de Azure Information Protection y AD RMS en [Comparación entre Azure Rights Management y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## <a name="recommended-reading-before-you-migrate-to-azure-information-protection"></a>Se recomienda leer antes de migrar a Azure Information Protection

Aunque no es necesario, podría resultar útil leer la documentación siguiente antes de comenzar la migración. Esta información le permite conocer mejor cómo funciona la tecnología cuando resulta relevante para el paso de migración.

- [Planear e implementar la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md): conocer las opciones de administración de claves que tiene para el inquilino de Azure Information Protection, en que su clave SLC equivalente en la nube es administrada por Microsoft (modo predeterminado) o por usted mismo ("traiga su propia clave" o configuración BYOK). 

- [Detección de servicios de RMS](../rms-client/client-deployment-notes.md#rms-service-discovery): en esta sección de las notas de implementación del cliente de RMS se explica que el orden para la detección de servicio es **Registro**, **SCP** y, luego, **nube**. Durante el proceso de migración cuando el SCP todavía está instalado, debe configurar a clientes con la configuración del registro para el inquilino de Azure Information Protection para que no usen el clúster de AD RMS devuelto desde el SCP.

- [Información general sobre el conector Microsoft Rights Management](../deploy-use/deploy-rms-connector.md#overview-of-the-microsoft-rights-management-connector): en esta sección de la documentación del conector RMS se explica cómo los servidores locales se pueden conectar al servicio de Azure Rights Management para proteger documentos y correos electrónicos.

Además, si está familiarizado con el funcionamiento de AD RMS, le resultará útil leer [¿Cómo funciona Azure RMS? En segundo plano](../understand-explore/how-does-it-work.md) para ayudarlo a identificar qué procesos tecnológicos son iguales o diferentes para la versión en la nube.

## <a name="prerequisites-for-migrating-ad-rms-to-azure-information-protection"></a>Requisitos previos para migrar AD RMS a Azure Information Protection

Antes de iniciar la migración a Azure Information Protection, asegúrese de que se cumplen los siguientes requisitos previos y de que conoce las limitaciones.

- **Una implementación de RMS compatible:**
    
    - Las versiones siguientes de AD RMS admiten una migración a Azure Information Protection:
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
        - Windows Server 2016 (x64)
        
    - Se admiten todas las topologías de AD RMS válidas:
    
        - Bosque único, un solo clúster de RMS
        
        - Bosque único, varios clústeres de RMS solo con licencias
        
        - Varios bosques, varios clústeres de RMS
        
    Nota: De forma predeterminada, varios clústeres de AD RMS se migran a un único inquilino de Azure Information Protection. Si quiere usar inquilinos independientes de Azure Information Protection, necesita considerarlos como migraciones distintas. No se puede importar una clave de un clúster de RMS a más de un inquilino.

- **Todos los requisitos para ejecutar Azure Information Protection, incluida una suscripción para Azure Information Protection (el servicio Azure Rights Management no está activado):**

    Vea [Requisitos de Azure Information Protection](../get-started/requirements-azure-rms.md).

    Tenga en cuenta que, si tiene equipos que ejecutan Office 2010, debe instalar el cliente de Azure Information Protection, ya que este cliente proporciona la capacidad de autenticar a los usuarios en servicios en la nube. Para las versiones más recientes de Office, el cliente de Azure Information Protection es necesario para la clasificación y el etiquetado. Es opcional, pero se recomienda si se quieren proteger solo los datos. Para obtener más información, vea la [Guía para administradores del cliente de Azure Information Protection](../rms-client/client-admin-guide.md).

    Aunque es necesario tener una suscripción de Azure Information Protection para poder migrar de AD RMS, le recomendamos que no active el servicio Rights Management para el inquilino antes de iniciar la migración. En el proceso de migración se incluye este paso de activación después de exportar las claves y plantillas de AD RMS e importarlas al inquilino de Azure Information Protection. En cambio, si el servicio Rights Management ya está activado, aún podrá realizar la migración desde AD RMS con algunos pasos adicionales.


- **Preparación de Azure Information Protection:**

    - Sincronización de directorios entre el directorio local y Azure Active Directory

    - Grupos habilitados para correo en Azure Active Directory

    Consulte [Preparación de usuarios y grupos para Azure Information Protection](prepare.md).

- **Si ha usado la funcionalidad Information Rights Management (IRM) de Exchange Server** (por ejemplo, las reglas de transporte y Outlook Web Access) o SharePoint Server con AD RMS:

    - Plan durante un breve período de tiempo si IRM no estará disponible en estos servidores
 
    Aún puede usar IRM en estos servidores después de la migración. Sin embargo, uno de los pasos de migración es deshabilitar temporalmente el servicio IRM, instalar y configurar un conector, volver a configurar los servidores y, a continuación, volver a habilitar IRM.

    Se trata de la única interrupción del servicio durante el proceso de migración.

- **Si quiere administrar su propia clave de inquilino de Azure Information Protection con una clave protegida por HSM**:

    - Para esta configuración opcional se necesita el Almacén de claves de Azure y una suscripción de Azure compatible con un almacén de claves con claves protegidas por HSM. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


### <a name="cryptographic-mode-considerations"></a>Consideraciones del modo criptográfico

Si el clúster de AD RMS está actualmente en el modo criptográfico 1, no lo actualice al modo criptográfico 2 antes de iniciar la migración. En su lugar, realice la migración con el modo criptográfico 1 y regenere la clave de inquilino al final de la migración, como una de las tareas posteriores a la migración.

El modo criptográfico 1 solo se admite durante el proceso de migración.

Para confirmar el modo criptográfico de AD RMS:
 
- Para Windows Server 2012 R2 y Windows 2012: Propiedades del clúster de AD RMS > pestaña **General**. 

- Para Windows Server 2008 R2: compruebe si la revisión [RSA key length is increased to 2048 bits for AD RMS in Windows Server 2008 R2 and in Windows Server 2008](https://support.microsoft.com/help/2627272/rsa-key-length-is-increased-to-2048-bits-for-ad-rms-in-windows-server ) (Se ha aumentado la longitud de la clave RSA hasta 2048 bits para AD RMS en Windows Server 2008 R2 y Windows Server 2008) está instalada. Si no lo está, el clúster AD RMS se ejecuta en Modo criptográfico 1.

### <a name="migration-limitations"></a>Limitaciones de la migración

-   Aunque el proceso de migración permite migrar el certificado de licencia de servidor (SLC) a un módulo de seguridad de hardware (HSM) para Azure Information Protection, Exchange Online no es compatible actualmente con esta configuración para el servicio Rights Management usado por Azure Information Protection. Si quiere usar todas las funciones de IRM con Exchange Online después de migrar a Azure Information Protection, es necesario que la clave de inquilino de Azure Information Protection sea [administrada por Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). También puede ejecutar IRM con funcionalidad reducida en Exchange Online cuando sea el usuario quien administre la clave de inquilino de Azure Information Protection (BYOK). Para obtener más información sobre cómo usar Exchange Online con el servicio Azure Rights Management, vea [Paso 8. Configure la integración de IRM con Exchange Online](migrate-from-ad-rms-phase4.md#step-8-configure-irm-integration-for-exchange-online) con estas instrucciones de migración.

-   Si tiene software y clientes que no son compatibles con el servicio Rights Management usado por Azure Information Protection, no podrán proteger o usar contenido protegido por Azure Rights Management. Asegúrese de consultar las secciones de clientes y aplicaciones compatibles de [Requisitos para Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Si su implementación de AD RMS está configurada para colaborar con asociados externos (por ejemplo, con federación o dominios de usuario de confianza), estos también necesitarán realizar la migración a Azure Information Protection al mismo tiempo o lo antes posible después de completar la migración. Para seguir teniendo acceso al contenido protegido anteriormente por su organización con Azure Information Protection, necesitarán realizar cambios en la configuración del cliente similares a los que realice el usuario y que se incluyen en este documento.

    Debido a las posibles variaciones de configuración de los asociados, las instrucciones exactas para este cambio de configuración están fuera del ámbito de este documento. En cambio, vea la siguiente sección para obtener una guía de planeación y, para obtener ayuda adicional, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## <a name="migration-planning-if-you-collaborate-with-external-partners"></a>Planeación de la migración si colabora con asociados externos

Incluya los asociados de AD RMS en la fase de planeación de la migración porque también habrá que migrarlos a Azure Information Protection. Antes de realizar los siguientes pasos de migración, asegúrese de que se cumplan las siguientes condiciones:

- Tienen un inquilino de Azure Active Directory que admite el servicio Azure Rights Management.  
    
    Por ejemplo, tienen una suscripción a Office 365 E3 o E5, una suscripción a Enterprise Mobility + Security o una suscripción independiente a Azure Information Protection.

- Su servicio de Azure Rights Management aún no está activado, pero conocen su dirección URL de servicio de Azure Rights Management.

    Pueden obtener esta información al instalar la herramienta de Azure Rights Management, conectarse al servicio ([Connect-AadrmService](/powershell/aadrm/vlatest/connect-aadrmservice)) y, después, ver su información de inquilino del servicio de Azure Rights Management ([Get-AadrmConfiguration](/powershell/aadrm/vlatest/get-aadrmconfiguration)).

- Le han proporcionado las direcciones URL de su clúster de AD RMS y su dirección URL de servicio de Azure Rights Management para que pueda configurar los clientes migrados y redirigir las solicitudes de su contenido protegido de AD RMS al servicio de Azure Rights Management de sus inquilinos. Las instrucciones para configurar el redireccionamiento cliente están en el paso 7.

- Importarán sus claves raíz de clúster de AD RMS (SLC) en el inquilino antes de que empiece a migrar los usuarios. De forma similar, debe importar sus claves raíz de clúster de AD RMS antes de empezar a migrar sus usuarios. Las instrucciones para importar la clave se encuentran en este proceso de migración, en el [Paso 4. Exporte los datos de configuración de AD RMS e impórtelos en Azure Information Protection](migrate-from-ad-rms-phase2.md#step-4-export-configuration-data-from-ad-rms-and-import-it-to-azure-information-protection). 

## <a name="overview-of-the-steps-for-migrating-ad-rms-to-azure-information-protection"></a>Información general sobre los pasos para migrar AD RMS a Azure Information Protection

Los pasos de migración se pueden dividir en cinco fases que se pueden realizar en momentos diferentes y por distintos administradores.

[**FASE 1: PREPARACIÓN DE LA MIGRACIÓN**](migrate-from-ad-rms-phase1.md)

- **Paso 1: descarga de la herramienta de administración de Azure RMS e identificar la dirección URL del inquilino**

    El proceso de migración requiere que ejecute uno o varios de los cmdlets de PowerShell desde el módulo de Azure RMS que se instala con la herramienta de administración de Azure RMS Management. También necesita saber la dirección URL de servicio de Azure Rights Management de su inquilino para completar muchos de los pasos de la migración. Puede identificar este valor mediante PowerShell.

- **Paso 2. Preparación para la migración de clientes**

     Si no puede migrar todos los clientes a la vez y los migrará en lotes, use controles de incorporación e implemente un script previo a la migración.

- **Paso 3: preparación de la implementación de Exchange para la migración**

    Este paso es necesario si usa actualmente la característica de IRM de Exchange Online o Exchange local para proteger los correos electrónicos.

[**FASE 2: CONFIGURACIÓN DEL LADO SERVIDOR PARA AD RMS**](migrate-from-ad-rms-phase2.md)

- **Paso 4. Exportar los datos de configuración de AD RMS e importarlos en Azure Information Protection**

    Exporte los datos de configuración (claves, plantillas y direcciones URL) de AD RMS a un archivo XML y, después, suba ese archivo al servicio Azure Rights Management de Azure Information Protection con el cmdlet Import-AadrmTpd de PowerShell. A continuación, identifique qué clave de certificado de emisor de licencias de servidor (SLC) importada desea utilizar como la clave de inquilino para el servicio Azure Rights Management. Podrían ser necesarios pasos adicionales, dependiendo de la configuración de claves de AD RMS:

    - **Migración entre claves protegidas por software**:

        Claves administradas de forma centralizada y basadas en contraseña en AD RMS a clave de inquilino de Azure Information Protection administrada por Microsoft. Esta es la ruta de migración más sencilla y no se necesita ningún paso adicional.

    - **Migración entre claves protegidas por HSM**:

        Claves almacenadas por un HSM para AD RMS en una clave de inquilino de Azure Information Protection administrada por el cliente (el escenario “aportar tu propia clave” o BYOK). Para completar este procedimiento es necesario realizar pasos adicionales para transferir la clave desde el HSM de Thales local a Azure Key Vault y autorizar al servicio Azure Rights Management a usar esta clave. Su clave protegida por HSM existente tiene que estar protegida por módulo, ya que Rights Management Services no admite las claves protegidas por OCS.

    - **Migración de clave protegida por software a clave protegida por HSM**:

        Claves basadas en contraseña y administradas de forma centralizada en AD RMS para la clave de inquilino de Azure Information Protection administrada por el cliente (el escenario “aportar tu propia clave” o BYOK). Este procedimiento es el que necesita más configuraciones, ya que primero hay que extraer la clave de software e importarla en un HSM local y, después, completar los pasos adicionales para transferir la clave desde el HSM de Thales local a un HSM de Azure Key Vault y autorizar al servicio Azure Rights Management a usar el almacén de claves donde se almacena la clave.

- **Paso 5. Activación del servicio de Azure Rights Management**

    Si es posible, realice este paso después del proceso de importación y no antes. Si el servicio se activó antes de la importación, se requieren pasos adicionales.

- **Paso 6. Configurar las plantillas importadas**

    Al importar las plantillas de directiva de derechos, su estado se archiva. Si quiere que los usuarios puedan verla y usarla, debe cambiar el estado de la plantilla a publicada en el Portal de Azure clásico.


[**FASE 3: CONFIGURACIÓN DEL LADO CLIENTE**](migrate-from-ad-rms-phase3.md)

- **Paso 7: reconfiguración de los clientes para usar Azure Information Protection**

    Debe volver a configurar los equipos Windows existentes para usar el servicio de Azure Rights Management en lugar de AD RMS. Este paso se aplica a los equipos de su organización y en los equipos de las organizaciones asociadas si ha colaborado con ellas al ejecutar AD RMS.

    Además, si ha implementado la [extensión de dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx) para admitir dispositivos móviles como iPads y teléfonos iOS, teléfonos y tabletas Android, Windows Phone y equipos Mac, debe quitar los registros SRV en DNS que redirigen estos clientes para usar AD RMS.


[**FASE 4: CONFIGURACIÓN DE SERVICIOS AUXILIARES**](migrate-from-ad-rms-phase4.md)

- **Paso 8: configuración de la integración de IRM en Exchange Online**

    Este paso completa la migración de AD RMS para Exchange Online para usar ahora el servicio de Azure Rights Management.

- **Paso 9: configuración de la integración de IRM para Exchange Server y SharePoint Server**

    Este paso completa la migración de AD RMS para Exchange o SharePoint local para usar el servicio de Azure Rights Management, que requiere la implementación del conector Rights Management.


[**FASE 5: TAREAS POSTERIORES A LA MIGRACIÓN**](migrate-from-ad-rms-phase5.md )

- **Paso 10: desaprovisionamiento de AD RMS**

    Cuando haya confirmado que todos los clientes usan el servicio Azure Rights Management y ya no obtienen acceso a los servidores de AD RMS, puede desaprovisionar la implementación de AD RMS.

- **Paso 11: quitar controles de incorporación**

    Ya no son necesarios los controles de incorporación configurados durante la fase de preparación.

- **Paso 12: regenerar la clave de inquilino de Azure Information Protection**

    Este paso es necesario si no estaba realizando la ejecución en modo criptográfico 2 antes de la migración y es opcional pero recomendado para que todas las migraciones ayuden a proteger la seguridad de la clave de inquilino de Azure Information Protection.


## <a name="next-steps"></a>Pasos siguientes
Para iniciar la migración, vaya a [Fase 1: preparación](migrate-from-ad-rms-phase1.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]
