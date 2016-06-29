---
# required metadata

title: "Administración de Microsoft: Operaciones de ciclo de vida de clave de inquilino | Azure RMS"
description:
keywords:
author: cabailey
manager: mbaldwin
ms.date: 06/14/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 3c48cda6-e004-4bbd-adcf-589815c56c55

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: esaggese
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---


# Administración de Microsoft: Operaciones de ciclo de vida de clave de inquilino

*Se aplica a: Azure Rights Management, Office 365*

Si Microsoft administra su clave de inquilino para Azure Rights Management (la predeterminada), use las siguientes secciones para más información acerca de las operaciones del ciclo de vida que son relevantes para esta topología.

## Revocar su clave de inquilino
Cuando anule la suscripción de Azure RMS, Azure RMS dejará de usar su clave de inquilino y no será necesario que realice ninguna acción.

## Vuelva a introducir su clave de inquilino
La acción de volver a introducir la clave también se le conoce como revertir su clave. No vuelva a introducir su clave de inquilino a menos que sea necesario. Otros clientes, como Office 2010, no se diseñaron para tratar cambios de clave correctamente. En este escenario, debe desactivar el estado de RMS en los equipos usando la directiva de grupo o un mecanismo equivalente. Sin embargo, hay algunos eventos legítimos que pueden forzarle a volver a introducir la clave de inquilino. Por ejemplo:

-   La compañía se ha dividido en una o dos compañías. Cuando vuelve a introducir la clave de inquilino, la nueva compañía no tendrá acceso al nuevo contenido que publiquen sus empleados. Pueden acceder al antiguo contenido si tienen una copia de la antigua clave de inquilino.

-   Cree que la copia maestra de su clave de inquilino (la copia en su posesión) se ha puesto en peligro.

Puede volver a escribir la clave de inquilino al [ponerse en contacto con el soporte técnico de Microsoft](../get-started/information-support#to-contact-microsoft-support) para abrir un **caso de soporte técnico de Azure Rights Management con una solicitud para volver a escribir la clave de inquilino de Azure RMS**. Debe demostrar que es un administrador del inquilino de Azure RMS y comprender que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico Standard; la acción de volver a escribir la clave de inquilino no es un servicio de soporte técnico gratuito.

Cuando vuelve a introducir su clave de inquilino, el nuevo contenido está protegido usando la nueva clave de inquilino. Esto sucede en fases, por lo que para un período de tiempo, algún contenido nuevo continuará siendo protegido por la antigua clave de inquilino. El contenido protegido anteriormente permanece protegido para su antigua clave de inquilino. Para admitir este escenario, Azure RMS retiene su clave de inquilino antigua para que pueda emitir licencias para contenido antiguo.

## Realizar una copia de seguridad y recuperar la clave de inquilino
Microsoft es responsable de realizar la copia de seguridad de su clave de inquilino y no se requiere que realice ninguna acción.

## Exportar su clave de inquilino
Puede exportar su configuración de Azure RMS y su clave de inquilino siguiendo las instrucciones de estos tres pasos:

### Paso 1: Iniciar exportación

-   Para ello, [póngase en contacto con el soporte técnico de Microsoft](../get-started/information-support#to-contact-microsoft-support) para abrir un **caso de soporte técnico de Azure Rights Management con una solicitud para una exportación de claves de Azure RMS**. Debe demostrar que es un administrador del inquilino de Azure RMS y comprender que este proceso tarda varios días en confirmarse. Se aplican cargos de soporte técnico estándar; la exportación de la clave de inquilino no es un servicio de soporte técnico gratuito.

### Paso 2: Esperar comprobación

-   Microsoft verifica que la solicitud para liberar su clave de inquilino de RMS es legítima. Este proceso puede tardar hasta 3 semanas.

### Paso 3: Recibir instrucciones de clave de CSS

-   Los Servicios de soporte al cliente de Microsoft (CSS) le enviarán su configuración de Azure RMS y clave de inquilino como cifrada en un archivo protegido con contraseña que tiene una extensión de nombre de archivo .tpd. Para ello, CSS le envía (como la persona que inició el informe) una herramienta por correo electrónico. Debe ejecutar la herramienta desde un símbolo del sistema de la siguiente manera:

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

### Paso 4: En curso: Proteger su clave de inquilino

-   Cuando haya recibido su clave de inquilino, manténgala a buen recaudo, ya que si alguien consigue acceso a ella, podrá descifrar todos los documentos que se hayan protegido con esa clave.

    Si el motivo por el que desea exportar la clave de inquilino es porque no quiere usar más Azure RMS, como procedimiento recomendado, desactive en este momento su inquilino de RMS. No se demore en hacerlo después de recibir su clave de inquilino, ya que esta precaución le ayudará a minimizar las consecuencias si alguien que no debería tener su clave de inquilino consigue acceso a ella. Para obtener más instrucciones, consulte [Retirada y desactivación de Azure Rights Management](decommission-deactivate.md).

## Responder a una infracción
Ningún sistema de seguridad, por seguro que sea, está completo sin un proceso de respuesta a infracción. Puede que se haya robado o puesto en peligro su clave de inquilino. Aunque esté bien protegido, se pueden encontrar vulnerabilidades en la tecnología HSM de la generación actual o algoritmos y longitudes de clave actuales.

Microsoft tiene un equipo dedicado a responder a incidentes de seguridad en sus productos y servicios. Tan pronto como aparece un informe fiable de un incidente, este equipo se pone a investigar el alcance, la causa del origen del mismo y cómo mitigarlo. Si este incidente afecta a sus activos, Microsoft notificará a sus administradores de inquilino de Azure RMS por correo electrónico usando la dirección que ha suministrado cuando realizó la suscripción.

Si tiene una infracción, la mejor acción que usted o Microsoft puede llevar a cabo dependerá del alcance de la infracción. Microsoft trabajará con usted en este proceso. La tabla siguiente muestra algunas situaciones típicas y la respuesta probable, aunque la respuesta exacta dependerá de toda la información que se revele durante la investigación.

|Descripción del incidente|Respuesta probable|
|------------------------|-------------------|
|Se ha filtrado su clave de inquilino.|Vuelva a introducir su clave de inquilino. Vea la sección [Vuelva a introducir su clave de inquilino](operations-tenant-key#re-key-your-tenant-key) de este artículo.|
|Un individuo no autorizado o malware han tenido derechos de uso de su clave de inquilino, pero la clave en sí no se ha filtrado.|La nueva introducción de la clave de inquilino no resulta útil aquí y requiere el análisis de la causa principal. Si un error de software o de proceso ha sido el responsable de que un individuo no autorizado obtuviera acceso, dicha situación se debe resolver.|
|Vulnerabilidad descubierta en el algoritmo de RSA, o longitud de clave, o ataques por fuerza bruta se hacen factibles computacionalmente.|Microsoft debe actualizar Azure RMS para que admita nuevos algoritmos y longitudes de clave más largas que sean resistentes, e indica a todos los clientes que renueven sus claves de inquilino.|




<!--HONumber=Jun16_HO2-->


