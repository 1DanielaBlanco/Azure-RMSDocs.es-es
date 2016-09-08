---
title: "Migración desde AD RMS a Azure Rights Management | Azure RMS"
description: "Use el siguiente conjunto de instrucciones para migrar su implementación de Active Directory Rights Management Services (AD RMS) en Azure Rights Management (Azure RMS). Después de la migración, los usuarios seguirán teniendo acceso a documentos y mensajes de correo electrónico que su organización protege mediante AD RMS, mientras que el contenido protegido recientemente usará Azure RMS."
author: cabailey
manager: mbaldwin
ms.date: 08/17/2016
ms.topic: article
ms.prod: 
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 26b043f1f9e7a1e0cd00c2f31c28f7d6685f0232
ms.openlocfilehash: bead12db04e6fcf2f9e4af5148d3f8a4ef4089da


---

# Migración desde AD RMS a Azure Rights Management

>*Se aplica a: Active Directory Rights Management Services, Azure Rights Management*

Use el siguiente conjunto de instrucciones para migrar su implementación de Active Directory Rights Management Services (AD RMS) en Azure Rights Management (Azure RMS). Después de la migración, los usuarios seguirán teniendo acceso a documentos y mensajes de correo electrónico que su organización protege mediante AD RMS, mientras que el contenido protegido recientemente usará Azure RMS.

¿No está seguro de si esta migración de AD RMS es conveniente para su organización?

-   Para obtener una introducción a Azure RMS, los problemas empresariales que puede resolver, cómo lo ven administradores y usuarios y cómo funciona, consulte [¿Qué es Azure Rights Management?](../understand-explore/what-is-azure-rms.md).

-   Para obtener una comparación de Azure RMS con AD RMS, consulte [Comparación de Azure Rights Management y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Requisitos previos para la migración desde AD RMS a Azure RMS.
Antes de iniciar la migración a Azure RMS, asegúrese de que se cumplen los siguientes requisitos previos y de que conoce las limitaciones.


- **Una implementación de RMS compatible:**
    
    - Las siguientes versiones de AD RMS son compatibles con una migración a Azure RMS:
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - Modo criptográfico 2:
    
        - Es necesario que los servidores y los clientes de AD RMS se ejecuten en el modo criptográfico 2 antes de iniciar la migración a Azure RMS. Para obtener más información, vea [AD RMS Cryptographic Modes](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx) (Modos criptográficos de AD RMS).
        
    - Se admiten todas las topologías de AD RMS válidas:
    
        - Bosque único, un solo clúster de RMS
        
        - Bosque único, varios clústeres de RMS solo con licencias
        
        - Varios bosques, varios clústeres de RMS
        
    Nota: De forma predeterminada, varios clústeres de RMS se migran a un único inquilino de Azure RMS. Si quiere usar inquilinos de Azure RMS independientes, tendrá que considerarlos como migraciones diferentes. No se puede importar una clave de un clúster de RMS a más de un inquilino de Azure RMS.

- **Todos los requisitos para ejecutar Azure RMS, incluido un inquilino de Azure RMS (no activado):**

    Consulte [Requisitos de Azure Rights Management](../get-started/requirements-azure-rms.md).

    Aunque debe tener un inquilino de Azure RMS para poder migrar desde AD RMS, se recomienda que no active el servicio Rights Management antes de la migración. El proceso de migración incluye este paso después de exportar las claves y plantillas de AD RMS e importarlas en Azure RMS. Sin embargo, aunque esté activado Azure RMS, puede migrar desde AD RMS.


- **Preparación para Azure RMS:**

    - Sincronización de directorios entre el directorio local y Azure Active Directory

    - Grupos habilitados para correo en Azure Active Directory

    Consulte [Preparación de Azure Rights Management](prepare.md).


- **Si ha usado la funcionalidad Information Rights Management (IRM) de Exchange Server** (por ejemplo, las reglas de transporte y Outlook Web Access) o SharePoint Server con AD RMS:

    - Plan durante un breve período de tiempo si IRM no estará disponible en estos servidores
 
    Aún puede utilizar IRM en estos servidores con Azure RMS después de la migración. Sin embargo, uno de los pasos de migración es deshabilitar temporalmente el servicio IRM, instalar y configurar un conector, volver a configurar los servidores y, a continuación, volver a habilitar IRM.

    Se trata de la única interrupción del servicio durante el proceso de migración.

- **Si quiere administrar su propia clave de inquilino de Azure RMS con una clave protegida por HSM**:

    - Para esta configuración opcional se necesita el Almacén de claves de Azure y una suscripción de Azure compatible con un almacén de claves con claves protegidas por HSM. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


Limitaciones:

-   Aunque el proceso de migración permite migrar la clave del certificado de licencias del servidor (SLC) a un módulo de seguridad de hardware (HSM) para Azure RMS, Exchange Online actualmente no admite esta configuración. Si quiere usar la funcionalidad completa de IRM con Exchange Online después de migrar a Azure RMS, la clave del inquilino de Azure RMS debe estar [administrada por Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). Como alternativa, puede ejecutar IRM con funcionalidad reducida en Exchange Online cuando sea el usuario quien  administre el inquilino de Azure RMS (BYOK). Para más información sobre el uso de Exchange Online con Azure RMS, consulte [Paso 6. Configure la integración de IRM con Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) con estas instrucciones de migración.

-   Si tiene software y clientes que no son compatibles con Azure RMS, no podrá proteger o consumir contenido protegido por Azure RMS. Asegúrese de consultar las secciones de clientes y aplicaciones compatibles del artículo [Requisitos para Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Si importa su clave de local a Azure RMS como archivada (sin establecer el TPD como activo durante el proceso de importación) y migra los usuarios en lotes en una migración por fases, el contenido protegido recientemente por los usuarios migrados no será accesible para los usuarios que permanecen en AD RMS. En este escenario, siempre que sea posible, mantenga un tiempo de migración corto y migre los usuarios en lotes lógicos, de forma que si colaboran entre sí se miren juntos.

    Esta limitación no se aplica cuando se establece el TPD como activo durante el proceso de importación, porque todos los usuarios protegerán el contenido con la misma clave. Se recomienda esta configuración, ya que le permite migrar todos los usuarios de forma independiente y a su propio ritmo.

-   Si colabora con asociados externos (por ejemplo, mediante el uso de la federación o de dominios de usuario de confianza), estos también deberán migrar a Azure RMS al mismo tiempo o tan pronto como sea posible una vez haya completado la migración. Para seguir teniendo acceso al contenido previamente protegido por su organización con AD RMS, se deberán realizar cambios en la configuración del cliente similares a los que realice el usuario, incluidos en este documento.

    Debido a las posibles variaciones de configuración de los asociados, las instrucciones exactas para este cambio de configuración están fuera del ámbito de este documento. Para obtener ayuda, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## Introducción de los pasos de migración de AD RMS a Azure RMS


Los pasos de migración se pueden dividir en cuatro fases que se pueden realizar en momentos diferentes y por distintos administradores.

[**FASE 1: CONFIGURACIÓN DEL LADO SERVIDOR PARA AD RMS**](migrate-from-ad-rms-phase1.md)

- **Paso 1: Descarga de la herramienta de administración de Azure RMS Management**

    El proceso de migración requiere que ejecute uno o varios de los cmdlets de Windows PowerShell desde el módulo de Azure RMS que se instala con la herramienta de administración de Azure RMS Management.

- **Paso 2. Exporte los datos de configuración de AD RMS e impórtelos en Azure RMS.**

    Exporte los datos de configuración (claves, plantillas y direcciones URL) de AD RMS a un archivo XML y, luego, cargue ese archivo en Azure RMS mediante el cmdlet Import-AadrmTPD de Windows PowerShell. Podrían ser necesarios pasos adicionales, dependiendo de la configuración de claves de AD RMS:

    - **Migración entre claves protegidas por software**:

        Claves administradas centralmente basadas en contraseña de AD RMS para la clave de inquilino de Azure RMS administrada por Microsoft. Esta es la ruta de migración más sencilla y no se necesita ningún paso adicional.

    - **Migración entre claves protegidas por HSM**:

        De claves almacenadas por un módulo de seguridad de hardware (HSM) para AD RMS a clave de inquilino de Azure RMS administrada por el cliente (el escenario "aporte su propia clave" o BYOK). Para completar este procedimiento es necesario realizar pasos adicionales para transferir la clave desde el HSM de Thales local al Almacén de claves de Azure y autorizar a Azure RMS a usar esta clave. Su clave protegida por HSM existente tiene que estar protegida por módulo, ya que Rights Management Services no admite las claves protegidas por OCS.

    - **Migración de clave protegida por software a clave protegida por HSM**:

        Claves basadas en contraseña administradas centralmente en AD RMS para la clave del inquilino de Azure RMS administrada por clientes (el escenario "bring your own key" o "BYOK"). Este procedimiento es el que necesita más configuraciones, ya que primero hay que extraer la clave de software e importarla en un HSM local y, después, completar los pasos adicionales para transferir la clave desde el HSM de Thales a un HSM del Almacén de claves de Azure y autorizar a Azure RMS a usar el almacén de claves donde se almacena la clave.

- **Paso 3: Activación del inquilino de Azure RMS**

    Si es posible, realice este paso después del proceso de importación y no antes.

- **Paso 4. Configure las plantillas importadas.**

    Al importar las plantillas de directiva de derechos, su estado se archiva. Si quiere que los usuarios puedan verla y usarla, debe cambiar el estado de la plantilla a publicada en el Portal de Azure clásico.


[**FASE 2: CONFIGURACIÓN DEL LADO CLIENTE**](migrate-from-ad-rms-phase2.md)


- **Paso 5: Reconfiguración de clientes para usar Azure RMS**

    Debe volver a configurar los equipos de Windows existentes para utilizar el servicio de Azure RMS en lugar de AD RMS. Este paso se aplica a los equipos de su organización y en los equipos de las organizaciones asociadas si ha colaborado con ellas al ejecutar AD RMS.

    Además, si ha implementado la [extensión para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx) para admitir dispositivos móviles como iPads y teléfonos iOS, teléfonos y tabletas Android, Windows Phone y equipos Mac, debe quitar los registros SRV en DNS que redirigen estos clientes para usar AD RMS.


[**FASE 3: CONFIGURACIÓN DE SERVICIOS AUXILIARES**](migrate-from-ad-rms-phase3.md)


- **Paso 6: Configuración de la integración de IRM con Exchange Online.**

    Este paso es necesario si desea usar Exchange Online con Azure RMS.


- **Paso 7: Implementación del conector RMS**

    Este paso es necesario si desea utilizar cualquiera de los siguientes servicios locales con Azure RMS:

    - Exchange Server (por ejemplo, las reglas de transporte y Outlook Web Access)

    - Servidor de SharePoint

    - Windows Server que se ejecuta la infraestructura de clasificación de archivos (FCI)


[**FASE 4: TAREAS POSTERIORES A LA MIGRACIÓN**](migrate-from-ad-rms-phase4.md )

- **Paso 8. Retire AD RMS**

    Cuando haya confirmado que todos los clientes usan Azure RMS y ya no obtienen acceso a los servidores de AD RMS, puede retirar la implementación de AD RMS.


- **Paso 9: Regeneración de la clave del inquilino de Azure RMS**

    Aunque este paso es opcional, se recomienda completarlo si la topología de claves de inquilino de Azure RMS que ha elegido en el paso 2 es administrada por Microsoft. Este paso no es válido si la topología de claves de inquilino de Azure RMS que ha elegido es administrada por el cliente (BYOK).


## Pasos siguientes
Para iniciar la migración, vaya a [Fase 1: Configuración del lado servidor](migrate-from-ad-rms-phase1.md).




<!--HONumber=Aug16_HO4-->


