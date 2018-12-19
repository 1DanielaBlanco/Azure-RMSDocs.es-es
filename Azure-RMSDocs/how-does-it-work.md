---
title: Funcionamiento de Azure RMS - Azure Information Protection
description: Analice cómo funciona Azure RMS, los controles criptográficos que usa y los diagramas detallados sobre cómo funciona este proceso.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/05/2018
ms.topic: conceptual
ms.service: information-protection
ms.assetid: ed6c964e-4701-4663-a816-7c48cbcaf619
ms.reviewer: esaggese
ms.suite: ems
ms.openlocfilehash: 7c1d488ff738b0eea9042f1580ea74b7099f3ac5
ms.sourcegitcommit: 5b4eb0e17fb831d338d8c25844e9e6f4ca72246d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53174121"
---
# <a name="how-does-azure-rms-work-under-the-hood"></a>¿Cómo funciona Azure RMS? En segundo plano

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection) y [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Una cuestión importante que hay que comprender sobre el funcionamiento de Azure RMS es que el servicio de protección de datos de Azure Information Protection no ve ni almacena sus datos como parte del proceso de protección. La información que protege nunca se envía a Azure, ni se almacena allí, a menos que la almacene de manera explícita en Azure o use otro servicio en la nube que la almacene en Azure. Azure RMS simplemente hace que los datos de un documento sean ilegibles para cualquiera que no sea un usuario y servicio autorizado:

- Los datos se cifran en el nivel de aplicación e incluyen una directiva que define el uso autorizado para ese documento.

- Cuando se usa un documento protegido por un usuario legítimo o se procesa por un servicio autorizado, se descifran los datos del documento y se aplican derechos definidos en la directiva.

En un nivel alto, puede ver la manera en que funciona este proceso en la imagen siguiente. Se protege un documento que contiene la fórmula secreta y luego lo abre correctamente un usuario o servicio autorizado. El documento se protege con una clave de contenido (la clave verde de esta imagen). Es única para cada documento y se coloca en el encabezado de archivo donde se protege mediante la clave raíz de inquilino de Azure Information Protection (la clave roja de esta imagen). Su clave de inquilino se puede generar y administrar por Microsoft o bien, puede generar y administrar su propia clave de inquilino.

A lo largo del proceso de protección cuando Azure RMS está cifrando y descifrando, y aplicando restricciones, autorizando y aplicando restricciones, la fórmula secreta nunca se envía a Azure.

![Cómo Azure RMS protege un archivo](./media/AzRMS_SecretColaFormula_final.png)

Para obtener una descripción detallada de lo que está sucediendo, vea la sección [Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido](#walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption) de este artículo.

Para consultar detalles técnicos acerca de las longitudes de claves y algoritmos que usa Azure RMS, vea la siguiente sección.

## <a name="cryptographic-controls-used-by-azure-rms-algorithms-and-key-lengths"></a>Controles criptográficos usados por Azure RMS: Longitudes de clave y algoritmos
Aunque no necesite saber en detalle cómo funciona esta tecnología, es posible que se le pregunte acerca de los controles criptográficos que utiliza. Por ejemplo, para confirmar que la protección de seguridad es un estándar industrial.


|Controles criptográficos|Uso en Azure RMS|
|-|-|
|Algoritmo: AES<br /><br />Longitud de clave: 128 bits y 256 bits [[1]](#footnote-1)|Protección de documentación|
|Algoritmo: RSA<br /><br />Longitud de clave: 2048 bits [[2]](#footnote-2)|Protección de claves|
|SHA-256|Firma de certificados|

###### <a name="footnote-1"></a>Nota al pie 1 

El cliente de Azure Information Protection y la aplicación Rights Management sharing usan 256 bits para la protección genérica y la protección nativa cuando el archivo tiene una extensión de nombre de archivo .ppdf o es un archivo de imagen o texto protegido (como .ptxt o .pjpg).

###### <a name="footnote-2"></a>Nota al pie 2

La longitud de la clave es de 2048 bits cuando el servicio Azure Rights Management está activado. Una longitud de clave de 1024 bits es compatible con los siguientes escenarios opcionales:

- Durante una migración desde el entorno local si el clúster de AD RMS se ejecuta en el modo criptográfico 1.

- Después de una migración desde el entorno local si el clúster de AD RMS usaba Exchange Online.

- Para claves archivadas que se crearon en el entorno local antes de la migración para que el contenido anteriormente protegido por AD RMS pueda seguir abierto después de migrar al servicio Azure Rights Management.

- Si los clientes eligen traer su propia clave (BYOK) mediante Azure Key Vault. Azure Information Protection admite longitudes de clave de 1024 bits y 2048 bits. Para una mayor seguridad, le recomendamos una longitud de clave de 2048 bits.

### <a name="how-the-azure-rms-cryptographic-keys-are-stored-and-secured"></a>Almacenamiento y protección de las claves criptográficas de Azure RMS

Azure RMS crea una sola clave AES ("clave de contenido") para cada documento o correo electrónico que protege. Esta clave se inserta en el documento y se mantiene aunque se edite el documento. 

La clave de contenido tiene la protección de la clave RSA de la organización (la "clave de inquilino de Azure Information Protection") como parte de la directiva del documento, que también firma el autor de este. Esta clave de inquilino es común para todos los documentos y correos electrónicos de la organización protegidos por el servicio Azure Rights Management. La clave solo se puede cambiar con la intervención de un administrador de Azure Information Protection si la organización usa una clave de inquilino administrada por el cliente (lo que se conoce como "traiga su propia clave" o BYOK). 

Esta clave de inquilino tiene la protección de los servicios en línea de Microsoft, en un entorno muy controlado y bajo una estrecha supervisión. Al usar una clave de inquilino administrada por el cliente (BYOK), esta seguridad mejora gracias al uso de una matriz de módulos de seguridad de hardware (HSM) punteros en cada región de Azure, sin posibilidad de extraer, exportar ni compartir las claves bajo ninguna circunstancia. Para obtener más información sobre la clave de inquilino y BYOK, vea [Planeamiento e implementación de su clave de inquilino de Azure Information Protection](plan-implement-tenant-key.md).

Las licencias y los certificados que se envían a un dispositivo Windows están protegidos con la clave privada de dispositivo del cliente, que se crea la primera vez que un usuario del dispositivo usa Azure RMS. Esta clave privada, a su vez, está protegida con DPAPI en el cliente, lo cual protege estos secretos con una clave derivada de la contraseña del usuario. En dispositivos móviles, las claves se usan solo una vez, de modo que, como no se almacenan en los clientes, no es necesario proteger estas claves en el dispositivo. 


## <a name="walkthrough-of-how-azure-rms-works-first-use-content-protection-content-consumption"></a>Tutorial de cómo funciona Azure RMS: Primer uso, protección de contenido, consumo de contenido
Para comprender con más detalle el funcionamiento de Azure RMS, veamos un flujo típico que se produce tras la [activación del servicio de Azure Rights Management](activate-service.md). Es el momento en que el usuario usa por primera vez el servicio Rights Management en su equipo Windows (este proceso se conoce a veces como **inicialización del entorno del usuario** o arranque), **protege contenido** (un documento o correo electrónico) y **consume** (abre y usa) contenido que otra persona ha protegido.

Una vez se inicializa el entorno del usuario, dicho usuario puede proteger entonces documentos o consumir documentos protegidos en dicho equipo.

> [!NOTE]
> Si este usuario se mueve a otro equipo Windows, u otro usuario emplea este mismo equipo Windows, se repite el proceso de inicialización.

### <a name="initializing-the-user-environment"></a>Inicialización del entorno de usuario
Para que un usuario pueda proteger contenido o consumir contenido protegido en un equipo Windows, el entorno del usuario debe estar preparado en el dispositivo. Este es un proceso único y ocurre de manera automática sin intervención del usuario cuando un usuario trata de proteger o de consumir contenido protegido:

![Flujo de activación del cliente de RMS, paso 1: autenticación del cliente](./media/AzRMS.png)

**Qué ocurre en el paso 1**: el cliente RMS del equipo conecta primero con el servicio Azure Rights Management y autentica al usuario mediante su cuenta de Azure Active Directory.

Cuando la cuenta del usuario está federada con Azure Active Directory, esta autenticación es automática y al usuario no se le solicitan credenciales.

![Activación del cliente de RMS, paso 2: los certificados se descargan en el cliente](./media/AzRMS_useractivation2.png)

**Qué ocurre en el paso 2**: cuando se autentica el usuario, la conexión se redirige automáticamente al inquilino de Azure Information Protection de la organización, que emite certificados que permiten al usuario autenticarse en el servicio Azure Rights Management para consumir contenido protegido y para proteger contenido sin conexión.

Uno de estos certificados es el certificado de cuenta de derechos, a menudo abreviado como RAC. Este certificado autentica al usuario en Azure Active Directory y es válido durante 31 días. El certificado lo renueva automáticamente el cliente de RMS, siempre y cuando la cuenta de usuario aún esté en Azure Active Directory y la cuenta esté habilitada. El administrador no puede configurar este certificado. 

Se almacena una copia de este certificado en Azure, de manera que si el usuario se mueve a otro dispositivo, los certificados se crean usando las mismas claves.

### <a name="content-protection"></a>Protección de contenido
Cuando un usuario protege un documento, el cliente de RMS lleva a cabo las siguientes acciones en un documento desprotegido:

![Protección del documento de RMS, paso 1: se cifra el documento](./media/AzRMS_documentprotection1.png)

**Qué ocurre en el paso 1**: El cliente de RMS crea una clave aleatoria (la clave de contenido) y descifra el documento con esta clave con el algoritmo de cifrado simétrico de AES.

![Protección del documento de RMS, paso 2: se crea una directiva](./media/AzRMS_documentprotection2.png)

**Qué ocurre en el paso 2**: después el cliente de RMS crea un certificado que incluye una directiva para el documento que contiene a su vez los [derechos de uso](configure-usage-rights.md) para usuarios o grupos y otras restricciones, como una fecha de expiración. Estas opciones se pueden definir en una plantilla que un administrador haya configurado anteriormente, o bien especificarse al proteger el contenido (a veces se denomina “directiva ad-hoc”).   

El atributo de Azure AD principal que se usa para identificar los usuarios y grupos seleccionados es el atributo ProxyAddresses de Azure AD, que almacena todas las direcciones de correo electrónico de un usuario o grupo. Sin embargo, si una cuenta de usuario no tiene ningún valor en el atributo ProxyAddresses de AD, se utiliza el valor de UserPrincipalName del usuario.

El cliente de RMS usa a continuación la clave de la organización que se obtuvo cuando se inicializó el entorno del usuario y usa esta clave para cifrar la directiva y la clave de contenido simétrico. El cliente de RMS también firma la directiva con el certificado del usuario que se obtuvo cuando se inicializó el entorno del usuario.

![Protección del documento de RMS, paso 3: la directiva se inserta en el documento](./media/AzRMS_documentprotection3.png)

**Qué ocurre en el paso 3**: Por último, el cliente de RMS incrusta la directiva en un archivo con el cuerpo del documento cifrado anteriormente, que en conjunto, constituyen un documento protegido.

Este documento se puede almacenar en cualquier lugar o compartir mediante cualquier método y la directiva siempre permanece con el documento cifrado.

### <a name="content-consumption"></a>Consumo de contenido
Cuando un usuario quiere consumir un documento protegido, el cliente de RMS se inicia solicitando acceso al servicio Azure Rights Management:

![Consumo de documento de RMS, paso 1: el usuario se autentica y obtiene la lista de derechos](./media/AzRMS_documentconsumption1.png)

**Qué ocurre en el paso 1**: el usuario autenticado envía la directiva del documento y los certificados del usuario al servicio Azure Rights Management. El servicio descifra y evalúa la directiva y crea una lista de derechos (de haberlos) que el usuario tiene para el documento. Para identificar al usuario, se usa el atributo ProxyAddresses de Azure AD correspondiente a la cuenta del usuario y a los grupos a los que pertenece. Por motivos de rendimiento, la pertenencia a grupos se almacena [en caché](prepare.md#group-membership-caching-by-azure-information-protection). Si la cuenta de usuario no tiene valores para el atributo ProxyAddresses de Azure AD, se usa el valor de UserPrincipalName de Azure AD.

![Consumo de documento de RMS, paso 2: la licencia de uso se devuelve al cliente](./media/AzRMS_documentconsumption2.png)

**Qué ocurre en el paso 2**: El servicio extrae a continuación la clave de contenido de AES desde la directiva descifrada. Esta clave se cifra a continuación con la clave de RSA pública del usuario que se obtuvo con la solicitud.

La clave de contenido que se ha vuelto a cifrar se incrusta a continuación en una licencia de uso cifrada con la lista de derechos de usuario, que se devuelve a continuación al cliente de RMS.

![Consumo de documento de RMS, paso 3: el documento se descifra y se aplican los derechos](./media/AzRMS_documentconsumption3.png)

**Qué ocurre en el paso 3**: Por último, el cliente de RMS toma la licencia de uso cifrada y la descifra con su propia clave privada de usuario. Esto permite al cliente de RMS descifrar el cuerpo del documento cuando se necesita y representarlo en la pantalla.

El cliente también descifra la lista de derechos y los pasa a la aplicación, que aplica dichos derechos en la interfaz del usuario de la aplicación.

> [!NOTE]
> Cuando los usuarios externos a su organización consumen contenido que ha protegido, el flujo de consumo es el mismo. Lo que cambia en este escenario es cómo se autentica el usuario. Para obtener más información, consulte [Cuando comparto un documento protegido con una persona ajena a mi organización, ¿cómo se autentica ese usuario?](./faqs-rms.md#when-i-share-a-protected-document-with-somebody-outside-my-company-how-does-that-user-get-authenticated)


### <a name="variations"></a>Variaciones
Los tutoriales anteriores cubren los escenarios estándar pero hay algunas variaciones:

- **Protección de correo electrónico**: al usarse Exchange Online y Cifrado de mensajes de Office 365 con nuevas funciones para proteger mensajes de correo electrónico, la autenticación para el consumo también puede usar la federación con un proveedor de identidades sociales o con un código de acceso de un solo uso. A continuación, los flujos del proceso son muy similares, solo que el consumo de contenido se produce del lado del servicio en una sesión del explorador web a través de una copia temporalmente en caché del correo electrónico saliente.

- **Dispositivos móviles**: cuando los dispositivos móviles protegen o consumen archivos con el servicio Azure Rights Management, los flujos del proceso son mucho más sencillos. Los dispositivos móviles no recorren primero el proceso de inicialización de usuario porque en su lugar, cada transacción (para proteger o consumir contenido) es independiente. Como con equipos de Windows, los dispositivos móviles se conectan al servicio Azure Rights Management y autentican. Para proteger contenido, los dispositivos móviles envían una directiva y el servicio Azure Rights Management les envía una licencia de publicación y una clave simétrica para proteger el documento. Para consumir contenido, cuando los dispositivos móviles se conectan al servicio Azure Rights Management y autentican, envían la directiva del documento al servicio Azure Rights Management y solicitan una licencia de usuario para consumir el documento. En respuesta, el servicio Azure Rights Management envía las restricciones y las claves necesarias a los dispositivos móviles. Ambos procesos usan TLS para proteger el intercambio de claves y otras comunicaciones.

- **Conector RMS**: cuando se usa el servicio Azure Rights Management con el conector RMS, los flujos del proceso no cambian. La única diferencia es que el conector actúa como una retransmisión entre los servicios locales (como Exchange Server y SharePoint Server) y el servicio Azure Rights Management. El propio conector no lleva a cabo ninguna operación, como la inicialización del entorno del usuario, o cifrado o descifrado. Retransmite simplemente la comunicación que iría normalmente a un servidor AD RMS, controlando la traducción entre los protocolos que se usan en cada lado. Este escenario permite usar el servicio Azure Rights Management con servicios locales.

- **Protección genérica (.pfile)**: cuando el servicio Azure Rights Management protege un archivo genéricamente, el flujo es básicamente el mismo para la protección de contenido, con la excepción de que el cliente de RMS crea una directiva que concede todos los derechos. Cuando se consume el archivo, se descifra antes de pasarse a la aplicación de destino. Este escenario le permite proteger todos los archivos, aunque no admitan RMS de manera nativa.

- **PDF protegido (.ppdf)**: cuando el servicio Azure Rights Management protege de manera nativa un archivo de Office, también crea una copia de dicho archivo y lo protege de la misma manera. La única diferencia es que la copia del archivo se encuentra en formato PPDF, que el visor del cliente de Azure Information Protection y la aplicación RMS sharing saben cómo abrir solo para visualización. Este escenario le permite enviar datos adjuntos protegidos mediante correo electrónico, sabiendo que el destinatario de un dispositivo móvil siempre podrá leerlos aunque el dispositivo móvil no tenga una aplicación que admita de manera nativa archivos de Office protegidos.

- **Cuentas de Microsoft**: Azure Information Protection puede autorizar las direcciones de correo electrónico para su uso cuando se autentican con una cuenta Microsoft. Sin embargo, no todas las aplicaciones pueden abrir contenido protegido cuando se usa una cuenta Microsoft para la autenticación. [Información adicional](secure-collaboration-documents.md#supported-scenarios-for-opening-protected-documents).

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre el servicio Azure Rights Management, lea el resto de artículos de la sección **Conceptos básicos y exploración**, como [Compatibilidad de aplicaciones con el servicio Azure Rights Management](applications-support.md), para aprender de qué manera las aplicaciones existentes se pueden integrar con Azure Rights Management para proporcionar una solución de protección de la información. 

Revise [Terminología de Azure Information Protection](./terminology.md) para familiarizarse con los términos que se puede encontrar a medida que configure y use el servicio Azure Rights Management, y asegúrese de leer también [Requirements for Azure Information Protection](requirements.md) (Requisitos de Azure Information Protection) antes de empezar su implementación. Si desea profundizar y probarlo por usted mismo, utilice el tutorial [Edit the policy and create a new label](infoprotect-quick-start-tutorial.md) (Edición de la directiva y creación de una nueva etiqueta).

Si está preparado para empezar a implementar la protección de datos en su organización, vea los pasos de implementación y los vínculos a instrucciones de procedimientos incluidos en el [Mapa de ruta de implementación de Azure Information Protection](deployment-roadmap.md).

> [!TIP]
> Para obtener más información y ayuda, use los recursos y vínculos que aparecen en [Información y soporte técnico para Azure Information Protection](information-support.md).
