---
title: "Configuración de condiciones para una etiqueta de Azure Information Protection"
description: "Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda."
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 09/07/2017
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e915f959-eafb-4375-8d2c-2f312edf2d29
ms.openlocfilehash: 09ee8587e6b254584f70dbe2475063831fd5b845
ms.sourcegitcommit: 6636defa6eca24360f15fb9ef93c2b82dc36cf76
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2017
---
# <a name="how-to-configure-conditions-for-automatic-and-recommended-classification-for-azure-information-protection"></a>Configuración de las condiciones para la clasificación automática y recomendada en Azure Information Protection

>*Se aplica a: Azure Information Protection*

Al configurar las condiciones de una etiqueta, puede asignar automáticamente la etiqueta a un documento o a un correo electrónico. También puede indicar a los usuarios que seleccionen la etiqueta que usted recomienda: 

- La clasificación automática se aplica a Word, Excel y PowerPoint cuando se guardan archivos, y a Outlook cuando se envían correos electrónicos. No se puede utilizar la clasificación automática para archivos que anteriormente se etiquetaron manualmente.
 
- La clasificación recomendada se aplica a Word, Excel y PowerPoint cuando se guardan archivos.

Al configurar condiciones, puede usar patrones predefinidos, como **Número de la tarjeta de crédito** o **Número de la Seguridad Social (SSN) de EE. UU.**. O puede definir un patrón o una cadena personalizada como condición de una clasificación automática. Estas condiciones se aplican al texto del cuerpo en documentos y correos electrónicos, así como a encabezados y pies de página. Para obtener más información sobre las condiciones, vea la sección [Detalles sobre los tipos de información](#details-about-the-information-types).

Modo de evaluar varias condiciones cuando se aplican a más de una etiqueta:

1. Las etiquetas se ordenan para la evaluación, según la posición que especifique en la directiva: la etiqueta que se coloca al principio tiene la posición más baja (menos sensible) y la etiqueta que se coloca al final la más alta (más sensible).

2. Se aplica la etiqueta más sensible.
 
3. Se aplica la última etiqueta secundaria.

> [!TIP]
>Para conseguir la mejor experiencia de usuario y garantizar la continuidad empresarial, conviene comenzar con la clasificación recomendada al usuario, en lugar de la clasificación automática. Esta configuración permite a los usuarios aceptar la acción de etiquetado o protección, o de reemplazar estas sugerencias si no resultan adecuadas para su documento o mensaje de correo electrónico.

Mensaje de ejemplo cuando se configura una condición para aplicar una etiqueta como acción recomendada, con una sugerencia de directiva personalizada:

![Detección y recomendación de Azure Information Protection](../media/info-protect-recommend-calloutsv2.png)

En este ejemplo, el usuario puede hacer clic en **Cambiar ahora** para aplicar la etiqueta recomendada, o bien invalidar la recomendación seleccionando **Descartar**.

## <a name="to-configure-recommended-or-automatic-classification-for-a-label"></a>Para configurar la clasificación automática o recomendada para una etiqueta

1. Si aún no lo ha hecho, abra una nueva ventana del explorador e inicie sesión en [Azure Portal](https://portal.azure.com) como administrador de seguridad o administrador global. Después, vaya a la hoja **Azure Information Protection**. 
    
    Por ejemplo, en el menú del centro, haga clic en **Más servicios** y comience a escribir **Information** en el cuadro Filtro. Seleccione **Azure Information Protection**.

2. Si la etiqueta que quiere configurar se va a aplicar a todos los usuarios, quédese en la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global).
    
    Si la etiqueta que quiere configurar se encuentra en una [directiva con ámbito](configure-policy-scope.md) para que se aplique únicamente a los usuarios seleccionados, en la selección del menú **DIRECTIVAS**, seleccione **Directivas con ámbito**. Después, seleccione la directiva con ámbito en la hoja **Azure Information Protection - Scoped policies** (Azure Information Protection: directivas con ámbito).

3. En la hoja **Azure Information Protection - Global policy** (Azure Information Protection: directiva global) o la hoja **Directiva:\<nombre>**, seleccione la etiqueta que quiere configurar. 

4. En la hoja **Etiqueta**, en la sección **Configure conditions for automatically applying this label** (Configurar condiciones para aplicar esta etiqueta automáticamente), haga clic en **Agregar una nueva condición**(Add a new condition).

5. En la hoja **Condición**, seleccione **Tipos de información** si quiere usar una condición predefinida, o **Personalizada** si quiere especificar la suya propia, y luego haga clic en **Guardar**:
    - En **Tipos de información**: seleccione entre las condiciones disponibles de la lista y luego elija el número mínimo de repeticiones y si la repetición debe tener un valor único para ser incluida en el recuento de repeticiones.
        
        Para usar la lista completa de condiciones, debe usar la versión preliminar actual del cliente de Azure Information Protection. Si tiene la versión de disponibilidad general actual del cliente, solo se admiten las cinco condiciones siguientes: **Código SWIFT**, **Número de la tarjeta de crédito**, **Número de enrutamiento ABA**, **Número de la Seguridad Social (SSN) de EE. UU.** y **Número de cuenta bancaria internacional (IBAN)**. [Más información](#details-about-the-information-types).
    
    - En **Personalizada**: especifique un nombre y una frase para buscar coincidencia, sin comillas ni caracteres especiales. A continuación, especifique si la coincidencia será una expresión regular, si se usará distinción entre mayúsculas y minúsculas y el número mínimo de repeticiones, y si la repetición deberá tener un valor único para incluirse en el recuento de repeticiones.
        
        Si tiene la versión preliminar actual del cliente de Azure Information Protection, las expresiones regulares usan los patrones de expresiones regulares de Office 365. Para obtener más información, vea [Definición de expresiones regulares basadas en coincidencias](https://technet.microsoft.com/library/jj674702(v=exchg.150).aspx#Anchor_2) en la documentación de Office. 
        
    **Ejemplo de opciones de repeticiones**: supongamos que selecciona la opción integrada de número de la Seguridad Social y establece el número mínimo de repeticiones en 2. En un documento en el que se muestra el mismo número de la Seguridad Social dos veces, si establece **Contar solo las repeticiones con valores únicos** en **Activado**, la condición no se cumpliría. Si establece esta opción en **Desactivado**, la condición se cumple.

6. En la hoja **Etiqueta**, configure lo siguiente y luego haga clic en **Guardar**:
    
    - Elija clasificación automática o recomendada: en **Select how this label is applied: automatically or recommended to user** (Seleccionar cómo se aplica esta etiqueta: automáticamente o recomendado al usuario), seleccione **Automática** o **Recomendada**.
    
    - Especifique el texto del mensaje de usuario o de la sugerencia de directiva: mantenga el texto predeterminado o especifique su propia cadena.

7. Para que los cambios estén disponibles para los usuarios, en la hoja inicial de **Azure Information Protection**, haga clic en **Publicar**.

## <a name="details-about-the-information-types"></a>Detalles sobre los tipos de información

Si tiene la versión preliminar actual del cliente de Azure Information Protection, se admiten todos los tipos de información que se muestran en el portal:

- Los tipos de información usan los tipos de información confidencial de la prevención de pérdida de datos (DLP) y la detección de patrones integradas en Office 365. Puede elegir entre numerosos tipos comunes de información confidencial, algunos de los cuales son específicos de regiones determinadas. Para obtener más información sobre los tipos de información que puede seleccionar, consulte [Qué buscan los tipos de información confidencial](https://support.office.com/article/What-the-sensitive-information-types-look-for-fd505979-76be-4d9f-b459-abef3fc9e86b) en la documentación de Office. 

- La lista de tipos de información que se pueden seleccionar desde Azure Portal se actualiza periódicamente para incluir cualquier dato que se agregue a la prevención de pérdida de datos de Office. Sin embargo, la lista excluye los tipos de información confidencial personalizados que haya definido y cargado como un paquete de reglas para el Centro de seguridad y cumplimiento de Office 365. 

- Cuando Azure Information Protection evalúa los tipos de información que selecciona, no usa la configuración del nivel de confianza de DLP de Office, sino que encuentra coincidencias en función de la confianza más baja.

Si tiene la versión de disponibilidad general actual del cliente, solo se admiten los siguientes tipos de información:

- [Código SWIFT](#swift-code )

- [Número de tarjeta de crédito](#credit-card-number )

- [Número de enrutamiento ABA](#aba-routing-number )

- [Número del seguro social (N.º de SS) de EE. UU.](#usa-social-security-number-ssn)

- [Número de cuenta bancaria internacional (IBAN)](#international-banking-account-number-iban)

Vea las secciones siguientes para obtener más información sobre cada uno de estos tipos de información de la versión de disponibilidad general del cliente.

### <a name="swift-code"></a>Código SWIFT

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Una de las siguientes frases: **swift**, **swiftnumber**, **swiftroutingnumber** 

2. Un código Swift, en un patrón con formato:  

    a. 4 letras (código del banco)  

    b. 2 letras (código de país)  

    c. 2 letras o dígitos (código de ubicación)  

    d. 3 letras o dígitos opcionales (código de sucursal)  


Ejemplos para prueba:

- **NEDSZAJJXXX Swiftroutingnumber**

- **NEDSZAJJ100 Swiftnumber** 

----


### <a name="credit-card-number"></a>Número de la tarjeta de crédito

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

- Un número de tarjeta de crédito válido, en un patrón con formato o sin formato, que pase la [comprobación de Luhn](https://wikipedia.org/wiki/Luhn_algorithm). Este tipo de información detecta tarjetas de todas las principales marcas del mundo, como Visa, MasterCard, Discover Card, American Express y Diners.

    - **Con formato**:
    
        - 16 dígitos: (dddd-dddd-dddd-dddd)  
        
    - **Sin formato**:
    
        - (dddddddddddddddd)  


Ejemplos para prueba:

- **4242-4242-4242-4242**

- **4242424242424242** 

----

### <a name="aba-routing-number"></a>Número de enrutamiento ABA

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Al menos una de las siguientes frases: **aba**, **rtn**, **número de enrutamiento** 

2. Un número de enrutamiento ABA, que incluye 9 dígitos que pueden estar en un patrón con formato o sin formato: 

    - **Con formato**: 
        
        a. Cuatro dígitos que comienzan con 0, 1, 2, 3, 6, 7 o 8 
        
        b. Un guión 
        
        c. Cuatro dígitos 
        
        d. Un guión 
        
        e. Un dígito 
        
        Ejemplo: 3456 9876 1 ABA 
        
    - **Sin formato**: 
        
        9 dígitos consecutivos que comienzan con 0, 1, 2, 3, 6, 7 o 8 
        
        Ejemplo: 345698761 RTN 
 

Ejemplos para prueba:

- **3456-9876-1 ABA**

- **345698761 RTN** 

----

### <a name="usa-social-security-number-ssn"></a>Número de la Seguridad Social (SSN) de EE. UU.

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. Al menos una de las siguientes frases: **ssn**, **seguridad social**, **ssid**, **ss#** 

2. Un número de la Seguridad Social: 9 dígitos, que pueden estar en un patrón con formato o sin formato:

    - **Con formato**: 
    
        - Nueve dígitos en el siguiente formato: dd-ddd-dddd o ddd dd dddd 
        
    - **Sin formato**: 
    
        - Nueve dígitos en el siguiente formato: ddddddddd 


Ejemplos para prueba:

- **N.º de SS 123-45-6789**

- **N.º SS 123456789** 


----

### <a name="international-banking-account-number-iban"></a>Número de cuenta bancaria internacional (IBAN)

Busque coincidencia con este tipo de información cuando el contenido incluya lo siguiente:  

1. La siguiente frase: **IBAN** 

2. Un número IBAN: comienza con un código de país (dos letras), le siguen dígitos de comprobación (dos) y luego el número bban (hasta 30 dígitos).


Ejemplos para prueba:

- **GB29 NWBK 6016 1331 9268 19 IBAN**


## <a name="next-steps"></a>Pasos siguientes

Para más información sobre cómo configurar la directiva de Azure Information Protection, use los vínculos de la sección [Configuring your organization's policy](configure-policy.md#configuring-your-organizations-policy) (Configuración de la directiva de la organización).  

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


