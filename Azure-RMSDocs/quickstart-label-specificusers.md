---
title: 'Inicio rápido: Creación de una nueva etiqueta de Azure Information Protection para usuarios específicos'
description: Cree y configure una nueva etiqueta que clasifica los documentos y correos electrónicos para usuarios específicos mediante el uso de una directiva de ámbito.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 11/14/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: dca90c7635702226e7414947aad6f3d89cf91efd
ms.sourcegitcommit: ad37950f6a747c86f6496c6de859e18446f9b03f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2018
ms.locfileid: "51644662"
---
# <a name="quickstart-create-a-new-azure-information-protection-label-for-specific-users"></a>Inicio rápido: Creación de una nueva etiqueta de Azure Information Protection para usuarios específicos

En este tutorial, creará una nueva etiqueta que solo determinados usuarios pueden ver y aplicar para clasificar y proteger sus documentos y correos electrónicos.

Esta configuración usa una directiva de ámbito.

Puede finalizar esta configuración en menos de 10 minutos.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará:

1. Una suscripción que incluya el plan 1 o el plan 2 de Azure Information Protection.
    
    Si no tiene una de estas suscripciones, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

2. Ha agregado la hoja Azure Information Protection a Azure Portal y ha confirmado que el servicio de protección está activado.

    Si necesita ayuda con estas acciones, consulte [Quickstart: Get started in the Azure portal](quickstart-viewpolicy.md) (Inicio rápido: introducción a Azure Portal).

3. Un grupo habilitado para correo electrónico en Azure AD que contenga los usuarios podrá ver y aplicar la nueva etiqueta.
    
    Si no tiene un grupo adecuado, cree uno denominado **Equipo de ventas** y agregue al menos un usuario.

4. Para probar la nueva etiqueta: el cliente de Azure Information Protection debe estar instalado en equipos para los usuarios. 
    
    Para probar la etiqueta por usted mismo, instale el cliente visitando el [Centro de descarga de Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=53018) y descargando **AzInfoProtection.exe** desde la página de Azure Information Protection.

Para ver una lista completa de los requisitos previos para utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).
    
## <a name="create-a-new-label"></a>Creación de una nueva etiqueta

En primer lugar, cree la nueva etiqueta.

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**.
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.
    
    Si no es el administrador global, utilice el siguiente vínculo para roles alternativos: [Inicio de sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal).

2. En la opción de menú **Clasificaciones** > **Etiquetas**: en la hoja **Azure Information Protection: etiquetas**, haga clic en **Agregar una nueva etiqueta**.

3. En la hoja **Etiqueta**, especifique al menos lo siguiente:
    
    - **Nombre para mostrar de la etiqueta**: un nombre para la nueva etiqueta que verán los usuarios y que identifica la clasificación del contenido. Por ejemplo: `Sales - Restricted`.
    
    - **Descripción**: información sobre herramientas para ayudar a los usuarios a identificar cuándo se debe seleccionar esta nueva etiqueta. Por ejemplo: `Business data that is restricted to the Sales Team.`

4. Asegúrese de que **Habilitado** está establecido en **Activado** (valor predeterminado) y seleccione **Guardar**.

## <a name="add-the-label-to-a-new-scoped-policy"></a>Agregue la etiqueta a una nueva directiva de ámbito

Ahora, agregue la etiqueta recién creada a una nueva directiva de ámbito.

1. En la opción de menú **Clasificaciones** > **Directivas**: en la hoja **Azure Information Protection: directivas**, seleccione **Agregar una directiva**. 

2. En la hoja **Directiva**, para el cuadro **Nombre de la directiva**, escriba un nombre que identifique al grupo de usuarios que verá en la etiqueta recién creada. Por ejemplo, `Sales`.

3. Seleccione la opción **Seleccionar a qué usuarios o grupos se aplica esta directiva**.

4. En la hoja **Usuarios y grupos de AAD**, seleccione **Usuarios o grupos**. A continuación, en la nueva hoja **Usuarios o grupos**, busque y seleccione el grupo que ha identificado en los requisitos previos. Por ejemplo, **Equipo de ventas**. Haga clic en **Seleccionar** en esa hoja y, a continuación, **Aceptar**.

5. De nuevo en la hoja **Directiva**, seleccione **Agregar o quitar etiquetas**.

6. En la hoja **Directiva: agregar o quitar etiquetas**, seleccione la etiqueta que ha creado, por ejemplo, **Ventas - Restringido** y, a continuación, seleccione **Aceptar**.

7. De nuevo en la hoja **Directiva**, seleccione **Guardar**. 

Ya se ha publicado la nueva etiqueta solo para los miembros del grupo especificado. 

## <a name="test-your-new-label"></a>Prueba de la nueva etiqueta

Para probar esta etiqueta, necesita un mínimo de dos equipos porque el cliente de Azure Information Protection no admite varios usuarios en el mismo equipo:

 - En el primer equipo, inicie sesión como miembro del grupo Equipo de ventas. Abra Word y confirme que puede ver la nueva etiqueta. Si Word ya está abierto, reinícielo para forzar una actualización de la directiva.

- En el segundo equipo, inicie sesión como un usuario que no es miembro del grupo Equipo de ventas. Abra Word y confirme que no se ve la nueva etiqueta. Como antes, si Word ya está abierto, reinícielo.

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no desea mantener esta etiqueta y la directiva de ámbito, haga lo siguiente:

1. En la opción de menú **Clasificaciones** > **Directivas**: en la hoja **Azure Information Protection: directivas**, seleccione el menú contextual (**...**) para la directiva de ámbito que acaba de crear. Por ejemplo: **Ventas**.

2. Seleccione **Eliminar directiva** y, si se le pide que confirme, seleccione **Aceptar**.

3. En la opción de menú **Clasificaciones** > **Etiquetas** de la hoja **Azure Information Protection: etiqueta**, seleccione el menú contextual (**...**) para la etiqueta que acaba de crear.  Por ejemplo, **Ventas - restringido**.

4.  Seleccione **Eliminar esta etiqueta** y, si se le pide que confirme, seleccione **Aceptar**.


## <a name="next-steps"></a>Pasos siguientes

Este inicio rápido incluye las opciones mínimas para que pueda crear rápidamente una nueva etiqueta para usuarios específicos. Para ver todas las instrucciones, consulte uno de los artículos siguientes:

- [Creación de una nueva etiqueta](configure-policy-new-label.md)

- [Configuración de la directiva para usuarios específicos mediante directivas de ámbito](configure-policy-scope.md)

Además, si desea que la etiqueta proteja el contenido de forma que solo los miembros de Equipo de ventas puedan abrirlo, deberá configurar la etiqueta para aplicar la protección. Para ver instrucciones, consulte [Configuración de una etiqueta para la protección de Rights Management](configure-policy-protection.md).

