---
title: "¿Cómo funciona Azure RMS? | Azure RMS"
description: 
keywords: 
author: cabailey
manager: mbaldwin
ms.date: 06/02/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5d825d6c8b2c8b7a9c34ac940c5a08439a9ae562
ms.openlocfilehash: 505f2c94bb4fd056b4d2f51c147c6b0b84efac00


---


# ¿Cómo funciona Azure RMS? En segundo plano

*Se aplica a: Azure Rights Management, Office 365*

Una cuestión importante que hay que comprender acerca de cómo funciona Azure RMS es que el servicio de Rights Management (y Microsoft) no ve ni almacena sus datos como parte del proceso de protección de la información. La información que protege nunca se envía a Azure, ni se almacena allí, a menos que la almacene de manera explícita en Azure o use otro servicio en la nube que la almacene en Azure. Azure RMS simplemente hace que los datos de un documento sean ilegibles para cualquiera que no sea un usuario y servicio autorizado:

-   Los datos se cifran en el nivel de aplicación e incluyen una directiva que define el uso autorizado para ese documento.

-   Cuando se usa un documento protegido por un usuario legítimo o se procesa por un servicio autorizado, se descifran los datos del documento y se aplican derechos definidos en la directiva.

En un nivel alto, puede ver la manera en que funciona este proceso en la imagen siguiente. Se protege un documento que contiene la fórmula secreta y luego lo abre correctamente un usuario o servicio autorizado. El documento se protege con una clave de contenido (la clave verde de esta imagen). Es única para cada documento y se coloca en el encabezado de archivo donde se protege por su clave raíz de inquilino de RMS (la clave roja de esta imagen). Su clave de inquilino se puede generar y administrar por Microsoft o bien, puede generar y administrar su propia clave de inquilino.

A lo largo del proceso de protección cuando Azure RMS está cifrando y descifrando, y aplicando restricciones, autorizando y aplicando restricciones, la fórmula secreta nunca se envía a Azure.

![Cómo Azure RMS protege un archivo](../media/AzRMS_SecretColaFormula_final.png)

Para obtener una descripción detallada de lo que está sucediendo, vea la sección [Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de este artículo.

Para consultar detalles técnicos acerca de las longitudes de claves y algoritmos que usa Azure RMS, vea la siguiente sección.

## Controles criptográficos usados por Azure RMS: Longitudes de clave y algoritmos
Aunque no tenga que saber usted mismo cómo funciona RMS, puede que se le pregunte acerca de los controles criptográficos que usa, para asegurarse de que la protección de seguridad es estándar en el sector.


|Controles criptográficos|Uso en Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Longitud de clave: 128 bits y 256 bits [[1]](#footnote-1)|Protección de documentación|
|Algoritmo: RSA<br /><br />Longitud de clave: 2048 bits|Protección de claves|
|SHA-256|Firma de certificados|

###### Nota al pie 1 

La aplicación de uso compartido Rights Management usa 256 bits para la protección genérica y la protección nativa cuando el archivo tiene una extensión de nombre de archivo .ppdf o es un archivo de imagen o texto protegido (como .ptxt o .pjpg).

Almacenamiento y protección de las claves criptográficas:

- Azure RMS crea una sola clave AES ("clave de contenido") para cada documento o correo electrónico que protege. Esta clave se inserta en el documento y se mantiene aunque se edite el documento. 

- La clave de contenido tiene la protección de la clave RSA de la organización (la "clave de inquilino de Azure RMS") como parte de la directiva del documento, que también firma el autor de este. Esta clave de inquilino es común para todos los documentos y correos electrónicos de la organización protegidos por Azure RMS. La clave solo se puede cambiar con la intervención de un administrador de Azure RMS si la organización usa una clave de inquilino administrada por el cliente (que se conoce como "aportar tu propia clave" o BYOK). 

    Esta clave de inquilino tiene la protección de los servicios en línea de Microsoft, en un entorno muy controlado y bajo una estrecha supervisión. Al usar una clave de inquilino administrada por el cliente (BYOK), esta seguridad mejora gracias al uso de una matriz de módulos de seguridad de hardware (HSM) punteros en cada región de Azure, sin posibilidad de extraerse ni compartirse las claves bajo ninguna circunstancia. Para más información sobre la clave de inquilino y BYOK, vea [Planning and implementing your Azure Rights Management tenant key](../plan-design/plan-implement-tenant-key.md) (Planeación e implementación de la clave de inquilino de Azure Rights Management).

- Las licencias y los certificados que se envían a un dispositivo Windows están protegidos con la clave privada de dispositivo del cliente, que se crea la primera vez que un usuario del dispositivo usa Azure RMS. Esta clave privada, a su vez, está protegida con DPAPI en el cliente, que protege estos secretos con una clave derivada de la contraseña del usuario. En dispositivos móviles, las claves se usan solo una vez, de modo que, como no se almacenan en los clientes, no es necesario proteger estas claves en el dispositivo. 



## Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido
Para comprender con más detalle el funcionamiento de Azure RMS, veamos un flujo típico que se produce tras la [activación del servicio de Azure RMS](../deploy-use/activate-service.md). Es el momento en que el usuario usa por primera vez RMS en su equipo Windows (este proceso se conoce a veces como **inicialización del entorno del usuario** o arranque), **protege contenido** (un documento o correo electrónico) y **consume** (abre y usa) contenido que otra persona ha protegido.

Una vez se inicializa el entorno del usuario, dicho usuario puede proteger entonces documentos o consumir documentos protegidos en dicho equipo.

> [!NOTE]
> Si este usuario se mueve a otro equipo Windows, u otro usuario emplea este mismo equipo Windows, se repite el proceso de inicialización.

### Inicialización del entorno de usuario
Para que un usuario pueda proteger contenido o consumir contenido protegido en un equipo Windows, el entorno del usuario debe estar preparado en el dispositivo. Este es un proceso único y ocurre de manera automática sin intervención del usuario cuando un usuario trata de proteger o de consumir contenido protegido:

![Activación del cliente RMS: paso 1](../media/AzRMS.png)

**Qué ocurre en el paso 1**: El cliente RMS del equipo conecta primero con Azure RMS y autentica al usuario mediante su cuenta de Azure Active Directory.

Cuando la cuenta del usuario está federada con Azure Active Directory, esta autenticación es automática y al usuario no se le solicitan credenciales.

![Activación del cliente RMS: paso 2](../media/AzRMS_useractivation2.png)

**Qué ocurre en el paso 2**: Cuando se autentica el usuario, la conexión se redirige automáticamente al inquilino de RMS de la organización, que emite certificados que permiten al usuario autenticarse en Azure RMS para consumir contenido protegido y para proteger contenido sin conexión.

Se almacena una copia del certificado del usuario en Azure RMS de manera que si el usuario se mueve a otro dispositivo, los certificados se crean usando las mismas claves.

### Protección de contenido
Cuando un usuario protege un documento, el cliente de RMS lleva a cabo las siguientes acciones en un documento desprotegido:

![Protección de documento RMS - paso 1](../media/AzRMS_documentprotection1.png)

**Qué ocurre en el paso 1**: El cliente de RMS crea una clave aleatoria (la clave de contenido) y descifra el documento usando esta clave con el algoritmo de cifrado simétrico de AES.

![Protección de documentos con RMS: paso 2](../media/AzRMS_documentprotection2.png)

**Qué ocurre en el paso 2**: El cliente de RMS crea después un certificado que incluye una directiva para el documento, basándose en una plantilla o especificando derechos concretos para el documento. Esta directiva incluye los derechos para diferentes usuarios o grupos y otras restricciones, como una fecha de expiración.

El cliente de RMS usa a continuación la clave de la organización que se obtuvo cuando se inicializó el entorno del usuario y usa esta clave para cifrar la directiva y la clave de contenido simétrico. El cliente de RMS también firma la directiva con el certificado del usuario que se obtuvo cuando se inicializó el entorno del usuario.

![Protección de documentos con RMS: paso 3](../media/AzRMS_documentprotection3.png)

**Qué ocurre en el paso 3**: Por último, el cliente de RMS inserta la directiva en un archivo con el cuerpo del documento cifrado anteriormente y, en conjunto, constituyen un documento protegido.

Este documento se puede almacenar en cualquier lugar o compartir mediante cualquier método y la directiva siempre permanece con el documento cifrado.

### Consumo de contenido
Cuando un usuario quiere consumir un documento protegido, el cliente de RMS se inicia solicitando acceso al servicio de Azure RMS:

![Consumo de documento RMS: paso 1](../media/AzRMS_documentconsumption1.png)

**Qué ocurre en el paso 1**: El usuario autenticado envía la directiva del documento y los certificados del usuario a Azure RMS. El servicio descifra y evalúa la directiva y crea una lista de derechos (de haberlos) que el usuario tiene para el documento.

![Consumo de documento RMS - paso 2](../media/AzRMS_documentconsumption2.png)

**Qué ocurre en el paso 2**: El servicio extrae después la clave de contenido de AES desde la directiva descifrada. Esta clave se cifra a continuación con la clave de RSA pública del usuario que se obtuvo con la solicitud.

La clave de contenido que se ha vuelto a cifrar se incrusta a continuación en una licencia de uso cifrada con la lista de derechos de usuario, que se devuelve a continuación al cliente de RMS.

![Consumo de documentos de RMS: paso 3](../media/AzRMS_documentconsumption3.png)

**Qué ocurre en el paso 3**: Por último, el cliente de RMS toma la licencia de uso cifrada y la descifra con su propia clave privada de usuario. Esto permite al cliente de RMS descifrar el cuerpo del documento cuando se necesita y representarlo en la pantalla.

El cliente también descifra la lista de derechos y los pasa a la aplicación, que aplica dichos derechos en la interfaz del usuario de la aplicación.

### Variaciones
Los tutoriales anteriores cubren los escenarios estándar pero hay algunas variaciones:

-   **Dispositivos móviles**: Cuando los dispositivos móviles protegen o consumen archivos con Azure RMS, los flujos del proceso son mucho más sencillos. Los dispositivos móviles no recorren primero el proceso de inicialización de usuario porque en su lugar, cada transacción (para proteger o consumir contenido) es independiente. Como con equipos de Windows, los dispositivos móviles se conectan al servicio de Azure RMS y autentican. Para proteger contenido, los dispositivos móviles envían una directiva y Azure RMS les envía una licencia de publicación y clave simétrica para proteger el documento. Para consumir contenido, cuando los dispositivos móviles se conectan al servicio de Azure RMS y autentican, envían la directiva del documento a Azure RMS y solicitan una licencia de usuario para consumir el documento. En respuesta, Azure RMS envía las restricciones y las claves necesarias a los dispositivos móviles. Ambos procesos usan TLS para proteger el intercambio de claves y otras comunicaciones.

-   **Conector RMS**: cuando se usa Azure RMS con el conector RMS, los flujos del proceso no cambian. La única diferencia es que el conector actúa como una retransmisión entre los servicios locales (como Exchange Server y SharePoint Server) y Azure RMS. El propio conector no lleva a cabo ninguna operación, como la inicialización del entorno del usuario, o cifrado o descifrado. Retransmite simplemente la comunicación que iría normalmente a un servidor AD RMS, controlando la traducción entre los protocolos que se usan en cada lado. Este escenario le permite usar Azure RMS con los servicios locales.

-   **Protección genérica (.pfile)**: cuando Azure RMS protege un archivo genéricamente, el flujo es básicamente el mismo para protección de contenido excepto en que el cliente de RMS crea una directiva que concede todos los derechos. Cuando se consume el archivo, se descifra antes de pasarse a la aplicación de destino. Este escenario le permite proteger todos los archivos, aunque no admitan RMS de manera nativa.

-   **PDF protegido (.ppdf)**: cuando Azure RMS protege de manera nativa un archivo de Office, también crea una copia de dicho archivo y lo protege de la misma manera. La única diferencia es que la copia del archivo se encuentra en formato PPDF, que la aplicación de uso compartido RMS sabe cómo abrir solo para visualización. Este escenario le permite enviar datos adjuntos protegidos mediante correo electrónico, sabiendo que el destinatario de un dispositivo móvil siempre podrá leerlos aunque el dispositivo móvil no tenga una aplicación que admita de manera nativa archivos de Office protegidos.

## Pasos siguientes

Para más información sobre Azure RMS, lea el resto de artículos de la sección **Understand & Explore** (Descripción y exploración), como [How applications support Azure Rights Management](applications-support.md) (Compatibilidad de aplicaciones con Azure Rights Management) para aprender de qué manera las aplicaciones existentes se pueden integrar con Azure RMS para proporcionar una solución de protección de la información. 

Revise [Terminology for Azure Rights Management](../get-started/terminology.md) (Terminología de Azure Rights Management) para familiarizarse con los términos que se puede encontrar a medida que configure y use Azure RMS, y asegúrese de leer también [Requirements for Azure Rights Management](../get-started/requirements-azure-rms.md) (Requisitos de Azure Rights Management) antes de empezar su implementación. Si quiere algo más rápido, vea [Quick start tutorial for Azure Rights Management](../get-started/quick-start-tutorial.md) (Tutorial de inicio rápido de Azure Rights Management).

Si está listo para empezar a implementar Azure RMS para su organización, vea [Azure Rights Management deployment roadmap](../plan-design/deployment-roadmap.md) (Plan para la implementación de Azure Rights Management) para ver los pasos de implementación y los vínculos con instrucciones de procedimiento.

> [!TIP]
> Para más información y ayuda, use los recursos y vínculos que aparecen en [Information and support for Azure Rights Management](../get-started/information-support.md) (Información y servicio de atención de Azure Rights Management).



<!--HONumber=Jun16_HO4-->


