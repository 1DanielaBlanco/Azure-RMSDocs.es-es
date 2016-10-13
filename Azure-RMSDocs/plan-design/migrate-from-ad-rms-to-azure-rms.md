---
title: "Migración desde AD RMS a Azure Information Protection | Azure Information Protection"
description: "Instrucciones para migrar la implementación de Active Directory Rights Management Services (AD RMS) a Azure Information Protection. Después de la migración, los usuarios seguirán teniendo acceso a los documentos y mensajes de correo electrónico protegidos por su organización con AD RMS, y el nuevo contenido protegido usará Azure Information Protection."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 828cf1f7-d0e7-4edf-8525-91896dbe3172
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bb240b92a86bfc37685556ba2ce71b9eea56ae88
ms.openlocfilehash: c3e926b48dfc66da71e4e3f16f9359b3cb8322c6


---

# Migración desde AD RMS a Azure Information Protection

>*Se aplica a: Active Directory Rights Management Services, Azure Information Protection, Office 365*

Use el siguiente conjunto de instrucciones para migrar su implementación de Active Directory Rights Management Services (AD RMS) a Azure Information Protection. Después de la migración, los usuarios seguirán teniendo acceso a documentos y mensajes de correo electrónico que la organización haya protegido con el uso de AD RMS y el nuevo contenido protegido usará el servicio Azure Rights Management de Azure Information Protection.

¿No está seguro de si esta migración de AD RMS es conveniente para su organización?

-   Vea una introducción a Azure Information Protection en [¿Qué es Azure Information Protection?](../understand-explore/what-is-information-protection.md)

-   Vea una comparación de Azure Information Protection y AD RMS en [Comparación entre Azure Rights Management y AD RMS](../understand-explore/compare-azure-rms-ad-rms.md).

## Requisitos previos para migrar AD RMS a Azure Information Protection
Antes de iniciar la migración a Azure Information Protection, asegúrese de que se cumplen los siguientes requisitos previos y de que conoce las limitaciones.

- **Una implementación de RMS compatible:**
    
    - Las versiones siguientes de AD RMS admiten una migración a Azure Information Protection:
    
        - Windows Server 2008 R2 (x64)
        
        - Windows Server 2012 (x64)
        
        - Windows Server 2012 R2 (x64)
        
    - Modo criptográfico 2:

        - Es necesario que los servidores y los clientes de AD RMS se ejecuten en el modo criptográfico 2 antes de iniciar la migración a Azure Information Protection.
        
        Aunque es necesario que la clave actual del certificado de emisor de licencias de servidor (SLC) use el modo criptográfico 2, las claves anteriores que se hayan configurado para el modo criptográfico 1 también se admiten en Azure Information Protection como claves archivadas. Para obtener más información sobre los modos criptográficos y como pasar al modo criptográfico 2, consulte [AD RMS Cryptographic Modes](https://technet.microsoft.com/library/hh867439(v=ws.10).aspx) (Modos criptográficos de AD RMS).
        
    - Se admiten todas las topologías de AD RMS válidas:
    
        - Bosque único, un solo clúster de RMS
        
        - Bosque único, varios clústeres de RMS solo con licencias
        
        - Varios bosques, varios clústeres de RMS
        
    Nota: De forma predeterminada, varios clústeres de RMS se migran a un único inquilino de Azure Information Protection. Si quiere usar inquilinos de Azure Information Protection independientes, necesita considerarlos como migraciones distintas. Una clave de un clúster de RMS no se puede importar a más de un inquilino de Azure Information Protection.

- **Todos los requisitos para ejecutar Azure Information Protection, incluido un inquilino de Azure Information Protection (no activado):**

    Vea [Requisitos de Azure Information Protection](../get-started/requirements-azure-rms.md).

    Aunque es necesario tener un inquilino de Azure Information Protection para poder migrar de AD RMS, le recomendamos que no active el servicio Rights Management antes de la migración. En el proceso de migración se incluye este paso después de exportar las claves y plantillas de AD RMS e importarlas en Azure Information Protection. Pero, si el servicio Rights Management ya está activado, aún podrá realizar la migración desde AD RMS.


- **Preparación de Azure Information Protection:**

    - Sincronización de directorios entre el directorio local y Azure Active Directory

    - Grupos habilitados para correo en Azure Active Directory

    Vea [Preparación de Azure Information Protection](prepare.md).


- **Si ha usado la funcionalidad Information Rights Management (IRM) de Exchange Server** (por ejemplo, las reglas de transporte y Outlook Web Access) o SharePoint Server con AD RMS:

    - Plan durante un breve período de tiempo si IRM no estará disponible en estos servidores
 
    Puede seguir usando IRM en estos servidores con el servicio Azure Rights Management después de la migración. Sin embargo, uno de los pasos de migración es deshabilitar temporalmente el servicio IRM, instalar y configurar un conector, volver a configurar los servidores y, a continuación, volver a habilitar IRM.

    Se trata de la única interrupción del servicio durante el proceso de migración.

- **Si quiere administrar su propia clave de inquilino de Azure Information Protection con una clave protegida por HSM**:

    - Para esta configuración opcional se necesita el Almacén de claves de Azure y una suscripción de Azure compatible con un almacén de claves con claves protegidas por HSM. Para obtener más información, consulte la [página de precios del Almacén de claves de Azure](https://azure.microsoft.com/en-us/pricing/details/key-vault/). 


Limitaciones:

-   Aunque el proceso de migración permite migrar el certificado de licencia de servidor (SLC) a un módulo de seguridad de hardware (HSM) para Azure Information Protection, Exchange Online no es compatible actualmente con esta configuración para el servicio Rights Management usado por Azure Information Protection. Si quiere usar todas las funciones de IRM con Exchange Online después de migrar a Azure Information Protection, es necesario que la clave de inquilino de Azure Information Protection sea [administrada por Microsoft](../plan-design/plan-implement-tenant-key.md#choose-your-tenant-key-topology-managed-by-microsoft-the-default-or-managed-by-you-byok). Como alternativa, puede ejecutar IRM con funcionalidad reducida en Exchange Online cuando sea el usuario quien administre el inquilino de Azure Information Protection (BYOK). Para más información sobre cómo usar Exchange Online con el servicio Azure Rights Management, vea [Paso 6. Configure la integración de IRM con Exchange Online](migrate-from-ad-rms-phase3.md#step-6-configure-irm-integration-for-exchange-online) con estas instrucciones de migración.

-   Si tiene software y clientes que no son compatibles con el servicio Rights Management usado por Azure Information Protection, no podrán proteger o usar contenido protegido por Azure Rights Management. Asegúrese de consultar las secciones de clientes y aplicaciones compatibles del artículo [Requisitos para Azure Rights Management](../get-started/requirements-azure-rms.md).

-   Si importa la clave de local en Azure Information Protection como archivada (sin establecer el TPD como activo durante el proceso de importación) y migra los usuarios en lotes en una migración por fases, el nuevo contenido protegido por los usuarios migrados no será accesible para los usuarios que permanecen en AD RMS. En este escenario, siempre que sea posible, mantenga un tiempo de migración corto y migre los usuarios en lotes lógicos, de forma que si colaboran entre sí se miren juntos.

    Esta limitación no se aplica cuando se establece el TPD como activo durante el proceso de importación, porque todos los usuarios protegerán el contenido con la misma clave. Se recomienda esta configuración, ya que le permite migrar todos los usuarios de forma independiente y a su propio ritmo.

-   Si colabora con asociados externos (por ejemplo, con federación o dominios de usuario de confianza), estos también necesitarán realizar la migración a Azure Information Protection al mismo tiempo (o lo antes posible) después de completar la migración. Para seguir teniendo acceso al contenido protegido anteriormente por su organización con Azure Information Protection, necesitarán realizar cambios en la configuración del cliente similares a los que realice el usuario y que se incluyen en este documento.

    Debido a las posibles variaciones de configuración de los asociados, las instrucciones exactas para este cambio de configuración están fuera del ámbito de este documento. Para obtener ayuda, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#support-options-and-community-resources).

## Información general sobre los pasos para migrar AD RMS a Azure Information Protection


Los pasos de migración se pueden dividir en cuatro fases que se pueden realizar en momentos diferentes y por distintos administradores.

[**FASE 1: CONFIGURACIÓN DEL LADO SERVIDOR PARA AD RMS**](migrate-from-ad-rms-phase1.md)

- **Paso 1: Descarga de la herramienta de administración de Azure RMS Management**

    El proceso de migración requiere que ejecute uno o varios de los cmdlets de Windows PowerShell desde el módulo de Azure RMS que se instala con la herramienta de administración de Azure RMS Management.

- **Paso 2. Exportar los datos de configuración de AD RMS e importarlos en Azure Information Protection**

    Exporte los datos de configuración (claves, plantillas y direcciones URL) de AD RMS a un archivo XML y, después, suba ese archivo al servicio Azure Rights Management de Azure Information Protection con el cmdlet Import-AadrmTpd de Windows PowerShell. Podrían ser necesarios pasos adicionales, dependiendo de la configuración de claves de AD RMS:

    - **Migración entre claves protegidas por software**:

        Claves administradas de forma centralizada y basadas en contraseña en AD RMS a clave de inquilino de Azure Information Protection administrada por Microsoft. Esta es la ruta de migración más sencilla y no se necesita ningún paso adicional.

    - **Migración entre claves protegidas por HSM**:

        Claves almacenadas por un HSM para AD RMS en una clave de inquilino de Azure Information Protection administrada por el cliente (el escenario “aportar tu propia clave” o BYOK). Para completar este procedimiento es necesario realizar pasos adicionales para transferir la clave desde el HSM de Thales local a Azure Key Vault y autorizar al servicio Azure Rights Management a usar esta clave. Su clave protegida por HSM existente tiene que estar protegida por módulo, ya que Rights Management Services no admite las claves protegidas por OCS.

    - **Migración de clave protegida por software a clave protegida por HSM**:

        Claves basadas en contraseña y administradas de forma centralizada en AD RMS para la clave de inquilino de Azure Information Protection administrada por el cliente (el escenario “aportar tu propia clave” o BYOK). Este procedimiento es el que necesita más configuraciones, ya que primero hay que extraer la clave de software e importarla en un HSM local y, después, completar los pasos adicionales para transferir la clave desde el HSM de Thales local a un HSM de Azure Key Vault y autorizar al servicio Azure Rights Management a usar el almacén de claves donde se almacena la clave.

- **Paso 3: Activar el inquilino de Azure Information Protection**

    Si es posible, realice este paso después del proceso de importación y no antes.

- **Paso 4. Configure las plantillas importadas.**

    Al importar las plantillas de directiva de derechos, su estado se archiva. Si quiere que los usuarios puedan verla y usarla, debe cambiar el estado de la plantilla a publicada en el Portal de Azure clásico.


[**FASE 2: CONFIGURACIÓN DEL LADO CLIENTE**](migrate-from-ad-rms-phase2.md)


- **Paso 5: Volver a configurar los clientes para usar Azure Information Protection**

    Necesita volver a configurar los equipos Windows existentes para usar el servicio de Azure Information Protection en lugar de AD RMS. Este paso se aplica a los equipos de su organización y en los equipos de las organizaciones asociadas si ha colaborado con ellas al ejecutar AD RMS.

    Además, si ha implementado la [extensión para dispositivos móviles](http://technet.microsoft.com/library/dn673574.aspx) para admitir dispositivos móviles como iPads y teléfonos iOS, teléfonos y tabletas Android, Windows Phone y equipos Mac, debe quitar los registros SRV en DNS que redirigen estos clientes para usar AD RMS.


[**FASE 3: CONFIGURACIÓN DE SERVICIOS AUXILIARES**](migrate-from-ad-rms-phase3.md)


- **Paso 6: Configuración de la integración de IRM con Exchange Online.**

    Este paso es necesario si quiere usar Exchange Online con el servicio Azure Rights Management de Azure Information Protection.


- **Paso 7: Implementación del conector RMS**

    Este paso es necesario si quiere usar cualquiera de los siguientes servicios locales con el servicio Azure Rights Management para proteger documentos de Office y correos electrónicos:

    - Exchange Server (por ejemplo, las reglas de transporte y Outlook Web Access)

    - Servidor de SharePoint

    - Windows Server que se ejecuta la infraestructura de clasificación de archivos (FCI)


[**FASE 4: TAREAS POSTERIORES A LA MIGRACIÓN**](migrate-from-ad-rms-phase4.md )

- **Paso 8. Retire AD RMS**

    Cuando haya confirmado que todos los clientes usan Azure Information Protection y ya no acceden a los servidores de AD RMS, puede retirar la implementación de AD RMS.


- **Paso 9: Volver a generar la clave de inquilino de Azure Information Protection**

    Aunque este paso es opcional, se recomienda completarlo si la topología de claves de inquilino de Azure Information Protection que ha elegido en el paso 2 es administrada por Microsoft. Este paso no es válido si la topología de claves de inquilino de Azure Information Protection que ha elegido es administrada por el cliente (BYOK).


## Pasos siguientes
Para iniciar la migración, vaya a [Fase 1: Configuración del lado servidor](migrate-from-ad-rms-phase1.md).




<!--HONumber=Sep16_HO4-->


