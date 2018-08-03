---
title: 'Administración de Microsoft: operaciones de ciclo de vida de clave de inquilino de AIP'
description: Información sobre las operaciones del ciclo de vida que son pertinentes si Microsoft administra la clave de inquilino para Azure Information Protection (la predeterminada).
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 03/07/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: cac2506f7c98431048c29291ca95f197a02c7fcd
ms.sourcegitcommit: 949bf02d5d12bef8e26d89ad5d6a0d5cc7826135
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39473770"
---
# <a name="microsoft-managed-tenant-key-life-cycle-operations"></a>Administración de Microsoft: Operaciones del ciclo de vida de claves de inquilino

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](http://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Si Microsoft administra su clave de inquilino para Azure Information Protection (la predeterminada), lea las secciones siguientes para saber profundizar en las operaciones del ciclo de vida que son relevantes para esta topología.

## <a name="revoke-your-tenant-key"></a>Revocar su clave de inquilino
Al cancelar la suscripción a Azure Information Protection, la solución deja de usar la clave de inquilino y no es necesario realizar ninguna otra acción.

## <a name="rekey-your-tenant-key"></a>Regenerar su clave de inquilino
La acción de regenerar la clave también se conoce como revertir la clave. Al realizar esta operación, Azure Information Protection deja de usar la clave de inquilino existente para proteger documentos y correos electrónicos, y comienza a usar otra clave. Las directivas y las plantillas se retiran inmediatamente, pero el cambio es gradual para los clientes y los servicios existentes que usen Azure Information Protection. De este modo, durante cierto tiempo, parte del contenido nuevo sigue protegido por la clave de inquilino anterior.

Para regenerar la clave, debe configurar el objeto de clave de inquilino y especificar la clave alternativa que se usará. A continuación, se marcará automáticamente la clave usada anteriormente como archivada para Azure Information Protection. Esta configuración garantiza que el contenido que se haya protegido con esta clave seguirá estando disponible.

Ejemplos de cuándo tendrá que regenerar la clave de Azure Information Protection:

- Ha realizado la migración de Active Directory Rights Management Services (AD RMS) mediante una clave de modo criptográfico 1. Ha finalizado la migración y quiere cambiar a una clave que use el modo criptográfico 2.

- La compañía se ha dividido en una o dos compañías. Cuando regenera la clave de inquilino, la nueva empresa no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

- Quiere cambiar de una topología de administración de claves a otra.

- Cree que la copia maestra de su clave de inquilino está en peligro.

Para regenerar la clave, puede seleccionar una clave administrada por Microsoft diferente para que pase a ser su clave de inquilino, pero no puede crear una clave administrada por Microsoft. Para crear una clave, debe cambiar la topología de clave para que la administre el cliente (BYOK).

Si ha realizado la migración desde Active Directory Rights Management Services (AD RMS) y elige la topología de clave administrada por Microsoft para Azure Information Protection, tendrá más de una clave administrada por Microsoft. En este escenario, tendrá al menos dos claves administrada por Microsoft para su inquilino. Al menos una de ellas será la clave que haya importado desde AD RMS. También tendrá la clave predeterminada que se creó automáticamente para su inquilino de Azure Information Protection.

Para seleccionar una clave diferente a su clave de inquilino activa de Azure Information Protection, use el cmdlet [Set-AadrmKeyProperties](/powershell/module/aadrm/set-aadrmkeyproperties) del módulo AADRM. Para ayudarle a identificar qué clave se usará, use el cmdlet [Get-AadrmKeys](/powershell/module/aadrm/get-aadrmkeys). Puede identificar la clave predeterminada que se ha creado automáticamente para su inquilino de Azure Information Protection ejecutado el comando siguiente:

    (Get-AadrmKeys) | Sort-Object CreationTime | Select-Object -First 1

Para cambiar la topología de claves para que la administre el cliente (BYOK), vea [Implementación de BYOK para la clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md#implementing-byok-for-your-azure-information-protection-tenant-key).

## <a name="backup-and-recover-your-tenant-key"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Microsoft es responsable de realizar la copia de seguridad de su clave de inquilino y no se requiere que realice ninguna acción.

## <a name="export-your-tenant-key"></a>Exportar su clave de inquilino
Para exportar la configuración de Azure Information Protection y su clave de inquilino, siga las instrucciones de estos tres pasos:

### <a name="step-1-initiate-export"></a>Paso 1: Iniciar exportación

- [Póngase en contacto con Soporte técnico de Microsoft](../information-support.md#to-contact-microsoft-support) para abrir una **incidencia de soporte técnico de Azure Information Protection en la que solicite exportar una clave de Azure Information Protection**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico estándar; la exportación de la clave de inquilino no es un servicio de soporte técnico gratuito.

### <a name="step-2-wait-for-verification"></a>Paso 2: Esperar comprobación

- Microsoft comprobará que la solicitud para liberar su clave de inquilino de Azure Information Protection es legítima. Este proceso puede tardar hasta tres semanas.

### <a name="step-3-receive-key-instructions-from-css"></a>Paso 3: Recibir instrucciones de clave de CSS

- Los Servicios de soporte técnico de Microsoft (CSS) le envían la configuración de Azure Information Protection y la clave de inquilino cifrada en un archivo protegido por contraseña. Este archivo tiene una extensión de nombre de archivo **.tpd**. Para ello, CSS le envía (como la persona que inició el informe) una herramienta por correo electrónico. Debe ejecutar la herramienta desde un símbolo del sistema de la siguiente manera:

    ```
    AadrmTpd.exe -createkey
    ```
    Esto genera un plan de claves RSA y guarda las mitades públicas y privadas como archivos en la carpeta actual. Por ejemplo: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** y **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Responda al correo electrónico de CSS, adjuntando el archivo que tiene un nombre que comienza por **PublicKey**. CSS le enviará un archivo TPD como archivo .xml que está cifrado con su clave de RSA. Copie este archivo en la misma carpeta en la que ejecutó la herramienta AadrmTpd originalmente y ejecute la herramienta de nuevo, con el archivo que comienza por **PrivateKey** y el archivo de CSS. Por ejemplo:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    El resultado de este comando deben ser dos archivos: uno que contiene la contraseña de texto sin formato para el TPD protegido con contraseña y otro que es el propio TPD protegido con contraseña. Los archivos tienen un nuevo GUID, por ejemplo:
     
    - Password-5E4C2018-8C8C-4548-8705-E3218AA1544E.txt

    - ExportedTPD-5E4C2018-8C8C-4548-8705-E3218AA1544E.xml

    Realice una copia de seguridad de estos archivos y guárdelos de manera segura para poder continuar descifrando el contenido protegido con esta clave de inquilino. Además, si está migrando a AD RMS, puede importar este archivo TPD (el archivo que empieza por **ExportedTDP**) a su servidor de AD RMS.

### <a name="step-4-ongoing-protect-your-tenant-key"></a>Paso 4: En curso: Proteger su clave de inquilino

Cuando haya recibido su clave de inquilino, manténgala a buen recaudo, ya que si alguien consigue acceso a ella, podrá descifrar todos los documentos que se hayan protegido con esa clave.

Si el motivo para exportar la clave de inquilino es que ya no quiere usar Azure Information Protection, le recomendamos que desactive ahora el servicio Azure Rights Management del inquilino de Azure Information Protection. No se demore en hacerlo después de recibir su clave de inquilino, ya que esta precaución le ayuda a minimizar las consecuencias si alguien que no debería tener su clave de inquilino consigue acceso a ella. Para obtener más instrucciones, consulte [Retirada y desactivación de Azure Rights Management](decommission-deactivate.md).

## <a name="respond-to-a-breach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegida, pueden encontrarse vulnerabilidades en la tecnología de generación de claves actual, así como en las longitudes y los algoritmos actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft enviará una notificación por correo electrónico a sus administradores de inquilino de Azure Information Protection, usando para ello la dirección de correo que haya especificado al suscribirse.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta depende de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Regenere su clave de inquilino. Consulte la sección [Regenerar su clave de inquilino](#rekey-your-tenant-key) de este artículo.|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|Regenerar la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft necesita actualizar Azure Information Protection para que admita nuevos algoritmos y claves más largas que sean resistentes, así como indicar a todos los clientes que renueven sus claves de inquilino.|


