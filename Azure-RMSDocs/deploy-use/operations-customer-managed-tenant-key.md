---
# required metadata

title: "Administración de cliente: Operaciones de ciclo de vida de clave de inquilino | Azure RMS"
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: c5b19c59-812d-420c-9c54-d9776309636c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Administración de cliente: Operaciones de ciclo de vida de clave de inquilino

*Se aplica a: Azure Rights Management, Office 365*

Si administra su clave de inquilino para Azure Rights Management (el escenario Aportar tu propia clave, o BYOK), use las siguientes secciones para más información acerca de las operaciones del ciclo de vida que son relevantes para esta topología.

## Revocar su clave de inquilino
Cuando anule la suscripción de Azure RMS, Azure RMS dejará de usar su clave de inquilino y no será necesario que realice ninguna acción.

## Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, debe desactivar el estado de RMS en los equipos usando la directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure RMS retiene su clave de inquilino antigua para que pueda emitir licencias para contenido antiguo.

Para volver a crear la clave del inquilino, genere y cree una nueva clave a través de Internet o en persona. Para ello, use los procedimientos de la sección [Implementación de "Aporte su propia clave" (BYOK)](..\plan-design\plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) del tema [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](..\plan-design\plan-implement-tenant-key.md).

## Realizar una copia de seguridad y recuperar la clave de inquilino
Es responsable de realizar copias de seguridad de su clave de inquilino. Si ha generado su clave de inquilino en un HSM de Thales, para realizar una copia de seguridad de la clave acortada, el archivo de Word y las tarjetas de administrador.

Si ha transferido su clave siguiendo los procedimientos de la sección [Implementación de "Aporte su propia clave" (BYOK)](../plan-design/plan-implement-tenant-key.md#implementing-your-azure-rights-management-tenant-key) desde el artículo [Planeamiento e implementación de la clave de inquilino de Azure Rights Management](../plan-design/plan-implement-tenant-key.md), Azure RMS conservará el archivo de clave acortado, para proteger frente a errores los nodos de Azure RMS. Sin embargo, no considere esto una copia de seguridad completa. Por ejemplo, si alguna vez necesita una copia de texto simple de su clave para usarla fuera de un HSM de Thales, Azure RMS no podrá recuperarla para usted porque solo tiene una copia no recuperable.

## Exportar su clave de inquilino
Si usa BYOK, no puede exportar su clave de inquilino desde Azure RMS. La copia en Azure RMS es irrecuperable. Si desea eliminar esta clave para que no se pueda volver a usar, póngase en contacto con los servicios de atención al cliente y soporte técnico de Microsoft (CSS).

## Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft notificará a sus administradores de inquilino de Azure RMS por correo electrónico usando la dirección que ha suministrado cuando realizó la suscripción.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción; Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Vea [Vuelva a introducir su clave de inquilino](#re-key-your-tenant-key)..|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en la tecnología HSM de generación actual.|Microsoft debe actualizar los HSM. Si no hay motivos para creer que la vulnerabilidad afectó a las claves, Microsoft indicará a todos los clientes que renueven sus claves de inquilino.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft debe actualizar Azure RMS para que admita nuevos algoritmos y longitudes de clave más largas que sean resistentes, e indica a todos los clientes que renueven sus claves de inquilino.|




<!--HONumber=Apr16_HO4-->


