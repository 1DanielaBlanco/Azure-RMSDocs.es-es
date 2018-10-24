---
title: 'Conceptos: usar Python para obtener un token de acceso.'
description: Este artículo le permitirá comprender cómo usar Python para obtener un token de acceso de OAuth2. Esto es necesario para la implementación del delegado de autenticación.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a7577bab58b701e945bea9829d7ed31b41909f88
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445791"
---
# <a name="acquire-an-access-token-python"></a>Obtener un token de acceso (Python)

En este ejemplo, se muestra cómo realizar una llamada a un script de Python externo para obtener un token de OAuth2. Esto es necesario para la implementación del delegado de autenticación.

Este código no está pensado para su uso en entornos de producción, pero puede usarse con fines de desarrollo y para comprender conceptos de autenticación. El ejemplo es multiplataforma.

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar el ejemplo que se encuentra a continuación, es necesario completar lo siguiente:

- Instalar Python 2.7.
- Implementar utils.h/cpp en el proyecto. 
- auth.py tiene que agregarse al proyecto y existir en el mismo directorio al compilar los archivos binarios.

## <a name="sampleauthacquiretoken"></a>sample::auth::AcquireToken()

En el ejemplo de autenticación simple, se demuestra una función `AcquireToken()` sencilla que no admite ningún parámetro y devuelve un valor de token codificado de forma rígida. En este ejemplo, sobrecargamos AcquireToken() para aceptar parámetros de autenticación y realizar una llamada a un script de Python externo para devolver el token.

### <a name="authh"></a>auth.h

En auth.h, se sobrecarga `AcquireToken()`; la función sobrecargada y los parámetros actualizados son los siguientes:

```cpp
//auth.h
#include <string>

namespace sample {
  namespace auth {
    std::string AcquireToken();

    std::string AcquireToken(
        const std::string& userName, //A string value containing the user's UPN.
        const std::string& password, //The user's password in plaintext
        const std::string& clientId, //The AAD client ID of your application.
        const std::string& resource, //The resource URL for which an OAuth2 token is required. Provided by challenge object.
        const std::string& authority); //The authentication authority endpoint. Provided by challenge object.
    }
}
```

Los primeros tres parámetros se obtendrán mediante la entrada del usuario, o bien se codificará de forma rígida en la aplicación. Los últimos dos parámetros los proporciona el SDK para el delegado de autenticación. 


### <a name="authcpp"></a>auth.cpp

En auth.cpp, agregamos la definición de función sobrecargada y, después, definimos el código necesario para llamar al script de Python. La función acepta todos los parámetros especificados y los pasa al script de Python. El script ejecuta y devuelve el token en formato de cadena.

```cpp
#include "auth.h"
#include "utils.h"

#include <fstream>
#include <functional>
#include <memory>
#include <string>

using std::string;
using std::runtime_error;

namespace sample {
    namespace auth {

    string AcquireToken() { //ignore in this sample
    }

    //This function implements token acquisition in the application by calling an external Python script.
    //The Python script requires username, password, clientId, resource, and authority.
    //Username, Password, and ClientId are provided by the user/developer
    //Resource and Authority are provided as part of the OAuth2Challenge object that is passed in by the SDK to the AuthDelegate.
    string AcquireToken(
        const string& userName,
        const string& password,
        const string& clientId,
        const string& resource,
        const string& authority) {

    string cmd = "python";
    if (sample::FileExists("auth.py"))
        cmd += " auth.py -u ";

    else
        throw runtime_error("Unable to find auth script.");

    cmd += userName;
    cmd += " -p ";
    cmd += password;
    cmd += " -a ";
    cmd += authority;
    cmd += " -r ";
    cmd += resource;
    cmd += " -c ";
    cmd += (!clientId.empty() ? clientId : "6b069eef-9dde-4a29-b402-8ce866edc897");

    string result = sample::Execute(cmd.c_str());
    if (result.empty())
        throw runtime_error("Failed to acquire token. Ensure Python is installed correctly.");

    return result;
    }
    }
}

```

## <a name="python-script"></a>Script de Python

Este script obtiene tokens de autenticación directamente mediante una solicitud HTTP sencilla. Esto se incluye únicamente como un medio para obtener tokens de autenticación con el fin de que los usen las aplicaciones de ejemplo y no se concibe para su uso en el código de producción. El script funciona solo en inquilinos que admiten la autenticación HTTP antigua y sin formato de nombre de usuario y contraseña. La autenticación basada en certificados o MFA producirá errores.

```python
import getopt
import sys
import json
import urllib
import urllib2
import re

def printUsage():
  print('auth.py -u <username> -p <password> -a <authority> -r <resource> -c <clientId>')

def main(argv):
  try:
    options, args = getopt.getopt(argv, 'hu:p:a:r:c:')
  except getopt.GetoptError:
    printUsage()
    sys.exit(-1)

  username = ''
  password = ''
  authority = ''
  resource = ''
  clientId = ''

  for option, arg in options:
    if option == '-h':
      printUsage()
      sys.exit()
    elif option == '-u':
      username = arg
    elif option == '-p':
      password = arg
    elif option == '-a':
      authority = arg
    elif option == '-r':
      resource = arg
    elif option == '-c':
      clientId = arg

  if username == '' or password == '' or authority == '' or resource == '' or clientId == '':
    printUsage()
    sys.exit(-1)

  # Find everything after the last '/' and replace it with 'token'
  if not authority.endswith('token'):
    regex = re.compile('^(.*[\/])')
    match = regex.match(authority)
    authority = match.group()
    authority = authority + 'token'

  # Build REST call
  headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept': 'application/json'
  }

  params = {
    'resource': resource,
    'client_id': clientId,
    'grant_type': 'password',
    'username': username,
    'password': password
  }

  req = urllib2.Request(
    url = authority,
    headers = headers,
    data = urllib.urlencode(params))

  f = urllib2.urlopen(req)
  response = f.read()
  f.close()
  sys.stdout.write(json.loads(response)['access_token'])

if __name__ == '__main__':
  main(sys.argv[1:])
```

## <a name="update-acquireoauth2token"></a>Actualizar AcquireOAuth2Token

Por último, actualice la función `AcquireOAuth2Token` en `AuthDelegateImpl` para llamar a la función `AcquireToken` sobrecargada. Las URL de autoridad y recurso se obtienen al leer `challenge.GetResource()` y `challenge.GetAuthority()`. El objeto `OAuth2Challenge` se pasa al delegado de autenticación cuando se agrega el motor. El procesamiento lo realiza el SDK y el desarrollador no necesita realizar otras acciones. 

```cpp
bool AuthDelegateImpl::AcquireOAuth2Token(
    const mip::Identity& /*identity*/,
    const OAuth2Challenge& challenge,
    OAuth2Token& token) {

    //call our AcquireToken function, passing in username, password, clientId, and getting the resource/authority from the OAuth2Challenge object
    string accessToken = sample::auth::AcquireToken(mUserName, mPassword, mClientId, challenge.GetResource(), challenge.GetAuthority());
    token.SetAccessToken(accessToken);
    return true;
}
```

Al agregar `engine`, el SDK realizará una llamada a la función AcquireOAuth2Token, pasará el desafío, ejecutará el script de Python, recibirá un token y, después, presentará el token al servicio.


