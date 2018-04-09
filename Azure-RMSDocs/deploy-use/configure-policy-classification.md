---
title: Configuración de condiciones para una etiqueta de Azure Information Protection
description: Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda.
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 04/02/2018
ms.topic: article
ms.prod: ''
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: f7242c05d830ecd1b702e4e9bb049e72740843f3
ms.sourcegitcommit: b17432ed155394111c878eb57b5fa7adf9df9755
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection

>*Se aplica a: [Azure Information Protection](https://azure.microsoft.com/pricing/details/information-protection)*

Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda. 

Al configurar estas condiciones, puede usar patrones predefinidos, como **Número de la tarjeta de crédito** o **Número del seguro social de Estados Unidos (SSN)**. O puede definir un patrón o una cadena personalizada como condición de una clasificación automática. Estas condiciones se aplican al texto del cuerpo en documentos y correos electrónicos, así como a encabezados y pies de página. Para más información sobre las condiciones, vea el paso 5 del [siguiente procedimiento](#to-configure-recommended-or-automatic-classification-for-a-label).

Para conseguir la mejor experiencia de usuario y garantizar la continuidad empresarial, conviene comenzar con la clasificación recomendada al usuario, en lugar de la clasificación automática. Esta configuración permite a los usuarios aceptar la clasificación y cualquier protección asociada, o reemplazar estas sugerencias si no resultan adecuadas para su documento o mensaje de correo electrónico.

Mensaje de ejemplo cuando se configura una condición para aplicar una etiqueta como acción recomendada, con una sugerencia de directiva personalizada:

![Detección y recomendación de Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

En este ejemplo, el usuario puede hacer clic en **Cambiar ahora** para aplicar la etiqueta recomendada, o bien invalidar la recomendación seleccionando **Descartar**.

> [!IMPORTANT]
>No configure una etiqueta para la clasificación automática y un permiso definido por el usuario. La opción de permisos definidos por el usuario es una [configuración de protección](configure-policy-protection.md) que permite a los usuarios especificar a quién se le deben conceder permisos.
>
>Cuando una etiqueta se configura para la clasificación automática y los permisos definidos por el usuario, se comprueba el contenido de las condiciones y no se aplica la configuración de los permisos definidos por el usuario. Puede utilizar la clasificación recomendada y los permisos definidos por el usuario.

## <a name="how-automatic-or-recommended-labels-are-applied"></a>Cómo se aplican las etiquetas automáticas o recomendadas

**Para la versión de disponibilidad general del cliente de Azure Information Protection:**

- La clasificación automática se aplica a Word, Excel y PowerPoint cuando se guardan documentos, y a Outlook cuando se envían correos electrónicos. 
    
    No se puede utilizar la clasificación automática para documentos y correos electrónicos etiquetados previamente de manera manual, o etiquetados previamente de manera automática, con una clasificación más alta. 

- La clasificación recomendada se aplica a Word, Excel y PowerPoint cuando se guardan documentos. No se puede utilizar la clasificación recomendada para Outlook.
    
    Puede utilizar la clasificación recomendada para los documentos etiquetados previamente, con o sin una clasificación más alta. 


**Para la versión preliminar actual del cliente de Azure Information Protection:**

- La clasificación automática se aplica a Word, Excel, PowerPoint y Outlook. Para los documentos, la clasificación automática se ejecuta [continuamente en segundo plano](#more-information-about-running-continuously). Para Outlook, la clasificación automática se ejecuta cuando se envían mensajes de correo electrónico. 
    
    No se puede utilizar la clasificación automática para documentos etiquetados previamente de manera manual, o etiquetados previamente de manera automática, con una clasificación más alta. La excepción a este comportamiento es el uso del analizador de Azure Information Protection con el parámetro OverrideLabel activado.

- La clasificación recomendada se aplica a Word, Excel y PowerPoint. Para estos documentos, la clasificación recomendada se ejecuta [continuamente en segundo plano](#more-information-about-running-continuously). No se puede utilizar la clasificación recomendada para Outlook.
    
    Puede utilizar la clasificación recomendada para los documentos etiquetados previamente, con o sin una clasificación más alta. 

#### <a name="more-information-about-running-continuously"></a>Más información sobre la ejecución continua

De forma predeterminada, la versión preliminar actual del cliente de Azure Information Protection comprueba periódicamente los documentos en busca de las reglas de condición que especifique. Este comportamiento permite la clasificación automática y recomendada y la protección de los documentos que están almacenados en SharePoint Online. Los archivos de gran tamaño también se guardan más rápidamente porque las reglas de condición ya se han ejecutado. 

Las reglas de condición no se ejecutan en tiempo real mientras el usuario escribe. En su lugar, se ejecutan periódicamente como una tarea en segundo plano si se modifica el documento.

Puede cambiar este comportamiento para que el cliente de Azure Information Protection aplique etiquetas automáticas y recomendadas del mismo modo que la versión de disponibilidad general del cliente. Esta configuración requiere una [configuración avanzada del cliente](../rms-client/client-admin-guide-customizations.md#turn-off-classification-running-continuously-in-the-background).

### <a name="how-multiple-conditions-are-evaluated-when-they-apply-to-more-than-one-label"></a>Cómo evaluar varias condiciones cuando se aplican a más de una etiqueta

Para la versión de disponibilidad general del cliente de Azure Information Protection y el cliente de la versión preliminar actual:

1. Las etiquetas se ordenan para la evaluación, según la posición que especifique en la directiva: la etiqueta que se coloca al principio tiene la posición más baja (menos sensible) y la etiqueta que se coloca al final la más alta (más sensible).

2. Se aplica la etiqueta más sensible.
 
3. Se aplica la última subetiqueta.


## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Para configurar la clasificación automática o recomendada para una etiqueta

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e [inicie sesión en Azure Portal](configure-policy.md#signing-in-to-the-azure-portal). Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del concentrador, haga clic en **Todos los servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la etiqueta que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. En la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) o la hoja **Directiva:\<nombre>**, seleccione la etiqueta que quiere configurar. 

4. En la hoja **Etiqueta**, en la sección **Configure conditions for automatically applying this label** (Configurar condiciones para aplicar esta etiqueta automáticamente), haga clic en **Agregar una nueva condición**(Add a new condition).

5. En la hoja **Condición**, seleccione **Tipos de información** si quiere usar una condición predefinida, o **Personalizada** si quiere especificar la suya propia:
    - En **Tipos de información**: seleccione entre las condiciones disponibles de la lista y luego elija el número mínimo de repeticiones y si la repetición debe tener un valor único para ser incluida en el recuento de repeticiones.
        
        Los tipos de información usan los tipos de información de confidencialidad de prevención de pérdida de datos (DLP) y la detección de patrones de Office 365. Puede elegir entre numerosos tipos comunes de información confidencial, algunos de los cuales son específicos de regiones determinadas. Para obtener más información, vea [Qué buscan los tipos de información confidencial](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) en la documentación de Office.
        
        La lista de tipos de información que se pueden seleccionar desde Azure Portal se actualiza periódicamente para incluir cualquier dato que se agregue a la prevención de pérdida de datos de Office. Sin embargo, la lista excluye los tipos de información confidencial personalizados que haya definido y cargado como un paquete de reglas para el Centro de seguridad y cumplimiento de Office 365. 
        
        Cuando Azure Information Protection evalúa los tipos de información que selecciona, no usa la configuración del nivel de confianza de DLP de Office, sino que encuentra coincidencias en función de la confianza más baja.
    
    - En **Personalizada**: especifique un nombre y una frase para buscar coincidencia, sin comillas ni caracteres especiales. A continuación, especifique si la coincidencia será una expresión regular, si se usará distinción entre mayúsculas y minúsculas y el número mínimo de repeticiones, y si la repetición deberá tener un valor único para incluirse en el recuento de repeticiones.
        
        Las expresiones regulares usan los patrones de expresiones regulares de Office 365. Para obtener más información, vea [Definición de expresiones regulares basadas en coincidencias](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) en la documentación de Office. También puede que le resulte útil la referencia a la [sintaxis de expresiones regulares de Perl](http://www.boost.org/doc/libs/1_66_0/libs/regex/doc/html/boost_regex/syntax/perl_syntax.html) de Boost.
        
6. Decida si tiene que cambiar **Número mínimo de repeticiones** y **Contar solo las repeticiones con valores únicos** y luego seleccione **Guardar**. 
    
    Ejemplo de opciones de repeticiones: imagine que selecciona el tipo de información de número de la Seguridad Social, establece el número mínimo de repeticiones en 2 y un documento tiene el mismo número de la Seguridad Social dos veces: si establece **Contar solo las repeticiones con valores únicos** en **Activado**, la condición no se cumple. Si establece esta opción en **Desactivado**, la condición se cumple.

7. De vuelta en la hoja **Etiqueta**, configure lo siguiente y luego haga clic en **Guardar**:
    
    - Elija clasificación automática o recomendada: en **Select how this label is applied: automatically or recommended to user** (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado al usuario), seleccione **Automática** o **Recomendada**.
    
    - Especifique el texto del mensaje de usuario o de la sugerencia de directiva: mantenga el texto predeterminado o especifique su propia cadena.

8. Para que los cambios estén disponibles para los usuarios, en la hoja inicial de **Azure Information Protection**, haga clic en **Publicar**.

## <a name="next-steps"></a>Pasos siguientes

Considere la posibilidad de implementar el [analizador de Azure Information Protection](deploy-aip-scanner.md), que puede usar las reglas de clasificación automática para detectar, clasificar y proteger archivos en recursos compartidos de red y almacenes de archivos locales.  

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).

[!INCLUDE[Commenting house rules](../includes/houserules.md)]

