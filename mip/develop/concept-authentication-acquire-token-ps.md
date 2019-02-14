---
title: 'Conceptos: uso de PowerShell para adquirir un token de acceso.'
description: Este artículo le ayudará a comprender cómo usar PowerShell para adquirir un token de acceso de OAuth2. Esto es necesario para la implementación del delegado de autenticación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 02/04/2019
ms.author: bryanla
ms.openlocfilehash: 85c06979a5010a17b60751ccd8a09529be2c362d
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56252901"
---
# <a name="acquire-an-access-token-powershell"></a>Adquirir un token de acceso (PowerShell)

Este ejemplo muestra cómo llamar a un script de PowerShell externo para obtener un token de OAuth2. La implementación del delegado de autenticación requiere un token de acceso de OAuth2 válido.

## <a name="prerequisites"></a>Requisitos previos

- Completa [configuración e instalación SDK (MIP)](setup-configure-mip.md). Entre otras tareas, deberá registrar su aplicación cliente en el inquilino de Azure Active Directory (Azure AD). Azure AD proporcionará un identificador de aplicación, también conocido como Id. de cliente, que se usa en la lógica de adquisición de tokens.

Este código no está pensado para su uso en producción. Solo puede usarse para el desarrollo y la descripción de conceptos de autenticación. 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Creamos una sola función denominada AcquireToken. Puesto que el valor devuelto será codificado de forma rígida para este tutorial, no se acepta ningún parámetro y devolver una cadena (el token).

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();
  }
}
```

### <a name="authcpp"></a>auth.cpp

Nuestro archivo de origen devuelve un valor de token que estará codificados de forma rígida en un paso posterior.

```cpp
//auth.cpp
#include <string>
#include "auth.h"

namespace sample {
  namespace auth {
    string AcquireToken() {
      std::string mToken = "your token here";
      return mToken;
    }
  }
}
```

## <a name="mint-a-token"></a>Inventar un token

Por último, inventa un token para colocar en la variable mToken. El ejemplo siguiente muestra un script de PowerShell que puede usarse para obtener el token de OAuth2 mediante ADAL y PowerShell en Windows. Este token se concede únicamente para el punto de conexión del Centro de cumplimiento y seguridad de Office 365. Por lo tanto, las acciones de protección se producirán un error a menos que se actualice la dirección URL del recurso. 

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>Instalar [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) desde la Galería de PS

Puede omitir este paso si ha completado, anteriormente en [configuración e instalación SDK (MIP)](setup-configure-mip.md).

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Usar Get-ADALToken para obtener el token de acceso

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://syncservice.o365syncservice.com/"
#replace <application-id> and <redirect-uri>, with the Redirect URI and Application ID from your Azure AD application registration.
$clientId = "<application-id>"
$redirectUri = "<redirect-uri>"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copie el token del Portapapeles en a auth.cpp como el valor de `string mToken`, reemplazando "su token aquí" arriba. Puede que sea necesario volver a ejecutar el script, en función de cuánto tiempo tomen los pasos siguientes.


