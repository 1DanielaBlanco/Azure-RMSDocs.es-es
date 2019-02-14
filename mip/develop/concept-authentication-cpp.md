---
title: 'Conceptos: autenticación en el SDK de MIP.'
description: Este artículo le permitirá comprender cómo el SDK de MIP implementa la autenticación y los requisitos para que las aplicaciones cliente puedan proporcionar la lógica de adquisición de tokens de acceso de OAuth2.
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: dd2e8c5c3344da351715069910741c5651f4e617
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56257981"
---
# <a name="microsoft-information-protection-sdk---authentication-concepts"></a>SDK de Microsoft Information Protection: conceptos de autenticación

La autenticación en el SDK de MIP se realiza mediante la extensión de la clase `mip::AuthDelegate` para implementar el método preferido de autenticación. `mip::AuthDelegate` contiene:

- `mip::AuthDelegate::OAuth2Challenge`: clase que administra la información de la autoridad de OAuth2 y la proporciona a la aplicación cliente.
- `mip::AuthDelegate::OAuth2Token`: clase que administra la adquisición de tokens de acceso de OAuth2 (desde la aplicación cliente) y el almacenamiento de tokens.
- `mip::AuthDelegate::AcquireOAuth2Token()`: función virtual pura cuya implementación determina el método de la adquisición de tokens de acceso. Después de recibir una llamada del SDK, adquiere el token de acceso y, después, lo devuelve a la lógica de autenticación del SDK.

`mip::AuthDelegate::AcquireOAuth2Token` acepta los parámetros siguientes y devuelve un operador booleano que indica si la adquisición de tokens ha sido correcta o no:

- `mip::Identity`: La identidad del usuario o servicio se autentique, si se conoce.
- `mip::AuthDelegate::OAuth2Challenge`: Acepta dos parámetros, **autoridad** y **recursos**. **Authority** es el servicio con el que se generará el token. **Resource** es el servicio al que intentamos acceder. El SDK pasará estos parámetros al delegado cuando reciba la llamada.
- `mip::AuthDelegate::OAuth2Token`: El resultado de token se escribe en este objeto. Lo usará el SDK cuando se cargue el motor. Fuera de nuestra implementación de autenticación, no tendría que ser necesario obtener o establecer este valor.

**Importante:** No llame las aplicaciones `AcquireOAuth2Token` directamente. El SDK llamará a esta función cuando sea necesario.

## <a name="consent"></a>Consentimiento

Azure AD necesita que una aplicación conceda el permiso antes de acceder a las API o recursos protegidos con la identidad de una cuenta. El consentimiento se registra como una confirmación permanente de permiso en el inquilino de la cuenta, ya sea para la cuenta específica (consentimiento del usuario) o para todas las cuentas (consentimiento del administrador). El consentimiento se produce en varios escenarios según la API a la que se acceda y los permisos que busque la aplicación, así como la cuenta usada para iniciar sesión: 

- las cuentas del *mismo inquilino* donde se ha registrado la aplicación, si su usuario o un administrador no han concedido de forma explícita y previa el acceso mediante la característica “Conceder permisos”.
- las cuentas de *otro inquilino*, si la aplicación está registrada como multiinquilino y el administrador de inquilinos no ha concedido de forma previa el consentimiento a todos los usuarios.

La clase de enumeración `mip::Consent` implementa un método fácil de usar que permite a los desarrolladores de aplicaciones proporcionar una experiencia de consentimiento personalizada basada en el punto de conexión al que accede el SDK. La notificación puede informar a un usuario de los datos que se recopilarán, cómo se eliminarán los datos o cualquier otra información exigida por ley o directivas de cumplimiento. Cuando el usuario conceda el permiso, la aplicación podrá continuar. 

### <a name="implementation"></a>Implementación

El consentimiento se implementa al extender la clase base `mip::Consent` e implementar `GetUserConsent` para devolver uno de los valores de enumeración `mip::Consent`. 

El objeto derivado de `mip::Consent` se pasa en el constructor `mip::FileProfile::Settings` o `mip::ProtectionProfile::Settings`.

Cuando un usuario realiza una operación para la que sería necesario el consentimiento, el SDK llama al método `GetUserConsent` y lo pasa en la URL de destino como el parámetro. En este método, implementaríamos la visualización de la información necesaria para el usuario, permitiéndole decidir si quiere conceder el permiso o no para el uso del servicio. 

### <a name="consent-options"></a>Opciones de consentimiento

- **AcceptAlways**: Consentimiento y recordar la decisión.
- **Aceptar**: Una vez consentimiento.
- **Reject**: No se acepta.

Cuando el SDK solicita el consentimiento del usuario con este método, la aplicación cliente debe presentar la dirección URL al usuario. Las aplicaciones cliente deben proporcionar algún medio de obtener el consentimiento del usuario y devolver la enumeración de consentimiento adecuada que corresponda a la decisión del usuario.

### <a name="sample-implementation"></a>Implementación de ejemplo

#### <a name="consentdelegateimplh"></a>consent_delegate_impl.h

```cpp
class ConsentDelegateImpl final : public mip::ConsentDelegate {
public:
  ConsentDelegateImpl() = default;
  
  virtual mip::Consent GetUserConsent(const std::string& url) override;

};
```

#### <a name="consentdelegateimplcpp"></a>consent_delegate_impl.cpp

Cuando el SDK necesita el consentimiento, *llama al método* `GetUserConsent` y la URL se pasa como un parámetro. En el ejemplo siguiente, el usuario recibe una notificación que indica que el SDK se conectará a la URL especificada y, después, devolverá `Consent::AcceptAlways`. No es en realidad un buen ejemplo, ya que no se presenta al usuario una opción real.

```cpp
Consent ConsentDelegateImpl::GetUserConsent(const string& url) {
  //Print the consent URL, ask user to choose
  std::cout << "SDK will connect to: " << url << std::endl;

  std::cout << "1) Accept Always" << std::endl;
  std::cout << "2) Accept" << std::endl;
  std::cout << "3) Reject" << std::endl;
  std::cout << "Select an option: ";
  char input;
  std::cin >> input;

  switch (input)
  {
  case '1':
    return Consent::AcceptAlways;
    break;
  case '2':
    return Consent::Accept;
    break;
  case '3':
    return Consent::Reject;
    break;
  default:
    return Consent::Reject;
  }  
}
```

## <a name="next-steps"></a>Pasos siguientes

Por fines de simplicidad, en los ejemplos se demuestra que el delegado implementará la adquisición de tokens mediante la llamada a un script externo. El script puede reemplazarse por cualquier otro tipo de script, una biblioteca de OAuth2 de código abierto o una biblioteca de OAuth2 personalizada.

- [Adquirir un token de acceso mediante PowerShell](concept-authentication-acquire-token-ps.md)
- [Adquirir un token de acceso mediante Python](concept-authentication-acquire-token-py.md)
