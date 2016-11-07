---
title: "Administración de cliente: Operaciones de ciclo de vida de clave de inquilino | Azure Information Protection"
description: "Información sobre las operaciones del ciclo de vida que son relevantes si administra la clave de inquilino para Azure Information Protection (el escenario “aportar tu propia clave” o BYOK)."
author: cabailey
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b4abffcbe6e49ea25f3cf493a1e68fcd6ea25b26
ms.openlocfilehash: c879d4de6b8b99c401b36e03dd3b16dc8b722344


---


# <a name="customermanaged-tenant-key-lifecycle-operations"></a>Administración de cliente: Operaciones de ciclo de vida de clave de inquilino

>*Se aplica a: Azure Information Protection, Office 365*

Si administra su clave de inquilino para Azure Information Protection (el escenario “aportar tu propia clave” o BYOK), en las secciones siguientes encontrará más información sobre las operaciones del ciclo de vida relevantes para esta topología.

## <a name="revoke-your-tenant-key"></a>Revocar su clave de inquilino
En Azure Key Vault puede cambiar los permisos en el almacén de claves que contiene su clave de inquilino de Azure Information Protection para que el servicio Azure Rights Management ya no pueda acceder a la clave. Pero, tras hacer esto, ningún usuario podrá abrir los documentos y correos electrónicos que se protegieron anteriormente con el servicio Azure Rights Management.

Al cancelar la suscripción a Azure Information Protection, la solución deja de usar la clave de inquilino y no es necesario realizar ninguna otra acción.


## <a name="rekey-your-tenant-key"></a>Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, necesita desactivar el estado de Rights Management en los equipos con una directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure Information Protection conserva su clave de inquilino anterior para que pueda emitir licencias para contenido antiguo.

Para volver a generar la clave de inquilino, primero vuelva a generar la clave de inquilino de Azure Information Protection en Azure Key Vault. Después, vuelva a ejecutar el cmdlet Add-AadrmKeyVaultKey y especifique la nueva URL de clave.

## <a name="backup-and-recover-your-tenant-key"></a>Realizar una copia de seguridad y recuperar la clave de inquilino
Es responsable de realizar copias de seguridad de su clave de inquilino. Si ha generado su clave de inquilino en un HSM de Thales, para realizar una copia de seguridad de la clave acortada, el archivo de Word y las tarjetas de administrador.

Si ha transferido la clave según los procedimientos de la sección [Implementación del método Aportar tu propia clave (BYOK)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) del artículo [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md), el Almacén de claves conservará el archivo de clave acortada como medida de protección en caso de que se produzcan errores en algún nodo de servicio. Este archivo está vinculado al mundo de la seguridad para la región o instancia específica de Azure. Sin embargo, no considere esto una copia de seguridad completa. Por ejemplo, si alguna vez necesita una copia de texto sin formato de la clave para usarla fuera de un HSM de Thales, el Almacén de claves de Azure no podrá recuperarla, ya que solo tiene una copia no recuperable.

## <a name="export-your-tenant-key"></a>Exportar su clave de inquilino
Si usa BYOK, no podrá exportar su clave de inquilino desde Azure Key Vault o desde Azure Information Protection. La copia del Almacén de claves de Azure no se puede recuperar. 

## <a name="respond-to-a-breach"></a>Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft enviará una notificación por correo electrónico a sus administradores de inquilino de Azure Information Protection, usando para ello la dirección que haya especificado al suscribirse.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Vea [Regeneración de la clave de inquilino](#re-key-your-tenant-key).|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en la tecnología HSM de generación actual.|Microsoft debe actualizar los HSM. Si no hay motivos para creer que la vulnerabilidad afectó a las claves, Microsoft indicará a todos los clientes que renueven sus claves de inquilino.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft necesita actualizar Azure Key Vault o Azure Information Protection para que admitan nuevos algoritmos y claves más largas que sean resistentes, así como indicar a todos los clientes que renueven sus claves de inquilino.|





<!--HONumber=Nov16_HO1-->


