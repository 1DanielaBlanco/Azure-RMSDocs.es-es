---
title: 'Conceptos: implementación de un delegado de autenticación (C++)'
description: Este artículo le permitirá comprender cómo implementar un delegado de autenticación en C++.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: 9a9256d4c67845f43eeb1598926ea5c02f07f822
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445740"
---
# <a name="microsoft-information-protection-sdk---implementing-an-authentication-delegate-c"></a>SDK de Microsoft Information Protection: implementar un delegado de autenticación (C++)

El SDK de MIP implementa un delegado de autenticación para controlar los desafíos de autenticación y responder con un token. No implementa por sí mismo la obtención de tokens. El proceso de obtención de tokens tiene que configurarlo el desarrollador mediante la extensión de la clase `mip::AuthDelegate` (en concreto, la función miembro `AcquireOAuth2Token`).

## <a name="building-authdelegateimpl"></a>Compilar AuthDelegateImpl

Para extender la clase base `mip::AuthDelegate`, creamos una clase llamada `sample::auth::AuthDelegateImpl`. Esta clase implementa la función `AcquireOAuth2Token` y configura el constructor para aceptar los parámetros de autenticación.

### <a name="authdelegateimplh"></a>auth_delegate_impl.h

Para este ejemplo, el constructor predeterminado solo acepta el nombre de usuario, la contraseña y el [identificador de la aplicación](/azure/active-directory/develop/developer-glossary.md#application-id-client-id). Estos valores se almacenarán en las variables privadas `mUserName`, `mPassword` y `mClientId`.

Es importante tener en cuenta que la información como el proveedor de identidades o el URI de recursos no es necesaria para la implementación (por lo menos, no son necesarias en el constructor `AuthDelegateImpl`). Esa información se pasa como parte de `AcquireOAuth2Token` en el objeto `OAuth2Challenge`. En su lugar, pasaremos esos detalles a la llamada `AcquireToken` en `AcquireOAuth2Token`.

```cpp
//auth_delegate_impl.h
#include <string.h>
#include "mip/common_types.h"

namespace sample {
namespace auth {
class AuthDelegateImpl final : public mip::AuthDelegate { //extend mip::AuthDelegate base class
public:
  AuthDelegateImpl() = delete;

  //constructor accepts username, password, and clientId, all plain strings.
  AuthDelegateImpl(
    const std::string& userName,
    const std::string& password,
    const std::string& clientId
  );

  bool AcquireOAuth2Token(const mip::Identity& identity, const OAuth2Challenge& challenge, OAuth2Token& token) override;

private:
  std::string mUserName;
  std::string mPassword;
  std::string mClientId;
};

}
}
```

### <a name="authdelegateimplcpp"></a>auth_delegate_impl.cpp

`AcquireOAuth2Token` es donde se realizará la llamada al proveedor de OAuth2. En el ejemplo siguiente, hay dos llamadas a `AcquireToken()`. En la práctica, solo se realizará una llamada. Estas implementaciones se describirán en las secciones de [Pasos siguientes](#next-steps).

```cpp
//auth_delegate_impl.cpp
#include "auth_delegate_impl.h"
#include <stdexcept>
#include "auth.h" //contains the auth class used later for token acquisition

using std::runtime_error;
using std::string;

namespace sample {
namespace auth {

AuthDelegateImpl::AuthDelegateImpl(
    const string& userName,
    const string& password,
    const string& clientId)
    : mUserName(userName),
    mPassword(password),
    mClientId(clientId) {
}

//Here we could simply add our token acquisition code to AcquireOAuth2Token
//Instead, that code is implemented in auth.h/cpp to demonstrate calling an external library
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/, //This won't be used
    const OAuth2Challenge& challenge,
    const OAuth2Token& token) {

      //sample::auth::AcquireToken is the code where the token acquisition routine is implemented.
      //AcquireToken() returns a string that contains the OAuth2 token.

      //Simple example for getting hard coded token. Comment out if not used.
      string accessToken = sample::auth::AcquireToken();

      //Practical example for calling external OAuth2 library with provided authentication details.
      string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetAuthority(), challenge.GetResource());  

      //set the passed in OAuth2Token value to the access token acquired by our provider
      token.SetAccessToken(accessToken);
      return true;
    }
}
}
```

## <a name="next-steps"></a>Pasos siguientes

Para completar la implementación de autenticación, es necesario compilar el código de la función `AcquireToken()`. En los ejemplos siguientes, se explican varias formas de obtener el token.

- [Ejemplo de obtención de tokens de PowerShell/sencillo](concept-authentication-acquire-token-ps.md)
- [Ejemplo de obtención de tokens de Python](concept-authentication-acquire-token-py.md)
