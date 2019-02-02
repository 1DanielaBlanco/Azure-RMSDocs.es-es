---
title: 'clase MIP:: Identity'
description: 'Documenta la clase MIP:: Identity de Microsoft Information Protection (MIP) SDK.'
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 8c2946e312caeb6d87d66004fa306ca1c68e7f92
ms.sourcegitcommit: be05adc7750e22c110b261882de0389b9dfb2726
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/02/2019
ms.locfileid: "55651884"
---
# <a name="class-mipidentity"></a>clase MIP:: Identity 
Abstracción para la identidad.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
Identity() pública  |  Default [identidad](class_mip_identity.md) constructor se utiliza cuando no se conoce una dirección de correo electrónico del usuario.
Identidad explícita pública (const std:: String & correo electrónico)  |  [Identidad](class_mip_identity.md) constructor se utiliza cuando se sabe que una dirección de correo electrónico del usuario.
Public const std:: String & GetEmail() const  |  Obtener el correo electrónico.
pública SetDelegatedEmail void (const std:: String & delegatedEmail)  |  Establece el correo electrónico delegado, una dirección de correo electrónico delegado está en nombre de usuario para el que se llevan a cabo la opertations.
Public const std:: String & GetDelegatedEmail() const  |  Obtener el correo electrónico de delegado, una dirección de correo electrónico delegados es en nombre de usuario para el que se llevan a cabo la opertations.
  
## <a name="members"></a>Miembros
  
### <a name="identity-function"></a>Función Identity
Default [identidad](class_mip_identity.md) constructor se utiliza cuando no se conoce una dirección de correo electrónico del usuario.
  
### <a name="identity-function"></a>Función Identity
[Identidad](class_mip_identity.md) constructor se utiliza cuando se sabe que una dirección de correo electrónico del usuario.

Parámetros:  
* **correo electrónico**: dirección de correo electrónico del usuario.


  
### <a name="getemail-function"></a>Función GetEmail
Obtener el correo electrónico.

  
**Devuelve**: El correo electrónico.
  
### <a name="setdelegatedemail-function"></a>Función SetDelegatedEmail
Establece el correo electrónico delegado, una dirección de correo electrónico delegado está en nombre de usuario para el que se llevan a cabo la opertations.

Parámetros:  
* **delegatedEmail**: el correo electrónico de delegación.


  
### <a name="getdelegatedemail-function"></a>Función GetDelegatedEmail
Obtener el correo electrónico de delegado, una dirección de correo electrónico delegados es en nombre de usuario para el que se llevan a cabo la opertations.

  
**Devuelve**: El correo electrónico de delegado.