---
title: 'Guía de inicio rápido: Introducción a Azure Information Protection en Azure Portal (AIP)'
description: Si su organización ha empezado a utilizar recientemente Azure Information Protection, empiece aquí para agregar el servicio a Azure Portal, confirmar que el servicio de protección está activado y ver la directiva.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 12/15/2018
ms.topic: quickstart
ms.service: information-protection
ms.openlocfilehash: c890d6acf2557093441a175bc8ed8657e8d1d9da
ms.sourcegitcommit: bc082cffaa698b89b28aef7034290553c26f667b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2018
ms.locfileid: "53411820"
---
# <a name="quickstart-get-started-with-azure-information-protection-in-the-azure-portal"></a>Guía de inicio rápido: Introducción a Azure Information Protection en Azure Portal

En este tutorial, podrá agregar Azure Information Protection a Azure Portal, confirmar que el servicio de protección está activado y ver la directiva predeterminada de su organización. 

Puede finalizar este inicio rápido en 5 minutos.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial rápido, necesitará:

- Una suscripción que incluya el plan 1 o el plan 2 de Azure Information Protection.
    
    Si no tiene una de estas suscripciones, puede crear una cuenta [gratuita](https://portal.office.com/Signup/Signup.aspx?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7) para su organización.

Para ver una lista completa de los requisitos previos para utilizar Azure Information Protection, consulte [Requisitos de Azure Information Protection](requirements.md).

## <a name="add-azure-information-protection-to-the-azure-portal"></a>Adición de Azure Information Protection a Azure Portal

Azure Information Protection no está automáticamente disponible en Azure Portal. Debe agregarlo.

1. Inicie sesión en [Azure Portal](https://portal.azure.com) con la cuenta de administrador global del inquilino. 
    
    Si no es el administrador global, utilice el siguiente vínculo para roles alternativos: [Inicio de sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal)

2. En el menú del concentrador, seleccione **Crear un recurso** y, a continuación, en el cuadro de búsqueda de Marketplace, escriba **Azure Information Protection**. 
    
3. En la lista de resultados, seleccione **Azure Information Protection**. Después, en la hoja **Azure Information Protection**, haga clic en **Crear**.
    
    > [!TIP] 
    > Opcionalmente, seleccione **Anclar al panel** para crear un icono de **Azure Information Protection** en el panel, de modo que pueda omitir el examen del servicio la próxima vez que inicie sesión en el portal.
    
    Haga clic en **Crear** de nuevo.

## <a name="confirm-the-protection-service-is-activated"></a>Confirmación de que el servicio de protección está activado

El servicio de protección ahora está activado automáticamente para los nuevos inquilinos, pero resulta conveniente confirmar que no requiere una activación manual. 

1. En la hoja **Azure Information Protection**, seleccione **Administrar** > **Activación de la protección**.

2. Confirme si la protección está activada para el inquilino: 
    
    - Si la protección está activada, verá el siguiente mensaje de confirmación:
        
        ![Estado de Azure Information Protection para Azure RMS](./media/info-protect-azurerms-activated.png)
        
    - Si la protección no está activada, lo verá en la información de estado y se mostrará la opción para activarlo:
        
        ![Estado de Azure Information Protection para Azure RMS](./media/info-protect-azurerms-deactivated.png)

3. Si la protección no está activada, seleccione **Activar**. 

    Una vez completada la activación, en la barra de información se verá **Activation finished successfully** (La activación ha finalizado correctamente).

## <a name="view-your-organizations-default-policy---labels-and-policy-settings"></a>Visualización de la directiva predeterminada de su organización: configuración de directiva y etiquetas

La primera vez que se conecta al servicio Azure Information Protection mediante Azure Portal, se crea una directiva predeterminada para el inquilino. La directiva predeterminada contiene las etiquetas y los valores de configuración, que pueden usar tal cual o bien personalizar.

1. Seleccione **Clasificaciones** > **Directivas** > **Global** para mostrar la directiva de Azure Information Protection predeterminada que se crea para el inquilino.
    
2. Dedique unos minutos a familiarizarse con las etiquetas que se muestran:
    
    - Etiquetas de clasificación: **Personal**, **Público**, **General**, **Confidencial** y **Extremadamente confidencial**. Las dos últimas etiquetas se expanden y muestran subetiquetas, que proporcionan ejemplos de cómo una clasificación puede tener subcategorías:
    
    - Con la configuración predeterminada, algunas etiquetas no tienen distintivos visuales configurados. Los marcadores visuales son pie de página, encabezado y marca de agua. En función de la directiva predeterminada, algunas etiquetas también podrían tener protección establecida. Por ejemplo: 
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](./media/info-protect-policy-default-labelsv2.png)
    
3. Después de las etiquetas, en la sección **Configure settings to display and apply on Information Protection end users** (Configuración de valores para mostrar y aplicar en los usuarios finales de Information Protection), también verá algunas configuraciones de directiva. Por ejemplo, no hay ninguna etiqueta predeterminada establecida, no se requiere que los documentos y los correos electrónicos tengan una etiqueta y los usuarios no tienen que dar ninguna justificación cuando cambian etiquetas:
    
    ![Paso 3 del tutorial de inicio rápido de Azure Information Protection - Directiva predeterminada](./media/info-protect-policy-default-settings-quickstart.png) 

4. Dado que solo ve las etiquetas y los valores de configuración, puede cerrar todas las hojas que haya abierto.

## <a name="next-steps"></a>Pasos siguientes

Ahora que ha visto las etiquetas y la configuración de directiva en Azure Portal, el siguiente tutorial puede resultarle útil: [Edición de la directiva de Azure Information Protection y creación de una nueva etiqueta](infoprotect-quick-start-tutorial.md).

Como alternativa, para obtener instrucciones detalladas para configurar todos los aspectos de la directiva de Azure Information Protection, consulte [Configuración de la directiva de Azure Information Protection](configure-policy.md).
