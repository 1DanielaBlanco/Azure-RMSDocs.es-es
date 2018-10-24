---
title: 'Conceptos: uso de PowerShell para adquirir un token de acceso.'
description: Este artículo le ayudará a comprender cómo usar PowerShell para adquirir un token de acceso de OAuth2. Esto es necesario para la implementación del delegado de autenticación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 3206fb99cd72c5d609375ec673e7798d33c735c3
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453391"
---
# <a name="acquire-an-access-token-powershell"></a>Adquirir un token de acceso (PowerShell)

En este ejemplo se muestra cómo llamar a un script de PowerShell externo para obtener un token de OAuth2. Esto es necesario para la implementación del delegado de autenticación.

Este código no está pensado para su uso en producción, pero se puede usar para el desarrollo y la comprensión de conceptos de autenticación. 

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

### <a name="authh"></a>auth.h

Creamos una sola función denominada AcquireToken. Puesto que el valor devuelto estará codificado de forma rígida para este tutorial, no aceptamos ningún parámetro y simplemente devolvemos una cadena (el token).

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

Nuestro archivo de origen devuelve un valor de token que estará codificado de forma rígida en un paso posterior.

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

Por último, inventa un token para colocar en la variable mToken. El ejemplo siguiente muestra un script de PowerShell que puede usarse para obtener el token de OAuth2 mediante ADAL y PowerShell en Windows. Este token se concede únicamente para el punto de conexión del Centro de cumplimiento y seguridad de Office 365. Por lo tanto, las acciones de protección se producirán un error a menos que se actualice la dirección URL del recurso. Se recomienda pasar directamente a la sección de [pasos siguientes](#next-steps) si desea probar con el etiquetado y la protección en este momento.

### <a name="install-adalpshttpswwwpowershellgallerycompackagesadalps31942-from-ps-gallery"></a>Instalar [ADAL.PS](https://www.powershellgallery.com/packages/ADAL.PS/3.19.4.2) desde la Galería de PS

```PowerShell
Install-Module -Name ADAL.PS
```

### <a name="use-get-adaltoken-to-obtain-the-access-token"></a>Usar Get-ADALToken para obtener el token de acceso

```PowerShell
#Install the ADAL.PS package if it's not installed.
if(!(Get-Package adal.ps)) { Install-Package -Name adal.ps }

$authority = "https://login.windows.net/common/oauth2/authorize" 
#this is the security and compliance center endpoint
$resourceUrl = "https://dataservice.o365filtering.com"
#clientId and redirectUri are from the RMS Sharing Application. 
#Once custom app registration is supported, a custom id and uri will be required. 
$clientId = "6b069eef-9dde-4a29-b402-8ce866edc897"
$redirectUri = "com.microsoft.rms-sharing-for-win://authorize"

$response = Get-ADALToken -Resource $resourceUrl -ClientId $clientId -RedirectUri $redirectUri -Authority $authority -PromptBehavior:Always
$response.AccessToken | clip
```

Copie el token del Portapapeles en a auth.cpp como el valor de `string mToken`, reemplazando "su token aquí" arriba. Puede que sea necesario volver a ejecutar el script, en función de cuánto tiempo tomen los pasos siguientes.


