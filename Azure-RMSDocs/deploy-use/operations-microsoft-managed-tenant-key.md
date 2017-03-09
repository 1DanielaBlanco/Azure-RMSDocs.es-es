---
title: "Administración de Microsoft: operaciones de ciclo de vida de clave de inquilino de AIP"
description: "Información sobre las operaciones del ciclo de vida que son relevantes si Microsoft administra la clave de inquilino para Azure Information Protection (la predeterminada)."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 2131f40b51f34de7637c242909f10952b1fa7d9f
ms.openlocfilehash: caacc4174ddb63e9c9091c0df294b93cf947a7c4
ms.lasthandoff: 02/24/2017


---


# <a name="microsoft-managed-tenant-key-lifecycle-operations"></a>Administración de Microsoft: Operaciones de ciclo de vida de clave de inquilino

>*Se aplica a: Azure Information Protection, Office 365*

Si Microsoft administra su clave de inquilino para Azure Information Protection (la predeterminada), use las secciones siguientes para obtener más información sobre las operaciones del ciclo de vida que son relevantes para esta topología.

## <a name="revoke-your-tenant-key"></a>Revocar su clave de inquilino
Al cancelar la suscripción a Azure Information Protection, la solución deja de usar la clave de inquilino y no es necesario realizar ninguna otra acción.

## <a name="re-key-your-tenant-key"></a>Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, necesita desactivar el estado de Rights Management en los equipos con una directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Para volver a generar la clave de inquilino, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) para abrir una **incidencia de soporte técnico de Azure Information Protection con una solicitud para volver a generar la clave de inquilino de Azure Information Protection**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Standard; la acción de volver a escribir la clave de inquilino no es un servicio de soporte técnico gratuito.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure Information Protection conserva su clave de inquilino anterior para que pueda emitir licencias para contenido antiguo.

## <a name="backup-and-recover-your-tenant-key"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Microsoft es responsable de realizar la copia de seguridad de su clave de inquilino y no se requiere que realice ninguna acción.

## <a name="export-your-tenant-key"></a>Exportar su clave de inquilino
Para exportar la configuración de Azure Information Protection y su clave de inquilino, siga las instrucciones de estos tres pasos:

### <a name="step-1-initiate-export"></a>Paso 1: Iniciar exportación

-   Para hacerlo, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support.md#to-contact-microsoft-support) para abrir una **incidencia de soporte técnico de Azure Information Protection con una solicitud para una exportación de clave de Azure Information Protection**. Necesita demostrar que es un administrador del inquilino de Azure Information Protection y que comprende que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico estándar; la exportación de la clave de inquilino no es un servicio de soporte técnico gratuito.

### <a name="step-2-wait-for-verification"></a>Paso 2: Esperar comprobación

-   Microsoft comprobará que la solicitud para liberar su clave de inquilino de Azure Information Protection es legítima. Este proceso puede tardar hasta 3 semanas.

### <a name="step-3-receive-key-instructions-from-css"></a>Paso 3: Recibir instrucciones de clave de CSS

-   Los Servicios de soporte al cliente de Microsoft (CSS) le enviarán la configuración de Azure Information Protection y la clave de inquilino cifrada en un archivo protegido por contraseña que tiene la extensión de nombre de archivo .tpd. Para ello, CSS le envía (como la persona que inició el informe) una herramienta por correo electrónico. Debe ejecutar la herramienta desde un símbolo del sistema de la siguiente manera:

    ```
    AadrmTpd.exe -createkey
    ```
    Esto genera un plan de claves RSA y guarda las mitades públicas y privadas como archivos en la carpeta actual. Por ejemplo: **PublicKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt** y **PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt**.

    Responda al correo electrónico de CSS, adjuntando el archivo que tiene un nombre que comienza por **PublicKey**. CSS le enviará un archivo TPD como archivo .xml que está cifrado con su clave de RSA. Copie este archivo en la misma carpeta en la que ejecutó la herramienta AadrmTpd originalmente y ejecute la herramienta de nuevo, con el archivo que comienza por **PrivateKey** y el archivo de CSS. Por ejemplo:

    ```
    AadrmTpd.exe -key PrivateKey-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt -target TPD-77172C7B-8E21-48B7-9854-7A4CEAC474D0.xml
    ```
    El resultado de este comando deben ser dos archivos: uno que contiene la contraseña de texto simple para el TPD protegido con contraseña y otro que es el propio TPD protegido con contraseña. Para fines de referencias cruzadas, ambos deben tener el mismo GUID que los archivos de clave pública y privada cuando ejecutó el comando AadrmTpd.exe -createkey:

    -   Password-FA29D0FE-5049-4C8E-931B-96C6152B0441.txt

    -   ExportedTPD-FA29D0FE-5049-4C8E-931B-96C6152B0441.xml

    Realice una copia de seguridad de estos archivos y guárdelos de manera segura para poder continuar descifrando el contenido protegido con esta clave de inquilino. Además, si está migrando a AD RMS, puede importar este archivo TPD (el archivo que empieza por **ExportedTDP**) a su servidor de AD RMS.

### <a name="step-4-ongoing-protect-your-tenant-key"></a>Paso 4: En curso: Proteger su clave de inquilino

-   Cuando haya recibido su clave de inquilino, manténgala a buen recaudo, ya que si alguien consigue acceso a ella, podrá descifrar todos los documentos que se hayan protegido con esa clave.

    Si el motivo para exportar la clave de inquilino es que ya no quiere usar Azure Information Protection, le recomendamos que desactive ahora el servicio Azure Rights Management del inquilino de Azure Information Protection. No se demore en hacerlo después de recibir su clave de inquilino, ya que esta precaución le ayudará a minimizar las consecuencias si alguien que no debería tener su clave de inquilino consigue acceso a ella. Para obtener más instrucciones, consulte [Retirada y desactivación de Azure Rights Management](decommission-deactivate.md).

## <a name="respond-to-a-breach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft enviará una notificación por correo electrónico a sus administradores de inquilino de Azure Information Protection, usando para ello la dirección que haya especificado al suscribirse.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Consulte la sección [Vuelva a introducir su clave de inquilino](operations-microsoft-managed-tenant-key.md#re-key-your-tenant-key) de este artículo.|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft necesita actualizar Azure Information Protection para que admita nuevos algoritmos y claves más largas que sean resistentes, así como indicar a todos los clientes que renueven sus claves de inquilino.|

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


