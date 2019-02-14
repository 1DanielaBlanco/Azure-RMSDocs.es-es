---
title: clase mip::LoggerDelegate
description: Documenta la clase mip::loggerdelegate de Microsoft Information Protection (MIP) SDK.
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.collection: M365-security-compliance
ms.author: bryanla
ms.date: 01/28/2019
ms.openlocfilehash: 6751335ab3c74b879af57c362f46eefbb89b8c78
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2019
ms.locfileid: "56256862"
---
# <a name="class-miploggerdelegate"></a>clase mip::LoggerDelegate 
Una clase que define la interfaz para el registrador de SDK de MIP.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public void Init(const std::string& storagePath, LogLevel logLevel)  |  Inicialice el registrador.
public LogLevel GetLogLevel() const  |  Obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.
public void Flush()  |  Vacíe el registrador.
public void WriteToLog(const LogLevel level, const std::string& message, const std::string& function, const std::string& file, const int32_t line)  |  Escriba una instrucción de registro en el archivo de registro.
  
## <a name="members"></a>Miembros
  
### <a name="init-function"></a>Función Init
Inicialice el registrador.

Parámetros:  
* **storagePath**: la ruta de acceso a la ubicación donde se puede almacenar el estado persistente, incluidos los registros,. 


* **logLevel**: obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.


  
### <a name="getloglevel-function"></a>Función GetLogLevel
Obtenga el nivel de registro más bajo que pueda desencadenar un evento de registro.

  
**Devuelve**: El nivel de registro más bajo que desencadene un evento de registro.
  
### <a name="flush-function"></a>Flush (función)
Vacíe el registrador.
  
### <a name="writetolog-function"></a>Función WriteToLog
Escriba una instrucción de registro en el archivo de registro.

Parámetros:  
* **level**: nivel de registro para la instrucción de registro. 


* **message**: el mensaje para la instrucción de registro. 


* **function**: el nombre de función para la instrucción de registro. 


* **file**: el nombre de archivo donde se generó la instrucción de registro. 


* **line**: el número de línea donde se generó la instrucción de registro.

