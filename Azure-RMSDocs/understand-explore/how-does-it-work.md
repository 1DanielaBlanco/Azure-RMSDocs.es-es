---
title: "¿Cómo funciona Azure RMS? - Azure Information Protection"
description: "Desglose de cómo funciona Azure RMS, los controles criptográficos que usa y los diagramas acerca de cómo funciona este proceso paso a paso."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 01/29/2018
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: eb65f99d1a0fbc2c9aaee25a585561bd2511b723
ms.sourcegitcommit: 972acdb468ac32a28e3e24c90694aff4b75206fc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2018
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>¿Cómo funciona Azure RMS? En segundo plano

>*Válido para: Azure Information Protection, Office 365*

Una cuestión importante que hay que comprender acerca del funcionamiento de Azure RMS es que el servicio de protección de datos de Azure Information Protection no ve ni almacena sus datos como parte del proceso de protección. La información que protege nunca se envía o se almacena en Azure, a menos que la almacene de manera explícita en Azure o use otro servicio en la nube que lo haga. Azure RMS simplemente hace que los datos de un documento sean ilegibles para cualquiera que no sea un usuario y servicio autorizado:

- Los datos se cifran en el nivel de aplicación e incluyen una directiva que define el uso autorizado para ese documento.

- Cuando un usuario legítimo usa un documento protegido o un servicio autorizado procesa este documento, se descifran los datos en el documento y se aplican los derechos que se definen en la directiva.

En un nivel alto, puede ver cómo funciona este proceso en la siguiente imagen. Se protege un documento que contiene la fórmula secreta y luego lo abre correctamente un usuario o servicio autorizado. El documento se protege con una clave de contenido (la clave verde de esta imagen). Es única para cada documento y se coloca en el encabezado de archivo donde se protege mediante la clave raíz de inquilino de Azure Information Protection (la clave roja de esta imagen). Microsoft puede generar y administrar la clave de inquilino o puede generarla y administrarla usted mismo.

A lo largo del proceso de protección en el que Azure RMS cifra y descifra, autoriza y aplica restricciones, la fórmula secreta nunca se envía a Azure.

![¿Cómo protege Azure RMS un archivo?](../media/AzRMS_SecretColaFormula_final.png)

Para una descripción detallada de lo que está sucediendo, consulte la sección [Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de este artículo.

Para información técnica acerca de los algoritmos y longitudes de clave que usa Azure RMS, consulte la siguiente sección.

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Controles criptográficos que utiliza Azure RMS: Algoritmos y longitudes de clave
Aunque no es necesario conocer en detalle cómo funciona esta tecnología, es posible que se le pregunte acerca de los controles criptográficos que usa. Por ejemplo, para confirmar que la protección de seguridad es un estándar del sector.


|Controles criptográficos|Uso en Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Longitud de la clave: 128 bits y 256 bits [[1]](#footnote-1)|Protección de documentación|
|Algoritmo: RSA<br /><br />Longitud de la clave: 2048 bits [[2]](#footnote-2)|Protección de claves|
|SHA-256|Firma de certificados|

###### <a name="footnote-1"></a>Nota al pie 1 

La aplicación de Rights Management sharing y el cliente de Azure Information Protection usan 256 bits para la protección genérica y protección nativa cuando el archivo tiene una extensión de nombre de archivo .ppdf o es un texto protegido o un archivo de imagen (como .ptxt o .pjpg).

###### <a name="footnote-2"></a>Nota al pie 2

La longitud de la clave cuando el servicio Azure Rights Management está activado es de 2048 bits. La longitud de clave de 1024 bits es compatible para los siguientes escenarios opcionales:

- Durante una migración desde el entorno local si el clúster de AD RMS se ejecuta en el modo criptográfico 1.

- Después de una migración desde el entorno local, si el clúster de AD RMS utilizaba Exchange Online.

- Para las claves archivadas que se crearon en el entorno local antes de la migración, para que el servicio Azure Rights Management después de la migración pueda seguir abriendo el contenido que anteriormente estuvo protegido por AD RMS.

- Si los clientes eligen aportar su propia clave (BYOK) mediante Azure Key Vault. Azure Information Protection admite longitudes de clave de 1024 bits y 2048 bits. Para una mayor seguridad, se recomienda una longitud de clave de 2048 bits.

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>Almacenamiento y protección de las claves criptográficas de Azure RMS

Para cada documento o correo electrónico que protege, Azure RMS crea una sola clave AES ("clave de contenido") y esa clave se inserta en el documento y se mantiene aunque se edite el documento. 

La clave de contenido está protegida con la clave RSA de la organización ("clave de inquilino de Azure Information Protection") como parte de la directiva del documento, que también firma el autor de este. Esta clave de inquilino es común para todos los documentos y correos electrónicos de la organización que están protegidos por el servicio Azure Rights Management, y solo un administrador de Azure Information Protection puede cambiar esta clave si la organización usa una clave de inquilino administrada por el cliente (lo que se conoce como BYOK o "aporte su propia clave"). 

Esta clave de inquilino está protegida en los servicios en línea de Microsoft, en un entorno muy controlado y bajo una estrecha supervisión. Cuando se usa una clave de inquilino administrada por el cliente (BYOK), esta seguridad mejora gracias al uso de una matriz de módulos de alto nivel de seguridad de hardware (HSM) en cada región de Azure, sin la posibilidad de que se extraigan, exporten o compartan las claves bajo ninguna circunstancia. Para más información acerca de la clave de inquilino y BYOK, consulte [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](../plan-design/plan-implement-tenant-key.md).

Las licencias y los certificados que se envían a un dispositivo Windows están protegidos con la clave privada de dispositivo del cliente, que se crea la primera vez que un usuario del dispositivo usa Azure RMS. Esta clave privada, a su vez, está protegida con DPAPI en el cliente, que protege estos secretos con una clave derivada de la contraseña del usuario. En los dispositivos móviles, las claves se usan solo una vez, de modo que, como no se almacenan en los clientes, no es necesario proteger estas claves en el dispositivo. 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido
Para comprender con más detalle el funcionamiento de Azure RMS, examinemos un flujo típico que se produce tras la [activación del servicio Azure Rights Management](../deploy-use/activate-service.md) y cuando un usuario usa por primera vez el servicio Rights Management en su equipo Windows (un proceso que a veces se conoce como **inicialización del entorno del usuario** o arranque), **protege contenido** (un documento o correo electrónico) y, a continuación, **consume** (abre y usa) el contenido que ha protegido otra persona.

Una vez se inicia el entorno del usuario, ese usuario puede proteger los documentos o consumir documentos protegidos en ese equipo.

> [!NOTE]
> Si este usuario se mueve a otro equipo Windows, u otro usuario utiliza este mismo equipo Windows, se repite el proceso de inicialización.

### <a name="initializing-the-user-environment"></a>Inicialización del entorno de usuario
Antes de que un usuario pueda proteger el contenido o consumir contenido protegido en un equipo Windows, se debe preparar el entorno del usuario en el dispositivo. Este es un proceso único y ocurre de manera automática sin intervención del usuario cuando un usuario intenta proteger o consumir contenido protegido:

![Flujo de activación de cliente de RMS - paso 1, autenticar el cliente](../media/AzRMS.png)

**¿Qué ocurre en el paso 1?**: En el equipo, el cliente de RMS se conecta primero al servicio Azure Rights Management y autentica al usuario mediante su cuenta de Azure Active Directory.

Cuando la cuenta de usuario está federada con Azure Active Directory, esta autenticación es automática y al usuario no se le solicitan las credenciales.

![Activación del cliente de RMS - paso 2, los certificados se descargan en el cliente](../media/AzRMS_useractivation2.png)

**¿Qué ocurre en el paso 2?**: Cuando se autentica el usuario, la conexión se redirige automáticamente al inquilino de Azure Information Protection de la organización, que emite certificados que permiten al usuario autenticarse en el servicio Azure Rights Management para consumir contenido protegido y para proteger contenido sin conexión.

Se almacena una copia del certificado de usuario en Azure, por lo que si el usuario se mueve a otro dispositivo, se crean los certificados mediante las mismas claves.

### <a name="content-protection"></a>Protección de contenido
Cuando un usuario protege un documento, el cliente de RMS realiza las siguientes acciones en un documento desprotegido:

![Protección del documento RMS - paso 1, se cifra el documento](../media/AzRMS_documentprotection1.png)

**¿Qué ocurre en el paso 1?**: El cliente de RMS crea una clave aleatoria (la clave de contenido) y descifra el documento usando esta clave con el algoritmo de cifrado simétrico de AES.

![Protección del documento RMS - paso 2, se crea la directiva](../media/AzRMS_documentprotection2.png)

**¿Qué ocurre en el paso 2?**: El cliente de RMS crea a continuación un certificado que incluye una directiva para el documento que contiene a su vez los [derechos de utilización](../deploy-use/configure-usage-rights.md) para usuarios o grupos y otras restricciones, como una fecha de expiración. Estas opciones se pueden definir en una plantilla que un administrador haya configurado anteriormente, o bien especificarse al proteger el contenido (a veces se denomina "directiva ad-hoc").   

El atributo de Azure AD principal que se usa para identificar los usuarios y grupos seleccionados es el atributo ProxyAddresses de Azure AD, que almacena todas las direcciones de correo electrónico de un usuario o grupo. Sin embargo, si una cuenta de usuario no tiene ningún valor en el atributo ProxyAddresses de AD, se utiliza en su lugar el valor de UserPrincipalName del usuario.

El cliente de RMS, a continuación, utiliza la clave de la organización que se obtuvo cuando se inicializó el entorno del usuario y utiliza esta clave para cifrar la directiva y la clave de contenido simétrica. El cliente de RMS también firma la directiva con el certificado del usuario que se obtuvo cuando se inicializó el entorno del usuario.

![Protección de documentos de RMS - paso 3, se inserta la directiva en el documento](../media/AzRMS_documentprotection3.png)

**¿Qué ocurre en el paso 3?**: Por último, el cliente de RMS inserta la directiva en un archivo con el cuerpo del documento cifrado anteriormente y, en conjunto, constituyen un documento protegido.

Este documento se puede almacenar en cualquier lugar o compartir mediante cualquier método y la directiva siempre permanece con el documento cifrado.

### <a name="content-consumption"></a>Consumo de contenido
Cuando un usuario quiere consumir un documento protegido, el cliente de RMS se inicia solicitando acceso al servicio Azure Rights Management:

![Consumo de documento RMS - paso 1, el usuario se autentica y obtiene la lista de derechos](../media/AzRMS_documentconsumption1.png)

**¿Qué ocurre en el paso 1**: El usuario autenticado envía la directiva del documento y los certificados del usuario al servicio Azure Rights Management. El servicio descifra y evalúa la directiva y crea una lista de derechos (en caso de haberlos) que el usuario tiene para el documento. Para identificar al usuario, se usa el atributo ProxyAddresses de Azure AD correspondiente a la cuenta del usuario y a los grupos de los que el usuario es miembro. Por motivos de rendimiento, la pertenencia a grupos se almacena [en caché](../plan-design/prepare.md#group-membership-caching-by-azure-information-protection). Si la cuenta de usuario no tiene valores para el atributo ProxyAddresses de Azure AD, se usa el valor de UserPrincipalName de Azure AD en su lugar.

![Consumo del documento RMS - paso 2, la licencia de uso se devuelve al cliente](../media/AzRMS_documentconsumption2.png)

**¿Qué ocurre en el paso 2**: El servicio extrae después la clave de contenido de AES desde la directiva descifrada. Esta clave se cifra a continuación con la clave de RSA pública del usuario que se obtuvo con la solicitud.

A continuación, la clave de contenido que se ha vuelto a cifrar se inserta en una licencia de uso cifrada con la lista de derechos de usuario, que se devuelve a continuación al cliente de RMS.

![Consumo de documento RMS - paso 3, el documento se descifra y se aplican los derechos](../media/AzRMS_documentconsumption3.png)

**¿Qué ocurre en el paso 3?**: Por último, el cliente de RMS toma la licencia de uso cifrada y la descifra con su propia clave privada de usuario. Esto permite al cliente de RMS descifrar el cuerpo del documento cuando se necesita y representarlo en la pantalla.

El cliente también descifra la lista de derechos y los pasa a la aplicación, que aplica dichos derechos en la interfaz del usuario de la aplicación.

> [!NOTE]
> Cuando los usuarios externos a su organización consumen contenido que ha protegido, el flujo de consumo es el mismo. Lo que cambia en este escenario es cómo se autentica el usuario. Para más información, consulte [Cuando comparto un documento protegido con una persona ajena a mi organización, ¿cómo se autentica ese usuario?](../get-started/faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)


### <a name="variations"></a>Variaciones
Los tutoriales anteriores cubren los escenarios estándar pero hay algunas variaciones:

-   **Dispositivos móviles**: Cuando los dispositivos móviles protegen o consumen archivos con el servicio Azure Rights Management, los flujos del proceso son mucho más sencillos. Los dispositivos móviles no recorren primero el proceso de inicialización de usuario porque, en su lugar, cada transacción (para proteger o consumir contenido) es independiente. Como con equipos de Windows, los dispositivos móviles se conectan al servicio Azure Rights Management y se autentican. Para proteger contenido, los dispositivos móviles envían una directiva y el servicio Azure Rights Management les envía una licencia de publicación y una clave simétrica para proteger el documento. Para consumir contenido, cuando los dispositivos móviles se conectan al servicio Azure Rights Management y se autentican, envían la directiva del documento al servicio Azure Rights Management y solicitan una licencia de usuario para consumir el documento. En respuesta, el servicio Azure Rights Management envía las restricciones y las claves necesarias a los dispositivos móviles. Ambos procesos usan TLS para proteger el intercambio de claves y otras comunicaciones.

-   **Conector RMS**: Cuando se usa el servicio Azure Rights Management con el conector RMS, los flujos del proceso no cambian. La única diferencia es que el conector actúa como una retransmisión entre los servicios locales (como Exchange Server y SharePoint Server) y el servicio Azure Rights Management. El propio conector no lleva a cabo ninguna operación, como la inicialización del entorno del usuario, o cifrado o descifrado. Retransmite simplemente la comunicación que iría normalmente a un servidor AD RMS, controlando la traducción entre los protocolos que se usan en cada lado. Este escenario permite usar el servicio Azure Rights Management con servicios locales.

-   **Protección genérica (.pfile)**: Cuando el servicio Azure Rights Management protege un archivo genéricamente, el flujo es básicamente el mismo para la protección de contenido, con la excepción de que el cliente de RMS crea una directiva que concede todos los derechos. Cuando se consume el archivo, se descifra antes de pasarse a la aplicación de destino. Este escenario le permite proteger todos los archivos, aunque no admitan RMS de manera nativa.

-   **PDF protegido (.ppdf)**: Cuando el servicio Azure Rights Management protege de manera nativa un archivo de Office, también crea una copia de dicho archivo y lo protege de la misma manera. La única diferencia es que la copia del archivo se encuentra en formato PPDF, que el visor del cliente de Azure Information Protection y la aplicación RMS sharing saben cómo abrir solo para visualización. Este escenario le permite enviar datos adjuntos protegidos mediante correo electrónico, sabiendo que el destinatario de un dispositivo móvil siempre podrá leerlos aunque el dispositivo móvil no tenga una aplicación que admita de manera nativa archivos de Office protegidos.

## <a name="next-steps"></a>Pasos siguientes

Para más información acerca del servicio Azure Rights Management, lea el resto de artículos de la sección **Conceptos básicos y exploración**, como [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md), para aprender de qué manera las aplicaciones existentes se pueden integrar con Azure Rights Management para proporcionar una solución de protección de la información. 

Revise [Terminología de Azure Information Protection](../get-started/terminology.md) para familiarizarse con los términos que se puede encontrar a medida que configure y use el servicio Azure Rights Management, y asegúrese de leer también [Requisitos de Azure Information Protection](../get-started/requirements-azure-rms.md) antes de empezar su implementación. Si quiere algo más rápido, vea [Tutorial de inicio rápido de Azure Information Protection](../get-started/infoprotect-quick-start-tutorial.md).

Si está preparado para empezar a implementar la protección de datos en su organización, vea los pasos de implementación y los vínculos a instrucciones de procedimientos incluidos en el [Mapa de ruta de implementación de Azure Information Protection](../plan-design/deployment-roadmap.md).

> [!TIP]
> Para más información y ayuda, use los recursos y vínculos que aparecen en [Información y soporte técnico para Azure Information Protection](../get-started/information-support.md).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]